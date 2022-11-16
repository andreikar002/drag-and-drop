<template>
  <div>
    <div class="w-96">
      <div class="flex flex-row w-full gap-8">
        <div v-for="zone in dropableZones" :key="zone.id">
          <div
            class="w-32 h-32 border dropable-element"
            :id="zone.id"
          >
            <div
              class="w-32 h-32 border draggable-element"
              :id="zone.id_dragable"
            >
              {{ dragableElements[zone.id_dragable] }}
            </div>
          </div>
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
      dropableZones: [
        { id: 'dropable-1', id_dragable: 'dragable-1', isFull: true },
        { id: 'dropable-2', id_dragable: 'dragable-2', isFull: true },
        { id: 'dropable-3', id_dragable: 'dragable-3', isFull: true },
        { id: 'dropable-4', id_dragable: 'dragable-4', isFull: true },
        { id: 'dropable-5', id_dragable: 'dragable-5', isFull: true },
        { id: 'dropable-6', id_dragable: 'dragable-6', isFull: true },
        { id: 'dropable-7', id_dragable: 'dragable-7', isFull: true },
        { id: 'dropable-8', id_dragable: 'dragable-8', isFull: true },
        { id: 'dropable-9', id_dragable: 'dragable-0', isFull: true },
      ],
      dragableElements: {
        'dragable-1': '1',
        'dragable-2': '2',
        'dragable-3': '3',
        'dragable-4': '4',
        'dragable-5': '5',
        'dragable-6': '6',
        'dragable-7': '7',
        'dragable-8': '8',
        'dragable-0': '9',
      },
      currentDrag: {
        isActive: false,
        id: 0,
        shiftX: 0,
        shiftY: 0,
        pageX: 0,
        pageY: 0,
        element: null,
        dropableId: 0,
        dragableId: 0,
      },
    }
  },
  mounted() {
    window.document.onmousedown = (event) => {
      if (event.which != 1) {
        return
      }
      if (!event.target.className.includes('draggable-element')) return
    //   console.log(event)
      this.currentDrag.element = event.target
      this.currentDrag.pageX = event.x
      this.currentDrag.pageY = event.y
      this.currentDrag.shiftX = event.x - event.target.offsetLeft
      this.currentDrag.shiftY = event.y - event.target.offsetTop
      this.currentDrag.dragableId = event.target.id
      this.currentDrag.dropableId = event.target.parentElement.id
      this.currentDrag.isActive = true
    }

    window.document.onmousemove = (event) => {
      if (!this.currentDrag.isActive) return

      const element = this.currentDrag.element
      //   if (element.parentNode != document.body)
      //     document.body.appendChild(element)
      element.style.position = 'absolute'
      element.style.zIndex = 9999
      //   console.log(event, this.currentDrag.shiftX, this.currentDrag.shiftY, element)

      element.style.left = event.x - this.currentDrag.shiftX + 'px'
      element.style.top = event.y - this.currentDrag.shiftY + 'px'
    }

    window.document.onmouseup = (event) => {
      if (this.currentDrag.isActive) {
        this.currentDrag.element.style.position = 'static'
        this.currentDrag.element.style.left = 0
        this.currentDrag.element.style.top = 0

        var newDragable = window.document.elementFromPoint(
          event.clientX,
          event.clientY
        )
        var newDropable = newDragable.parentElement
        // console.log(newDropable, newDragable)

        if (newDropable?.className?.includes('dropable-element')) {
          var newDropableId = newDropable.id
          var newDragableId = newDragable.id
          var oldDragableId = this.currentDrag.dragableId
          var oldDropableId = this.currentDrag.dropableId

          for (var key in this.dropableZones) {
            if (this.dropableZones[key].id == newDropableId)
              this.dropableZones[key].id_dragable = oldDragableId
            if (this.dropableZones[key].id == oldDropableId)
              this.dropableZones[key].id_dragable = newDragableId
          }
        }

        this.currentDrag = {
          isActive: false,
          id: 0,
          shiftX: 0,
          shiftY: 0,
          pageX: 0,
          pageY: 0,
          element: null,
          dropableId: 0,
          dragableId: 0,
        }
      }
    }
  },
}
</script>
