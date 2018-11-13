<template>
  <table>
    <thead>
      <transition-group name="flip-list" tag="tr">
        <th 
          v-for="column in columns" :key="`column-${column}`"
          :class="[isDraggbleColumn == column ? 'draggble' : '']"
          v-text="column"
          @mousedown="isDraggbleColumn = column"
          @mouseover="sort(column)"
          @mouseup="isDraggbleColumn = ''"
        />
      </transition-group>
    </thead>
    <tbody>
      <template v-for="(row, index) in rows">
      <transition-group name="flip-list" tag="tr" :key="`row-${index}`">
        <td 
          v-for="column in columns" :key="`column-${index}-${column}`"
          :class="[isDraggbleColumn == column ? 'draggble' : '']"
          v-text="row[column]"
        />
      </transition-group>
      </template>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'TableSortable',
  props: {
    rows:    { type: Array, default: () => ([]) },
    columns: { type: Array, default: () => ([]) },
  },
  data: () => ({
    isDraggbleColumn: null
  }),
  created() {
    document.onmouseup = this.ClearDraggble
  },
  beforeDestroy() {
    document.removeEventListener('mouseup', this.ClearDraggble)
  },
  methods: {
    sort(column2) {
      if (!this.isDraggbleColumn || column2 == this.isDraggbleColumn) return;
      let columns = [...this.columns]
      let indexColumn1 = columns.findIndex( column => column == this.isDraggbleColumn )
      columns.splice(indexColumn1, 1)
      let indexColumn2 = columns.findIndex( column => column == column2 )
      let append = (indexColumn1 == indexColumn2) ? 1 : 0;
      columns.splice(indexColumn2 + append, 0, this.isDraggbleColumn)
      this.$emit('sort', columns)
    },
    ClearDraggble() {
      this.isDraggbleColumn = null
    }
  }
}
</script>

<style scoped lang="scss">
@import '../assets/var.scss';
table {
  width: 100%;
  border: #{$border};
  background-color: $color-bg;

  thead th {
    border-bottom: #{$border};
    cursor: move;
    user-select: none;
  }

  .draggble { background-color: $color-bg-active; }
}
</style>

<style lang="scss" scoped>
.flip-list-move {
  transition: transform .3s;
}
</style>
