<script setup>
  function clicked(key) {
    if (currentGuess.value.length >= 5 && key !== "🔙" && key !== "ENTER") {
      return
    } else if (guesses.value.length >= 6) {
      return
    } else {
      if (key === "🔙") {
        currentGuess.value = currentGuess.value.slice(0, -1)
      } else if (key === "ENTER" && currentGuess.value.length == 5) {
        guesses.value.push(currentGuess.value)
        currentGuess.value = ""
      } else if (key === "ENTER" && currentGuess.value.length < 5) {
        return
      } else {
        currentGuess.value += key
      }
    }
  }

  const currentGuess = ref("")

  const guesses = ref([])
  const answer = "VUEJS"
</script>
<template>
  <div class="flex flex-col mx-auto max-w-2xl">
    <div class="prose m-auto">
      <h1>Vuedle</h1>
    </div>
    <WordGrid
      :guesses="guesses"
      :answer="answer"
      :currentGuess="currentGuess"
    />
    <Keyboard
      @click="clicked"
      class="mt-8"
    />
  </div>
</template>
