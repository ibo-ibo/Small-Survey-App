<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadSurveys">{{ btnText }}</base-button>
      </div>
      <ul v-if="displayResults">
        <p v-if="error">Something went wrong :(</p>
        <p v-if="isLoading">Loading</p>
        <p v-if="!isLoading && !results">No stored result found.</p>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';
import BaseCard from '../UI/BaseCard.vue';

export default {
  components: {
    SurveyResult,
    BaseCard,
  },
  data() {
    return {
      results: [],
      displayResults: false,
      btnText: 'See Results',
      isLoading: false,
      error: false,
    };
  },
  methods: {
    async loadSurveys() {
      try {
        this.error = false;
        this.isLoading = true;
        this.displayResults = !this.displayResults;
        this.displayResults
          ? (this.btnText = 'Hide Results')
          : (this.btnText = 'See Results');
        const res = await fetch(
          `https://vue-app-b88b3-default-rtdb.europe-west1.firebasedatabase.app/surveys.json`
        );

        const data = await res.json();
        this.results = data;
        this.isLoading = false;
      } catch (err) {
        this.isLoading = false;
        this.error = true;
      }
    },
  },

  mounted() {
    this.loadSurveys();
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
