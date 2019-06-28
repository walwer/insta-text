<template>
  <div class="center">
    <p>Done!</p>
    <div class="btn" @click="reload">
      <span>Make another one!</span>
    </div>
  </div>
</template>

<script>
    export default {
        name: "_step2",
        methods: {
            reload: function () {
                window.location.reload();
            }
        }
    }
</script>

<style scoped>

</style>
