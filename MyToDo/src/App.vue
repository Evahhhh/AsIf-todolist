<template>
  <body class="page">
    <div class="sidebar">
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/img/logo2.png"
        width="150"
      />
      <NewTask />
    </div>
    <div class="content">

      <Sort />
      <DisplayList />

    </div>
  </body>
</template>

<style scoped>
.page{
  display: flex;
}

.sidebar{
  background-color: #34DA9F;
  flex-basis: 25%;
  padding: 20px;
  display : flex;
  align-items: center;
  flex-direction : column;
  gap : 30px;
}

.content{
  flex-basis: 75%;
  padding: 20px;
}
</style>

<script>
import Sort from './components/Sort.vue';
import NewTask from './components/NewTask.vue';
import DisplayList from './components/DisplayList.vue';

export default {
  components: {
    Sort,
    NewTask,
    DisplayList,
  },
};
</script>
