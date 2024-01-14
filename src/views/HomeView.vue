<template>
  <div class="home">
      <TransactionComp/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import TransactionComp from "@/components/TransactionsComp.vue";


@Options({
  components: {
      TransactionComp,
  },
})
export default class HomeView extends Vue {}
</script>
