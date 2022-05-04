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
    display: flex;
    height: 55px;
    background-color: #860707;
  }

  .quiz-text {
    margin-left: 40px;
    font-size: 1rem;
    font-family: sans-serif;
    display: flex;
    align-items: center;
    color: white;
  }

  .p-styling {
    margin: 0;
  }
</style>
