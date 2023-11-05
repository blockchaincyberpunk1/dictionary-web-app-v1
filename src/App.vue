<template>
  <div id="app">
    <Header />
    <!-- Passes the searchWord method directly to the event listener -->
    <WordInput @search="searchWord" />
    <!-- Conditional rendering based on the presence of word definitions -->
    <WordDefinition v-if="wordDefinitions.length" :definition="wordDefinitions[0]" />
    <!-- Conditional rendering based on the presence of an error -->
    <WordNotFound v-else :message="errorDetails" />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import WordInput from '@/components/WordInput.vue';
import WordDefinition from '@/components/WordDefinition.vue';
import WordNotFound from '@/components/WordNotFound.vue';

export default {
  name: 'App',
  components: {
    Header,
    WordInput,
    WordDefinition,
    WordNotFound,
  },
  data() {
    return {
      baseUrl: 'https://api.dictionaryapi.dev/api/v2/entries/en/',
      wordDefinitions: [],
      errorDetails: {},
    };
  },
  methods: {
    async searchWord(word) {
      // Clear previous state before new search
      this.wordDefinitions = [];
      this.errorDetails = {};

      try {
        const response = await fetch(`${this.baseUrl}${word}`);
        const data = await response.json();
        if (response.ok) {
          this.wordDefinitions = data;
        } else {
          this.errorDetails = {
            title: 'Word Not Found',
            message: 'The word you searched for could not be found.',
            resolution: 'Please try a different word.'
          };
        }
      } catch (error) {
        // Handle network errors or other unexpected issues
        this.errorDetails = {
          title: 'Error',
          message: 'An unexpected error occurred.',
          resolution: 'Please check your internet connection or try again later.'
        };
      }
    },
  },
}
</script>

<style>
/* ... No changes to the style ... */
</style>
