<template>
    <h2 class="text-4xl text-black p-2">My games</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 p-2">
        <div v-for="(url, index) in links" :key="index">
            <iframe frameborder="0" :src="url.buttonLink" class="w-full" height="167"><a :href="url.projectLink">{{ url.name }} by PersedawnyGames</a></iframe>
        </div>
    </div>
</template>

<script setup lang="ts">
const links = [
    { name: 'Danganronpa Memory', buttonLink: 'https://itch.io/embed/2551703?linkback=true', projectLink: 'https://persedawnygames.itch.io/danganronpa-memory' },
    { name: 'Your World', buttonLink: 'https://itch.io/embed/2553993?linkback=true', projectLink: 'https://persedawnygames.itch.io/your-world' }
]
</script>