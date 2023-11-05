<template>
  <!-- Conditionally render the wrapper only if definition exists -->
  <div v-if="definition" class="word-definition-wrapper">
    <!-- Main word and phonetic section -->
    <div class="word-main">
      <div class="word-and-phonetic">
        <!-- Display the word using h1 for semantic importance -->
        <h1>{{ definition.word }}</h1>
        <!-- Display the phonetics if available -->
        <p class="phonetics" v-if="phonetic.text">{{ phonetic.text }}</p>
      </div>
      <!-- Pronunciation component, only rendered if there's an audio source -->
      <div class="pronounce" v-if="phonetic.audio">
        <speak-word :url="phonetic.audio" />
      </div>
    </div>
    <!-- Loop through each meaning and pass it to the WordMeaning component -->
    <word-meaning
      v-for="(meaning, index) in definition.meanings"
      :key="`meaning-${index}`"
      :meaning="meaning"
    />
    <!-- Separator for styling -->
    <div class="horizontal-separator"></div>
    <!-- Source link, only shown if there are source URLs -->
    <p v-if="definition.sourceUrls.length" class="source">
      <span class="label">Source:</span>
      <!-- Link to the first source URL -->
      <a :href="definition.sourceUrls[0]" target="_blank" class="link">
        {{ definition.sourceUrls[0] }}
        <!-- External link icon -->
        <svg class="icon-external-link" xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 14 14">
          <path fill="none" stroke="#838383" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M6.09 3.545H2.456A1.455 1.455 0 0 0 1 5v6.545A1.455 1.455 0 0 0 2.455 13H9a1.455 1.455 0 0 0 1.455-1.455V7.91m-5.091.727 7.272-7.272m0 0H9m3.636 0V5"/>
        </svg>
      </a>
    </p>
  </div>
</template>

<script>
import WordMeaning from '@/components/WordMeaning.vue';
import SpeakWord from '@/components/SpeakWord.vue';

export default {
  name: 'WordDefinition',
  components: {
    WordMeaning,
    SpeakWord
  },
  props: {
    definition: Object // Assume definition is always provided for simplicity
  },
  computed: {
    // Compute the phonetic details, preferring ones with audio
    phonetic() {
      return this.definition.phonetics?.find(p => p.audio) || { text: this.definition.phonetic, audio: '' };
    }
  }
};
</script>

<style>
/* Styles are simplified for clarity */
.word-definition-wrapper .word-main {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 40px;
}

.word-definition-wrapper .word-and-phonetic h1 {
  font-size: 4.48rem;
  line-height: 5.46rem;
  margin-bottom: 8px;
}

.word-definition-wrapper .word-and-phonetic p.phonetics {
  font-size: 1.58rem;
  line-height: 2.1rem;
  color: var(--purple);
}

.word-definition-wrapper .horizontal-separator {
  border-bottom: 1px solid var(--hr-color);
  margin-bottom: 20px;
}

.word-definition-wrapper .source {
  text-decoration: underline;
}

.word-definition-wrapper .source .label {
  color: var(--grey-variant-1);
  margin-right: 20px;
}

.word-definition-wrapper .source .link {
  color: var(--text-color);
}

.word-definition-wrapper .source .icon-external-link {
  vertical-align: middle;
  margin-left: 10px;
}

@media screen and (max-width: 570px) {
  .word-definition-wrapper .word-and-phonetic h1 {
    font-size: 2.56rem;
    line-height: 3.2rem;
  }
}
</style>
