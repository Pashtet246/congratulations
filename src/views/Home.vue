<template>
  <div class="home">
    <Header/>
    <Congratulations/>
  </div>
</template>

<script>
import Congratulations from '@/components/Congratulations.vue';

export default {
  name: 'home',
  components: {
    Congratulations
  },
};
</script>
