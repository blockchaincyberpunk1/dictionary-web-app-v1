<template>
  <!-- Input wrapper with dynamic class binding for error state -->
  <div class="input-wrapper" :class="{ 'has-error': attemptedEmptySearch }">
    <input
      type="text"
      placeholder="Search for any word..."
      v-model.trim="word"
      @keyup.enter="validateWordAndSearch"
      :aria-describedby="attemptedEmptySearch ? 'inputError' : undefined"
    />
    <div id="inputError" class="error-message" v-if="attemptedEmptySearch">
      Whoops, can't be empty…
    </div>
  </div>
</template>

<script>
export default {
  name: 'WordInput',
  data() {
    return {
      word: '', // The word to be searched
      attemptedEmptySearch: false, // Tracks if a search was attempted with an empty input
    };
  },
  methods: {
    validateWordAndSearch() {
      // Reset error state
      this.attemptedEmptySearch = !this.word;
      // If the word is not empty, emit the search event
      if (this.word) {
        this.$emit('search', this.word);
      }
    }
  }
};
</script>

<style>
.input-wrapper {
  position: relative;
  margin-bottom: 15px;
}

.input-wrapper.has-error input[type="text"] {
  border-color: var(--red); /* Error state border color */
}

/* .input-wrapper input[type="text"] {
 Add style to the input so that it looks like a search input.
} */

/* Error message styling */
.input-wrapper .error-message {
  color: var(--red);
  position: absolute;
  top: 100%;
  left: 0;
  font-size: 0.85rem; /* Smaller font size for error message */
}

@media screen and (max-width: 570px) {
  /* Responsive styling adjustments remain unchanged */
}
</style>
