<template>
  <div class="page">
    <div class="top">
      <div class="box">
        <div class="items">
          <div
            v-for="item in selectedLeft"
            :key="item.id"
            class="item"
          >
            {{ item.name }}
          </div>
        </div>
        <small>selected: {{ selectedLeft.length }} / 6</small>
      </div>

      <div class="box">
        <div v-if="selectedRight" class="item big">
          {{ selectedRight.name }}
        </div>
        <div v-else class="placeholder">SELECTED ITEM</div>
      </div>
    </div>

    <div class="bottom">
      <div class="box">
        <div class="items">
          <div
            v-for="item in leftItems"
            :key="item.id"
            class="item"
            :class="{ active: isLeftSelected(item) }"
            @click="toggleLeft(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>

      <div class="box">
        <div class="items">
          <div
            v-for="item in rightItems"
            :key="item.id"
            class="item"
            :class="{ active: selectedRight?.id === item.id }"
            @click="selectRight(item)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const leftItems = ref([
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' }
])

const rightItems = ref([
  { id: 11, name: 'Jacket 1' },
  { id: 12, name: 'Jacket 2' },
  { id: 13, name: 'Jacket 3' },
  { id: 14, name: 'Jacket 4' },
  { id: 15, name: 'Hoodie 1' },
  { id: 16, name: 'Hoodie 2' },
  { id: 17, name: 'Hoodie 3' },
  { id: 18, name: 'Hoodie 4' }
])

const selectedLeft = ref([])
const selectedRight = ref(null)

const isLeftSelected = (item) =>
  selectedLeft.value.some(i => i.id === item.id)

const toggleLeft = (item) => {
  const index = selectedLeft.value.findIndex(i => i.id === item.id)

  if (index !== -1) {
    selectedLeft.value.splice(index, 1)
    return
  }

  if (selectedLeft.value.length < 6) {
    selectedLeft.value.push(item)
  }
}

const selectRight = (item) => {
  selectedRight.value = item
}
</script>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.top, .bottom {
  display: flex;
  gap: 40px;
}

.box {
  border: 2px solid black;
  padding: 10px;
  width: 300px;
  min-height: 150px;
}

.items {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.item {
  border: 2px solid black;
  padding: 8px;
  cursor: pointer;
}

.item.active {
  background: #ddd;
}

.big {
  font-size: 18px;
}

.placeholder {
  opacity: 0.5;
}
</style>
