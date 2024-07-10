<template>
	<div class="diy_edit page_submit_resume" id="submit_resume_edit">
		<div class='warp'>
			<div class='container'>
				<div class='row diy_edit_content_box'>
						<div v-if="$check_field('set','enterprise_name') || $check_field('add','enterprise_name') || $check_field('get','enterprise_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								企业名称:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_enterprise_name" v-model="form['enterprise_name']" placeholder="请输入企业名称" v-if="(form['enterprise_name'] && $check_field('set','enterprise_name')) || (!form['enterprise_name'] && $check_field('add','enterprise_name'))"  :disabled="disabledObj['enterprise_name_isDisabled']"/>
							<span v-else-if="$check_field('get','enterprise_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','contacts') || $check_field('add','contacts') || $check_field('get','contacts')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								联系人:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_contacts" v-model="form['contacts']" placeholder="请输入联系人" v-if="(form['contacts'] && $check_field('set','contacts')) || (!form['contacts'] && $check_field('add','contacts'))"  :disabled="disabledObj['contacts_isDisabled']"/>
							<span v-else-if="$check_field('get','contacts')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','recruitment_positions') || $check_field('add','recruitment_positions') || $check_field('get','recruitment_positions')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								招聘岗位:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_recruitment_positions" v-model="form['recruitment_positions']" placeholder="请输入招聘岗位" v-if="(form['recruitment_positions'] && $check_field('set','recruitment_positions')) || (!form['recruitment_positions'] && $check_field('add','recruitment_positions'))"  :disabled="disabledObj['recruitment_positions_isDisabled']"/>
							<span v-else-if="$check_field('get','recruitment_positions')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','job_type') || $check_field('add','job_type') || $check_field('get','job_type')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								工作类型:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_job_type" v-model="form['job_type']" placeholder="请输入工作类型" v-if="(form['job_type'] && $check_field('set','job_type')) || (!form['job_type'] && $check_field('add','job_type'))"  :disabled="disabledObj['job_type_isDisabled']"/>
							<span v-else-if="$check_field('get','job_type')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','salary') || $check_field('add','salary') || $check_field('get','salary')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								薪资:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_salary" v-model="form['salary']" placeholder="请输入薪资" v-if="(form['salary'] && $check_field('set','salary')) || (!form['salary'] && $check_field('add','salary'))"  :disabled="disabledObj['salary_isDisabled']"/>
							<span v-else-if="$check_field('get','salary')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','user') || $check_field('add','user') || $check_field('get','user')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								用户:
							</span>
						</div>
						<div class="diy_field diy_down">
							<select id="form_user" :disabled="disabledObj['user_isDisabled']" v-model="form['user']" v-if="(form['user'] && $check_field('set','user')) || (!form['user'] && $check_field('add','user'))" >
								<option v-for="o in list_user_user" :value="o['user_id']">
									{{o['nickname'] + '-' + o['username']}}
								</option>
							</select>
							<span v-else-if="$check_field('get','user')">{{ form['user'] }}</span>
						</div>
					</div>
							<div v-if="$check_field('set','job_applicants_name') || $check_field('add','job_applicants_name') || $check_field('get','job_applicants_name')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								求职人姓名:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_job_applicants_name" v-model="form['job_applicants_name']" placeholder="请输入求职人姓名" v-if="(form['job_applicants_name'] && $check_field('set','job_applicants_name')) || (!form['job_applicants_name'] && $check_field('add','job_applicants_name'))"  :disabled="disabledObj['job_applicants_name_isDisabled']"/>
							<span v-else-if="$check_field('get','job_applicants_name')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','job_intention') || $check_field('add','job_intention') || $check_field('get','job_intention')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								求职意向:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_job_intention" v-model="form['job_intention']" placeholder="请输入求职意向" v-if="(form['job_intention'] && $check_field('set','job_intention')) || (!form['job_intention'] && $check_field('add','job_intention'))"  :disabled="disabledObj['job_intention_isDisabled']"/>
							<span v-else-if="$check_field('get','job_intention')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','education') || $check_field('add','education') || $check_field('get','education')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								学历:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_education" v-model="form['education']" placeholder="请输入学历" v-if="(form['education'] && $check_field('set','education')) || (!form['education'] && $check_field('add','education'))"  :disabled="disabledObj['education_isDisabled']"/>
							<span v-else-if="$check_field('get','education')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','graduation_school') || $check_field('add','graduation_school') || $check_field('get','graduation_school')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								毕业学校:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_graduation_school" v-model="form['graduation_school']" placeholder="请输入毕业学校" v-if="(form['graduation_school'] && $check_field('set','graduation_school')) || (!form['graduation_school'] && $check_field('add','graduation_school'))"  :disabled="disabledObj['graduation_school_isDisabled']"/>
							<span v-else-if="$check_field('get','graduation_school')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','major') || $check_field('add','major') || $check_field('get','major')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								专业:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_major" v-model="form['major']" placeholder="请输入专业" v-if="(form['major'] && $check_field('set','major')) || (!form['major'] && $check_field('add','major'))"  :disabled="disabledObj['major_isDisabled']"/>
							<span v-else-if="$check_field('get','major')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','gender') || $check_field('add','gender') || $check_field('get','gender')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								性别:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_gender" v-model="form['gender']" placeholder="请输入性别" v-if="(form['gender'] && $check_field('set','gender')) || (!form['gender'] && $check_field('add','gender'))"  :disabled="disabledObj['gender_isDisabled']"/>
							<span v-else-if="$check_field('get','gender')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','age') || $check_field('add','age') || $check_field('get','age')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								年龄:
							</span>
						</div>
								<!-- 文本 -->
									<div class="diy_field diy_text">
							<input type="text" id="form_age" v-model="form['age']" placeholder="请输入年龄" v-if="(form['age'] && $check_field('set','age')) || (!form['age'] && $check_field('add','age'))"  :disabled="disabledObj['age_isDisabled']"/>
							<span v-else-if="$check_field('get','age')">{{ form['${obj.name}'] }}</span>
						</div>
										</div>
							<div v-if="$check_field('set','personal_introduction') || $check_field('add','personal_introduction') || $check_field('get','personal_introduction')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								个人介绍:
							</span>
						</div>
								<!-- 多文本 -->
						<div class="diy_field diy_desc">
							<textarea id="form_personal_introduction" v-model="form['personal_introduction']" v-if="(form['personal_introduction'] && $check_field('set','personal_introduction')) || (!form['personal_introduction'] && $check_field('add','personal_introduction'))" :disabled="disabledObj['personal_introduction_isDisabled']" />
							<span v-else-if="$check_field('get','personal_introduction')">{{ form['${obj.name}'] }}</span>
						</div>
							</div>
							<div v-if="$check_field('set','curriculum_vitae') || $check_field('add','curriculum_vitae') || $check_field('get','curriculum_vitae')" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								个人简历:
							</span>
						</div>
								<!-- 文件 -->
						<input type="file" style="display: none;" id="form_file_curriculum_vitae" title="curriculum_vitae" @change="change_file($event.target.files,'curriculum_vitae')"/>
						<!-- 修改权限 -->
						<div class="diy_field diy_img" v-if="form['curriculum_vitae'] && $check_field('set','curriculum_vitae')">
							<label for="form_file_curriculum_vitae">
								<!--<span>{{form['curriculum_vitae']}} </span>-->
								<a :href="$fullUrl(form['curriculum_vitae'])" target="_blank" style="color: rgb(64, 158, 255);">点击下载</a>
							</label>
						</div>
						<!-- 添加权限 -->
						<div class="diy_field diy_img" v-else-if="!form['curriculum_vitae'] && $check_field('add','curriculum_vitae')">
							<label for="form_file_curriculum_vitae">
								<div class="btn_add_img">
									<span>+</span>
								</div>
							</label>
						</div>
						<!-- 查询权限 -->
						<div class="diy_field diy_img" v-else-if="$check_field('get','curriculum_vitae')">
							<span>{{form['curriculum_vitae']}} </span>
						</div>
							</div>
	


					<div v-if="user_group === '管理员' || $check_examine()" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								审核状态:
							</span>
						</div>
						<div class="diy_field diy_select" v-if="$check_action('/submit_resume/edit','examine')">
							<!--<span> {{ form['examine_state'] }} </span>-->
							<select v-model="form['examine_state']">
								<option value="未审核">
									未审核
								</option>
								<option value="已通过">
									已通过
								</option>
								<option value="未通过">
									未通过
								</option>
							</select>
						</div>
						<div class="diy_field diy_text" v-else>
							<span>
								{{ form['examine_state'] }}
							</span>
						</div>
					</div>
					<div v-if="user_group === '管理员' || $check_examine()" class="form-item col-12 col-md-6">
						<div class="diy_title">
							<span>
								审核回复:
							</span>
						</div>
						<div class="diy_field diy_desc" v-if="$check_action('/submit_resume/edit','examine')">
							<textarea v-model="form['examine_reply']"></textarea>
						</div>
						<div class="diy_field diy_text" v-else>
							<span>
								{{ form['examine_reply'] }}
							</span>
						</div>
					</div>


				</div>
				<div class="diy_edit_submit_box row">
					<div class="col-12">
						<div class="btn_box">
							<button class="btn_submit" @click="submit()">提交</button>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import mixin from "@/mixins/page.js";
	export default {
		mixins: [mixin],
		components: {},
		data() {
			return {
				url_get_obj: "~/api/submit_resume/get_obj?",
				url_add: "~/api/submit_resume/add?",
				url_set: "~/api/submit_resume/set?",

				// 登录权限
				oauth: {
					"signIn": true,
					"user_group": []
				},

				// 查询条件
				query: {
						"enterprise_name": "",
							"contacts": "",
							"recruitment_positions": "",
							"job_type": "",
							"salary": "",
							"user": 0,
							"job_applicants_name": "",
							"job_intention": "",
							"education": "",
							"graduation_school": "",
							"major": "",
							"gender": "",
							"age": "",
							"personal_introduction": "",
							"curriculum_vitae": "",
						"submit_resume_id": 0,
				},

				obj: {
						"enterprise_name":  '', // 企业名称
							"contacts":  '', // 联系人
							"recruitment_positions":  '', // 招聘岗位
							"job_type":  '', // 工作类型
							"salary":  '', // 薪资
							"user": 0, // 用户
							"job_applicants_name":  '', // 求职人姓名
							"job_intention":  '', // 求职意向
							"education":  '', // 学历
							"graduation_school":  '', // 毕业学校
							"major":  '', // 专业
							"gender":  '', // 性别
							"age":  '', // 年龄
							"personal_introduction":  '', // 个人介绍
							"curriculum_vitae":  '', // 个人简历
						"examine_state": "未审核",
					"examine_reply": "",
					"submit_resume_id": 0,
				},

				// 表单字段
				form: {
						"enterprise_name":  '', // 企业名称
							"contacts":  '', // 联系人
							"recruitment_positions":  '', // 招聘岗位
							"job_type":  '', // 工作类型
							"salary":  '', // 薪资
							"user": 0, // 用户
							"job_applicants_name":  '', // 求职人姓名
							"job_intention":  '', // 求职意向
							"education":  '', // 学历
							"graduation_school":  '', // 毕业学校
							"major":  '', // 专业
							"gender":  '', // 性别
							"age":  '', // 年龄
							"personal_introduction":  '', // 个人介绍
							"curriculum_vitae":  '', // 个人简历
						"examine_state": "未审核",
					"examine_reply": "",
					"submit_resume_id": 0,
				},
				disabledObj:{
						"enterprise_name_isDisabled": false,
							"contacts_isDisabled": false,
							"recruitment_positions_isDisabled": false,
							"job_type_isDisabled": false,
							"salary_isDisabled": false,
							"user_isDisabled": false,
							"job_applicants_name_isDisabled": false,
							"job_intention_isDisabled": false,
							"education_isDisabled": false,
							"graduation_school_isDisabled": false,
							"major_isDisabled": false,
							"gender_isDisabled": false,
							"age_isDisabled": false,
							"personal_introduction_isDisabled": false,
							"curriculum_vitae_isDisabled": false,
					},

																// 用户列表
				list_user_user: [],
																			
				// ID字段
				field: "submit_resume_id",

			}
		},
		methods: {
			
				
				
				
				
						/**
			 * 获取注册用户用户列表
			 */
			async get_list_user_user() {
				// if(this.user_group !== "管理员" && this.form["user"] === 0) {
				//     this.form["user"] = this.user.user_id;
				// }
				var json = await this.$get("~/api/user/get_list?user_group=注册用户");
				if(json.result && json.result.list){
					this.list_user_user = json.result.list;
				}
				else if(json.error){
					console.error(json.error);
				}
			},
					async get_user_session_user(){
				var _this = this;
				var json = await this.$get("~/api/user_group/get_obj?name=注册用户");
				if(json.result && json.result.obj){
					var source_table = json.result.obj.source_table;
					var user_id = _this.$store.state.user.user_id;
					if (user_id){
						var url = "~/api/"+source_table+"/get_obj?"
						this.$get(url, {"user_id":_this.$store.state.user.user_id}, function(res) {
							if (res.result && res.result.obj) {
								var arr = []
								for (let key in res.result.obj) {
									arr.push(key)
								}
								var arrForm = []
								for (let key in _this.form) {
									arrForm.push(key)
								}
								_this.form["user"] = user_id
								_this.disabledObj['user' + '_isDisabled'] = true
								for (var i=0;i<arr.length;i++){
                  if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
                    for (var j = 0; j < arrForm.length; j++) {
                      if (arr[i] === arrForm[j]) {
                        if (arr[i] !== "user") {
                          _this.form[arrForm[j]] = res.result.obj[arr[i]]
                          _this.disabledObj[arrForm[j] + '_isDisabled'] = true
                          break;
                        }
                      }
                    }
                  }
								}
							}
						});
					}
				}
				else if(json.error){
					console.error(json.error);
				}
			},
	
				
				
				
				
				
				
				
				
				
	
			/**
			 * 修改文件
			 * @param { Object } files 上传文件对象
			 * @param { String } str 表单的属性名
			 */
			change_file(files, str) {
				var form = new FormData();
				form.append("file", files[0]);
				this.$post("~/api/submit_resume/upload?", form, (res) => {
					if (res.result) {
						this.form[str] = res.result.url;
					} else if (res.error) {
						this.$toast(res.error.message);
					}
				});
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_before(param){
				var form = $.db.get("form");
				// if (form) {
        //   delete(form.examine_state)
        //   delete(form.examine_reply)
        //   this.obj = $.push(this.obj ,form);
				// 	this.form = $.push(this.form ,form);
				// }
				// var arr = []
				// for (let key in form) {
				// 	arr.push(key)
				// }
				// for (var i=0;i<arr.length;i++){
				// 	this.disabledObj[arr[i] + '_isDisabled'] = true
				// }
        if (form) {
          var arr = []
          for (let key in form) {
            arr.push(key)
          }
          var arrForm = []
          for (let key in this.form) {
            arrForm.push(key)
          }
          for (var i=0;i<arr.length;i++){
            if (arr[i]!=='examine_state' && arr[i]!=='examine_reply') {
              for (var j = 0; j < arrForm.length; j++) {
                if (arrForm[j] === arr[i]) {
                  this.form[arrForm[j]] = form[arr[i]]
                  this.obj[arrForm[j]] = form[arr[i]]
                  this.disabledObj[arrForm[j] + '_isDisabled'] = true
                  break;
                }
              }
            }
          }
        }
																														
        $.db.del("form");
				return param;
			},

			/**
			 * 获取对象后获取缓存表单
			 * @param {Object} json
			 * @param {Object} func
			 */
			get_obj_after(json ,func){
				// var form = $.db.get("form");
				// var obj = Object.assign({} ,form ,this.obj);
				// if (obj) {
        //   delete(obj.examine_state)
        //   delete(obj.examine_reply)
				// 	this.obj = $.push(this.obj ,obj);
				// }
				// if (form) {
        //   delete(form.examine_state)
        //   delete(form.examine_reply)
				// 	this.form = $.push(this.form ,form);
				// }

				if(func){
					func(json);
				}
			},

		},
		created() {
																				this.get_user_session_user();
					this.get_list_user_user();
																														},
	}
</script>

<style>




</style>
