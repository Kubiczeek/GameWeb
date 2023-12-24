<template>
  <span>
    <slot />
  </span>
</template>

<script setup></script>

<style lang="scss" scoped>
span {
  display: inline;
  font-size: 2rem;
  color: $default;
  width: 50%;
  font-weight: 400;
  border: 3px solid $default;
  border-radius: 6px;
  background-color: $main_black;
  text-align: center;
  transition: all 0.2s ease-in-out;

  &:hover {
    border: 3px solid $hover;
    color: $hover;
    cursor: pointer;
  }
}
</style>
