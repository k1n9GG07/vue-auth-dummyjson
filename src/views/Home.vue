<template>
  <div class="home-view">
    <div class="hero-section">
      <div class="hero-content">
        <h1 class="hero-title">Home page</h1>
        <p class="hero-text">
          Amet minim mollit non deserunt ullamco est sit aliqua dolor do amet 
          sint. Velit officia consequat duis enim velit mollit. Exercitation veniam 
          consequat sunt nostrud amet.
        </p>
        <router-link to="/login" class="btn-auth">Authorization</router-link>
      </div>
      <div class="hero-image">
        <svg class="tools-icon" viewBox="0 0 512 512" fill="none" xmlns="http://www.w3.org/2000/svg">
          <!-- Updated tool icon according to design requirements -->
          <path data-v-2dc54a20="" d="M470.39,114.71,397.29,41.61a32,32,0,0,0-45.26,0L245.41,148.23l-34.61-34.61a16,16,0,0,0-22.62,0L30.56,271.24a32,32,0,0,0,0,45.26l73.1,73.1a32,32,0,0,0,45.26,0L306.55,231.95l34.61,34.61a16,16,0,0,0,22.62,0L470.39,160a32,32,0,0,0,0-45.26ZM127.1,367.1,53.1,293.1,210.5,135.7l74,74Z" fill="#21243D"/>
          <path d="M256 300l-100 100-50-50 100-100z" fill="#9DBE5C"/>
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home-view {
  padding-top: 60px;
}

.hero-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 40px;
}

.hero-content {
  flex: 1;
}

.hero-title {
  font-size: 44px;
  line-height: 60px;
  margin-bottom: 25px;
  color: #21243D;
  font-weight: 700;
}

.hero-text {
  font-size: 16px;
  line-height: 24px;
  color: #21243D;
  margin-bottom: 35px;
  max-width: 500px;
}

.hero-image {
  flex: 1;
  display: flex;
  justify-content: flex-end;
}

.tools-icon {
  width: 300px;
  height: 300px;
}

@media (max-width: 800px) {
  .hero-section {
    flex-direction: column-reverse;
    text-align: center;
  }
  .hero-image {
    justify-content: center;
  }
}
</style>
