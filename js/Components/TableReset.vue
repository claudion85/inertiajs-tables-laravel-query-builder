<template>
  <button
    ref="button"
    type="button"
    dusk="reset-table"
    :class="getTheme('button')"
    aria-haspopup="true"
    @click.prevent="onClick"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      class="h-5 w-5 mr-2 text-gray-400"
      viewBox="0 0 20 20"
      fill="currentColor"
    >
      <path
        fill-rule="evenodd"
        d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
        clip-rule="evenodd"
      />
    </svg>
    <span>{{ translations.reset ?? 'Reset' }}</span>
  </button>
</template>

<script setup>
import {inject} from "vue";
import { getTranslations } from "../translations.js";
import {twMerge} from "tailwind-merge";
import {get_theme_part} from "../helpers.js";

const translations = getTranslations();

const props = defineProps({
    onClick: {
        type: Function,
        required: true
    },

    color: {
        type: String,
        default: 'primary',
        required: false,
    },

    ui: {
        required: false,
        type: Object,
        default: {} ,
    },
});

// Theme
const fallbackTheme = {
    button: {
        base: "w-full border rounded-md shadow-xs px-4 py-2 inline-flex justify-center text-sm font-medium focus:outline-hidden focus:ring-2 focus:ring-offset-2",
        color: {
            primary: "bg-white dark:bg-gray-900 text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-800 border-gray-300 dark:border-gray-700 focus:ring-indigo-500",
            dootix: "bg-white dark:bg-gray-900 text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-gray-800 border-gray-300 dark:border-gray-700 focus:ring-cyan-500",
        },
    },
}
const themeVariables = inject('themeVariables');
const getTheme = (item) => {
    return twMerge(
        get_theme_part([item, 'base'], fallbackTheme, themeVariables?.inertia_table?.reset_button, props.ui),
        get_theme_part([item, 'color', props.color], fallbackTheme, themeVariables?.inertia_table?.reset_button, props.ui),
    )
}
</script>
