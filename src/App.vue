<template>
  <div id="nav">
    <Navbar/>
  </div>
  <router-view/>
</template>

<script>
import Navbar from '@/components/Navbar'

export default ({
  components: {
    Navbar,
  },
})
</script>


<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@500&display=swap');
#app {
  font-family: 'Quicksand', sans-serif;
  color: #2c3e50;
}
</style>
