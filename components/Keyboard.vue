<script lang="ts" setup>
  const keys = [
    ["Q", "W", "E", "R", "T", "Y", "U", "I", "O", "P"],
    ["A", "S", "D", "F", "G", "H", "J", "K", "L"],
    ["ENTER", "Z", "X", "C", "V", "B", "N", "M", "🔙"],
  ]

  defineEmits(["click"])
</script>

<template>
  <div class="flex flex-col">
    <div
      v-for="row in keys"
      :key="row"
      class="flex mx-auto"
    >
      <button
        v-for="keyButton in row"
        :key="keyButton"
        @click="$emit('click', keyButton)"
        class="p-4 m-1 bg-gray-200 rounded"
      >
        {{ keyButton }}
      </button>
    </div>
  </div>
</template>
