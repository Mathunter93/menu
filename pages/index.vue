<template>
  <Login v-if="!logged"/>
  <Home  v-else/>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  data() {
    let logged = Boolean
    return {
      logged: false
    }
  },
  mounted(): Boolean {
    if (localStorage.getItem("menu_user") === null) {
      return this.logged = false
    }else {
      let logged_in = localStorage.getItem("menu_user")
      return this.logged = true
    }
  }
})
</script>
