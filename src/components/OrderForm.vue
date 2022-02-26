<template>
  <div class="order-form">
    <form>
      <template v-for="(_, index) in items" :key="index">
        <OrderItemForm @orderItemUpdated="updateItem(index, $event)" />
      </template>
      <Button @click="addItem"> + Add order item </Button>
      <div>
        <label>To version tests :D </label>
        <select class="form-control" v-model="version">
          <option>v1</option>
          <option>v2</option>
          <option>v3</option>
        </select>
        <Button @click="finishOrder"> {{ finishText }} </Button>
      </div>
    </form>
    <div class="result">
      <pre>{{ result }}</pre>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from "vue";
import OrderItemForm from "./OrderItemForm.vue";
import Button from "./Button.vue";
import { OrderItem } from "../interfaces/OrderItem";

const finishText = ref("Finish order");
const result = ref({});
const version = ref("v1");
const items: Partial<OrderItem>[] = reactive([{}]);
const addItem = () => items.push({});
const updateItem = (index, item) => (items[index] = { ...item });
const finishOrder = async () => {
  finishText.value = "Saving order...";

  // Configure a service with these params preseted
  const headers = new Headers();
  headers.append("Content-type", "application/json");
  headers.append("Accept", "application/json");
  // Configure env to key API_URL
  const response = await fetch(`http://localhost/api/orders/${version.value}`, {
    method: "POST",
    body: JSON.stringify(items),
    headers,
  });

  result.value = await response.json();
  finishText.value = "Finish order";
};
</script>

<style scoped>
pre {
  color: white;
  margin-top: 30px;
  padding-left: 20px;
  border-left: 10px solid #333;
  background-color: #555;
}
</style>
