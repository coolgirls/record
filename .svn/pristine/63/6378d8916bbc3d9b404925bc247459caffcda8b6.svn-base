<template>
	<view class="content">
		<view class="list-item" v-for="(item,index) of lists" @click="goSkip" :data-id="item.ID" :data-status="item.Status">
			<view class="item-left">
				<view class="left-desc"><label>姓名：</label><text>{{item.Name}}</text></view>
				<view class="left-desc"><label>联系电话：</label><text>{{item.Phone}}</text></view>
				<view class="left-desc"><label>申请日期：</label><text>2019-11-7 15:00</text></view>
			</view>
			<view class="item-right blue" v-if="item.Status==0">待审核</view>
			<view class="item-right red" v-else-if="item.Status==-1">不通过</view>
			<view class="item-right blue" v-else>通过</view>
		</view>	
	</view>
</template>

<script>
	import webSite from '../../config.js'
	var _self,timer = null;
	export default {
		data() {
			return {
				lists:[],
				type:'',
				page:1
			}
		},
		onLoad(options) {
			this.type=options.type;
			var page=this.page;
			_self = this;
			if(_self.type==1){
				_self.userList(page)
			}else{
				_self.adminList(page)
			}
		},
		onPage(){
			var type=_self.type;
			if(type==0){
				_self.adminList(page)
			}
		},
		onReachBottom:function(){
		  if(timer != null){
		   clearTimeout(timer);
		  }
		  timer = setTimeout(function(){
			var type=_self.type;
			var page=_self.page*1+1;
			console.log('触底',page);
			if(type==1){
				_self.userList(page)
			}else{
				_self.adminList(page)
			}  
		  }, 1000);
		},
		methods: {
           userList(pageNum){
			   let pageIndex = pageNum;
			   var phone=uni.getStorageSync('phone');
			   var name=uni.getStorageSync('name');
			   uni.request({
			      	url:webSite.url+'AuditInfo/QueryAuditPageList',
			      	data:{
						'page':pageIndex,
						'limit':5,
						'Name':name,
						'Phone':phone
					},
			      	header: {
			      		'Content-Type': 'application/x-www-form-urlencoded',
			      		'Accept':'application/json'
			      	},
			      	method: 'GET',
			      	success:(res)=>{
			      		console.log('用户',res);
						console.log('pageu',this.page);
						if(res.data.code="0"){
							if(res.data.data != undefined){
								if (pageIndex > 1){
								  var listBefore = _self.lists;
								  var currentList = res.data.data;
								  _self.lists=listBefore.concat(currentList);
								}else{
								  _self.lists=res.data.data;
								}
							  }
							_self.page=pageIndex;
						}else{
							uni.showToast({
								title:res.data.ErrMsg
							})
						}
			      	}
			   })
		   },
		   adminList(pageNum){
			    let pageIndex = pageNum;
			   uni.request({
			      	url:webSite.url+'AuditInfo/QueryAuditPage',
			      	data:{
						'page':pageIndex,
						'limit':5
					},
			      	header: {
			      		'Content-Type': 'application/x-www-form-urlencoded',
			      		'Accept':'application/json'
			      	},
			      	method: 'GET',
			      	success:(res)=>{
			      		console.log('管理员',res);
						console.log('pageA',_self.page);
						if(res.data.code="0"){
							if(res.data.data != undefined){
								if (pageIndex > 1){
								  var listBefore = _self.lists;
								  var currentList = res.data.data;
								  _self.lists=listBefore.concat(currentList);
								}else{
								  _self.lists=res.data.data;
								}
							  }
							_self.page=pageIndex;
						}else{
							uni.showToast({
								title:res.data.ErrMsg
							})
						}
			      	}
			   })
		   },
		   /*跳转*/
		   goSkip(e){
			   console.log('e',e);
			   var ID=e.target.dataset.id;
			   var status=e.target.dataset.status;
			   console.log('ID',ID);
			   var type=_self.type;
			   if(type==1){
			   	 uni.navigateTo({
			   	 	url:'../approveDetail/approveDetail?id='+ID
			   	 })
			   }else{
				  if(status==0){
					  uni.navigateTo({
					  	url:'../approve/approve?id='+ID
					  })
				  }else{
					 uni.navigateTo({
					 	url:'../approveDetail/approveDetail?id='+ID
					 }) 
				  }
			   }  
		   }
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f7f9;
	}
	.content {
		font-size:14px;
		.list-item{
			display: flex;
			justify-content: space-between;
			background:#fff;
			border-radius:8upx;
			padding:16upx;
			margin:40upx 30upx;
			.item-left{
				display: flex;
				flex-direction: column;
				.left-desc{
					display: flex;
					height:40upx;
					margin-bottom:20upx;
					label{
						width: 160upx;
						display: flex;
					}
				}
			}
			.item-right{
				&.red{
					color: #e51c23;
				}
				&.blue{
					color: #00b7ee;
				}
			}
		}
        
	}
</style>
