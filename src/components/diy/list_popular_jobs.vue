<template>
	<div class="diy_home diy_list diy_popular_jobs" id="diy_popular_jobs_list">
		<!-- 列表 -->
		<div class="diy_view_list list list-x" v-if="show">
			<router-link class="diy_card goods diy_list_box_wrap" v-for="(o, i) in list" :key="i"
				:to="'/popular_jobs/details?popular_jobs_id=' + o['popular_jobs_id']">
				<!-- 图片 -->
				<div class="diy_list_img_box" v-if="imgList.length" >
					<div class="diy_row" v-for="(item,index) in imgList" :key="item+index" v-show="$check_field('get',item.name,'/popular_jobs/details') && +item.is_img_list">
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
						<div class="diy_row" :class="{[item.name]:true}" v-if="$check_field('get',item.name,'/popular_jobs/details') && +item.is_img_list">
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
							<th class="diy_title" v-if="$check_field('get','business_address')">
						企业地址
					</th>
							<th class="diy_title" v-if="$check_field('get','enterprise_logo')">
						企业logo
					</th>
							<th class="diy_title" v-if="$check_field('get','contacts')">
						联系人
					</th>
							<th class="diy_title" v-if="$check_field('get','consultation_telephone')">
						咨询电话
					</th>
							<th class="diy_title" v-if="$check_field('get','recruitment_positions')">
						招聘岗位
					</th>
							<th class="diy_title" v-if="$check_field('get','job_type')">
						工作类型
					</th>
							<th class="diy_title" v-if="$check_field('get','number_of_recruiters')">
						招聘人数
					</th>
							<th class="diy_title" v-if="$check_field('get','salary')">
						薪资
					</th>
							<th class="diy_title" v-if="$check_field('get','work_address')">
						工作地址
					</th>
							<th class="diy_title" v-if="$check_field('get','fringe_benefits')">
						福利待遇
					</th>
							<th class="diy_title" v-if="$check_field('get','position_information')">
						职位信息
					</th>
							<th class="diy_title" v-if="$check_field('get','recruitment_requirements')">
						招聘要求
					</th>
					</tr>
				<tr class="diy_row" v-for="(o,i) in list" :key="o+i">
						<td class="diy_field diy_text" v-if="$check_field('get','enterprise_name')">
						<span>
							{{ o["enterprise_name"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','business_address')">
						<span>
							{{ o["business_address"] }}
						</span>
					</td>
							<td class="diy_field" v-if="$check_field('get','enterprise_logo')">
						<img class="diy_img" :src="o['enterprise_logo']" />
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','contacts')">
						<span>
							{{ o["contacts"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','consultation_telephone')">
						<span>
							{{ o["consultation_telephone"] }}
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
							<td class="diy_field diy_text" v-if="$check_field('get','number_of_recruiters')">
						<span>
							{{ o["number_of_recruiters"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','salary')">
						<span>
							{{ o["salary"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','work_address')">
						<span>
							{{ o["work_address"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','fringe_benefits')">
						<span>
							{{ o["fringe_benefits"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','position_information')">
						<span>
							{{ o["position_information"] }}
						</span>
					</td>
							<td class="diy_field diy_text" v-if="$check_field('get','recruitment_requirements')">
						<span>
							{{ o["recruitment_requirements"] }}
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
						{
							title: "企业logo",
							name: "enterprise_logo",
							type: "图片",
							is_img_list: "1"
						},
						],
						itemList: [
								{
									title: "企业名称",
									name: "enterprise_name",
									type: "文本",
									is_img_list: "1"
								},
								{
									title: "企业地址",
									name: "business_address",
									type: "文本",
									is_img_list: "1"
								},
								{
									title: "联系人",
									name: "contacts",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "咨询电话",
									name: "consultation_telephone",
									type: "文本",
									is_img_list: "0"
								},
								{
									title: "招聘岗位",
									name: "recruitment_positions",
									type: "文本",
									is_img_list: "1"
								},
								{
									title: "工作类型",
									name: "job_type",
									type: "下寻",
									is_img_list: "0"
								},
								{
									title: "招聘人数",
									name: "number_of_recruiters",
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
									title: "工作地址",
									name: "work_address",
									type: "文本",
									is_img_list: "0"
								},
						],
						richList: [
								{
									title: "福利待遇",
									name: "fringe_benefits",
									type: "多文本"
								},
								{
									title: "职位信息",
									name: "position_information",
									type: "多文本"
								},
								{
									title: "招聘要求",
									name: "recruitment_requirements",
									type: "多文本"
								},
						],
																};
		},
		methods: {
			get_user_name(name,id){
				var obj = null;
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
															},
		created() {
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

