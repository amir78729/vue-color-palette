<template>
  <div class=" container bg-light">
    <button @click="changeColor" class="btn btn-primary">change color</button>
    <div id="h" style="height: 100px; width: 100px; background-color: black"></div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      colors: ['#FFEE00']
    }
  },
  methods: {
    changeColor () {
      document.getElementById('h').style.backgroundColor = this.colors[0]
    }
  }
}
</script>

<style>

</style>
