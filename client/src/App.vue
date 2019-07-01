<template>
  <div id="app">
    <h1 class="title">Titanic Survivor Predictor</h1>
    <TitanicPredict/>
  </div>
</template>

<script>
import TitanicPredict from './components/TitanicPredict.vue'

export default {
  name: 'app',
  components: {
    TitanicPredict
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: 0;
  font-family: 'Montserrat', sans-serif;
}

.title {
  text-align: center;
  margin-top: 40px;
  margin-bottom: -20px;
}

</style>
