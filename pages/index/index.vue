<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<view class="title" @click="gotoNext">页面跳转</view>
			<view class="title" @click="scan">钉钉扫码</view>
			<!-- <view class="title" @click="uniScan">uni扫码</view> -->
			<view class="title" @click="select">钉钉选人</view>
			<view class="title" @click="selectPart">钉钉选部门</view>
			<view class="title" @click="createChat">钉钉创建群聊</view>
			<view class="title" @click="selectAddress">钉钉通讯录</view>
			<view class="title" @click="selectExternal">钉钉外部联系人</view>
			<view class="title" @click="editExternal">钉钉编辑外部联系人</view>
			<!-- <view class="title" @click="selectPeople">钉钉单选自定义联系人</view> -->
			<view class="title" @click="createDing">钉钉钉</view>
			<view class="title" @click="callPhone1">钉钉打电话</view>
			<view class="title" @click="saveFile">钉钉钉盘转存</view>
			<view class="title" @click="createTalk">钉钉会话</view>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {

		},
		onShareAppMessage(res) {
			console.log(res);
			return {
				title: '自定义分享标题',
				path: '/pages/test/test?id=123'
			}
		},
		created() {},
		methods: {
			uniScan() {
				uni.scanCode({})
			},
			callPhone1() {
				dd.showCallMenu({
					phoneNumber: '15201896096', // 期望拨打的电话号码
					code: '+86', // 国家代号，中国是+86
					showDingCall: true, // 是否显示钉钉电话
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			gotoNext() {
				uni.navigateTo({
					url: './jump'
				})
			},
			createTalk() {
				dd.chooseChatForNormalMsg({
					isConfirm: true, //是否弹出确认窗口，默认为true
					success: res => {
						console.log(JSON.stringify(res));
					},
					fail: err => {
						// dd.alert({
						//     content:JSON.stringify(err)
						// })
					}
				})
			},
			saveFile() {
				dd.saveFileToDingTalk({
					url: "https://file.1237125.cn/group1/M00/00/60/CgoDiF4EF5OAHcIKABd5NKwI8M4227.png?filename=untitled1.png", // 文件在第三方服务器地址
					name: "文件名",
					success: (res) => {
						console.log(JSON.stringify(res));
					},
					fail: (err) => {
						// dd.alert({
						//     content:JSON.stringify(err)
						// })
					}
				})
			},
			callPhone() {
				dd.callUsers({
					users: [], //用户列表，工号
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				})
			},
			createDing() {
				dd.createDing({
					users: [], //默认选中用户工号列表；类型: Array<String>
					corpId: "ding7799dc8f5c0d3b6a24f2f5cc6abecb85", // 类型: String
					alertType: 2, // 钉发送方式 0:电话, 1:短信, 2：应用内；类型 Number
					alertDate: {
						"format": "yyyy-MM-dd HH:mm",
						"value": "2019-08-29 08:25"
					}, // 非必选，定时发送时间, 非定时DING不需要填写
					type: 1, // 附件类型 1：image, 2：link；类型: Number

					// 非必选
					// 附件信息
					attachment: {
						images: ["https://www.baidu.com/img/bd_logo1.png?where=super"], // 图片附件, type=1时, 必选；类型: Array<String>
						image: "https://www.baidu.com/img/bd_logo1.png?where=super", // 链接附件, type=2时, 必选；类型: String    
						title: "这是一个测试", // 链接附件, type=2时, 必选；类型: String
						url: "https://www.baidu.com/", // 链接附件, type=2时, 必选；类型 String
						text: "测试发钉成功" // 链接附件, type=2时, 必选；类型: String
					},

					text: '', // 正文
					bizType: 2, // 业务类型 0：通知DING；1：任务；2：会议；

					// 任务信息
					// bizType=1的时候选填
					// taskInfo: {    
					//    ccUsers: ['100', '101'],// 抄送用户列表, 工号，类型: Array<String>
					//    deadlineTime: {"format":"yyyy-MM-dd HH:mm", "value":"2015-05-09 08:00"}, // 任务截止时间    
					//    taskRemind: 30 // 任务提醒时间, 单位分钟；支持参数: 0：不提醒；15：提前15分钟；60：提前1个小时；180：提前3个小时；1440：提前一天；类型: Number
					// },

					// 日程信息
					// bizType=2的时候选填
					// confInfo: {      
					//    bizSubType: 0,  // 子业务类型如会议: 0:预约会议, 1:预约电话会议, 2:预约视频会议；类型: Number (注: 目前只有会议才有子业务类型)；
					//    location: '某某会议室', // 会议地点(非必选)，类型: String    
					//    startTime: {"format":"yyyy-MM-dd HH:mm", "value":"2015-05-09 08:00"},// 会议开始时间  
					//    endTime: {"format":"yyyy-MM-dd HH:mm", "value":"2015-05-09 08:00"},// 会议结束时间    
					//    remindMinutes: 30, // 会前提醒。单位分钟；1:不提醒, 0:事件发生时提醒, 5:提前5分钟, 15:提前15分钟, 30:提前30分钟, 60:提前1个小时, 1440:提前一天
					//    remindType: 2 // 会议提前提醒方式；0:电话, 1:短信, 2:应用内；类型: Number
					// },

					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				})
			},
			selectPeople() {
				dd.chooseUserFromList({
					title: '选人的标题', //标题
					users: [], //一组员工userid
					isShowCompanyName: true, //true|false，默认为 false
					disabledUsers: [], //不能选的人
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			editExternal() {
				dd.editExternalUser({
					title: "测试标题", //标题
					emplId: "", //需要编辑的员工id，不填，则为新增外部联系人
					name: "", //需要新增的外部联系人的名字
					mobile: "", //需要预填的手机号
					companyName: "", //需要预填的公司名
					deptName: "", //预填部门名字
					job: "", //预填职位
					remark: "", //备注信息
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			selectExternal() {
				dd.chooseExternalUsers({
					title: "选择外部联系人",
					multiple: true, //是否多选  true多选，false单选，默认是单选
					limitTips: "超出了",
					maxUsers: 10, //默认不限制
					pickedUsers: [], //已选，但可取消，只针对多选生效
					disabledUsers: [], //不可选，只针对多选生效
					requiredUsers: [], //必选，只针对多选生效，不会在结果中返回
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			selectAddress() {
				dd.choosePhonebook({
					multiple: true, //是否多选： true多选 false单选； 默认true
					maxUsers: 2, //人数限制，当multiple为true才生效，可选范围1-1500
					limitTips: "xxx", //超过人数限制的提示语可以用这个字段自定义
					title: "good luck", // 如果你需要修改选人页面的title，可以在这里赋值
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			createChat() {
				dd.createGroupChat({
					users: [], //默认选中的userId列表
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
			scan() {
				dd.scan({
					type: 'qr',
					success: (res) => {
						console.log(JSON.stringify(res));
					},
				})
			},
			select() {
				dd.complexChoose({
					title: "选一个人", //标题
					multiple: true, //是否多选
					limitTips: "超出了", //超过限定人数返回提示
					maxUsers: 1000, //最大可选人数
					pickedUsers: [], //已选用户
					pickedDepartments: [], //已选部门
					disabledUsers: [], //不可选用户
					disabledDepartments: [], //不可选部门
					requiredUsers: [], //必选用户（不可取消选中状态）
					requiredDepartments: [], //必选部门（不可取消选中状态）
					permissionType: "xxx", //可添加权限校验，选人权限，目前只有GLOBAL这个参数
					responseUserOnly: true, //返回人，或者返回人和部门
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				})
			},
			selectPart() {
				dd.chooseDepartments({
					title: "测试标题", //标题
					multiple: true, //是否多选
					limitTips: "超出了", //超过限定人数返回提示
					maxDepartments: 100, //最大选择部门数量
					pickedDepartments: [], //已选部门
					disabledDepartments: [], //不可选部门
					requiredDepartments: [], //必选部门（不可取消选中状态）
					permissionType: "xxx", //选人权限，目前只有GLOBAL这个参数
					success: function(res) {
						console.log(JSON.stringify(res));
					},
					fail: function(err) {}
				});
			},
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
		flex-direction: column;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
		padding: 10upx;
	}
</style>
