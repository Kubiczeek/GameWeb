<template>
  <NuxtLink class="button" :to="`/${redirectTo}`">
    <slot></slot>
  </NuxtLink>
</template>

<script setup>
defineProps(["redirectTo"]);
</script>

<style lang="scss">
.button {
  border-radius: 0.9rem;
  border: 3px solid $default;
  background-color: $main_black;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 87px;
  height: 87px;

  transition: all 0.2s ease-in-out;

  &:hover {
    border: 3px solid $hover;
  }

  &:hover > .button-img {
    filter: invert(54%) sepia(0%) saturate(2827%) hue-rotate(173deg)
      brightness(98%) contrast(85%);
  }
}

.button-img {
  width: 75%;
  height: 75%;
  filter: invert(17%) sepia(0%) saturate(0%) hue-rotate(232deg) brightness(104%)
    contrast(80%);

  transition: all 0.2s ease-in-out;
}
</style>
