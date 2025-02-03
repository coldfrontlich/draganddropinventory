<template>
  <div class="grid">
    <div
      v-for="(row, rowIndex) in grid"
      :key="rowIndex"
      class="row"
    >
      <div
        v-for="(cell, colIndex) in row"
        :key="colIndex"
        class="cell"
      >
        <img
          v-if="cell.imageUrl"
          :src="cell.imageUrl"
          :alt="`Cell ${getCellNumber(rowIndex, colIndex)}`"
        />
        <span
          v-if="cell.imageUrl"
          class="cell-number"
        >
          {{ getCellNumber(rowIndex, colIndex) }}
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import Item1 from '../assets/images/Item1.png';
import Item2 from '../assets/images/Item2.png';
import Item3 from '../assets/images/Item3.png';

const grid = reactive([
  [
    { imageUrl: Item1, isEmpty: false },
    { imageUrl: Item2, isEmpty: false },
    { imageUrl: Item3, isEmpty: false },
    { isEmpty: true },
    { isEmpty: true },
  ],
  [
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
  ],
  [
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
  ],
  [
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
  ],
  [
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
    { isEmpty: true },
  ],
]);

const getCellNumber = (rowIndex, colIndex) => {
  return rowIndex * 5 + colIndex + 1;
};
</script>

<style scoped>
.grid {
  display: flex;
  flex-direction: column;
  background-color: #262626;
  border-radius: 10px;
}

.row {
  display: flex;
}

.cell {
  width: 115px;
  height: 109.5px;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #3c3c3c;
  overflow: hidden;
}

.cell img {
  max-width: 100%;
  max-height: 100%;
}

.cell-number {
  position: absolute;
  bottom: 5px;
  right: 5px;
  font-size: 12px;
  color: #ccc;
  background-color: #3c3c3c;
  padding: 2px 5px;
  border: 1px solid #3c3c3c;
  border-top-left-radius: 8px; /* Скругление слева сверху */
  border-right: none; /* Убираем правый бордер */
  border-bottom: none; /* Убираем нижний бордер */
  transform: translate(2px, 2px);
  bottom: -0.5px; 
  right: -0.5px;
}
</style>