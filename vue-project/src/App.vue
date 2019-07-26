<template>
  <div id="app">
    <Header />
    <Checklist />
  </div>
</template>

<script>
import Header from './components/header';
import Checklist from './components/checklist';

export default {
  name: 'app',
  components: {
    Header,
    Checklist
  }
}
</script>

<style lang="scss">
  body{
    margin: 0;
    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */
    background-color: #232238;
  }
</style>