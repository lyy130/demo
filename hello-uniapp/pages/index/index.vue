<template>
	<view class="content">
		<view class="info paci">
			<view class="text-area">
				<view class="title">{{title}}</view>
			</view>
			<view class="much_container">
				<view :class="['much_box',current==index?'bgL':'bgA']" v-for="(item,index) in muchArr" @click="selectMuch(item,index)">{{item}}元</view>
			</view>
			<view class="text-area uni-form-item uni-column">
				<view class="title" id="moreMuch">其他充值金额</view>
				<view class="uni-form-item uni-column enter_much_box">
				    <input class="uni-input enter_much" auto-focus v-model="inputMuch"  @blur="enterMuch()"/>
				</view>
			</view>
			<view class="payment text-area">
				<view class="title">支付方式</view>
				<view class="paymentSelct">
					<!-- 微信 -->
					<view @click="weixin" ref="weixinRef"  :class="[isFlag[0]? 'bdA' : 'bdL']">
						<view>
							<image class="logD" src="/static/btn_weixin_01.png" v-if="isFlag[0]"></image>
							<image class="logD" src="/static/icon_weixin.png" v-else></image>
						</view>
						<view class="title">
							<text>微信支付</text>
							<text class="preferential">优惠</text>
							</view>
						<view>
							<image class="logo" src="/static/disabledbtn.png" v-if="isFlag[0]"></image>
							<image class="logo" src="/static/btn_gou.png" v-else></image>
						</view>
					</view>
					<!-- 支付宝 -->
					<view @click="zhifubao" ref="zhifubaoRef" :class="[isFlag[1]? 'bdA' : 'bdL']">
						<view>
							<image class="logD" src="/static/icon_zhifubao.png" v-if="isFlag[1]"></image>
							<image class="logD" src="/static/btn_zhifubao.png" v-else></image>
						</view>
						<view class="title">支付宝支付</view>
						<view>
							<image class="logo" src="/static/disabledbtn.png" v-if="isFlag[1]"></image>
							<image class="logo" src="/static/btn_gou.png" v-else></image>
						</view>
					</view>
					<!-- 银联 -->
					<view @click="yinlian" ref="yinlianRef" :class="[isFlag[2]? 'bdA' : 'bdL']">
						<view>
							<image class="logD" src="/static/icon_pay.png" v-if="isFlag[2]"></image>
							<image class="logD" src="/static/btn_pay.png" v-else></image>
						</view>
						<view class="title">银联支付</view>
						<view>
							<image class="logo" src="/static/disabledbtn.png" v-if="isFlag[2]"></image>
							<image class="logo" src="/static/btn_gou.png"  v-else></image>
						</view>
					</view>
					<!-- 更多 -->
					<view @click="gengduo" ref="gengduoRef" :class="[isFlag[3]? 'bdA' : 'bdL']" v-if='morePay'>
						<view>
							<image class="logD" src="/static/logo.png" v-if="isFlag[3]"></image>
							<image class="logD" src="/static/logo.png" v-else></image>
						</view>
						<view class="title">更多支付</view>
						<view>
							<image class="logo" src="/static/disabledbtn.png" v-if="isFlag[3]"></image>
							<image class="logo" src="/static/btn_gou.png"  v-else></image>
						</view>
					</view>
				</view>
				<view class="checkMore center" @click="clickCheckMore">+点击查看更多</view>
			</view>
		</view>
		<view class="pay_much paci">
			<view>
				<text id="payMuch">充值金额</text>
				<text style="font-size: 45rpx;">￥</text>
				<text style="font-size: 45rpx;">{{totolMuch}}</text>
			</view>
			<view id="payBtn">充值</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '充值金额',
				current:-1,
				muchArr:[5,10,30,50],
				isFlag:[true,true,true,true],
				totolMuch:0,
				morePay:false
			}
		},
		onLoad() {

		},
		methods: {
			//选择金额
			selectMuch(je,i){
				this.current = i;
				this.totolMuch = je;
			},
			//输入金额，失去焦点拿到金额渲染到下面
			enterMuch(){
				this.totolMuch = this.inputMuch;
			},
			//点击微信支付
			weixin(){
				this.muchArr.forEach((item,index) => {
					if(index !=0){
						this.$set(this.isFlag,index,true)
					}
					this.$set(this.isFlag,0,false)
				})
			},
			//点击支付宝支付
			zhifubao(){
				this.muchArr.forEach((item,index) => {
					if(index !=1){
						this.$set(this.isFlag,index,true)
					}
					this.$set(this.isFlag,1,false)
				})
				
			},
			//点击银联支付
			yinlian(){
				this.muchArr.forEach((item,index) => {
					if(index !=2){
						this.$set(this.isFlag,index,true)
					}
					this.$set(this.isFlag,2,false)
				})
			},
			//点击更多支付
			gengduo(){
				this.muchArr.forEach((item,index) => {
					if(index !=3){
						this.$set(this.isFlag,index,true)
					}
					this.$set(this.isFlag,3,false)
				})
			},
			clickCheckMore(){
				this.morePay = true;
			}
		}
	}
</script>

<style>
	 @import url("../../static/index.css");
	.content {
		display: flex;
		flex-direction: column;
		        width: 100%;
		        height: 100%;
		/* align-items: center;
		justify-content: center; */
	}
	.content .info{
		flex-wrap: wrap;
		position:relative;
		overflow:auto;
		flex: 1;
	}
	.logo {
		height: 30rpx;
		width: 30rpx;
	}
	.logD{
		height: 39rpx;
		width: 50rpx;
	}
	
	
</style>
