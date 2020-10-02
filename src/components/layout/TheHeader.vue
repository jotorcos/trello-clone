<template>
  <header>
    <span class="title">Vue Trello</span>
  </header>
</template>

<script>
export default {
  name: 'TheHeader',
}
</script>

<style lang="scss" scoped>
header {
  box-sizing: border-box;
  background-color: rgb(20, 103, 182);
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  margin: 0;
  padding: 1rem;

  .title {
    align-self: center;
    color: white;
    font-size: 1.2rem;
    font-weight: bold;
    margin-right: 1rem;
  }
}
</style>
