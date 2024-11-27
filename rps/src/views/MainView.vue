<script setup lang="ts">
import ScoreBoard from "@/components/ScoreBoard.vue";
import Game from "@/components/Game.vue";
</script>

<template>
  <main class="w-full h-screen bg-[#141539] flex flex-col py-3">
    <header>
      <ScoreBoard />
    </header>
    <div class="flex justify-center items-center flex-grow pt-14">
      <Game />
    </div>
    <footer class="self-end">
      <button
        class="border-2 w-24 flex justify-center items-center h-10 rounded-md mr-5 text-zinc-100 font-bold"
      >
        RULES
      </button>
    </footer>
  </main>
</template>
