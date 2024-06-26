<script lang="ts" setup>
  const props = defineProps<{
    guesses: string[]
    currentGuess: string
    answer: string
  }>()

  const guessesWithColors = computed(() => {
    return props.guesses.map((guess) => {
      return guess.split("").map((letter) => {
        return {
          letter,
          inAnswer: props.answer.includes(letter),
          inCorrectPosition: props.answer[guess.indexOf(letter)] === letter,
        }
      })
    })
  })

  // render current guess plus enough blank space to make 5 total characters
  const renderedCurrentGuess = computed(() => {
    return props.currentGuess + " ".repeat(5 - props.currentGuess.length)
  })

  const emptyLines = computed(() => {
    const _blanks = " ".repeat(5)
    const guessesLeft = 5 - props.guesses.length
    return Array.from({ length: guessesLeft }, () => _blanks)
  })
</script>

<template>
  <div class="grid grid-cols-5 gap-2 mx-auto">
    <template
      v-for="guess in guessesWithColors"
      :key="guess"
      class="font-bold text-center"
    >
      <div
        v-for="(letter, idx) in guess"
        :key="`${guess}-${letter}-${idx}`"
        class="size-12 flex justify-center items-center text-3xl text-white"
        :class="{
          'bg-gray-500': !letter.inAnswer,
          'bg-yellow-500': letter.inAnswer && !letter.inCorrectPosition,
          'bg-green-600': letter.inCorrectPosition,
        }"
      >
        {{ letter.letter }}
      </div>
    </template>
    <div
      v-for="(letter, idx) in renderedCurrentGuess"
      :key="`${letter}-${idx}`"
      class="border border-black size-12 flex justify-center items-center text-3xl text-black"
    >
      {{ letter }}
    </div>
    <template
      v-for="(line, line_idx) in emptyLines"
      :key="line"
      class="font-bold text-center"
    >
      <div
        v-for="(letter, idx) in line"
        :key="`${line_idx}-${idx}`"
        class="border border-black size-12 flex justify-center items-center text-3xl"
      >
        {{ letter.letter }}
      </div>
    </template>
  </div>
</template>
