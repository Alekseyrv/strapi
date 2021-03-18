<template>
  <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      <li v-for="item in items" :key="items.id" :class="{ 'in' : (item.descr == 'In office'), 'out' : (item.descr == 'working from home') }">
      {{ item.name +' ' + item.descr }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      items: [],
      error: null
    }
  },
  async mounted () {
    try {
      this.items = await this.$strapi.$items.find()
    } catch (error) {
      this.error = error
    }
  }
}
</script>


<style>
ul{
  list-style: none;
  padding-left: 0;
}
li {
  padding-bottom: 5px;
}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: left;
  font-family:
    'Helvetica Neue',
    sans-serif;
  font-weight: 300;
}
.out {
  color: red;
}
.in {
  color: green;
}
</style>
