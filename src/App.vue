<template>
  <div id="app">
    <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"
      :selectLocal="selectLocal"
      :selectAPI="selectAPI"
      :localIsSelected="localIsSelected"
      :APIIsSelected="APIIsSelected"
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">

        <div v-if="isIntroVisible" class="introWrapper">
          <h2>Please select which type of questions</h2>

          <button 
          @click="selectLocal" 
          :class='localIsSelected ? "questionSourceButtonSelected" : ""'
          >Local Questions
          </button>

          <button 
            @click="selectAPI" 
            :class='APIIsSelected ? "questionSourceButtonSelected" : ""'
          >API Questions
          </button>

        </div>

          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import {DB} from './DB.js'
export default {
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data() {
    return {
      DB: DB,
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      localIsSelected: false,
      APIIsSelected: false,
      isIntroVisible: true,
    }
  },
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    },
    selectLocal() {
      this.localIsSelected = true
      this.APIIsSelected = false
      this.isIntroVisible = false
      console.log(DB);
      this.questions = DB

    },
    selectAPI() {
     this.APIIsSelected = true
     this.localIsSelected = false
     this.isIntroVisible = false
      fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
        method: 'get'
      })
        .then((response) => {
          return response.json()
        })
        .then((jsonData) => {
          this.questions = jsonData.results
          console.log(this.questions);
        })
    }
  },
  mounted: function() {

    // if (this.localIsSelected){
    //   fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
    //     method: 'get'
    //   })
    //     .then((response) => {
    //       return response.json()
    //     })
    //     .then((jsonData) => {
    //       this.questions = jsonData.results
    //       console.log(this.questions);
    //     })
    // } 

  // if (this.APIIsSelected){
  //   console.log(DB);
  //   this.questions = DB
  // }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.questionSourceButtonSelected {
  background-color: green;
}

</style>