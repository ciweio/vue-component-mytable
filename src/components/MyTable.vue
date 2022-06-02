<template>
  <table class="table table-striped table-hover">
    <thead>
    <tr>
      <slot name="table_header"></slot>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item, index) in data" :key="item.gid">
      <slot name="table_body" :item="item" :index="index"></slot>
    </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "MyTable",
  props: {
    data: {
      type: Array,
      required: true,
      default: [],
    },
  },
}
</script>

<style lang="less" scoped>
table {
  width: 60%;
  margin: auto;
}
</style>