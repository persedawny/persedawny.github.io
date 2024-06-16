<template>
    <div class="bg-gray-100 flex flex-col items-center justify-center p-4">
        <h2 class="text-4xl p-2">My Slot Machine Game</h2>

        <!-- Display current coins -->
        <div class="mb-4">
            Coins: <span class="font-bold">{{ coins }}</span>
        </div>

        <!-- Display upgrade buttons -->
        <div class="mb-4 flex">
            <button @click="upgradeLuck"
                :class="{ 'bg-blue-500 hover:bg-blue-600': coins >= upgrades.luck.cost, 'bg-gray-300 cursor-not-allowed': coins < upgrades.luck.cost }"
                class="text-white px-4 py-2 rounded mr-2 transition-colors duration-300"
                :disabled="coins < upgrades.luck.cost">
                Upgrade Luck ({{ upgrades.luck.cost }} coins)
            </button>

            <button @click="upgradeJackpot"
                :class="{ 'bg-blue-500 hover:bg-blue-600': coins >= upgrades.jackpot.cost, 'bg-gray-300 cursor-not-allowed': coins < upgrades.jackpot.cost }"
                class="text-white px-4 py-2 rounded mr-2 transition-colors duration-300"
                :disabled="coins < upgrades.jackpot.cost">
                Upgrade Jackpot ({{ upgrades.jackpot.cost }} coins)
            </button>
        </div>

        <!-- Original slot machine UI -->
        <div class="bg-white p-6 rounded-lg shadow-lg max-w-lg">
            <div class="text-center mb-4">
                <h1 class="text-3xl font-bold">Slot Machine</h1>
            </div>
            <div class="grid grid-cols-3 gap-4 mb-4">
                <div v-for="(slot, index) in slots" :key="index" ref="slots"
                    class="slot border p-4 text-center text-2xl font-bold">
                    {{ slot }}
                </div>
            </div>
            <button @click="spin"
                class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition-colors duration-300">
                Spin
            </button>
        </div>
    </div>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
    setup() {
        const coins = ref(100); // Initial amount of coins

        const upgrades = reactive({
            luck: {
                level: 1,
                cost: 10,
                multiplier: 1.2, // Increases chances of getting higher rewards
            },
            jackpot: {
                level: 1,
                cost: 20,
                bonus: 50, // Increases jackpot bonus
            },
        });

        const playSound = () => {
            const audio = new Audio('src\\components\\coin.mp3');
            audio.play();
        }

        const upgradeLuck = () => {
            if (coins.value >= upgrades.luck.cost) {
                coins.value -= upgrades.luck.cost;
                upgrades.luck.level++;
                // Example adjustment: Increase multiplier with each upgrade
                upgrades.luck.multiplier += 0.1;
                // Adjust game logic to reflect upgraded luck
            }
        };

        const upgradeJackpot = () => {
            if (coins.value >= upgrades.jackpot.cost) {
                coins.value -= upgrades.jackpot.cost;
                upgrades.jackpot.level++;
                // Adjust game logic to reflect upgraded jackpot
            }
        };

        const slots = ref(['🍒', '🍋', '🍊']);
        const symbols = ['🍒', '🍋', '🍊', '🍉', '🍇', '⭐'];

        const spin = () => {
            playSound();
            const slotsElements = document.querySelectorAll('.slot');
            slotsElements.forEach(slot => slot.classList.add('spin'));

            setTimeout(() => {
                slots.value = slots.value.map(() => {
                    // Adjusted logic to reflect luck multiplier
                    let randomIndex = Math.floor(Math.random() * symbols.length);
                    // Increase probability for higher symbols based on luck level
                    for (let i = 0; i < upgrades.luck.level; i++) {
                        randomIndex = Math.random() < upgrades.luck.multiplier ? Math.floor(Math.random() * symbols.length) : randomIndex;
                    }
                    return symbols[randomIndex];
                });
                slotsElements.forEach(slot => slot.classList.remove('spin'));
            }, 500);
        };

        spin(); // Initial spin when component loads

        return {
            coins,
            upgrades,
            upgradeLuck,
            upgradeJackpot,
            slots,
            spin,
        };
    },
};
</script>

<style>
.slot {
    transition: transform 0.5s ease-in-out;
}

.spin {
    transform: rotateX(360deg);
}
</style>