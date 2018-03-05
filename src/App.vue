<template>
  <div id="app">
    <button>just HTML TAG</button>
    <local-component></local-component>
    <global-component></global-component>
  </div>
</template>

<script>
import Vue from 'vue'

Vue.component('global-component', {
  template: `<div>A global component</div>`
})

var cmp = {
  template: `<div>A local component</div>`
}


export default {
  name: 'app',
  components: {
    'local-component': cmp
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
