<template>
  <div>
    <Button class="return-button" redirectTo="">
      <img class="button-img" src="~/assets/svg/arrow.svg" />
    </Button>
  </div>
  <slot />
</template>

<script setup></script>

<style lang="scss" scoped>
div {
  width: 100%;
  display: flex;
  align-items: center;
}

.return-button {
  margin: 10px;
  width: 57px;
  height: 57px;
}
</style>
