<template>
  <div class="order-item-form">
    <div class="form-group">
      <label>ArticleCode</label>
      <input v-model="orderItem.ArticleCode" type="text" class="form-control" />
    </div>
    <div class="form-group">
      <label>ArticleName</label>
      <input v-model="orderItem.ArticleName" type="text" class="form-control" />
    </div>
    <div class="form-group">
      <label>Quantity</label>
      <input v-model="orderItem.Quantity" type="number" class="form-control" />
    </div>
    <div class="form-group">
      <label>UnitPrice</label>
      <input v-model="orderItem.UnitPrice" type="text" class="form-control" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, watch, defineEmits } from "vue";
import { OrderItem } from "../interfaces/OrderItem";

const orderItem: OrderItem = reactive({
  ArticleCode: "",
  ArticleName: "",
  Quantity: 0,
  UnitPrice: 0,
});

const emit = defineEmits(["orderItemUpdated"]);

watch(
  () => ({ ...orderItem }),
  (orderItemVal) => {
    emit("orderItemUpdated", orderItemVal);
  }
);
</script>

<style scoped>
.order-item-form {
  align-content: center;
  display: flex;
}
.form-group {
  margin-bottom: 10px;
}
</style>
