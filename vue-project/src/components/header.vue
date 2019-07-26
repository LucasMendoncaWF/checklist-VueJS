<template>
  <div id="header">
    <div class="logo">LogoEx</div>
    <Links />
  </div>
</template>

<script>
import Links from './links';

export default {
  name: 'Header',
  components:{
      Links
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      UOU: 'dwaadawd'
    }
  }
}
</script>

<style lang="scss">
    #header{
        position: sticky;
        background: #58147b;
        padding: 20px;
        display: flex;
        flex-wrap: wrap;

        .logo{
            color:white;
            font-family: Arial;
            font-weight: 700;
            font-size: 28px;
            cursor: pointer;

            &:hover{
                opacity: 0.6;
            }
        }
    }
</style>
