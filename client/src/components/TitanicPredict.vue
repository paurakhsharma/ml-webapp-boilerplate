<template>
  <div class="hello">
    <form @submit.prevent="predict">
      <label for="age">Age</label>
      <input type="number" id="age" placeholder="21" v-model="age">
      <label for="sex">Sex</label>
      <input type="text" id="sex" placeholder="female" v-model="sex">
      <label for="embarked">Embarked</label>
      <input type="text" id="embarked" placeholder="S" v-model="embarked">
      <button type="submit" @click.prevent='predict'>Predict</button>
    </form>
    <div class="result">
      <div
        class="survived"
        v-if="survived">
          <img src="../assets/undraw_joyride_hnno.png" alt="">
          <span class="result-msg">Survived</span>
        </div>
      <div 
        class="not-survived"
        v-if="notSurvived">
          <img src="../assets/undraw_feeling_blue_4b7q.png" alt="">
          <span class="result-msg">Not Survived</span>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TitanicPredict',
  props: {
    msg: String
  },
  data() {
    return {
      prediction: '',
      age: '',
      sex: '',
      embarked: ''
    }
  },
  methods: {
    predict() {
      this.axios
        .post('http://0.0.0.0:5000/predict', [
          {"Age": parseInt(this.age), "Sex": this.sex, "Embarked": this.embarked}
        ])
        .then((response) => {
          this.age = ''
          this.sex = ''
          this.embarked = ''
          this.prediction = parseInt(response.data.predictions[0])
      })
    }
  },
  computed: {
    survived() {
      return this.prediction === 1
    },
    notSurvived() {
      return this.prediction === 0
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped style>
.hello {
  height: 80vh;
  display: flex;
  align-items: center;
}

.hello form {
  display: flex;
  flex-direction: column;
  width: 40%;
  padding: 0 40px;
}

input {
  padding: 10px;
  border-radius: 5px;
  border: solid 1px #265741;
  box-shadow: 10px 15px 0.5;
  font-size: 18px;
}

label {
  margin-bottom: 5px;
  margin-top: 10px;
}

button {
  margin-top: 20px;
  padding: 15px;
  background: #42b983;
  border: none;
  border-radius: 5px;
  font-weight: 500;
  font-size: 24px;
  color: white;
  letter-spacing: 1.5px;
}

.result {
  display: flex;
  height: 100%;
  width: 100%;
  justify-content: center;
  align-items: center;
}

.survived {
  text-align: center;
  display: flex;
  flex-direction: column;
}

.not-survived {
  text-align: center;
  display: flex;
  flex-direction: column;
}

.result-msg {
  margin-top: 20px;
  font-size: 24px;
  padding: 10px;
  font-weight: 700;
}

</style>
