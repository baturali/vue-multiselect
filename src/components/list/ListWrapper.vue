<template>
  <div>
    <div
      v-if="filteredResults?.length || searchValue"
      class="relative z-10 ml-auto mr-auto w-0 h-0 border-l-[8px] border-l-transparent border-b-[12px] border-b-white border-r-[8px] border-r-transparent"
    ></div>
    <div
      class="flex flex-col w-96 -mt-[1px] rounded-md shadow-md border border-gray-300 overflow-hidden"
    >
      <div v-for="(item, index) in filteredResults" :key="item + index">
        <ListItem @click="emit('selected', item)">
          <span
            v-html="
              searchValue
                ? item.replace(
                    new RegExp(searchValue, 'gi'),
                    `<span style='text-decoration: underline'>$&</span>`,
                  )
                : item
            "
          />
        </ListItem>
      </div>
      <ListItem
        v-if="!filteredResults?.length && searchValue"
        class="flex-row justify-between"
        @click="emit('selected', searchValue)"
      >
        <span class="truncate">{{ searchValue }}</span>
        <span class="text-blue-300 min-w-20">(new value)</span>
      </ListItem>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import ListItem from './ListItem.vue'

const emit = defineEmits<{
  (e: 'selected', item: string): void
}>()

const props = defineProps({
  searchValue: String,
  list: Array<string>,
  selectedItems: Array<string>,
})

const filteredResults = computed(() => {
  const filterBySearchValue = (item: string) => {
    return props.searchValue
      ? item?.toLowerCase().includes(props.searchValue.toLowerCase())
      : true
  }

  const filterBySelectedItems = (item: string) =>
    !props.selectedItems?.includes(item)

  return props.list?.filter(filterBySearchValue).filter(filterBySelectedItems)
})
</script>
