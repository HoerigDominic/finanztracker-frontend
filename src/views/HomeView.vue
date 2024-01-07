<template>
  <div class="home">
      <NavBar/>
      <TransactionComp/>
  </div>
</template>

<script lang="ts">
//import TransactionCreate from "@/components/TransactionCreate.vue";
import { Options, Vue } from 'vue-class-component';
import NavBar from "@/components/Navbar.vue";
import TransactionComp from "@/components/TransactionsComp.vue";


@Options({
  components: {
      NavBar,
      TransactionComp,
  },
})
export default class HomeView extends Vue {}
</script>
