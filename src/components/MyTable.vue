<template>
  <table class="table table-striped table-hover">
    <thead>
      <tr>
        <slot name="table_header"></slot>
      </tr>
    </thead>
    <tbody>

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

</style>