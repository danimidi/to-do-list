<template>
  <button>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "icon-button",
};
</script>

<style scoped>
button {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  color: var(--primary-color);
  background-color: white;
  margin-right: 8px;
}
button:hover {
  background-color: var(--light-green);
}
</style>
