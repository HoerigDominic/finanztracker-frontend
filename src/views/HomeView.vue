<template>
  <div class="home">
    <TransAction/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HelloWorldTwo from "@/components/TransAction.vue";
import TransAction from "@/components/TransAction.vue";
import OffCanvas from "@/components/OffCanvas.vue";

@Options({
  components: {
      OffCanvas,
      TransAction
  },
})
export default class HomeView extends Vue {}
</script>
