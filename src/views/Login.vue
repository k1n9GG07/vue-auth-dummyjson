<template>
  <div class="login-view">
    <div class="login-card">
      <div class="login-header">
        <span class="login-title">Authorization</span>
        <span v-if="error" class="error-text">Invalid credentials</span>
      </div>
      
      <form @submit.prevent="handleLogin" class="login-form">
        <div class="form-group">
          <label for="username">Login</label>
          <input 
            type="text" 
            id="username" 
            v-model="username" 
            required
            class="login-input"
          />
        </div>
        
        <div class="form-group">
          <label for="password">Password</label>
          <input 
            type="password" 
            id="password" 
            v-model="password" 
            required
            class="login-input"
          />
        </div>
        
        <button type="submit" :disabled="loading" class="btn-submit">
          {{ loading ? '...' : 'Submit' }}
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const username = ref('');
const password = ref('');
const error = ref(null);
const loading = ref(false);

const handleLogin = async () => {
  loading.value = true;
  error.value = null;
  
  try {
    const response = await fetch('https://dummyjson.com/auth/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        username: username.value,
        password: password.value,
      })
    });
    
    const data = await response.json();
    
    if (!response.ok) {
      throw new Error('Invalid credentials');
    }
    
    localStorage.setItem('token', data.accessToken);
    router.push('/profile');
    
  } catch (err) {
    error.value = true;
  } finally {
    loading.value = false;
  }
};
</script>

<style scoped>
.login-view {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
}

.login-card {
  background: #FFFFFF;
  box-shadow: 0px 4px 10px rgba(187, 225, 250, 0.25);
  border-radius: 6px;
  padding: 40px;
  width: 100%;
  max-width: 400px;
  border: 1px solid #edf2f7;
}

.login-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
}

.login-title {
  font-weight: 500;
  font-size: 16px;
  color: #21243D;
}

.error-text {
  color: #ff6464;
  font-size: 14px;
  font-weight: 700;
}

.login-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  align-items: center;
}

.form-group {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}

.form-group label {
  font-size: 14px;
  color: #21243D;
}

.login-input {
  width: 100%;
  max-width: 180px;
  height: 35px;
  border: 1px solid #E0E0E0;
  border-radius: 6px;
  padding: 0 10px;
  outline: none;
}

.btn-submit {
  background: transparent;
  border: none;
  color: #21243D;
  font-size: 14px;
  cursor: pointer;
  margin-top: 10px;
}

.btn-submit:hover {
  color: #ff6464;
}
</style>
