<template>
  <div class="container">
    <div class="panel-top">
      <div class="flex-align">
        <label class="justify-label">城市</label>：
        <p>浙江省-杭州市</p>
      </div>
      <div class="flex-align">
        <label class="justify-label">医院</label>：
        <p>浙江明州康复医院</p>
      </div>
      <div class="flex-align">
        <label class="justify-label">是否有效</label>：
        <el-select v-model="effective" style="width:130px;" >
          <el-option
            v-for="(item, index) in effectives"
            :key="index"
            :value="item"/>
        </el-select>
      </div>
    </div>
    <div class="panel-middle-wrap">
      <div class="panel-half-width">
        <p class="panel-large-title">特价医院配置</p>
        <div class="panel-input">
          <label class="panel-title">【标准价格】</label>
          <div class="panel-input-wrap">
            <div class="flex-align flex-1">
              <label class="justify-label">半护理</label>(24h）：
              <el-input v-model="hospitalSemiCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">半护理</label>(12h）：
              <el-input v-model="hospitalSemiCare12" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">全护理</label>(24h）：
              <el-input v-model="hospitalFullCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">全护理</label>(12h）：
              <el-input v-model="hospitalFullCare12" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">特重护理</label>(24h）：
              <el-input v-model="hospitalSpecialCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">特重护理</label>(12h）：
              <el-input v-model="hospitalSpecialCare12" style="width:100px;" class="input-spacing"/>元
            </div>
          </div>
        </div>
        <div class="panel-item-wrap" style="margin-top:20px;">
          <div class="panel-btm-half">
            <label class="panel-title">【一对多价格】</label>
            <div class="panel-input">
              <el-radio v-model="extraPriceRadio" label="1" class="flex-radio">
                <p>按价格系数</p>
              </el-radio>
              <div class="radio-content">
                <span>一对二价格系数：</span>
                <el-input style="width:100px;" class="input-spacing"/>
                <span>一对三价格系数：</span>
                <el-input style="width:100px;" class="input-spacing"/>
              </div>
              <el-radio v-model="extraPriceRadio" label="2" class="flex-radio">
                <p>按固定价格</p>
              </el-radio>
              <div class="list-wrap">
                <div v-for="(item, index) in listGroups" :key="index" class="list-item-pos">
                  <el-select v-model="item.nurseType" style="width:130px;" >
                    <el-option
                      v-for="(item, index) in nurseTypes"
                      :key="index"
                      :value="item"/>
                  </el-select>
                  <el-select v-model="item.nurseKind" style="width:130px;" >
                    <el-option
                      v-for="(item, index) in nurseKinds"
                      :key="index"
                      :value="item"/>
                  </el-select>
                  <el-input style="width:100px;" class="input-spacing"/>元
                  <el-button v-if="index === 0" type="primary" size="small" plain @click="addList">添加</el-button>
                  <el-button v-if="index !== 0" type="danger" size="small" plain @click="deleteList(index)">删除</el-button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="panel-half-width">
        <label class="panel-title">【管理费】</label>
        <label class="panel-title">自主接单</label>
        <div class="panel-input">
          <el-radio v-model="selfOrder" label="1" class="flex-radio pos-radio">
            <span>固定价格</span>
            <el-input v-model="selfOrderFixPrice" style="width:100px;" class="input-spacing"/>元
          </el-radio>
          <el-radio v-model="selfOrder" label="2" class="flex-radio pos-radio">
            <span>梯度价格</span>
          </el-radio>
          <div class="list-wrap">
            <div v-for="(item, index) in gradientPrice" :key="index" class="list-item-pos">
              订单日价
              <el-input v-model="item.gradientPriceForm" style="width:100px;" class="input-spacing"/>元至
              <el-input v-model="item.gradientPriceTo" style="width:100px;" class="input-spacing"/>元 收取
              <el-input v-model="item.gradientPriceReceive" style="width:100px;" class="input-spacing"/>元
              <el-button v-if="index === 0" type="primary" size="small" plain @click="addGradientPrice">添加</el-button>
              <el-button v-if="index !== 0" type="danger" size="small" plain @click="deleteGradientPrice(index)">删除</el-button>
            </div>
          </div>
        </div>
        <label class="panel-title" style="margin-top:30px;">平台派单</label>
        <div class="panel-input">
          <el-radio v-model="platformOrder" label="1" class="flex-radio pos-radio">
            <span>固定价格</span>
            <el-input v-model="platformOrderFixPrice" style="width:100px;" class="input-spacing"/>元
          </el-radio>
          <el-radio v-model="platformOrder" label="2" class="flex-radio pos-radio">
            <span>梯度价格</span>
          </el-radio>
          <div class="list-wrap">
            <div v-for="(item, index) in platformGradientPrice" :key="index" class="list-item-pos">
              订单日价
              <el-input v-model="item.gradientPriceForm" style="width:100px;" class="input-spacing"/>元至
              <el-input v-model="item.gradientPriceTo" style="width:100px;" class="input-spacing"/>元 收取
              <el-input v-model="item.gradientPriceReceive" style="width:100px;" class="input-spacing"/>元
              <el-button v-if="index === 0" type="primary" size="small" plain @click="addPlatformGradientPrice">添加</el-button>
              <el-button v-if="index !== 0" type="danger" size="small" plain @click="deletePlatformGradientPrice(index)">删除</el-button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="form-btn-wrap">
      <el-button type="primary">保存</el-button>
      <el-button type="info">取消</el-button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HospitalPrice',
  data() {
    return {
      effectives: ['是', '否'],
      effective: '',
      hospitalSemiCare24: '',
      hospitalSemiCare12: '',
      hospitalFullCare24: '',
      hospitalFullCare12: '',
      hospitalSpecialCare24: '',
      hospitalSpecialCare12: '',
      hospitalSelfOrderRadio: 1,
      hospitalFixPriceSelfOrder: '',
      hospitalPercentSelfOrder: '',
      hospitalPlatformOrderRadio: 1,
      hospitalFixPricePlatformOrder: '',
      hospitalPercentPlatformOrder: '',
      extraPriceRadio: '1',
      listGroups: [{
        nurseType: '',
        nurseKind: ''
      }, {
        nurseType: '',
        nurseKind: ''
      }],
      nurseTypes: ['半护理', '全护理', '特重护理'],
      nurseKinds: ['一对二', '一对三'],
      selfOrder: '1',
      gradientPrice: [{}, {}],
      selfOrderFixPrice: '',
      platformOrderFixPrice: '',
      platformOrder: '1',
      platformGradientPrice: [{}, {}]
    }
  },
  methods: {
    addList: function() {
      this.listGroups.push({})
    },
    deleteList: function(index) {
      this.listGroups.splice(index, 1)
    },
    addGradientPrice: function() {
      this.gradientPrice.push({})
    },
    deleteGradientPrice: function(index) {
      this.gradientPrice.splice(index, 1)
    },
    addPlatformGradientPrice: function() {
      this.platformGradientPrice.push({})
    },
    deletePlatformGradientPrice: function(index) {
      this.platformGradientPrice.splice(index, 1)
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .container{
    width: 100%;
    min-height: 100vh;
    position: relative;
    padding: 30px;
    box-sizing: border-box;
    background: #f1f1f1;
    font-size: 14px;
    .panel-top{
      display: flex;
      width: 100%;
      height: 80px;
      background: #fff;
      align-items: center;
      padding: 0 40px;
      justify-content: space-between;
      box-sizing: border-box;
    }
    .flex-align{
      display: flex;
      align-items: center;
    }
    .justify-label{
      width: 65px;
      height: 36px;
      text-align: justify;
      text-align-last: justify;
      margin-top: 18px;
      font-weight: 400;
      &:after {
        display: inline-block;
        content: '';
        overflow: hidden;
        width: 100%;
        height: 0;
      }
    }
    .panel-middle-wrap{
      width: 100%;
      margin-top: 20px;
      display: flex;
      justify-content: space-between;
      .panel-half-width{
        width: 50%;
        background: #fff;
        padding: 10px 20px;
        box-sizing: border-box;
      }
    }
    .flex-1{
      flex: 1;
    }
    .pos-radio{
      margin-top: 10px !important;
    }
    .panel-input-wrap{
      display: flex;
      flex-wrap: wrap;
    }
  }
  .panel-large-title{
    font-size: 16px;
    font-weight: bold;
    display: block;
  }
  .panel-title{
    font-size: 14px;
    font-weight: bold;
    display: block;
    margin-top: 10px;
  }
  .input-spacing{
    margin-right: 10px;
  }
  .el-radio+.el-radio{
    margin: 0;
  }
  .panel-bottom-wrap{
    width: 100%;
    margin-top: 20px;
    position: relative;
    background: #fff;
    padding: 10px 20px;
    box-sizing: border-box;
    .panel-item-wrap{
      width: 100%;
      display: flex;
      .panel-btm-half{
        width: 50%;
      }
    }
  }
  .flex-radio{
    width: 100%;
    display: flex;
    align-items: center;
  }
  .list-item-pos{
    margin-top: 10px;
  }
  .fix-sm-title{
    width: 70px;
    display: inline-block;
  }
  .form-btn-wrap{
    width: 100%;
    padding: 20px 0;
    box-sizing: border-box;
    background: #fff;
    display: flex;
    justify-content: center;
  }
</style>
