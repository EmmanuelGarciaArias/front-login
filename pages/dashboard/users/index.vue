<template>
    <RegisterVue>
  </template>
  
  <script>
import RegisterVue from '~/components/users/RegisterVue.vue';
  export default {
    name: "Index",
    auth: true,
    layout: "DashboardVue",
    components: { RegisterVue }
}
  </script>
  