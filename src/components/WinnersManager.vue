<script setup>
import { ref } from 'vue';

const props = defineProps({
    players: Array,
    winners: Array,
});

const emit = defineEmits(['addWinner'])

const selectedWinner = ref('');

const handleAddWinner = () => {
    if (selectedWinner.value && !props.winners.includes(selectedWinner.value)) {
        emit('add-winner', selectedWinner.value);
        selectedWinner.value = '';
    }
};

const getWinnerDetails = (id) => {
    const winner = props.players.find((player) => player.id === id);
    return winner ? `${winner.id}. ${winner.name}` : 'Unknown Winner';
};
</script>

<template>
    <div>
        <h2>Winners</h2>
        <form @submit.prevent="handleAddWinner">
            <select v-model="selectedWinner" required>
                <option v-for="player in players" :key="player.id" :value="player.id">
                    {{ player.id }}. {{ player.name }}
                </option>
            </select>
            <button type="submit">Add Winner</button>
        </form>
        <ul>
            <li v-for="winner in winners" :key="winner">
                {{ getWinnerDetails(winner) }}
            </li>
        </ul>
    </div>
</template>