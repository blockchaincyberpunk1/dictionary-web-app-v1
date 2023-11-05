<template>
  <div class="font-selector">
    <!-- Clickable selected font display that toggles the font picker -->
    <div class="selected-font" @click.stop="toggleFontPicker">
      {{ selectedFont.label }}
      <!-- SVG icon for dropdown indication -->
      <svg class="icon-dropdown" xmlns="http://www.w3.org/2000/svg" width="14" height="8" viewBox="0 0 14 8">
        <path fill="none" stroke="#A445ED" stroke-width="1.5" d="m1 1 6 6 6-6"/>
      </svg>
    </div>
    <!-- Font picker options, shown only when fontPickerOpen is true -->
    <div v-if="fontPickerOpen" class="font-options">
      <!-- Loop through each font option and display it -->
      <span
        v-for="font in fontOptions"
        :key="font.value"
        :class="font.value"
        @click="chooseFont(font)"
      >
        {{ font.label }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FontSelector',
  data() {
    return {
      selectedFont: { label: 'Sans Serif', value: 'sans-serif' },
      fontOptions: [
        { label: 'Sans Serif', value: 'sans-serif' },
        { label: 'Serif', value: 'serif' },
        { label: 'Mono', value: 'monospace' },
      ],
      fontPickerOpen: false,
    };
  },
  methods: {
    toggleFontPicker() {
      this.fontPickerOpen = !this.fontPickerOpen;
    },
    hideFontPicker() {
      if (this.fontPickerOpen) {
        this.fontPickerOpen = false;
      }
    },
    applyFont(font) {
      // Apply the font to the root element and save the preference
      document.documentElement.setAttribute('data-font', font);
      localStorage.setItem('dictionary-font', font);
    },
    chooseFont(font) {
      // Set the selected font and apply it
      this.selectedFont = font;
      this.applyFont(font.value);
      this.fontPickerOpen = false;
    },
    getAppliedFont() {
      // Retrieve the applied font from local storage and apply it
      const appliedFont = localStorage.getItem('dictionary-font');
      const validFont = this.fontOptions.find(item => item.value === appliedFont);
      if (validFont) {
        this.chooseFont(validFont);
      }
    },
  },
  beforeMount() {
    // Initialize the component with the applied font and set up event listeners
    this.getAppliedFont();
    window.addEventListener('click', this.hideFontPicker);
  },
  beforeDestroy() {
    // Clean up event listeners when the component is destroyed
    window.removeEventListener('click', this.hideFontPicker);
  },
};
</script>

<style>
/* Styles omitted for brevity */
</style>
