<template>
  <div>
    <Suspense>
      <!-- <template #default> -->
      <AsyncCityView />
      <!-- </template> -->
      <template #fallback>
        <div class="container mt-5">
          <CityViewSkeleton />
        </div>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from '../components/AsyncCityView.vue';
import CityViewSkeleton from '../components/CityViewSkeleton.vue';


</script>

<style lang="scss" scoped></style>