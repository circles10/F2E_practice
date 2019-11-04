<template>
  <div class="title">
    <div class="green-rect"></div>
    <div>{{titleName}}</div>
  </div>
</template>

<script>
  export default {
    name: 'component-title',
    props: ['titleName']
  }
</script>

<style lang="scss" scoped>
.title {
  background-color: #F0F0F0;
  padding: 15px;
  font-size: 20px;
  font-weight: bold;
  border: 1px #D0D0D0 solid;
}

.green-rect {
  background-color: #00A600;
  width: 6px;
  height: 24px;
  float: left;
  margin-right: 10px;
}
</style>