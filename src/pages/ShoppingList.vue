<template>
  <q-card-section class="row text-center">
    <q-card-section class="col text-h4 text-primary">
      {{ header || "welCome" }}
    </q-card-section>
  </q-card-section>
</template>

<script>
export default {
  name:"ShoppingList",
  title:"쇼핑 리스트",
  data(){
    return {
      header:"Shopping List App"
    }
  }
}
</script>

<style>

</style>
