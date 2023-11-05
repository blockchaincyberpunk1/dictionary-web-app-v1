<template>
  <!-- Only render if meaning prop is provided -->
  <div v-if="meaning" class="word-meaning">
    <!-- Semantic use of <section> for distinct part of content -->
    <section class="part-of-speech">
      <!-- Use of <header> for introductory content -->
      <header>
        <h3>{{ meaning.partOfSpeech }}</h3>
        <div class="border"></div> <!-- Simplified border implementation -->
      </header>
    </section>

    <!-- Definitions list -->
    <section>
      <h4>Meaning</h4> <!-- Changed to h4 for proper heading hierarchy -->
      <ul class="meaning-list">
        <!-- Loop through definitions -->
        <li v-for="(definition, index) in meaning.definitions" :key="`definition-${index}`">
          {{ definition.definition }}
          <!-- Conditional rendering for example -->
          <em v-if="definition.example" class="example">"{{ definition.example }}"</em>
        </li>
      </ul>
    </section>

    <!-- Synonyms section -->
    <section v-if="meaning.synonyms.length">
      <h4>Synonyms</h4> <!-- Changed to h4 for proper heading hierarchy -->
      <p>{{ meaning.synonyms.join(', ') }}</p> <!-- Use of <p> for paragraph content -->
    </section>
  </div>
</template>

<script>
export default {
  name: 'WordMeaning',
  props: {
    meaning: {
      type: Object,
      required: true // Ensure that the prop is required
    }
  }
}
</script>

<style>
.word-meaning {
  margin-bottom: 40px;
}

/* Styling for part-of-speech section */
.word-meaning .part-of-speech header {
  display: flex;
  align-items: center; /* Align items vertically */
  margin-bottom: 20px;
}

/* Styling for the border after the part of speech */
.word-meaning .part-of-speech .border {
  flex-grow: 1;
  height: 1px;
  background-color: var(--hr-color);
  margin-left: 10px; /* Added margin for spacing */
}

/*   
.word-meaning ul.meaning-list {
   Add styles for the definitions list here 
}

  
.word-meaning ul.meaning-list li {
   Add styles for individual list items here 
} */

/* Styling for the example text */
.word-meaning .example {
  display: block;
  font-style: normal; /* Italic style removed for better readability */
  color: var(--grey-variant-1);
  margin-top: 8px; /* Adjusted margin for spacing */
}

@media screen and (max-width: 570px) {
  /* Responsive adjustments */
  /* Add responsive styles here */
}
</style>

