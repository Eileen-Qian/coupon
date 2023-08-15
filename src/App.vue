<script>
import { RouterLink, RouterView } from 'vue-router'
const { VITE_APP_URL, VITE_APP_PATH } = import.meta.env

export default {
  data() {
    return {
      isLoading: false,
    }
  },
  components: {
    RouterView,
    RouterLink,
  },
  mounted() {
    this.isLoading = true;
    setTimeout(() => {
      this.isLoading = false;
    }, 1000)

    console.log(import.meta.env.VITE_APP_URL, import.meta.env.VITE_APP_PATH);
    console.log(`${VITE_APP_URL}/v2/api/${VITE_APP_PATH}/products/all`);

    this.$http.get(`${VITE_APP_URL}/v2/api/${VITE_APP_PATH}/products/all`)
      // axios.get('https://randomuser.me/api/')
      .then((res) => {
        console.log(res);
      })

  }
}

</script>

<template>
  <div class="container">
    <header>
      <VueLoading v-model:active="isLoading"></VueLoading>
      <nav class="navbar navbar-expand-lg bg-light">
        <div class="container-fluid">
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
              <li class="nav-item">
                <RouterLink to="/">Home</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink to="/about">About</RouterLink>
              </li>
              <li class="nav-item">
                <RouterLink to="/bill">Bill</RouterLink>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
  </div>

  <RouterView />
</template>

<style scoped>
</style>
