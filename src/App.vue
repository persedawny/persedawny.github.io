<template>
    <div class="flex flex-col min-h-screen">
        <nav class="bg-white border-gray-200 dark:bg-gray-900">
            <div class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
                <a href="https://persedawny.github.io/" class="flex items-center space-x-3 rtl:space-x-reverse">
                    <span class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white">Persedawny</span>
                </a>
                <div class="hidden w-full md:block md:w-auto" id="navbar-default">
                    <ul
                        class="font-medium flex flex-col p-4 md:p-0 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 rtl:space-x-reverse md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
                        <li>
                            <a v-on:click.prevent.stop="OnLinkPressed('MyGames')"
                                class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">
                                My Games
                            </a>
                        </li>
                        <li>
                            <a v-on:click.prevent.stop="OnLinkPressed('OtherProjects')"
                                class="block py-2 px-3 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">Other
                                Projects</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>

        <div class="flex flex-grow justify-center bg-gray-200">
            <div class="bg-white w-4/5">
                <component :is="component"></component>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

import MyGamesComponent from './components/MyGamesComponent.vue';
import OtherProjectsComponent from './components/OtherProjectsComponent.vue';

const component = ref(MyGamesComponent);

function OnLinkPressed(text) {
    switch (text) {
        case 'MyGames':
            component.value = MyGamesComponent;
            break;
        case 'OtherProjects':
            component.value = OtherProjectsComponent;
            break;
        default:
            break;
    }
}
</script>
