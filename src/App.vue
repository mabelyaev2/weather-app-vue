<template>
    <div class="weather-app">
      <Form></Form>
  </div>
</template>

<script>
import Form from './Form'

export default {
  components: {
    Form
  }
}
</script>

<style lang="css">

body {
  padding: 0;
  margin: 0;
  width: 100%;
  height: auto;
  background: url('~@/assets/sky.svg') no-repeat;
}

</style>

