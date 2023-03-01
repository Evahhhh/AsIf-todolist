<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/img/logo.png"
      width="100"
    />
  </header>
  <main>
    <NewTask />
  </main>
</template>

<style scoped>
header{
  background-color: #34DA9F;
  display: flex;
  justify-content: center;
  padding: 10px;
}
</style>

<script setup>
import NewTask from './components/NewTask.vue';
</script>
