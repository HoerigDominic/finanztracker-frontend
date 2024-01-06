<template>
  <div class="home">
      <Navbar/>
      <TransactionsList/>
      <TransactionCreate/>
  </div>
</template>

<script lang="ts">
import TransactionCreate from "@/components/TransactionCreate.vue";
import Navbar from "@/components/Navbar.vue";
import { Options, Vue } from 'vue-class-component';
import TransactionsList from "@/components/TransactionsList.vue";


@Options({
  components: {
      Navbar,
      TransactionsList,
      TransactionCreate
  },
})
export default class HomeView extends Vue {}
</script>
