<template>
  <div class="page_search">
	<div class="warp">
	  <div class="container">
		<div class="row">
		  <div class="col-12">
			<div class="card_result_search">
			  <div class="title">搜索结果</div>

				<!-- 文章搜索结果 -->
			  <list_result_search
				:list="result_article"
				title="招聘资讯"
				source_table="article"
			  ></list_result_search>

				<!-- 论坛搜索结果 -->
			  <list_result_search
				:list="result_forum"
				title="用户交流"
				source_table="forum"
			  ></list_result_search>

						  <list_result_search
				v-if="$check_action('/registered_users/list', 'get')"
				:list="result_registered_users_user_name"
				title="注册用户用户姓名"
				source_table="registered_users"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/registered_users/list', 'get')"
				:list="result_registered_users_gender"
				title="注册用户性别"
				source_table="registered_users"
			  ></list_result_search>
									  <list_result_search
				v-if="$check_action('/job_type/list', 'get')"
				:list="result_job_type_job_type"
				title="工作类型工作类型"
				source_table="job_type"
			  ></list_result_search>
									  <list_result_search
				v-if="$check_action('/popular_jobs/list', 'get')"
				:list="result_popular_jobs_enterprise_name"
				title="热门工作企业名称"
				source_table="popular_jobs"
			  ></list_result_search>
																				  <list_result_search
				v-if="$check_action('/popular_jobs/list', 'get')"
				:list="result_popular_jobs_recruitment_positions"
				title="热门工作招聘岗位"
				source_table="popular_jobs"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/popular_jobs/list', 'get')"
				:list="result_popular_jobs_job_type"
				title="热门工作工作类型"
				source_table="popular_jobs"
			  ></list_result_search>
																																	  <list_result_search
				v-if="$check_action('/submit_resume/list', 'get')"
				:list="result_submit_resume_recruitment_positions"
				title="投递简历招聘岗位"
				source_table="submit_resume"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/submit_resume/list', 'get')"
				:list="result_submit_resume_job_type"
				title="投递简历工作类型"
				source_table="submit_resume"
			  ></list_result_search>
																																																  <list_result_search
				v-if="$check_action('/experience_sharing/list', 'get')"
				:list="result_experience_sharing_share_theme"
				title="经验分享分享主题"
				source_table="experience_sharing"
			  ></list_result_search>
								  <list_result_search
				v-if="$check_action('/experience_sharing/list', 'get')"
				:list="result_experience_sharing_share_time"
				title="经验分享分享时间"
				source_table="experience_sharing"
			  ></list_result_search>
															</div>
		  </div>
		</div>
	  </div>
	</div>
  </div>
</template>

<script>
import mixin from "../../mixins/page.js";
import list_result_search from "../../components/diy/list_result_search.vue";

export default {
  mixins: [mixin],
  data() {
	return {
	  "query": {
		word: "",
	  },
	  "result_article": [],
	  "result_forum": [],
						"result_registered_users_user_name":[],
								"result_registered_users_gender":[],
									"result_job_type_job_type":[],
									"result_popular_jobs_enterprise_name":[],
																				"result_popular_jobs_recruitment_positions":[],
								"result_popular_jobs_job_type":[],
																																	"result_submit_resume_recruitment_positions":[],
								"result_submit_resume_job_type":[],
																																																"result_experience_sharing_share_theme":[],
								"result_experience_sharing_share_time":[],
													};
  },
  methods: {
	/**
	 * 获取文章
	 */
	get_article() {
	  this.$get("~/api/article/get_list?like=0", { page: 1, size: 10, title: this.query.word }, (json) => {
		if (json.result) {
		  this.result_article = json.result.list;
		}
	  });
	},
	/**
	 * 获取用户交流
	 */
	get_forum() {
	  this.$get("~/api/forum/get_list?like=0", { page: 1, size: 10, title: this.query.word }, (json) => {
		if (json.result) {
		  this.result_forum = json.result.list;
		}
	  });
	},

				/**
	 * 获取user_name
	 */
	get_registered_users_user_name(){
		let url = "~/api/registered_users/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "user_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_registered_users_user_name = json.result.list;
			result_registered_users_user_name.map(o => o.title = o['user_name'])
	  			this.result_registered_users_user_name = result_registered_users_user_name
		 	}
		});
	},
						/**
	 * 获取gender
	 */
	get_registered_users_gender(){
		let url = "~/api/registered_users/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "gender": this.query.word }, (json) => {
		  if (json.result) {
			var result_registered_users_gender = json.result.list;
			result_registered_users_gender.map(o => o.title = o['gender'])
	  			this.result_registered_users_gender = result_registered_users_gender
		 	}
		});
	},
							/**
	 * 获取job_type
	 */
	get_job_type_job_type(){
		let url = "~/api/job_type/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "job_type": this.query.word }, (json) => {
		  if (json.result) {
			var result_job_type_job_type = json.result.list;
			result_job_type_job_type.map(o => o.title = o['job_type'])
	  			this.result_job_type_job_type = result_job_type_job_type
		 	}
		});
	},
							/**
	 * 获取enterprise_name
	 */
	get_popular_jobs_enterprise_name(){
		let url = "~/api/popular_jobs/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "enterprise_name": this.query.word }, (json) => {
		  if (json.result) {
			var result_popular_jobs_enterprise_name = json.result.list;
			result_popular_jobs_enterprise_name.map(o => o.title = o['enterprise_name'])
	  			this.result_popular_jobs_enterprise_name = result_popular_jobs_enterprise_name
		 	}
		});
	},
																		/**
	 * 获取recruitment_positions
	 */
	get_popular_jobs_recruitment_positions(){
		let url = "~/api/popular_jobs/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "recruitment_positions": this.query.word }, (json) => {
		  if (json.result) {
			var result_popular_jobs_recruitment_positions = json.result.list;
			result_popular_jobs_recruitment_positions.map(o => o.title = o['recruitment_positions'])
	  			this.result_popular_jobs_recruitment_positions = result_popular_jobs_recruitment_positions
		 	}
		});
	},
						/**
	 * 获取job_type
	 */
	get_popular_jobs_job_type(){
		let url = "~/api/popular_jobs/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "job_type": this.query.word }, (json) => {
		  if (json.result) {
			var result_popular_jobs_job_type = json.result.list;
			result_popular_jobs_job_type.map(o => o.title = o['job_type'])
	  			this.result_popular_jobs_job_type = result_popular_jobs_job_type
		 	}
		});
	},
																															/**
	 * 获取recruitment_positions
	 */
	get_submit_resume_recruitment_positions(){
		let url = "~/api/submit_resume/get_list?like=0";
				url = url+"&examine_state=已通过";
				this.$get(url, { page: 1, size: 10, "recruitment_positions": this.query.word }, (json) => {
		  if (json.result) {
			var result_submit_resume_recruitment_positions = json.result.list;
			result_submit_resume_recruitment_positions.map(o => o.title = o['recruitment_positions'])
	  			this.result_submit_resume_recruitment_positions = result_submit_resume_recruitment_positions
		 	}
		});
	},
						/**
	 * 获取job_type
	 */
	get_submit_resume_job_type(){
		let url = "~/api/submit_resume/get_list?like=0";
				url = url+"&examine_state=已通过";
				this.$get(url, { page: 1, size: 10, "job_type": this.query.word }, (json) => {
		  if (json.result) {
			var result_submit_resume_job_type = json.result.list;
			result_submit_resume_job_type.map(o => o.title = o['job_type'])
	  			this.result_submit_resume_job_type = result_submit_resume_job_type
		 	}
		});
	},
																																														/**
	 * 获取share_theme
	 */
	get_experience_sharing_share_theme(){
		let url = "~/api/experience_sharing/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "share_theme": this.query.word }, (json) => {
		  if (json.result) {
			var result_experience_sharing_share_theme = json.result.list;
			result_experience_sharing_share_theme.map(o => o.title = o['share_theme'])
	  			this.result_experience_sharing_share_theme = result_experience_sharing_share_theme
		 	}
		});
	},
						/**
	 * 获取share_time
	 */
	get_experience_sharing_share_time(){
		let url = "~/api/experience_sharing/get_list?like=0";
				this.$get(url, { page: 1, size: 10, "share_time": this.query.word }, (json) => {
		  if (json.result) {
			var result_experience_sharing_share_time = json.result.list;
			result_experience_sharing_share_time.map(o => o.title = o['share_time'])
	  			this.result_experience_sharing_share_time = result_experience_sharing_share_time
		 	}
		});
	},
												
  },
  components: { list_result_search },
	created(){
    this.query.word = this.$route.query.word || "";
  },
  mounted() {
	this.get_article();
	this.get_forum();
					this.get_registered_users_user_name();
							this.get_registered_users_gender();
								this.get_job_type_job_type();
								this.get_popular_jobs_enterprise_name();
																			this.get_popular_jobs_recruitment_positions();
							this.get_popular_jobs_job_type();
																																this.get_submit_resume_recruitment_positions();
							this.get_submit_resume_job_type();
																																															this.get_experience_sharing_share_theme();
							this.get_experience_sharing_share_time();
												  },
  watch: {
	$route() {
	  $.push(this.query, this.$route.query);
	  this.get_article();
	  this.get_forum();
				  this.get_registered_users_user_name();
						  this.get_registered_users_gender();
							  this.get_job_type_job_type();
							  this.get_popular_jobs_enterprise_name();
																		  this.get_popular_jobs_recruitment_positions();
						  this.get_popular_jobs_job_type();
																															  this.get_submit_resume_recruitment_positions();
						  this.get_submit_resume_job_type();
																																														  this.get_experience_sharing_share_theme();
						  this.get_experience_sharing_share_time();
													},
  },
};
</script>

<style scoped>
.card_search {
  text-align: center;
}
.card_result_search>.title {
  text-align: center;
  padding: 10px 0;
}
</style>
