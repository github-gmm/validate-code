<template>
	<view class="content">
		<!-- 验证码 输入框 -->
		<view class="code-list">
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['one']?'input-focus':'']"
					type="number"
					v-model="one"
					label-position="left"
					@focus="inputFocusObj['one']=true;one=''"
					@blur="inputFocusObj['one']=false">
			</view>
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['two']?'input-focus':'']"
					type="number"
					maxlength="1"
					v-model="two"
					@focus="inputFocusObj['two']=true;two=''"
					@blur="inputFocusObj['two']=false"
					@keyup.delete.native="del(0)"
					label-position="left">
			</view>
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['three']?'input-focus':'']"
					type="number"
					maxlength="1"
					v-model="three"
					@focus="inputFocusObj['three']=true;three=''"
					@blur="inputFocusObj['three']=false"
					@keyup.delete.native="del(1)"
					label-position="left">
			</view>
			<view> - </view>
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['four']?'input-focus':'']"
					type="number"
					maxlength="1"
					v-model="four"
					@focus="inputFocusObj['four']=true;four=''"
					@blur="inputFocusObj['four']=false"
					@keyup.delete.native="del(2)"
					label-position="left">
			</view>
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['five']?'input-focus':'']"
					type="number"
					maxlength="1"
					v-model="five"
					@focus="inputFocusObj['five']=true;five=''"
					@blur="inputFocusObj['five']=false"
					@keyup.delete.native="del(3)"
					label-position="left">
			</view>
			<view class="input-code-view">
				<input :class="['input-text', inputFocusObj['six']?'input-focus':'']"
					type="number"
					maxlength="1"
					v-model="six"
					@focus="inputFocusObj['six']=true;six=''"
					@blur="inputFocusObj['six']=false"
					@keyup.delete.native="del(4)"
					label-position="left">
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				inputFocusObj: {
					pwd: false,
					one: false,
					two: false,
					three: false,
					four: false,
					five: false,
					six: false,
            	},
				one: '',
				two: '',
				three: '',
				four: '',
				five: '',
				six: '',
			}
		},
		watch: {
			one(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 ){
					if (val.length > 1) {
						this.copyFlag = true
						this.$nextTick(()=>{
							this.one = val.slice(0,1)
							this.two = val.slice(1,2)
							this.three = val.slice(2,3)
							this.four = val.slice(3,4)
							this.five = val.slice(4,5)
							this.six = val.slice(5,6)
						
						})
						setTimeout(() => {
							this.copyFlag = false;
						}, 0);
						inputList[0].blur();
					}
					if(!this.copyFlag) {
						inputList[1].focus();
					}
				}else {
					if (val && String(val).indexOf('.') > -1) {
						this.one = 0;
						inputList[1].focus();
					}
				}
			},
			two(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 && !this.copyFlag){
					inputList[2].focus();
				}
			},
			three(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 && !this.copyFlag){
					inputList[3].focus();
				}
			},
			four(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 && !this.copyFlag){
					inputList[4].focus();
				}
			},
			five(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 && !this.copyFlag){
					inputList[5].focus();
				}
			},
			six(val){
				let value = Number(val)
				let inputList = document.querySelectorAll('.uni-input-input');
				if ((value || val === '0') && value>-1 && !this.copyFlag){
					inputList[5].blur();
					uni.pageScrollTo({
						scrollTop: 0,
						duration: 0
					})
				}
			}
		},
		methods: {
			del(flag) {
				let inputList = document.querySelectorAll('.uni-input-input');
				inputList[flag].focus();
			},
		}
	}
</script>

<style lang="stylus" scoped>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.code-list {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;
    }
    .input-code-view {
        opacity: 1;
        border-radius: 32rpx;
        display: flex;
        align-items: center;
        justify-content: center;
        .input-text {
            width: 20rpx;
            height: 96rpx;
            padding: 0 38rpx;
            border-radius: 32rpx;
            background: #f6f6f6;
            border: 2rpx solid #f6f6f6;
            font-size: 32rpx;
            font-family: Alibaba, Alibaba-PuHuiTi;
            font-weight: PuHuiTi;
            color: #333333;
            line-height: 44rpx;
            text-align: center;
        }
    }
</style>
