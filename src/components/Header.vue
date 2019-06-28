<template>
  <div class="header">
    <h1 class="title">instaquotes</h1>
  </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style scoped lang="scss">
  .header {
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    position: fixed;
    top: 0;
    left: 0;
    background: #FFF;
  .title {
    padding: 30px;
    margin: 0;
    font-size: 20px;

    color: #333;
  }

  }
</style>
