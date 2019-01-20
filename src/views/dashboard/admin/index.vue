<template>
  <div class="dashboard-editor-container">

    <panel-group/>

    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
      <line-chart :chart-data="firstLineChartData"/>
    </el-row>
    <el-row style="background:#fff;padding:16px 16px 0;margin-bottom:32px;">
      <line-chart :chart-data="secondLineChartData"/>
    </el-row>
  </div>
</template>

<script>
import PanelGroup from './components/PanelGroup'
import LineChart from './components/LineChart'

const firstLineChartData = {
  firstData: {
    actualData: [120, 82, 91, 154, 162, 140, 145]
  }
}
const secondLineChartData = {
  secondData: {
    actualData: [154, 140, 120, 145, 82, 91, 162]
  }
}

export default {
  name: 'DashboardAdmin',
  components: {
    PanelGroup,
    LineChart
  },
  data() {
    return {
      firstLineChartData: firstLineChartData.firstData,
      secondLineChartData: secondLineChartData.secondData
    }
  },
  methods: {
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}
</style>
