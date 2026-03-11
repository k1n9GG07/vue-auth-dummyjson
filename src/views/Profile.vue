<template>
  <div class="profile-view">
    <div v-if="loading" class="loading">Loading profile...</div>
    <div v-else class="profile-container">
      <h1 class="profile-title" :class="{ 'error-title': error }">
        {{ error ? error : 'My profile' }}
      </h1>
      
      <div v-if="!error && user" class="profile-content">
        <div class="info-column">
          <div class="info-block">
            <span class="info-label">Username:</span>
            <span class="info-value">{{ user.username }}</span>
          </div>
          <div class="info-block">
            <span class="info-label">Name:</span>
            <span class="info-value">{{ user.firstName }}</span>
          </div>
          <div class="info-block" v-if="user.lastName">
            <span class="info-label">Lastname:</span>
            <span class="info-value">{{ user.lastName }}</span>
          </div>
          <div class="info-block">
            <span class="info-label">Gender:</span>
            <span class="info-value">{{ user.gender }}</span>
          </div>
          <div class="info-block">
            <span class="info-label">Email:</span>
            <span class="info-value">{{ user.email }}</span>
          </div>
        </div>
        <div class="image-column">
          <img :src="user.image" alt="Profile image" class="profile-avatar">
        </div>
      </div>
      
      <div v-if="error" class="error-actions">
        <router-link to="/login" class="btn-auth">Go to Login</router-link>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const user = ref(null);
const loading = ref(true);
const error = ref(null);

const fetchProfile = async () => {
  const token = localStorage.getItem('token');
  
  if (!token) {
    router.push('/login');
    return;
  }
  
  try {
    const response = await fetch('https://dummyjson.com/auth/me', {
      method: 'GET',
      headers: {
        'Authorization': `Bearer ${token}`
      }
    });
    
    const data = await response.json();
    
    if (!response.ok) {
      throw new Error(data.message || 'Token is invalid');
    }
    
    user.value = data;
    
  } catch (err) {
    error.value = err.message;
  } finally {
    loading.value = false;
  }
};

onMounted(fetchProfile);
</script>

<style scoped>
.profile-view {
  padding-top: 40px;
}

.profile-container {
  max-width: 800px;
  margin: 0 auto;
}

.profile-title {
  font-size: 44px;
  color: #21243D;
  margin-bottom: 50px;
  font-weight: 700;
}

.error-title {
  font-size: 24px;
  color: #ff6464;
}

.profile-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 60px;
}

.info-column {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.info-block {
  background: #FFFFFF;
  box-shadow: 0px 4px 10px rgba(187, 225, 250, 0.25);
  border-radius: 6px;
  padding: 10px 20px;
  display: flex;
  gap: 10px;
  border: 1px solid #edf2f7;
  width: fit-content;
}

.info-label {
  font-weight: 500;
  color: #21243D;
}

.info-value {
  color: #21243D;
}

.image-column {
  flex: 1;
  display: flex;
  justify-content: center;
}

.profile-avatar {
  width: 250px;
  height: 250px;
  border-radius: 50%;
  object-fit: cover;
  background-color: #f0f0f0;
}

.loading {
  text-align: center;
  font-size: 20px;
}

.error-actions {
  margin-top: 30px;
}

@media (max-width: 700px) {
  .profile-content {
    flex-direction: column-reverse;
    align-items: center;
  }
  .info-column {
    align-items: center;
  }
}
</style>
