<template>
  <my-table :data="list_commodity">
    <template v-slot:table_header>
      <th>#</th>
      <th>商品</th>
      <th>价格</th>
      <th>标签</th>
      <th>操作</th>
    </template>

    <template v-slot:table_body="{ item, index }">
      <td>{{ index + 1 }}</td>
      <td>{{ item.commodityDesc }}</td>
      <td>￥{{ item.commodityPrice }}</td>
      <td>

        <button type="button" class="btn btn-danger btn-sm" @click="item.isshow=true">+Tag</button>
        <input type="text" class="form-control" id="formGroupExampleInput" placeholder="+Tag"
               v-if="item.isshow" @keyup.enter="addTag(item.tag,$event)">
        <button type="button" class="btn btn-warning btn-sm">{{ item.tag }}</button>
      </td>
      <td>
        <button type="button" class="btn btn-danger btn-sm" @click="delItem(item.gid)">删除</button>
      </td>
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
    let {data: ret} = await this.$http.get('/commodity');
    for (let item of ret.data) {
      item.isshow = false;
      if (item.tag) {
        item.tag = item.tag.split(',');
        console.log(item.tag);
      }
    }
    this.list_commodity = ret.data;
  },
  methods: {
    addTag(tag, e) {
      tag.push(e.target.value);
      e.target.value = '';
    },
    delItem(gid) {
      this.list_commodity = this.list_commodity.filter(x => x.gid !== gid)
    }
  }
}
</script>

<style lang="less" scoped>
.form-control {
  display: inline;
  width: 100px;
}
</style>