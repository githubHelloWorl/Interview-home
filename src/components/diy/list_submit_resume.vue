<template>
	<div class="diy_home diy_list diy_submit_resume" id="diy_submit_resume_list">
		<!-- 列表 -->
		<div class="diy_view_list list list-x" v-if="show">
			<router-link class="diy_card goods diy_list_box_wrap" v-for="(o, i) in list" :key="i"
				:to="'/submit_resume/details?submit_resume_id=' + o['submit_resume_id']">
				<!-- 图片 -->
				<div class="diy_list_img_box" v-if="imgList.length" >
					<div class="diy_row" v-for="(item,index) in imgList" :key="item+index" v-show="$check_field('get',item.name,'/submit_resume/details') && +item.is_img_list">
						<div class="diy_title diy_list_img_title">
							<span>{{item.title}}:</span>
						</div>
						<div class="diy_field diy_img">
							<img :src="$fullUrl(o[item.name])" style="width:100%;height:100%" />
						</div>
					</div>
				</div>
				<!-- 内容 -->
				<div class="diy_list_item_box">
					<div class="diy_list_item_content" v-for="(item,index) in showItemList" :key="item+index">
						<div class="diy_row" :class="{[item.name]:true}" v-if="$check_field('get',item.name,'/submit_resume/details') && +item.is_img_list">
							<div class="diy_title">
								<span>{{item.title}}:</span>
							</div>
							<div class="diy_field diy_text">
								<span v-if="item.type == 'UID'" v-text="get_user_name(item.name,o[item.name])"></span>
								<span v-else-if="item.type == '日期'" v-text="$toTime(o[item.name],'yyyy-MM-dd')"></span>
								<span v-else-if="item.type == '时间'" v-text="$toTime(o[item.name],'hh:mm:ss')"></span>
								<span v-else-if="item.type == '日长'" v-text="$toTime(o[item.name],'yyyy-MM-dd hh:mm:ss')"></span>
								<span v-else v-text="o[item.name]"></span>
							</div>
						</div>
					</div>
				</div>
			</router-link>
		</div>
		<!-- 表格 -->
		<div class="diy_view_table" v-else>
			<table class="diy_table">
				<tr class="diy_row">
						<th class="diy_title" v-if="$check_field('get','enterprise_name')">
						企业名称
					</th>
							<th class="diy_title" v-if="$check_field('get','contacts')">
						联系人
					</th>
							<th class="diy_title" v-if="$check_field('get','recruitment_positions')">
						招聘岗位
					</th>
							<th class="diy_title" v-if="$check_field('get','job_type')">
						工作类型
					</th>
							<th class="diy_title" v-if="$check_field('get','salary')">
						薪资
					</th>
							<th class="diy_title" v-if="$check_field('get','user')">
						用户
					</th>
							<th class="diy_title" v-if="$check_field('get','job_applicants_name')">
						求职人姓名
					</th>
							<th class="diy_title" v-if="$check_field('get','job_intention')">
						求职意向
					</th>
							<th class="diy_title" v-if="$check_field('get','education')">
						学历
					</th>
							<th class="diy_title" v-if="$check_field('get','graduation_school')">
						毕业学校
					</th>
							<th class="diy_title" v-if="$check_field('get','major')">
						专业
					</th>
							<th class="diy_title" v-if="$check_field('get','gender')">
						性别
					</th>
							<th class="diy_title" v-if="$check_field('get','age')">
						年龄
					</th>
							<th class="diy_title" v-if="$check_field('get','personal_introduction')">
						个人介绍
					</th>
							</tr>
				<tr class="diy_row" v-for="(o,i) in list" :key="o+i">
						<td class="diy_field diy_text" v-if="$check_field('get','enterprise_name')">
						<span>
							{{ o["enterprise_name"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','contacts')">
						<span>
							{{ o["contacts"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','recruitment_positions')">
						<span>
							{{ o["recruitment_positions"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','job_type')">
						<span>
							{{ o["job_type"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','salary')">
						<span>
							{{ o["salary"] }}
						</span>
					</td>
							<td class="diy_field diy_uid" v-if="$check_field('get','user')">
						<span>
							{{ get_user_name('user',o['user']) }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','job_applicants_name')">
						<span>
							{{ o["job_applicants_name"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','job_intention')">
						<span>
							{{ o["job_intention"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','education')">
						<span>
							{{ o["education"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','graduation_school')">
						<span>
							{{ o["graduation_school"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','major')">
						<span>
							{{ o["major"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','gender')">
						<span>
							{{ o["gender"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','age')">
						<span>
							{{ o["age"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','personal_introduction')">
						<span>
							{{ o["personal_introduction"] }}
						</span>
					</td>
							</tr>
			</table>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			list: {
				type: Array,
				default: function() {
					return [];
				},
			},
			show: {
				type: Boolean,
				default: function(){
					return true;
				}
			}
		},
		data() {
			return {
						imgList: [
						],
						itemList: [
								{
									title: "企业名称",
									name: "enterprise_name",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "联系人",
									name: "contacts",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "招聘岗位",
									name: "recruitment_positions",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "工作类型",
									name: "job_type",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "薪资",
									name: "salary",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "用户",
									name: "user",
									type: "UID",
									is_img_list: "0"
								},
								{
									title: "求职人姓名",
									name: "job_applicants_name",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "求职意向",
									name: "job_intention",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "学历",
									name: "education",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "毕业学校",
									name: "graduation_school",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "专业",
									name: "major",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "性别",
									name: "gender",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "年龄",
									name: "age",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "个人简历",
									name: "curriculum_vitae",
									type: "文件",
									is_img_list: "0"
								},
						],
						richList: [
								{
									title: "个人介绍",
									name: "personal_introduction",
									type: "多文本"
								},
						],
										// 用户列表
				list_user_user: [],
													};
		},
		methods: {
			get_user_name(name,id){
				var obj = null;
										if (name == 'user'){
					obj = this.list_user_user.getObj({"user_id":id});
				}
														var ret = "";
				if(obj){
					ret = obj.nickname+"-"+obj.username;
					// if(obj.nickname){
					// 	ret = obj.nickname;
					// }
					// else{
					// 	ret = obj.username;
					// }
				}
				return ret;
			},
									/**
			 * 获取注册用户用户列表
			 */
			async get_list_user_user() {
				var json = await this.$get("~/api/user/get_list?user_group=注册用户");
				if(json.result && json.result.list){
					this.list_user_user = json.result.list;
				}
				else if(json.error){
					console.error(json.error);
				}
			},
												},
		created() {
									this.get_list_user_user();
												},
		computed:{
			showItemList(){
				let arr = [];
				let _type = ["视频","音频","文件"];
				this.itemList.forEach(item => {
					if(_type.indexOf(item.type) === -1 && !!+item.is_img_list){
						arr.push(item)
					}
				})
				return arr.slice(0,4);
			}
		}
	};
</script>

<style scoped>
	.media {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		flex-basis: 75%;
		min-height: 10rem;
	}

	.goods {
		display: flex;
		width: calc(25% - 1rem);
		margin: 0.5rem;
		padding: 0.5rem;
		flex-direction: column;
		justify-content: space-between;
		background-color: white;
		border-radius: 0.5rem;
	}

	.goods:hover {
		border: 0.2rem solid #909399;
		box-shadow: 0 0.1rem 0.3rem rgba(0, 0, 0, 0.15);
	}

	.goods:hover img {
		filter: blur(1px);
	}

	.price {
		font-size: 1rem;
		margin-right: 3px;
	}

	.price_ago {
		text-decoration: line-through;
		font-size: 0.5rem;
		color: #999;

	}

	.title {
		word-break: break-all;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		font-weight: 700;
		padding: .25rem;
	}

	.icon_cart {
		color: #FF5722;
		float: right;
	}

	@media (max-width: 992px) {

		.goods {
			width: calc(33% - 1rem);
			;
		}

	}

	@media (max-width: 768px) {

		.goods {
			width: calc(50% - 1rem);
			;
		}

	}
</style>

