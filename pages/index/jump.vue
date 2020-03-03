<template>
	<view class="content">
		<image class="logo" src="../../static/logo.png"></image>
		<view class="text-area">
			<view class="title" @click="getAuthCode">钉钉获取授权</view>
			<view class="title" @click="chooseDing">钉钉从钉盘选择文件</view>
			<view class="title" @click="chooseDirectory">钉钉从选取钉盘目录</view>
			<view class="title" @click="chooseChat">钉钉选择会话</view>
		</view>
	</view>
</template>

<script>
	export default {
		onLoad() {},
		computed: {},
		created() {},
		data() {
			return {}
		},
		methods: {
			chooseChat(){
				dd.chooseChat({
				    isAllowCreateGroup:false,//是否允许创建会话
				    filterNotOwnerGroup:false,//是否限制为自己创建的会话
				    success: res => {
				       console.log(JSON.stringify(res));
				    },
				    fail: err =>{
				        // dd.alert({
				        //     content:JSON.stringify(err)
				        // })
				    }
				})
			},
			chooseDirectory() {
				dd.chooseDingTalkDir({
					success: (res) => {
						console.log(JSON.stringify(res));
					},
					fail: (err) => {
						// uni.showToast({
						// 	title:'23333'
						// })
						// dd.alert({
						// 	content: JSON.stringify(err)
						// })
					}
				})
			},
			chooseDing() {
				dd.uploadAttachmentToDingTalk({
					image: {
						multiple: true,
						compress: false,
						max: 9,
						spaceId: "2292514952"
					},
					space: {
						spaceId: "2292514952",
						isCopy: 1,
						max: 9
					},
					file: {
						spaceId: "2292514952",
						max: 1
					},
					types: ["photo", "camera", "file", "space"], //PC端仅支持["photo","file","space"]
					success: (res) => {
						console.log(JSON.stringify(res));
					},
					fail: (err) => {
						// dd.alert({
						// 	content: JSON.stringify(err)
						// })
					}
				})
			},
			getAuthCode() {
				dd.getAuthCode({
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			}
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}

	.logo {
		height: 200upx;
		width: 200upx;
		margin-top: 200upx;
	}

	.title {
		font-size: 36upx;
		color: #8f8f94;
		padding: 10upx;
	}
</style>
