<template>
  <el-row :gutter="40" class="panel-group">
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('newVisitis')">
        <div class="card-panel-icon-wrapper icon-people">
          <svg-icon icon-class="peoples" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div align="center">
            当前区块链高度 : <font color="blueviolet" style="font-size: 30px;">{{channelBlockInfo.data.height.low}}</font>
          </div>
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('messages')">
        <div class="card-panel-icon-wrapper icon-message">
          <svg-icon icon-class="message" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            消息
          </div>
          <count-to :start-val="0" :end-val="81212" :duration="3000" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('purchases')">
        <div class="card-panel-icon-wrapper icon-money">
          <svg-icon icon-class="money" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            金额
          </div>
          <count-to :start-val="0" :end-val="9280" :duration="3200" class="card-panel-num" />
        </div>
      </div>
    </el-col>
    <el-col :xs="12" :sm="12" :lg="6" class="card-panel-col">
      <div class="card-panel" @click="handleSetLineChartData('shoppings')">
        <div class="card-panel-icon-wrapper icon-shopping">
          <svg-icon icon-class="shopping" class-name="card-panel-icon" />
        </div>
        <div class="card-panel-description">
          <div class="card-panel-text">
            订单
          </div>
          <count-to :start-val="0" :end-val="13600" :duration="3600" class="card-panel-num" />
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<!--<script>-->
<!--import CountTo from 'vue-count-to'-->

<!--export default {-->
<!--  components: {-->
<!--    CountTo-->
<!--  },-->
<!--  methods: {-->
<!--    handleSetLineChartData(type) {-->
<!--      this.$emit('handleSetLineChartData', type)-->
<!--    }-->
<!--  }-->
<!--}-->
<!--</script>-->

<script>
import axios from 'axios'
export default{
  data(){
    return{
      queryBlockByNumDrawer:false,
      channelBlockInfo:'',
      blockInfo:'',
      previousBlockInfo:'',
      previousBlockInfo2:'',
      previousBlockInfo3:'',
      previousBlockInfo4:'',
      open:false,
      blockInfoHash:'',
    }
  },
  created() {
    this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/channelBlockInfo")
      .then(res => {
        this.channelBlockInfo = res;
        //当前区块
        var number = Number(this.channelBlockInfo.data.height.low - 1);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+number)
          .then(res => {
            this.blockInfo = res;
          }).catch(err => {
          console.log("err "+err)
        })

        //前一个区块
        var previous = Number(this.channelBlockInfo.data.height.low - 2);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+previous)
          .then(res => {
            this.previousBlockInfo = res;
          }).catch(err => {
          console.log("err "+err)
        })

        //前2个区块
        var previous2 = Number(this.channelBlockInfo.data.height.low - 3);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+previous2)
          .then(res => {
            this.previousBlockInfo2 = res;
          }).catch(err => {
          console.log("err "+err)
        })

        //前3个区块
        var previous3 = Number(this.channelBlockInfo.data.height.low - 4);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+previous3)
          .then(res => {
            this.previousBlockInfo3 = res;
          }).catch(err => {
          console.log("err "+err)
        })

        //前4个区块
        var previous4 = Number(this.channelBlockInfo.data.height.low - 5);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+previous4)
          .then(res => {
            this.previousBlockInfo4 = res;
          }).catch(err => {
          console.log("err "+err)
        })

        //前5个区块
        var previous5 = Number(this.channelBlockInfo.data.height.low - 5);
        this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+previous5)
          .then(res => {
            this.previousBlockInfo5 = res;
          }).catch(err => {
          console.log("err "+err)
        })

      }).catch(err => {
      console.log("err "+err)
    })

    //this.getHash();
  },
  methods:{
    queryInfo(hash){
      this.open = true
      this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockBuHash?hash="+hash)
        .then(res => {
          this.blockInfoHash = res;
        }).catch(err => {
        console.log("err "+err)
      })
    },

    getHash(){
      var number = Number(this.channelBlockInfo.data.height.low );
      this.$httpBlock.get(this.$httpUrl+"/blockexplorerapi/queryBlockInfo?number="+number)
        .then(res => {
          this.blockInfo = res;
        }).catch(err => {
        console.log("err "+err)
      })
    },

    queryBlockByNum(){
      this.queryBlockByNumDrawer = true;
    }

  },
}
</script>
<style lang="scss" scoped>
.panel-group {
  margin-top: 18px;

  .card-panel-col {
    margin-bottom: 32px;
  }

  .card-panel {
    height: 108px;
    cursor: pointer;
    font-size: 12px;
    position: relative;
    overflow: hidden;
    color: #666;
    background: #fff;
    box-shadow: 4px 4px 40px rgba(0, 0, 0, .05);
    border-color: rgba(0, 0, 0, .05);

    &:hover {
      .card-panel-icon-wrapper {
        color: #fff;
      }

      .icon-people {
        background: #40c9c6;
      }

      .icon-message {
        background: #36a3f7;
      }

      .icon-money {
        background: #f4516c;
      }

      .icon-shopping {
        background: #34bfa3
      }
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
      float: left;
      margin: 14px 0 0 14px;
      padding: 16px;
      transition: all 0.38s ease-out;
      border-radius: 6px;
    }

    .card-panel-icon {
      float: left;
      font-size: 48px;
    }

    .card-panel-description {
      float: right;
      font-weight: bold;
      margin: 26px;
      margin-left: 0px;

      .card-panel-text {
        line-height: 18px;
        color: rgba(0, 0, 0, 0.45);
        font-size: 16px;
        margin-bottom: 12px;
      }

      .card-panel-num {
        font-size: 20px;
      }
    }
  }
}

@media (max-width:550px) {
  .card-panel-description {
    display: none;
  }

  .card-panel-icon-wrapper {
    float: none !important;
    width: 100%;
    height: 100%;
    margin: 0 !important;

    .svg-icon {
      display: block;
      margin: 14px auto !important;
      float: none !important;
    }
  }
}
</style>
