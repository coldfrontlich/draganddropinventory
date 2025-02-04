<template>
	<div class="grid">
		<div v-for="(row, rowIndex) in grid" :key="rowIndex" class="row">
			<div
				v-for="(cell, colIndex) in row"
				:key="colIndex"
				class="cell"
				:class="{ active: cell.itemId }"
				:draggable="!!cell.itemId"
				@dragstart="onDragStart($event, rowIndex, colIndex)"
				@dragover.prevent="onDragOver"
				@drop="onDrop($event, rowIndex, colIndex)"
				@click="handleCellClick(rowIndex, colIndex)"
			>
				<img
					v-if="cell.itemId"
					:src="items[cell.itemId]"
					:alt="`Cell ${rowIndex}-${colIndex}`"
				/>
				<span v-if="cell.itemId" class="cell-number">
					{{ cell.count }}
				</span>
			</div>
		</div>
		<ModalDelete
			v-if="showModal"
			:itemSrc="selectedItem"
			@close="closeModal"
			@delete="deleteItem"
		/>
	</div>
</template>

<script setup lang="ts">
import { reactive, watch, ref, computed } from 'vue'
import ModalDelete from './ModalDelete.vue'
import Item1 from '../assets/images/Item1.png'
import Item2 from '../assets/images/Item2.png'
import Item3 from '../assets/images/Item3.png'

interface Cell {
	itemId?: string
	isEmpty: boolean
	count?: number
}

interface DraggedCell {
	rowIndex: number
	colIndex: number
}

const items: { [key: string]: string } = {
	Item1: Item1,
	Item2: Item2,
	Item3: Item3,
}

const loadGrid = () => {
	const saved = localStorage.getItem('grid')
	return saved ? JSON.parse(saved) : getDefaultGrid()
}

const getDefaultGrid = (): Cell[][] => [
	[
		{ itemId: 'Item1', isEmpty: false, count: 4 },
		{ itemId: 'Item2', isEmpty: false, count: 2 },
		{ itemId: 'Item3', isEmpty: false, count: 5 },
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
]

const grid = reactive<Cell[][]>(loadGrid())

watch(
	() => grid,
	newGrid => {
		localStorage.setItem('grid', JSON.stringify(newGrid))
	},
	{ deep: true }
)

let draggedCell: DraggedCell | null = null

const onDragStart = (event: DragEvent, rowIndex: number, colIndex: number) => {
	const target = event.currentTarget as HTMLElement
	target.classList.add('dragging')
	draggedCell = { rowIndex, colIndex }
	event.dataTransfer?.setData('text/plain', '')
	event.dataTransfer!.effectAllowed = 'move'
}

const onDragOver = (event: DragEvent) => {
	event.preventDefault()
}

const onDrop = (
	event: DragEvent,
	targetRowIndex: number,
	targetColIndex: number
) => {
	event.preventDefault()

	if (!draggedCell) return

	const { rowIndex: srcRow, colIndex: srcCol } = draggedCell
	const source = grid[srcRow][srcCol]
	const target = grid[targetRowIndex][targetColIndex]

	if (target.isEmpty && source.itemId) {
		target.itemId = source.itemId
		target.count = source.count
		target.isEmpty = false

		source.itemId = undefined
		source.count = undefined
		source.isEmpty = true
	}

	draggedCell = null
}

const showModal = ref(false)
const selectedCell = reactive({
	rowIndex: -1,
	colIndex: -1,
})

const selectedItem = computed(() => {
	if (selectedCell.rowIndex === -1 || selectedCell.colIndex === -1) return null
	const cell = grid[selectedCell.rowIndex][selectedCell.colIndex]
	return cell.itemId ? items[cell.itemId] : null
})

const handleCellClick = (rowIndex: number, colIndex: number) => {
	if (!grid[rowIndex][colIndex].itemId) return
	selectedCell.rowIndex = rowIndex
	selectedCell.colIndex = colIndex
	showModal.value = true
}

const deleteItem = () => {
	if (selectedCell.rowIndex === -1 || selectedCell.colIndex === -1) return

	const cell = grid[selectedCell.rowIndex][selectedCell.colIndex]
	cell.itemId = undefined
	cell.count = undefined
	cell.isEmpty = true

	closeModal()
}

const closeModal = () => {
	showModal.value = false
	selectedCell.rowIndex = -1
	selectedCell.colIndex = -1
}
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
	user-select: none;
}

.cell.active {
	cursor: grab;
}

.cell img {
	max-width: 100%;
	max-height: 100%;
	pointer-events: none;
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
	border-top-left-radius: 8px;
	border-right: none;
	border-bottom: none;
	transform: translate(2px, 2px);
	bottom: -0.5px;
	right: -0.5px;
	pointer-events: none;
}

.cell.dragging {
	border: 1px solid #3c3c3c;
}

.cell:hover:not(.dragging) {
	border-color: #3c3c3c;
}

</style>
