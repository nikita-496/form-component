<template>
  <main class="main">
    <sign-up/>
  </main>
</template>

<script>
import SignUp from './components/SignUp.vue'

export default {
  name: 'App',
  components: {
    SignUp
  }
}
</script>

<style scoped lang="scss">
body{
  width:100%;
  .main{  
    @media(min-width: 360px){
      padding: 0em calc(10vw - 18px);
    }
    @media(min-width: 420px){
      padding: 0em calc(10vw - 10px);
    }
    @media(min-width: 480px){
      padding: 0em calc(50vw - 200px);
    }
    @media(min-width: 630px){
      padding: 0em calc(50vw - 230px);
    }
  }
}
</style>

