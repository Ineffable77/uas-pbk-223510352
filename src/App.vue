<template>
  <q-layout>
    <q-header elevated class="kepala">
      <Navbar />
    </q-header>

    <q-page-container class="badan">
      <router-view />
    </q-page-container>
  </q-layout>

  <footer class="q-pa-md text-center dark text-white footer-blur">
    <div class="q-mb-md">© 2024 RandyIvando.com All Rights Reserved.</div>
    <div class="text-caption">JL. Kubang Raya | email@gmail.com | telpon 08********</div>
  </footer>
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  name: 'App',
  nama: 'Footer',
  components: {
    Navbar
  }
};
</script>

<style scoped>
.kepala {
  background-color: rgba(0, 0, 0, 0.5);
  backdrop-filter: blur(3px);
}


.footer-blur {
  background-color: rgba(0, 0, 0, 0.5); 
  backdrop-filter: blur(3px); 
}
</style>
