<template>
  <div>
    <button v-on:click="increase">Increase</button>
    <p>{{ counter }}</p>
    <p v-on:mousemove="updateCoordinates">
      Coordinates: {{ x }} / {{ y }}
      - <span v-on:mousemove.stop="">DEAD AREA</span>
    </p>
    <input type="text" v-on:keyup.enter.space="alertMe">
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
