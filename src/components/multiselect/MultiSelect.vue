<template>
  <div class="w-96 pt-16 relative">
    <label class="mb-1 text-xs">Chart type</label>
    <div
      class="flex flex-row flex-wrap outline outline-sky-600 hover:outline-4 rounded-sm mt-1 gap-y-1 p-1 bg-white"
    >
      <InputLabel
        v-for="(item, index) in selectedItems"
        :key="item + index"
        :item="item"
        @remove="itemRemoveHandler"
      />
      <input
        v-model="searchValue"
        class="flex-1 h-7 p-1 pl-2 text-sm focus:outline-none"
        type="text"
        @keyup.ctrl.a="selectAllHandler"
      />
    </div>
    <ListWrapper
      @selected="itemSelectHandler"
      :search-value="searchValue"
      :list="list"
      :selected-items="selectedItems"
    />
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import InputLabel from '../input/InputLabel.vue'
import ListWrapper from '../list/ListWrapper.vue'

const searchValue = defineModel<string>()

const selectedItems = ref<string[]>([])

const list = [
  'Line chart',
  'Area chart',
  'Column chart',
  'Bar chart',
  'Pie chart',
  'Scatter chart',
  'Bubble chart',
]

const selectAllHandler = () => {
  selectedItems.value = [...new Set([...selectedItems.value, ...list])]
}

const itemSelectHandler = (item: string) => {
  if (!selectedItems.value.includes(item)) {
    selectedItems.value.push(item)
    searchValue.value = ''
  }
}

const itemRemoveHandler = (item?: string) => {
  selectedItems.value = selectedItems.value.filter(
    selected => selected !== item,
  )
}
</script>
