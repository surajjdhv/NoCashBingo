<template>
    <div>
        <h2>Add Players</h2>
        <form @submit.prevent="handleAddPlayer">
            <div class="input-group">
                <label for="player-name">Player Name </label>
                <input name="player-name" v-model="name" placeholder="Name" required />
            </div>
            <div class="input-group">
                <label for="player-tickets">Tickets </label>
                <input name="player-tickets" type="number" v-model.number="tickets" placeholder="Number of Tickets"
                    required min="1" />
            </div>
            <button type="submit">Add Player</button>
        </form>
        <ul>
            <li v-for="player in players" :key="player.id">
                {{ player.id }}. {{ player.name }} - {{ player.tickets }} tickets - {{ player.totalTicketCost }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
    players: Array,
    ticketPrice: Number, // Accept ticket price as a prop
});

const emit = defineEmits(['addPlayer'])

const name = ref('');
const tickets = ref(1);
const totalTicketCost = computed(() => { return props.ticketPrice * tickets.value });

const handleAddPlayer = () => {
    if (name.value.trim() && tickets.value > 0) {
        emit('add-player', { name: name.value.trim(), tickets: tickets.value, totalTicketCost: totalTicketCost.value });
        name.value = '';
        tickets.value = 1;
    }
};
</script>