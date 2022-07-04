<template>
  <button>
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  font: inherit;
  border: 1px solid #ffc9c9;
  background-color: #ffc9c9;
  color: #212529;
  padding: 0.5rem 2rem;
  cursor: pointer;
  border-radius: 4px;
}

button:hover,
button:active {
  background-color: #ffa8a8;
  border-color: #ffa8a8;
}
</style>
