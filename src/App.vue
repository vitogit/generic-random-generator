<template>
  <div id="app">

    <div class="container">
      <generator
        :name="generator.name"
        v-for="(generator, index) in generators"
        :key="index"/>
        <br>
        <button @click="newGenerator" class="button">Nuevo generador </button>
    </div>

  </div>
</template>

<script>
import generator from './generator.vue'

export default {
  name: 'app',
  components: {generator},
  data () {
    return {
      generators: [{name:'Generador NPC'}]
    }
  },
  methods: {
    newGenerator: function() {
      this.generators.push({})
    },
    saveGenerator: function() {
      
    }
  }
}
</script>

<style>

</style>
