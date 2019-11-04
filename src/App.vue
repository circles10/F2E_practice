<template>
  <div id="app">
    <Title :titleName="processing" />
    <Item :orders=setOrders(processing_list) />
    <Title :titleName="completed" />
    <Item :orders=setOrders(completed_list) />
  </div>
</template>

<script>
import Title from './components/title'
import Item from './components/item'
export default {
  name: 'app',
  data () {
    return {
      processing: '進行中',
      completed: '已完成',
      orders: [],
      processing_list: [],
      completed_list: [],
      sortName: 'date',
      isDesc: true
    }
  },
  components: {
    Title,
    Item
  },
  mounted () {
    this.$http.get('/data/item_info.json').then(function(res){
      this.orders = res.body.orders
      this.classifyOrders(this.orders)
      this.sortedBySortName(this.processing_list)
      this.sortedBySortName(this.completed_list)
    },function(){
      console.log('載入資料失敗')
    });
  },
  methods: {
    setOrders (list) {
      if (list !== undefined) {
        return list
      }
    },
    isProcessing (statusCode) {
      return (statusCode === 1 || statusCode === 2)
    },
    isCompleted (statusCode) {
      return (statusCode === 3 || statusCode === 4)
    },
    classifyOrders (list) {
      if (list !== undefined) {
        for (let i = 0; i < list.length; i++) {
          if (this.isProcessing(list[i].status.code)) {
            this.processing_list.push(list[i])
          } else if (this.isCompleted) {
            this.completed_list.push(list[i])
          }
        }
      }
    },
    compare (a, b) {
      if (a[this.sortName] < b[this.sortName]) {
        return -1
      }
      if (a[this.sortName] > b[this.sortName]) {
        return 1
      }
      return 0
    },
    sortedBySortName (list) {
      if (list !== undefined && list.length > 0) {
        list.sort(this.compare)

        if (this.isDesc) {
          list.reverse()
        }
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  margin: 60px auto 60px;
  color: #3C3C3C;
  max-width: 600px;
}
</style>
