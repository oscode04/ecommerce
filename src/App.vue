<template>
  <div id="app">
    <Man/>
    <!-- <Women style="display: none;"/> -->
    <!-- <NotAvail/> -->
  </div>
</template>

<script>
// import NotAvail from './components/NotAvail.vue'
import Man from './components/Man.vue';
// import Women from './components/Women.vue'

export default {
  name: 'App',
  components: {
    Man,
    // Women
// NotAvail
  }
}
</script>

