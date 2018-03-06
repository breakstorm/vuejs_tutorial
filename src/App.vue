<template>
  <div id="app">
    <input type='text' v-model='postBody' v-on:change='postPost()'>
    <button>just HTML TAG</button>
    <local-component></local-component>
    <global-component></global-component>
    <ul v-if='errors && errors.length'>
      <li v-for='error in errors'>{{ error.message }}</li>
    </ul>
    <ul v-if='posts && posts.length'>
      <li v-for='post in posts'>
        <p><strong>{{ post.title }}</strong></p>
        <p>{{ post.body }}</p>
      </li>
    </ul>
    
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'

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
      msg: 'Welcome to Your Vue.js App',
      posts: [],
      errors: [],
      postBody: ''
    }
  },
  created () {
    // try {
    //   const response = await axios.get('http://jsonplaceholder.typicode.com/posts')
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
    axios.get('http://jsonplaceholder.typicode.com/posts')
    .then(response => {
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e);
    })
  },
  methods: {
    // async postPost () {
    //   console.log('hello')
    //   const response = await axios.post('http://jsonplaceholder.typicode.com/posts', {
    //       body: this.postBody
    //     })
    //   if(!response) this.errors.push(e)
    //   console.log(response)
    // }
    postPost() {
      axios.post(`http://jsonplaceholder.typicode.com/posts`, {
        body: this.postBody
      })
      .then(response => {
        console.log(response)
      })
      .catch(e => {
        this.errors.push(e)
      })
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
