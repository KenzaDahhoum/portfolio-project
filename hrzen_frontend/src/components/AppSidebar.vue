<template>
  <v-navigation-drawer app v-model="drawerInternal" permanent>
    <v-list dense>
      <v-list-item to="/" router exact>
        <v-list-item-icon>
          <v-icon color="primary">mdi-home</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Home</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item to="/employees" router exact>
        <v-list-item-icon>
          <v-icon color="primary">mdi-account</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Employees</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item to="/attendance" router exact>
        <v-list-item-icon>
          <v-icon color="primary">mdi-checkbox-marked-circle-outline</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Attendance</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item to="/calendar" router exact>
        <v-list-item-icon>
          <v-icon color="primary">mdi-calendar</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Calendar</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item to="/payroll" router exact>
        <v-list-item-icon>
          <v-icon color="primary">mdi-cash</v-icon>
        </v-list-item-icon>
        <v-list-item-content>
          <v-list-item-title>Payroll</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script>
export default {
  name: 'AppSidebar',
  props: {
    drawer: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    drawerInternal: {
      get() {
        return this.drawer;
      },
      set(value) {
        this.$emit('update-drawer', value);
      }
    }
  }
};
</script>

<style scoped>
.v-list-item--active {
  background-color: #e0e0e0 !important;
}
</style>
