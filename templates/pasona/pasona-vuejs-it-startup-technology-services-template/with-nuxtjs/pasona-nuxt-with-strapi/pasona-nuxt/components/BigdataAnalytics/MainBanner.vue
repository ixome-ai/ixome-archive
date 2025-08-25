<template>
  <div class="bigdata-analytics-banner">
    <div class="container">
      <div class="bigdata-analytics-content">
        <h1>{{ heroData.title }}</h1>
        <p>{{ heroData.subtitle }}</p>
        <div class="cta-buttons">
          <a href="/support" class="btn btn-primary">Chat with Us</a>
          <a href="/account" class="btn btn-secondary">{{ isAuthenticated ? 'View Account' : 'Get Started' }}</a>
        </div>
        <!-- Einstein Animation -->
        <div class="einstein-animation">
          <svg class="animation-svg" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
            <rect x="10" y="10" width="180" height="120" fill="#f0f0f0" />
            <text x="20" y="50" font-size="16" fill="#007BFF">Chalkboard</text>
            <circle cx="100" cy="160" r="20" fill="#007BFF" class="animate-bounce" />
            <text x="80" y="180" font-size="12" fill="#fff">Einstein</text>
          </svg>
        </div>
      </div>
    </div>

    <div class="banner-boxes-area">
      <div class="container">
        <div class="row">
          <div class="col-lg-4 col-md-6 col-sm-6">
            <div class="single-banner-boxes">
              <div class="icon">
                <client-only>
                  <font-awesome-icon :icon="['fas', 'server']" class="fa-icon" />
                </client-only>
              </div>
              <h3>Basic Subscription</h3>
              <p>$10 for 100 tokens. Ideal for occasional troubleshooting of Control4 and Lutron systems.</p>
              <a href="/account" class="upgrade-link">Upgrade</a>
            </div>
          </div>
          <div class="col-lg-4 col-md-6 col-sm-6">
            <div class="single-banner-boxes">
              <div class="icon">
                <client-only>
                  <font-awesome-icon :icon="['fas', 'code']" class="fa-icon" />
                </client-only>
              </div>
              <h3>Pro Subscription</h3>
              <p>$50 for 1000 tokens. Perfect for frequent users needing advanced smart home support.</p>
              <a href="/account" class="upgrade-link">Upgrade</a>
            </div>
          </div>
          <div class="col-lg-4 col-md-6 col-sm-6">
            <div class="single-banner-boxes">
              <div class="icon">
                <client-only>
                  <font-awesome-icon :icon="['fas', 'users']" class="fa-icon" />
                </client-only>
              </div>
              <h3>Enterprise Subscription</h3>
              <p>$200 for 10000 tokens. Enterprise-level access for installers and large-scale projects.</p>
              <a href="/account" class="upgrade-link">Upgrade</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { faServer, faCode, faUsers } from '@fortawesome/free-solid-svg-icons';
import { library } from '@fortawesome/fontawesome-svg-core';
import { computed } from 'vue';

library.add(faServer, faCode, faUsers);

export default {
  name: 'MainBanner',
  components: {
    FontAwesomeIcon,
  },
  async setup() {
    // Initialize heroData with fallback
    let heroData = {
      title: 'Revolutionize Your Smart Home with AI Support',
      subtitle: 'IXome.ai offers subscription-based chatbot for Control4 and Lutron troubleshooting, with autonomous updates for seamless experience.',
    };

    // Strapi fetch
    try {
      const response = await $fetch('http://localhost:1337/api/hero?populate=*');
      if (response?.data?.attributes) {
        heroData = {
          title: response.data.attributes.title || heroData.title,
          subtitle: response.data.attributes.subtitle || heroData.subtitle,
        };
      }
    } catch (err) {
      console.error('Failed to fetch hero data:', err);
    }

    // Auth check using 'token' to match pages/index.vue
    const isAuthenticated = computed(() => !!localStorage.getItem('token'));

    return { heroData, isAuthenticated };
  },
};
</script>

<style scoped>
.bigdata-analytics-banner {
  padding: 50px 0;
  background: url('~/assets/img/bigdata-analytics/main-banner.jpg') no-repeat center center;
  background-size: cover;
  min-height: 400px;
}
@media (min-width: 768px) {
  .bigdata-analytics-banner {
    min-height: 600px;
  }
}
.container {
  max-width: 1140px;
  margin: 0 auto;
  padding: 0 15px;
}
.bigdata-analytics-content {
  text-align: center;
  color: #fff;
}
.bigdata-analytics-content h1 {
  font-size: 36px;
  font-weight: 700;
  margin-bottom: 15px;
}
@media (min-width: 768px) {
  .bigdata-analytics-content h1 {
    font-size: 48px;
  }
}
.bigdata-analytics-content p {
  font-size: 18px;
  margin-bottom: 20px;
}
.cta-buttons {
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
}
@media (min-width: 640px) {
  .cta-buttons {
    flex-direction: row;
    gap: 15px;
  }
}
.btn {
  display: inline-block;
  padding: 12px 25px;
  text-decoration: none;
  border-radius: 5px;
  font-weight: 500;
  transition: background-color 0.3s ease;
}
.btn-primary {
  background-color: #007bff;
  color: #fff;
}
.btn-primary:hover {
  background-color: #0056b3;
}
.btn-secondary {
  background-color: #fff;
  color: #333;
}
.btn-secondary:hover {
  background-color: #f1f1f1;
}
.einstein-animation {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}
.animation-svg {
  width: 150px;
  height: 150px;
}
@media (min-width: 768px) {
  .animation-svg {
    width: 200px;
    height: 200px;
  }
}
.banner-boxes-area {
  padding: 30px 0;
}
.row {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -15px;
}
.col-lg-4 {
  flex: 0 0 33.333%;
  max-width: 33.333%;
  padding: 0 15px;
}
.col-md-6 {
  flex: 0 0 50%;
  max-width: 50%;
  padding: 0 15px;
}
.col-sm-6 {
  flex: 0 0 50%;
  max-width: 50%;
  padding: 0 15px;
}
@media (max-width: 991px) {
  .col-lg-4 {
    flex: 0 0 50%;
    max-width: 50%;
  }
}
@media (max-width: 767px) {
  .col-lg-4, .col-md-6, .col-sm-6 {
    flex: 0 0 100%;
    max-width: 100%;
  }
}
.single-banner-boxes {
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.15);
  transition: box-shadow 0.3s ease;
}
.single-banner-boxes:hover {
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}
.icon {
  margin-bottom: 15px;
}
.fa-icon {
  width: 40px;
  height: 40px;
  color: #007bff;
}
.upgrade-link {
  color: #007bff;
  text-decoration: none;
  font-weight: 500;
}
.upgrade-link:hover {
  text-decoration: underline;
}
.animate-bounce {
  animation: bounce 2s infinite;
}
@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
</style>