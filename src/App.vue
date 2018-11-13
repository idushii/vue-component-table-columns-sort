<template>
  <div id="app">
    <table-sortable 
      class="table" 
      :rows=rows 
      :columns=columns
      @sort="ColumnsSort => columns = ColumnsSort"
    />
  </div>
</template>

<script>
import TableSortable from './components/TableSortable.vue'

export default {
  name: 'app',
  data: () => ({
    columns: [ '#', 'ФИО', 'Адрес', 'Телефон' ],
    rows: [
      { '#': '1',   ФИО: 'Иван',    Адрес: 'Улица Ведеркина, дом 1, кв 1', Телефон: '+7 999 123 123' },
      { '#': '2',   ФИО: 'Женя',    Адрес: 'Улица Ведеркина, дом 2, кв 5', Телефон: '+7 999 554 123' },
      { '#': '3',   ФИО: 'Евгений', Адрес: 'Улица Ведеркина, дом 3, кв 3', Телефон: '+7 999 123 321' },
      { '#': '4',   ФИО: 'Дима',    Адрес: 'Улица Ведеркина, дом 4, кв 8', Телефон: '+7 999 777 123' },
    ]
  }),
  components: {
    TableSortable
  }
}
</script>

<style lang="scss">
@import 'assets/var.scss';
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $color;
  padding: 1rem;

}
</style>
