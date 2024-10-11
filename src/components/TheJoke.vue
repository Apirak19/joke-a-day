<!-- <template>
  <main class="flex flex-col ">
    <h1>Below is count that was just created</h1>
    <p>{{ count }}</p>
    <button class="rounded bg-slate-500 px-2 py-1" @click="increment">
      increase the count
    </button>

    <form
      action=""
      class="flex flex-col gap-2 justify-center items-center"
      @submit="handleSubmit"
    >
      <h1 class="text-5xl">{{ yourAnswer }}</h1>
      <input
        type="text"
        class="text-slate-700 px-2 py-1"
        v-model="inputValue"
      />
      <button class="bg-slate-500 rounded px-2 py-1" type="submit">
        Change!
      </button>
    </form>
  </main>
</template>

<script setup lang="ts">
import { ref } from "vue";

const count = ref(0);
const yourAnswer = ref("not sure");
const inputValue = ref("");

const changeYourAnswer = (answer: string) => {
  yourAnswer.value = answer;
};

const handleSubmit = (event: Event) => {
  event.preventDefault();
  changeYourAnswer(inputValue.value);
};

const increment = () => {
  count.value++;
};
</script> -->
<script setup lang="ts">
import { ref, onMounted } from "vue";

const isLoading = ref(false);
const countDown = ref(5);
const punchline = ref("");
const joke = ref();
const getJoke = async () => {
  isLoading.value = true;
  countDown.value = 5;
  const response = await fetch(
    "https://official-joke-api.appspot.com/random_joke"
  );
  const data = await response.json();
  joke.value = data;
  const interval = setInterval(() => {
    countDown.value--;
    if (countDown.value === 0) {
      punchline.value = joke.value.punchline;
      isLoading.value = false;
      clearInterval(interval);
    }
  }, 1000);
};

onMounted(async () => {
  // startCountdown();
  // getJoke();
  const response = await fetch(
    "https://official-joke-api.appspot.com/random_joke"
  );
  const data = await response.json();
  joke.value = data;
  const interval = setInterval(() => {
    console.log(countDown.value);
    countDown.value--;

    if (countDown.value === 0) {
      clearInterval(interval);
      punchline.value = joke.value.punchline;
    }
  }, 1000);
});
</script>

<template class="justify-center">
  <main
    class="w-full flex flex-col items-center gap-4 text-2xl rounded bg-slate-700 p-8"
    v-if="joke"
  >
    <p>Joke no. {{ joke.id }}</p>
    <p>{{ joke.setup }}</p>
    <p v-if="countDown > 0" class="text-center">{{ countDown }}</p>
    <p v-if="countDown === 0" class="text-yellow-500">{{ punchline }}</p>
    <button
      :disabled="isLoading"
      class="bg-slate-600 px-4 py-2 rounded disabled:bg-slate-800 disabled:text-slate-600"
      @click="getJoke"
    >
      Get another joke
    </button>
  </main>
</template>
