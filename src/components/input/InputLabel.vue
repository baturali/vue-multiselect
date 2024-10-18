<template>
  <div
    class="flex flex-row items-center h-7 w-max rounded-sm bg-blue-100 text-sm z-99 mr-1 p-1"
  >
    <div class="max-w-[350px] text-xs px-1 truncate">{{ item }}</div>
    <div class="w-3 h-3 mr-1 stroke-gray-800 cursor-pointer">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        strokeWidth="{1.5}"
        stroke="currentColor"
        @click="emit('remove', props.item)"
      >
        <path
          strokeLinecap="round"
          strokeLinejoin="round"
          d="M6 18 18 6M6 6l12 12"
        />
      </svg>
    </div>
  </div>
</template>

<script setup lang="ts">
const emit = defineEmits<{
  (e: 'remove', item?: string): void
}>()

const props = defineProps({
  item: String,
})
</script>
