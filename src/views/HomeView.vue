<template>
  <div class="home">
      <Navbar/>
    <TransactionsList/>
      <TransaktionCreateEinnahme/>
      <TransaktionCreateAusgabe/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import TransactionsList from "@/components/TransactionsList.vue";
import TransaktionCreateEinnahme from "@/components/TransaktionCreateEinnahme.vue";
import Navbar from "@/components/Navbar.vue";
import TransaktionCreateAusgabe from "@/components/TransaktionCreateAusgabe.vue";

@Options({
  components: {
      TransaktionCreateAusgabe,
      Navbar,
      TransaktionCreateEinnahme,
      TransactionsList
  },
})
export default class HomeView extends Vue {}
</script>
