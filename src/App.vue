<template>
  <div id="app">
    <TheHeader :user="user"></TheHeader>
    <router-view class="container"></router-view>
    <TheFooter></TheFooter>
  </div>
</template>

<script>
import TheHeader from '@/components/layout/TheHeader'
import TheFooter from '@/components/layout/TheFooter'

export default {
  name: 'app',
  components: { TheHeader, TheFooter },

  data() {
    return {
      boardName: '',
    }
  },
}
</script>

<style lang="scss" scoped>
#app {
  box-sizing: border-box;
  color: #37474f;
  font-family: 'Lato', Helvetica, Arial, sans-serif;
  margin: 0 auto;
  padding: 0;
  text-align: center;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
}

.container {
  padding-bottom: 4rem;
}
</style>
