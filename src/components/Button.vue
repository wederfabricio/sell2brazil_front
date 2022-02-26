<template>
  <button type="button" class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  margin-bottom: 10px;
  border: 2px solid #ccc;
  color: #272727;
  background: white;
  padding: 5px 10px;
}
</style>
