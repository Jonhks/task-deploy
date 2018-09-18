<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <jm-menu></jm-menu>
    <jt-title></jt-title>
    <jf-form></jf-form>
  </div>
</template>

<script>
import jtTitle from './components/Title.vue'
import JmMenu from './components/Menu.vue'
import JfForm from './components/Form.vue'


export default {
  name: 'app',
  data () {
    return { 

    }
  },
  components: { jtTitle, JmMenu, JfForm }

}
</script>

<style lang="scss">
@import './sass/main.scss';


</style>
