<template>
  <n-grid
    x-gap="12"
    y-gap="12"
    cols="1 m:2 xl:3 "
    responsive="screen"
  >
    <n-gi
      v-for="item in store.restaurantList"
      :key="item.id"
    >
      <div class="border flex">
        <img
          src="@/assets/foodEmpty.jpg"
          alt="food"
          class="w-28 bg-cover flex-none"
        >
        <div
          class="flex flex-col h-28 p-2"
          style="min-width: 0px"
        >
          <div class="flex-[0_0_30%]">
            <h4 class="truncate">
              {{ item.name }}
            </h4>
          </div>
          <div class="flex-[0_0_40%]">
            <p class="truncate-3">
              {{ item.address }}
            </p>
          </div>

          <div class="flex-[0_0_20%] flex items-center pt-1">
            <n-button
              type="primary"
              ghost
              class="h-full p-1"
            >
              {{ item.phone }}
            </n-button>
          </div>
        </div>
      </div>
    </n-gi>
  </n-grid>
</template>

<script setup>
import { onBeforeMount } from "vue";
import { NGrid, NGi, NButton } from "naive-ui";
import { useStore } from "../store/main";
const store = useStore();

onBeforeMount(() => {
  store.getRestaurantData();
});
</script>
<style scoped>
.truncate-3 {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
</style>
