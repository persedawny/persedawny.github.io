<template>
  <div class="flex flex-col min-h-screen">
    <nav class="bg-white dark:bg-gray-900 border-b border-gray-300 dark:border-gray-700 shadow-md">
      <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
        <a href="https://persedawny.github.io/" class="flex items-center space-x-3 rtl:space-x-reverse">
          <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Persedawny</span>
        </a>
        <div class="hidden w-full md:block md:w-auto" id="navbar-default">
          <ul class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
            <li>
              <a v-on:click.prevent.stop="OnLinkPressed('MyGames')"
                :class="[
                  'block py-2 px-3 rounded hover:bg-gray-100 md:hover:bg-transparent cursor-pointer md:border-0 md:p-0 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent transition duration-300',
                  {
                    'text-blue-700 dark:text-blue-500': isActive('MyGames'),
                    'text-gray-900 dark:text-white': !isActive('MyGames')
                  }
                ]">
                My Games
              </a>
            </li>
            <li>
              <a v-on:click.prevent.stop="OnLinkPressed('Slots')"
                :class="[
                  'block py-2 px-3 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:p-0 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent cursor-pointer transition duration-300',
                  {
                    'text-blue-700 dark:text-blue-500': isActive('Slots'),
                    'text-gray-900 dark:text-white': !isActive('Slots')
                  }
                ]">
                Slots
              </a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div class="flex flex-grow justify-center bg-gray-100 dark:bg-gray-800">
      <div class="bg-white dark:bg-gray-900 w-11/12 md:w-4/5 lg:w-3/5 xl:w-2/5 p-6 rounded-lg shadow-lg">
        <component :is="currentComponent"></component>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

import MyGamesComponent from './components/MyGamesComponent.vue';
import SlotsComponent from './components/SlotsComponent.vue';

const component = ref('MyGames');

const componentMap = {
  'MyGames': MyGamesComponent,
  'Slots': SlotsComponent
};

const currentComponent = computed(() => componentMap[component.value]);

function OnLinkPressed(text: string) {
  component.value = text;
}

function isActive(text: string) {
  return component.value === text;
}
</script>