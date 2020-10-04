
<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
      <b-nav-item disabled>Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>

      <!-- <button 
        @click="selectLocal" 
        :class='localIsSelected ? "questionSourceButtonSelected" : ""'
      >Local Questions
      </button>

      <button 
        @click="selectAPI" 
        :class='APIIsSelected ? "questionSourceButtonSelected" : ""'
      >API Questions
      </button> -->

    </b-nav>
  
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect',
    'numTotal'
  ],
  methods: {
    selectLocal() {
      this.localIsSelected = true
      this.APIIsSelected = false
    },
    selectAPI() {
     this.APIIsSelected = true
     this.localIsSelected = false
    }
  },
  data: function () {
    return {
      localIsSelected: false,
      APIIsSelected: false,
    }
  }
}
</script>

<style scoped>
/* .questionSourceButtonSelected {
  background-color: green;
} */

</style>