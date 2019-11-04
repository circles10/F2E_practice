<template>
  <div>
    <div class="item" v-for="(info, index) in orders" :key="index">
      <table class="content">
        <tr>
          <td class="image-container">
            <img class="image-size" 
              :src="info.logo" 
              :class="{ grayscale: isCompleted(info.status.code) }">
          </td>
          <td>
            <span class="mrgn-R-40" :class="{ processing: isProcessing(info.status.code) }">
              {{info.status.type}}
            </span>
            <span v-if="isProcessing(info.status.code)">
              預計出貨：{{info.date}}
            </span>
            <div>
              {{info.name}}
            </div>
          </td>
          <td class="to-right">
            >
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'component-item',
    props: {
      orders: {
        type: Array,
        required: true
      }
    },
    data () {
      return {
      }
    },
    methods: {
      isProcessing (statusCode) {
        return (statusCode === 1 || statusCode === 2)
      },
      isCompleted (statusCode) {
        return (statusCode === 3 || statusCode === 4)
      }
    }
  }
</script>

<style lang="scss" scoped>
.item {
  font-size: 20px;
  font-weight: bold;
  border: 1px #D0D0D0 solid;
}

.content {
  width: 100%;
  line-height: 40px;
}

.image-size {
  width: 100px;
  height: 100px;
}

.image-container {
  width: 100px;
  height: 100px;
  text-align: center;
  padding: 20px;
}

.to-right {
  width: 45px;
  text-align: center;
  font-weight: bold;
  cursor: pointer;
}

.mrgn-R-40 {
 margin-right: 40px;
}

.processing {
  color: #00A600;
}

.grayscale {
  filter: grayscale(100%);
}
</style>