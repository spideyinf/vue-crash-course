<template>
  <div class="wrapper">
    <button v-on:click="increase">Increase</button>
    <p>{{ counter }}</p>
    <p v-on:mousemove="updateCoordinates">
      Coordinates: {{ x }} / {{ y }}
      - <span v-on:mousemove.stop="">DEAD AREA</span>
    </p>
    <input type="text" v-on:keyup.enter.space="alertMe">
    <p v-if="show">To see or not to see</p>
    <p v-else>Now you see me</p>
    <button @click="show = ! show">Switch</button>
  </div>
</template>

<script>
  export default {
    name: 'Counter',
    data() {
      return {
        counter: 1,
        x: 0,
        y: 0,
        show: true,
      }
    },
    methods: {
      increase: function() {
        this.counter++
      },
      updateCoordinates: function(event) {
        this.x = event.clientX
        this.y = event.clientY
      },
      alertMe: function() {
        alert('Alert!')
      }
    },
  }
</script>

<style scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    max-width: 768px;
    margin: 24px auto;
  }
</style>
