<template>
  <button :class="mode">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ["mode"]
};
</script>

<style scoped>
button {
  padding: 0.75rem 2rem;
  min-width: 7rem;
  font-family: inherit;
  font-size: 1rem;
  background-color: #3a0061;
  border: 1px solid #3a0061;
}

button:hover,
button:active {
  background-color: #270041;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #3a0061;
  border-color: #270041;
}

.flat:hover,
.flat:active {
  background-color: #edd2ff;
}
</style>
