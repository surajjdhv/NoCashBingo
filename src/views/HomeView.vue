<script setup>
import { ref } from 'vue';
import PlayerManager from '../components/PlayerManager.vue';
import WinnersManager from '../components/WinnersManager.vue';

const players = ref([]);
const winners = ref([]);
const ticketPrice = ref(0);
const nextPlayerId = ref(1); // Track the next player ID

const addPlayer = (player) => {
  // Assign a unique ID to each player
  players.value.push({ id: nextPlayerId.value, ...player });
  nextPlayerId.value += 1;
};

const addWinner = (winner) => {
  winners.value.push(winner);
};
</script>
<template>
  <main class="min-h-screen bg-slate-200 flex justify-center items-center">
    <section class=" max-w-[1360px] mx-auto">
      <h1 class="text-6xl font-bold">Welcome to NoCashBingo</h1>
      <div>
        <label for="ticket-price">Set Ticket Price: </label>
        <input type="number" v-model.number="ticketPrice" id="ticket-price" placeholder="Enter ticket price" min="1" />
      </div>
      <PlayerManager @add-player="addPlayer" :players="players" :ticket-price="ticketPrice" />
      <WinnersManager v-if="players.length > 1" @add-winner="addWinner" :winners="winners" :players="players" />
    </section>
  </main>
</template>
