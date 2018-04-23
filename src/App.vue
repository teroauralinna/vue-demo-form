<template>
  <div id="app" class="container">
    <div class="row justify-content-center">
      <div class="col-xs-12 col-sm-10 col-md-6">
        <h1 class="text-center">{{title}}</h1>
        <app-form></app-form>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Form from './components/form/Form.vue';

export default {
  name: 'app',
  data () {
    return {
      title: 'Vue.js Demo Form'
    }
  },
  components: {
    appForm: Form
  }
}
</script>

<style lang="scss">
  h1 {
    margin-bottom: 30px;
  }

  #app {
    padding: 20px;
  }
</style>
