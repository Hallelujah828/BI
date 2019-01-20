<template>
  <el-row :gutter="40" class="panel-group">
    <el-col v-for="(item, index) in cardPanels" :key="index" :xs="6" :sm="6" :lg="6" class="card-panel-col">
      <div class="card-panel">
        <div>
          <div class="card-panel-text">当前服务中订单</div>
          <div class="panel-item">
            <div class="card-panel-icon-wrapper icon-people">
              <svg-icon icon-class="peoples" class-name="card-panel-icon" />
            </div>
            <div class="card-panel-description">
              <count-to :start-val="0" :end-val="102400" :duration="2600" class="card-panel-num"/>
            </div>
          </div>
        </div>
        <div>
          <div class="card-panel-text">当前服务中订单收入</div>
          <div class="panel-item">
            <div class="card-panel-icon-wrapper icon-people">
              <svg-icon icon-class="peoples" class-name="card-panel-icon" />
            </div>
            <div class="card-panel-description">
              <count-to :start-val="0" :end-val="102400" :duration="2600" class="card-panel-num"/>
            </div>
          </div>
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
import CountTo from 'vue-count-to'

export default {
  components: {
    CountTo
  },
  data() {
    return {
      cardPanels: [{}, {}, {}, {}, {}, {}, {}, {}]
    }
  },
  methods: {
    handleSetLineChartData(type) {
      this.$emit('handleSetLineChartData', type)
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.panel-group {
  margin-left: -10px;
  margin-right: -10px;
  .card-panel-col{
    padding: 10px !important;
    margin-bottom: 32px;
  }
  .card-panel {
    font-size: 12px;
    position: relative;
    overflow: hidden;
    color: #666;
    background: #fff;
    padding:20px;
    box-shadow: 4px 4px 40px rgba(0, 0, 0, .05);
    border-color: rgba(0, 0, 0, .05);
    box-sizing: border-box;
    .panel-item{
      display: flex;
      align-items: center;
      height: 50px;
    }
    .icon-people {
      color: #40c9c6;
    }
    .icon-message {
      color: #36a3f7;
    }
    .icon-money {
      color: #f4516c;
    }
    .icon-shopping {
      color: #34bfa3
    }
    .card-panel-icon-wrapper {
      transition: all 0.38s ease-out;
      border-radius: 6px;
    }
    .card-panel-icon {
      font-size: 30px;
    }
    .card-panel-description {
      .card-panel-num {
        font-weight: bold;
        font-size: 20px;
        margin-left: 20px;
      }
    }
    .card-panel-text {
        font-weight: bold;
        line-height: 18px;
        color: rgba(0, 0, 0, 0.45);
        font-size: 16px;
      }
  }
}
</style>
