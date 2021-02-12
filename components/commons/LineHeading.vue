<style scoped>
.header-text::before,
.header-text::after {
  content: '';
  background: #000;
  height: 0.1em;
  flex: 1;
}
.header-text::before {
  margin-left: 0;
  margin-right: 1em;
}
.header-text::after {
  margin-right: 0;
  margin-left: 1em;
}
</style>

<template>
  <div class="header-text w-full flex items-center">
    <slot></slot>
  </div>
</template>
