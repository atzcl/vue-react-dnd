<template>
  <div class="box" v-dragSource v-bind:class="{dragging: isDragging}">{{ name }}</div>
</template>

<script>
import { DragSource } from 'vue-react-dnd'
import ItemTypes from './../SingleTarget/ItemTypes'

export default {
  name: 'Box',
  props: ['name'],
  mixins: [DragSource],

  data () {
    return {
      isDragging: false
    }
  },

  dragSource: {
    type () {
      return ItemTypes.BOX
    },
    specs: {
      beginDrag () {
        return {
          name: this.name
        }
      },

      endDrag (monitor) {
        const item = monitor.getItem()
        const dropResult = monitor.getDropResult()

        if (dropResult) {
          alert('You dropped ' + item.name + ' into ' + dropResult.name + '!')
        }
      }
    },
    collect (connect, monitor) {
      this.isDragging = monitor.isDragging()
    }
  }
}
</script>

<style lang="scss" scoped>
.box {
    border: 1px solid gray;
    background-color: white;
    padding: 0.5rem 1rem;
    margin-right: 1.5rem;
    margin-bottom: 1.5rem;
    cursor: move;
    float: left;

    &.dragging {
        opacity: 0.4;
    }
}
</style>
