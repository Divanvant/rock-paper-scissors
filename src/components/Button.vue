<template>
  <button>
    <slot />
  </button>
</template>

<style scoped>
button {
  background: transparent;
  text-transform: uppercase;
  letter-spacing: 2px;
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.5em 1.75em;
  font-size: 1em;
  font-family: inherit;
  cursor: pointer;
  transition: border-color 0.25s;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

.btn-white-outlined {
  border: 1px solid #fff;
}
</style>
