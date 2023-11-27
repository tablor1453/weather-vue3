<template>
  <div>
    <Suspense>
      <!-- <template #default> -->
      <AsyncCityView />
      <!-- </template> -->
      <template #fallback>
        loading...
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from '../components/AsyncCityView.vue';


</script>

<style lang="scss" scoped></style>