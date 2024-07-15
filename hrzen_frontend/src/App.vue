<template>
  <v-app>
    <app-navbar @toggle-drawer="toggleDrawer" @logout="handleLogout" />
    <app-sidebar :drawer="drawer" @update-drawer="updateDrawer" />
    <router-view />
  </v-app>
</template>

<script>
import AppNavbar from '@/components/AppNavbar.vue';
import AppSidebar from '@/components/AppSidebar.vue';

export default {
  components: {
    AppNavbar,
    AppSidebar
  },
  data() {
    return {
      drawer: true
    };
  },
  methods: {
    toggleDrawer() {
      this.drawer = !this.drawer;
    },
    updateDrawer(value) {
      this.drawer = value;
    },
    handleLogout() {
      this.drawer = false; // Hide the sidebar on logout
    }
  }
};
</script>
