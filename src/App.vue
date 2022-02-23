<template>
  <div>
    <MainPage />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MainPage from './components/MainPage.vue'

export default defineComponent({
  name: 'App',
  components: {
    MainPage,
  },
  setup() {
    // Setup

  },
});
</script>

<style lang="scss" module>
// Style
body{
  overflow: hidden;
}
</style>
