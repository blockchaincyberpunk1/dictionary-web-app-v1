<template>
  <!-- Conditional rendering based on the presence of a title in the message object -->
  <section v-if="message.title" class="message-wrapper" aria-live="polite">
    <!-- Use of aria-live for accessibility, to announce dynamic content changes -->
    <h1 aria-hidden="true">😕</h1> <!-- Emoji is decorative; hence, aria-hidden is true -->
    <h2>{{ message.title }}</h2> <!-- Changed to h2 for proper heading hierarchy -->
    <p>{{ message.message }}</p>
    <p class="resolution">{{ message.resolution }}</p>
  </section>
</template>

<script>
export default {
  props: {
    message: {
      type: Object,
      default: () => ({}) // Provide a default empty object
    }
  },
}
</script>

<style>
.message-wrapper {
  text-align: center;
  padding: 2rem; /* Added padding for better spacing */
}

.message-wrapper h1 {
  font-size: 6rem; /* Increased size for better visibility */
  margin-bottom: 1rem; /* Adjusted margin for consistent spacing */
}

.message-wrapper h2 {
  font-size: 1.6rem; /* Adjusted font size for better readability */
  margin-bottom: 1rem; /* Consistent margin spacing */
}

.message-wrapper p {
  font-size: 1.2rem; /* Standardized font size */
  margin-bottom: 1rem; /* Consistent margin spacing */
}

.message-wrapper .resolution {
  font-style: italic; /* Styling for resolution to differentiate it */
}
</style>
