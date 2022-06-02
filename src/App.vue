<template>
  <my-table :data="list_commodity">
    <template v-slot:table_header>
      <th>#</th>
      <th>商品</th>
      <th>价格</th>
      <th>标签</th>
      <th>操作</th>
    </template>
  </my-table>
</template>

<script>
import MyTable from "./components/MyTable.vue";

export default {
  name: 'App',
  components: {
    MyTable
  },
  data() {
    return {
      list_commodity: [],
    }
  },
  async created() {
    let {data} = await this.$http.get('/commodity');
    this.list_commodity = data.data;
    console.log(this.list_commodity)
  }
}
</script>