<template>
  <!-- Main container for the header -->
  <div class="header">
    <!-- Logo of the application -->
    <img src="@/assets/images/logo.svg" class="logo" alt="logo" />
    <!-- Container for settings which includes font selector and theme toggler -->
    <div class="settings">
      <!-- Font selector component for choosing fonts -->
      <font-selector />
      <!-- A vertical line separator for visual distinction between components -->
      <div class="vertical-separator"></div>
      <!-- Theme toggler component for switching themes -->
      <theme-toggler />
    </div>
  </div>
</template>

<script>
// Importing the necessary child components
import FontSelector from '@/components/FontSelector.vue';
import ThemeToggler from '@/components/ThemeToggler.vue';

export default {
  name: 'Header',
  components: {
    // Registering child components for use in the template
    FontSelector,
    ThemeToggler,
  },
};
</script>

<style>
/* Base styles for the header */
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 50px;
}

/* Styles for the settings container */
.header .settings {
  display: flex;
  align-items: center;
}

/* Styles for the vertical separator */
.header .settings .vertical-separator {
  width: 1px;
  height: 34px;
  background-color: var(--grey-variant-2);
  margin: 0 25px;
}

/* Responsive styles for smaller screens */
@media screen and (max-width: 570px) {
  .header {
    margin-bottom: 30px;
  }

  .header img.logo {
    max-width: 28px;
  }

  .header .settings .vertical-separator {
    margin: 0 16px;
  }
}
</style>
