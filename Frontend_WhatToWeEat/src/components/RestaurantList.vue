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
      <div
        class="border flex cursor-pointer hover:bg-wte-bg ease-in duration-200"
        @click="showDetailModel(item)"
      >
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

  <!--Click restaurant show detail modal-->
  <n-modal v-model:show="isDetailModal">
    <n-card
      style="width: 600px"
      :bordered="false"
      size="huge"
      role="dialog"
      aria-modal="true"
    >
      <h2>
        {{ currentRest.value.name }}
      </h2>
      <div class="flex justify-center py-5">
        <img
          src="@/assets/foodEmpty.jpg"
          alt="food"
          class="bg-cover flex-none w-3/5"
        >
      </div>

      <p>{{ currentRest.value.address }}</p>
      <p>{{ currentRest.value.phone }}</p>
      <div class="flex justify-end w-full gap-2">
        <n-button
          type="primary"
          class="ml-auto bg-wte-primary"
        >
          編輯
        </n-button>
        <n-button
          type="error"
          class="bg-wte-danger"
        >
          刪除
        </n-button>
      </div>
    </n-card>
  </n-modal>
</template>

<script setup>
import { onBeforeMount, ref, reactive } from "vue";
import { NGrid, NGi, NButton, NModal, NCard } from "naive-ui";
import { useStore } from "../store/main";
const store = useStore();
const isDetailModal = ref(false); //點擊檢視該餐廳詳細訊息
const currentRest = reactive({ value: {} }); //當前點選到的餐廳

onBeforeMount(() => {
  store.getRestaurantData();
});

function showDetailModel(item) {
  currentRest.value = item;
  isDetailModal.value = true;
}
</script>
<style scoped>
.truncate-3 {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
</style>
