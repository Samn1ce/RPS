<script setup lang="ts">
import { ref, computed, defineProps } from "vue";
import Triangle from "./icons/IconTriangle.vue";
import Scissors from "./icons/IconScissors.vue";
import Rock from "./icons/IconRock.vue";
import Paper from "./icons/IconPaper.vue";
import Options from "@/assets/Options.json";

// Define props to accept gameScore and updateScore
const props = defineProps({
  gameScore: Number,
  updateScore: Function,
});

// Create an icons object that maps the JSON icon names to SVG components
const icons = {
  IconPaper: Paper,
  IconScissors: Scissors,
  IconRock: Rock,
};

// Define a reactive variable to store the selected index
const selectedIndex = ref<number | null>(null);
const comSelectedOption = ref(Math.floor(Math.random() * Options.length));

// Computed property to get the selected option
const selectedOption = computed<any>(() =>
  selectedIndex.value !== null ? Options[selectedIndex.value] : null
);

// Computed property to get the computer's selected option
const computerOption = computed<any>(() => Options[comSelectedOption.value]);
console.log(computerOption);

// Function to handle click and set the selected index
const handleSelect = (index: number) => {
  selectedIndex.value = index;
  console.log("Selected index:", index); // Optional: For debugging
};

const handleClick = (index: number) => {
  handleSelect(index); // Select the user option
  comSelectedOption.value = Math.floor(Math.random() * Options.length); // Generate a new random option for the computer
  determineWinner();
  setStep(2);
};

const gameResult = ref<string>("");

const determineWinner = () => {
  if (selectedOption.value && computerOption.value) {
    if (selectedOption.value.name === computerOption.value.name) {
      gameResult.value = "It's a tie!";
    } else if (
      (selectedOption.value.name === "Rock" &&
        computerOption.value.name === "Scissors") ||
      (selectedOption.value.name === "Paper" &&
        computerOption.value.name === "Rock") ||
      (selectedOption.value.name === "Scissors" &&
        computerOption.value.name === "Paper")
    ) {
      gameResult.value = "You Win!";
      props.updateScore(1); // Update the score using the passed function
    } else {
      gameResult.value = "You Lose!";
    }
  }
};

const step = ref<number>(1);

const setStep = (value: any) => {
  step.value = value;
};
</script>

<template>
  <div
    class="flex flex-col gap-8 md:flex-row justify-center items-center md:h-full w-full max-w-7xl max-h-[700px]"
  >
    <div
      v-if="step === 1"
      class="relative w-full h-1/2 md:h-full flex justify-center items-center"
    >
      <Triangle />
      <div
        class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 grid grid-cols-2 gap-12 place-items-center w-60 md:w-72 lg:w-96 h-72 md:h-96"
      >
        <div
          v-for="(option, index) in Options"
          :key="index"
          @click="handleClick(index)"
          :class="[
            'w-36 h-36 md:w-36 md:h-36 lg:w-44 lg:h-44 flex items-center justify-center absolute cursor-pointer',
            index === 0 ? '-top-10 md:top-0 -left-10' : '',
            index === 1 ? '-top-10 md:top-0 -right-10' : '',
            index === 2 ? 'bottom-0' : '',
          ]"
        >
          <div
            class="w-full h-full bg-[#4865f4] absolute top-2 rounded-full"
            :style="{ backgroundColor: option.colorTop }"
          ></div>
          <div
            class="w-full h-full bg-[#5671f5] absolute rounded-full"
            :style="{ backgroundColor: option.colorBottom }"
          ></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <component class="absolute" :is="icons[option.icon]" />
        </div>
      </div>
    </div>

    <div
      v-else
      v-if="selectedOption"
      class="w-11/12 md:w-2/3 h-full grid grid-cols-2 md:flex items-center justify-between md:flex-nowrap"
    >
      <div
        class="text-white font-bold flex flex-col justify-between items-center gap-8 order-first"
      >
        <p>YOU PICKED</p>
        <div
          class="w-36 h-36 md:w-36 md:h-36 lg:h-52 lg:w-52 flex items-center justify-center relative col-span-2"
        >
          <div
            class="w-full h-full absolute top-2 rounded-full"
            :style="{ backgroundColor: selectedOption.colorTop }"
          ></div>
          <div
            class="w-full h-full absolute rounded-full"
            :style="{ backgroundColor: selectedOption.colorBottom }"
          ></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <component :is="icons[selectedOption.icon]" class="absolute" />
        </div>
      </div>
      <div
        class="text-zinc-100 text-4xl font-bold mx-auto md:mx-0 order-last md:order-2 col-span-2 self-center mt-10 md:mt-0"
      >
        <p>{{ gameResult }}</p>
        <button
          @click="setStep(1)"
          class="bg-white text-red-600 text-sm w-40 h-10 rounded-md"
        >
          PLAY AGAIN
        </button>
      </div>
      <div
        class="text-white font-bold flex flex-col justify-between items-center gap-8 order-2 md:order-last"
      >
        <p>HOUSE PICKED</p>
        <div
          class="w-36 h-36 md:w-36 md:h-36 lg:h-52 lg:w-52 flex items-center justify-center relative col-span-2"
        >
          <div
            class="w-full h-full absolute top-2 rounded-full"
            :style="{ backgroundColor: computerOption.colorTop }"
          ></div>
          <div
            class="w-full h-full absolute rounded-full"
            :style="{ backgroundColor: computerOption.colorBottom }"
          ></div>
          <div
            class="w-3/4 h-3/4 bg-slate-300 absolute top-3 mt-2 rounded-full"
          ></div>
          <div class="w-3/4 h-3/4 bg-zinc-200 absolute mt-2 rounded-full"></div>
          <component :is="icons[computerOption.icon]" class="absolute" />
        </div>
      </div>
    </div>
  </div>
</template>
