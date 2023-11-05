<template>
  <!-- Container for the theme toggle switch -->
  <div class="theme-toggler">
    <!-- Accessible label for the theme toggle checkbox -->
    <label for="toggler-checkbox" class="toggle-label">
      <!-- Checkbox bound to darkThemeEnabled data property -->
      <input
        type="checkbox"
        id="toggler-checkbox"
        v-model="darkThemeEnabled"
        @change="toggleTheme"
        class="toggle-checkbox"
      >
      <!-- Custom styled toggle switch -->
      <span class="toggler">
        <span class="toggler-button"></span>
      </span>
    </label>
    <!-- Moon icon that indicates dark mode -->
    <svg class="icon-moon" :class="{ active: darkThemeEnabled }" xmlns="http://www.w3.org/2000/svg" width="22" height="22" viewBox="0 0 22 22">
      <path fill="none" stroke="#838383" stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M1 10.449a10.544 10.544 0 0 0 19.993 4.686C11.544 15.135 6.858 10.448 6.858 1A10.545 10.545 0 0 0 1 10.449Z"/>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'ThemeToggler',
  data() {
    return {
      darkThemeEnabled: false, // Tracks if the dark theme is enabled
    };
  },
  methods: {
    toggleTheme() {
      // Toggle the theme and update the local storage
      this.darkThemeEnabled = !this.darkThemeEnabled;
      const theme = this.darkThemeEnabled ? 'dark' : 'light';
      localStorage.setItem('dictionary-theme', theme);
      document.documentElement.setAttribute('data-theme', theme);
    },
    getPreferredTheme() {
      // Get the preferred theme from local storage or system preference
      const userSetTheme = localStorage.getItem('dictionary-theme');
      if (userSetTheme) {
        this.darkThemeEnabled = userSetTheme === 'dark';
      } else {
        this.darkThemeEnabled = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
      }
      this.toggleTheme();
    }
  },
  beforeMount() {
    // Initialize the preferred theme before the component mounts
    this.getPreferredTheme();
  },
}
</script>

<style>
/* Styles are simplified for clarity*/
.theme-toggler {
  display: flex;
  align-items: center;
  user-select: none;
  -webkit-tap-highlight-color: transparent;
}

.toggle-label {
  line-height: 0;
}

.toggle-checkbox {
  display: none;
}

.toggler {
  display: inline-block;
  position: relative;
  width: 40px;
  height: 20px;
  border-radius: 10px;
  background-color: var(--grey-variant-1);
  margin-right: 20px;
  cursor: pointer;
  transition: 0.3s ease-in-out;
}

.toggler-button {
  position: absolute;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  left: 3px;
  top: 3px;
  background-color: var(--white);
  transition: 0.3s ease-in-out;
}

.toggle-checkbox:checked + .toggler {
  background-color: var(--purple);
}

.toggle-checkbox:checked + .toggler .toggler-button {
  left: 23px;
}

.icon-moon.active path {
  stroke: var(--purple);
}

@media screen and (max-width: 570px) {
  .toggler {
    margin-right: 12px;
  }
}
</style>
