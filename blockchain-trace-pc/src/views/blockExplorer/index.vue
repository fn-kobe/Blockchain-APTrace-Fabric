<template>
	<div class="app-container">
		<el-card style="width: 70%;height:100%;float: left;margin-left: 15px;">
			<div align="center">
				<el-tag type="info">区</el-tag>&nbsp;&nbsp;&nbsp;
				<el-tag type="warning">块</el-tag>&nbsp;&nbsp;&nbsp;
				<el-tag type="danger">信</el-tag>&nbsp;&nbsp;&nbsp;
				<el-tag>息</el-tag>
			</div><br>
			<el-card>
				<el-row>
					<el-col :span="24">区块编号：{{ blockInfo.data.header.number }}</el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">前置Hash：<el-link @click="queryInfo(blockInfo.data.header.previous_hash)" type="success">{{ blockInfo.data.header.previous_hash }}</el-link></el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">数据Hash：<el-link @click="queryInfo(blockInfo.data.header.data_hash)" type="success">{{ blockInfo.data.header.data_hash }}</el-link></el-col>
				</el-row>
			</el-card>
			<div align="center">
			<i class="el-icon-top"></i>
			<br>
			</div>
			<el-card>
				<el-row>
					<el-col :span="24">区块编号：{{ previousBlockInfo.data.header.number }}</el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">前置Hash：<el-link @click="queryInfo(previousBlockInfo.data.header.previous_hash)" type="success">{{ previousBlockInfo.data.header.previous_hash }}</el-link></el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">数据Hash：<el-link @click="queryInfo(previousBlockInfo.data.header.data_hash)" type="success">{{ previousBlockInfo.data.header.data_hash }}</el-link></el-col>
				</el-row>
			</el-card>
			<div align="center">
			<i class="el-icon-top"></i>
			<br>
			</div>

			<el-card>
				<el-row>
					<el-col :span="24">区块编号：{{ previousBlockInfo2.data.header.number }}</el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">前置Hash：<el-link @click="queryInfo(previousBlockInfo2.data.header.previous_hash)" type="success">{{ previousBlockInfo2.data.header.previous_hash }}</el-link></el-col>
				</el-row>
				<br>
				<el-row>
					<el-col :span="24">数据Hash：<el-link @click="queryInfo(previousBlockInfo2.data.header.data_hash)" type="success">{{ previousBlockInfo2.data.header.data_hash }}</el-link></el-col>
				</el-row>
			</el-card>

      <div align="center">
        <i class="el-icon-top"></i>
        <br>
      </div>
      <el-card>
        <el-row>
          <el-col :span="24">区块编号：{{ previousBlockInfo3.data.header.number }}</el-col>
        </el-row>
        <br>
        <el-row>
          <el-col :span="24">前置Hash：<el-link @click="queryInfo(previousBlockInfo3.data.header.previous_hash)" type="success">{{ previousBlockInfo3.data.header.previous_hash }}</el-link></el-col>
        </el-row>
        <br>
        <el-row>
          <el-col :span="24">数据Hash：<el-link @click="queryInfo(previousBlockInfo3.data.header.data_hash)" type="success">{{ previousBlockInfo3.data.header.data_hash }}</el-link></el-col>
        </el-row>
      </el-card>

      <div align="center">
        <i class="el-icon-top"></i>
        <br>
      </div>
      <el-card>
        <el-row>
          <el-col :span="24">区块编号：{{ previousBlockInfo4.data.header.number }}</el-col>
        </el-row>
        <br>
        <el-row>
          <el-col :span="24">前置Hash：<el-link @click="queryInfo(previousBlockInfo4.data.header.previous_hash)" type="success">{{ previousBlockInfo4.data.header.previous_hash }}</el-link></el-col>
        </el-row>
        <br>
        <el-row>
          <el-col :span="24">数据Hash：<el-link @click="queryInfo(previousBlockInfo4.data.header.data_hash)"type="success">{{ previousBlockInfo4.data.header.data_hash }}</el-link></el-col>
        </el-row>
      </el-card>

		</el-card>

		<el-card style="width: 27%;height: 100%;margin-left: 15px;float: right;">
			<div align="center">
				<font color="cornflowerblue">区块链网络信息</font>
			</div><br>
			<el-card style="width: 100%;">
				<div align="center">
					区块高度 : <font color="blueviolet" style="font-size: 30px;">{{channelBlockInfo.data.height.low}}</font>
				</div>
			</el-card>
			<el-card style="width: 100%;">
				<div align="center">
					通道 : <font color="blueviolet">tradingchannel</font>
				</div>
			</el-card>
			<el-card style="width: 100%;">
				<div align="center">
					节点信息<br><br>
				区块证书节点:<el-tag type="danger">blocknet.ca.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				网络共识节点:<el-tag type="warning">net.orderer.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				需求服务节点:<el-tag>peer0.org1.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				供应服务节点:<el-tag>peer0.org2.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				原料厂商节点:<el-tag>peer0.org3.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				零售服务节点:<el-tag>peer0.org4.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				物流公司节点:<el-tag>peer0.org5.trading.com</el-tag>&nbsp;&nbsp;&nbsp;<br><br>
				</div>
			</el-card>
		</el-card>

		<el-dialog center title="当前区块详情信息" :visible.sync="open" width="900px" append-to-body>
			<json-viewer :value="blockInfoHash" expand-depth=5 copyable boxed></json-viewer>
		</el-dialog>
	</div>
</template>

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

<style>
</style>
