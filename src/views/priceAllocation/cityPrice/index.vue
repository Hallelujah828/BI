<template>
  <div class="container">
    <div class="panel-top">
      <div class="flex-align">
        <label class="justify-label">城市</label>：
        <el-select v-model="provinceValue" style="width:130px;" >
          <el-option
            v-for="(provinceItem, provinceIndex) in provinceOptions"
            :key="provinceIndex"
            :value="provinceItem"/>
        </el-select>
        <el-select v-model="cityValue" style="width:130px; margin-left:10px;" >
          <el-option
            v-for="(cityItem, cityIndex) in cityOptions"
            :key="cityIndex"
            :value="cityItem"/>
        </el-select>
      </div>
      <div class="flex-align">
        <label class="justify-label">城市经理</label>：
        <el-input v-model="cityManager" style="width:150px;"/>
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
        <p class="panel-large-title">医院价格配置</p>
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
          <label class="panel-title">【管理费】</label>
          <div>
            <el-radio-group v-model="hospitalSelfOrderRadio" class="panel-input-wrap">
              <el-radio :label="1" class="flex-align flex-1 pos-radio">
                <span>按固定价格（自主接单）</span>
                <el-input v-model="hospitalFixPriceSelfOrder" style="width:80px;" class="input-spacing"/>元
              </el-radio>
              <el-radio :label="2" class="flex-align flex-1 pos-radio">
                <span>按百分比（自主接单）</span>
                <el-input v-model="hospitalPercentSelfOrder" style="width:80px;" class="input-spacing"/>%
              </el-radio>
            </el-radio-group>
            <el-radio-group v-model="hospitalPlatformOrderRadio" class="panel-input-wrap">
              <el-radio :label="1" class="flex-align flex-1 pos-radio">
                <span>按固定价格（平台派单）</span>
                <el-input v-model="hospitalFixPricePlatformOrder" style="width:80px;" class="input-spacing"/>元
              </el-radio>
              <el-radio :label="2" class="flex-align flex-1 pos-radio">
                <span>按百分比（平台派单）</span>
                <el-input v-model="hospitalPercentPlatformOrder" style="width:80px;" class="input-spacing"/>%
              </el-radio>
            </el-radio-group>
          </div>
          <label class="panel-title">【保险费】</label>
          <div class="flex-align flex-1">
            <label class="justify-label">保险费</label>：
            <el-input v-model="hospitalInsurance" style="width:100px;" class="input-spacing"/>元
          </div>
        </div>
      </div>
      <div class="panel-half-width">
        <p class="panel-large-title">居家价格配置</p>
        <div class="panel-input">
          <label class="panel-title">【标准价格】</label>
          <div class="panel-input-wrap">
            <div class="flex-align flex-1">
              <label class="justify-label">半护理</label>(24h）：
              <el-input v-model="homeSemiCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">半护理</label>(12h）：
              <el-input v-model="homeSemiCare12" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">全护理</label>(24h）：
              <el-input v-model="homeFullCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">全护理</label>(12h）：
              <el-input v-model="homeFullCare12" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">特重护理</label>(24h）：
              <el-input v-model="homeSpecialCare24" style="width:100px;" class="input-spacing"/>元
            </div>
            <div class="flex-align flex-1">
              <label class="justify-label">特重护理</label>(12h）：
              <el-input v-model="homeSpecialCare12" style="width:100px;" class="input-spacing"/>元
            </div>
          </div>
          <label class="panel-title">【管理费】</label>
          <div>
            <el-radio-group v-model="homeSelfOrderRadio" class="panel-input-wrap">
              <el-radio :label="1" class="flex-align flex-1 pos-radio">
                <span>按固定价格（自主接单）</span>
                <el-input v-model="homeFixPriceSelfOrder" style="width:80px;" class="input-spacing"/>元
              </el-radio>
              <el-radio :label="2" class="flex-align flex-1 pos-radio">
                <span>按百分比（自主接单）</span>
                <el-input v-model="homePercentSelfOrder" style="width:80px;" class="input-spacing"/>%
              </el-radio>
            </el-radio-group>
            <el-radio-group v-model="homePlatformOrderRadio" class="panel-input-wrap">
              <el-radio :label="1" class="flex-align flex-1 pos-radio">
                <span>按固定价格（平台派单）</span>
                <el-input v-model="homeFixPricePlatformOrder" style="width:80px;" class="input-spacing"/>元
              </el-radio>
              <el-radio :label="2" class="flex-align flex-1 pos-radio">
                <span>按百分比（平台派单）</span>
                <el-input v-model="homePercentPlatformOrder" style="width:80px;" class="input-spacing"/>%
              </el-radio>
            </el-radio-group>
          </div>
          <label class="panel-title">【保险费】</label>
          <div class="flex-align flex-1">
            <label class="justify-label">保险费</label>：
            <el-input v-model="homeInsurance" style="width:100px;" class="input-spacing"/>元
          </div>
        </div>
      </div>
    </div>
    <div class="panel-bottom-wrap">
      <p class="panel-large-title">额外状况配置</p>
      <div class="panel-item-wrap">
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
        <div class="panel-btm-half">
          <label class="panel-title">【节假日调整】</label>
          <el-radio-group v-model="holidayPriceRadio">
            <el-radio :label="1" class="flex-align flex-1 pos-radio" style="width:100%;">
              <span class="fix-sm-title">按固定价格</span>
              <el-select v-model="fixPriceAdjust" style="width:130px; margin-left:10px;" >
                <el-option
                  v-for="(item, index) in priceAdjust"
                  :key="index"
                  :value="item"/>
              </el-select>
              <el-input v-model="holidayFixPriceValue" class="input-spacing" style="width:100px;"/>元
            </el-radio>
            <el-radio :label="2" class="flex-align flex-1 pos-radio" style="width:100%;">
              <span class="fix-sm-title">按百分比</span>
              <el-select v-model="percentPriceAdjust" style="width:130px; margin-left:10px;" >
                <el-option
                  v-for="(item, index) in priceAdjust"
                  :key="index"
                  :value="item"/>
              </el-select>
              <el-input v-model="holidayPercentPriceValue" class="input-spacing" style="width:100px;"/>元
            </el-radio>
          </el-radio-group>
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
  name: 'CityPrice',
  data() {
    return {
      provinceOptions: ['浙江省', '上海'],
      provinceValue: '',
      cityOptions: ['宁波市', '上海'],
      cityValue: '',
      cityManager: '',
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
      hospitalInsurance: '',
      homeSemiCare24: '',
      homeSemiCare12: '',
      homeFullCare24: '',
      homeFullCare12: '',
      homeSpecialCare24: '',
      homeSpecialCare12: '',
      homeSelfOrderRadio: 1,
      homeFixPriceSelfOrder: '',
      homePercentSelfOrder: '',
      homePlatformOrderRadio: 1,
      homeFixPricePlatformOrder: '',
      homePercentPlatformOrder: '',
      homeInsurance: '',
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
      holidayPriceRadio: 1,
      fixPriceAdjust: '',
      percentPriceAdjust: '',
      priceAdjust: ['上调', '下调'],
      holidayFixPriceValue: '',
      holidayPercentPriceValue: ''
    }
  },
  methods: {
    addList: function() {
      this.listGroups.push({})
    },
    deleteList: function(index) {
      this.listGroups.splice(index, 1)
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .container{
    width: 100%;
    position: relative;
    padding: 30px;
    box-sizing: border-box;
    background: #f1f1f1;
    font-size: 14px;
    min-height: 100vh;
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
        width: 49.3%;
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
