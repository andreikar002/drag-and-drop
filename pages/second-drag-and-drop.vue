<template>
  <div>
    <div class="w-96">
      <div class="flex flex-row w-full gap-8">
        <div class="flex flex-col gap-2">
          <div class="border bg-gray-200 rounded-xl w-48 h-48"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FirstPage',

  data() {
    return {
      dropablesZone: [
        { id: 1, id_dragable: [1], isFull: true },
        { id: 2, id_dragable: [2], isFull: true },
        { id: 3, id_dragable: [3], isFull: true },
        { id: 4, id_dragable: [4], isFull: true },
        { id: 5, id_dragable: [5], isFull: true },
        { id: 6, id_dragable: [6], isFull: true },
        { id: 7, id_dragable: [7], isFull: true },
        { id: 8, id_dragable: [8], isFull: true },
        { id: 9, id_dragable: [9], isFull: true },
      ],
      firstZones: [
        { id: 1, id_dragable: [1], isFull: true },
        { id: 2, id_dragable: [2], isFull: true },
        { id: 3, id_dragable: [3], isFull: true },
        { id: 4, id_dragable: [4], isFull: true },
        { id: 5, id_dragable: [5], isFull: true },
        { id: 6, id_dragable: [6], isFull: true },
        { id: 7, id_dragable: [7], isFull: true },
        { id: 8, id_dragable: [8], isFull: true },
        { id: 9, id_dragable: [9], isFull: true },
      ],
      drabbleElements: [
        { id: 1, id_dropable: 1 },
        { id: 2, id_dropable: 2 },
        { id: 3, id_dropable: 3 },
        { id: 4, id_dropable: 4 },
        { id: 5, id_dropable: 5 },
        { id: 6, id_dropable: 6 },
        { id: 7, id_dropable: 7 },
        { id: 8, id_dropable: 8 },
        { id: 9, id_dropable: 9 },
      ],
    }
  },
  methods: {
    onDragStart(e, dragable) {
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.setData('itemId', dragable)
    },
    onDrop(e, drop_id) {
      const itemId = parseInt(e.dataTransfer.getData('itemId'))
      let lastDrop = 0
      for (var i in this.drabbleElements) {
        if (this.drabbleElements[i].id == itemId) {
          lastDrop = this.drabbleElements[i].id_dropable
        }
      }
      let nextDrag = 0
      let nextDrop = 0

      this.dropablesZone.forEach((zone) => {
        if (zone.id === drop_id) {
          nextDrag = zone.id_dragable
          zone.id_dragable = itemId
        }
      })
      this.drabbleElements.forEach((drag) => {
        if (drag.id === itemId) {
          drag.id_dropable = drop_id
        }
      })
      this.dropablesZone.forEach((zone) => {
        if (zone.id === lastDrop) {
          nextDrop = zone.id
          zone.id_dragable = nextDrag
        }
      })
      this.drabbleElements.forEach((drag) => {
        if (drag.id === nextDrag) {
          drag.id_dropable = nextDrop
        }
      })
      console.log(lastDrop, nextDrag)
    },
  },
}
</script>
