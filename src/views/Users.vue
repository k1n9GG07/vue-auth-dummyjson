<template>
  <div class="users-view">
    <div v-if="loading" class="loading">Loading...</div>
    <div v-else class="users-list">
      <div v-for="user in users" :key="user.id" class="user-card">
        <span class="user-name">{{ user.firstName }} {{ user.lastName }} {{ user.maidenName }}</span>
        <span class="user-email">{{ user.email }}</span>
      </div>
      <div class="user-card dots">...</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const users = ref([]);
const loading = ref(true);

const fetchUsers = async () => {
  try {
    const response = await fetch('https://dummyjson.com/users?limit=5');
    const data = await response.json();
    users.value = data.users;
  } catch (err) {
    console.error(err);
  } finally {
    loading.value = false;
  }
};

onMounted(fetchUsers);
</script>

<style scoped>
.users-view {
  display: flex;
  justify-content: center;
  padding-top: 40px;
}

.users-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  width: 100%;
  max-width: 450px;
}

.user-card {
  background: #FFFFFF;
  box-shadow: 0px 4px 10px rgba(187, 225, 250, 0.25);
  border-radius: 6px;
  padding: 15px 25px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #edf2f7;
}

.user-name {
  font-weight: 500;
  font-size: 16px;
  color: #21243D;
}

.user-email {
  font-size: 14px;
  color: #8695A4;
}

.dots {
  justify-content: flex-start;
  color: #8695A4;
  font-size: 24px;
}

.loading {
  text-align: center;
  font-size: 20px;
}
</style>
