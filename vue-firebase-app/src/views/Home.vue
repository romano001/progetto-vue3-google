<template>
  <div class="container mt-4">
    <h2>Lista Items</h2>
    <button class="btn btn-outline-danger float-end" @click="logoutAndGoBack">Logout</button>
    <div class="row mt-4">
      <ItemCard
        v-for="item in items"
        :key="item.id"
        :item="item"
        @click="viewItem(item)"
      />
    </div>
    <ItemDetail v-if="selectedItem" :item="selectedItem" @close="selectedItem = null" />
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { db, logout } from '../firebase';
import { collection, getDocs } from 'firebase/firestore';
import ItemCard from '../components/ItemCard.vue';
import ItemDetail from '../components/ItemDetail.vue';
import { useRouter } from 'vue-router';

const items = ref([]);
const selectedItem = ref(null);
const router = useRouter();

const viewItem = (item) => selectedItem.value = item;

const logoutAndGoBack = async () => {
  await logout();
  router.push('/');
};

onMounted(async () => {
  const querySnapshot = await getDocs(collection(db, 'items'));
  items.value = querySnapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
});
</script>
