<template>
  <div class="main">
    <Button redirectTo="trivia">
      <img class="button-img" src="~/assets/svg/question.svg" alt="Trivia" />
    </Button>
  </div>
</template>

<script setup></script>

<style lang="scss">
body {
  background-color: $main_black;
  color: $white;
}

.main {
  width: 100%;
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1rem;
}
</style>
