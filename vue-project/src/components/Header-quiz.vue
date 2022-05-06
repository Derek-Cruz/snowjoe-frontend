<template>
  <div class="quiz-header">
    <div class="quiz-text">
      <p class="p-styling">{{ header }}</p>
    </div>
  </div>
</template>

<script>

  export default {
    props: ['header']
  }

</script>

<style>
  .quiz-header {
    top: 0px;
    display: flex;
    height: 55px;
    width: 100%;
    background-color: #860707;
    position: fixed;
  }

  .quiz-text {
    margin-left: 58px;
    font-size: 1.2rem;
    font-family: sans-serif;
    display: flex;
    align-items: center;
    color: white;
  }

  .p-styling {
    margin: 0;
  }
</style>
