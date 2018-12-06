<template>
  	<div class="login_page fillcontain">
	  	<transition name="form-fade" mode="in-out">
	  		<section class="form_contianer">
		  		<div class="manage_tip">
		  			<p>这或许就是后台系统吧</p>
		  		</div>
		    	<el-form ref="loginForm">
					<el-form-item prop="username">
						<el-input  placeholder="用户名"><span>dsfsf</span></el-input>
					</el-form-item>
					<el-form-item prop="password">
						<el-input type="password" placeholder="密码" ></el-input>
					</el-form-item>
					<el-form-item label="" prop="agree">
                        <el-checkbox label="没事干点一点" name="agree"></el-checkbox>
                    </el-form-item>
					<el-form-item>
				    	<el-button type="primary"  class="submit_btn">登陆</el-button>
				  	</el-form-item>
				</el-form>
	  		</section>
	  	</transition>
  	</div>
</template>

<script>
	export default {
	   name:login,
	   data() {
		//手机号
		var validatePhone = (rule, value, callback) => {
		if (/^1[34578]{1}\d{9}$/.test(value) == false) {
			callback(new Error("请输入正确的手机号"));
		} else {
			callback();
		}
		};
		// 密码
		var validatePass = (rule, value, callback) => {
		if (/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[^]{6,20}$/.test(value) == false) {
			callback(new Error("请输入6-20位密码，必须包含大小写字母和数字"));
		} else {
			callback();
		}
		};
		// 确认密码
		var validatePass2 = (rule, value, callback) => {
		if (/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[^]{6,20}$/.test(value) == false) {
			callback(new Error("请输入6-20位密码，必须包含大小写字母和数字"));
		} else if (value !== this.ruleForm.password) {
			callback(new Error("两次输入密码不一致!"));
		} else {
			callback();
		}
		};
		// 联系人姓名
		var validateUsername = (rule, value, callback) => {
		if (/^[0-9a-zA-Z\u4e00-\u9fa5_]{2,20}$/.test(value) == false) {
			callback(
			new Error("姓名可包含2-20位汉字、数字、字母（大小写）、下划线!")
			);
		} else {
			callback();
		}
		};
		return {
		ruleForm: {
			phone: "",
			verycode: "",
			sms_code: "",
			password: "",
			checkPassword: "",
			username: "",
			company_name: "",
			agree: []
		},
		rules2: {
			phone: [
			{ required: true, message: "请输入手机号", trigger: "blur" },
			{ validator: validatePhone, trigger: "blur" }
			],
			verycode: [
			{ required: true, message: "请输入图片验证码", trigger: "blur" },
			{ min: 4, max: 4, message: "请输入正确的图片验证码", trigger: "blur" }
			],
			sms_code: [
			{ required: true, message: "请输入手机验证码", trigger: "blur" },
			{ min: 4, max: 4, message: "请输入正确的手机验证码", trigger: "blur" }
			],
			password: [
			{ required: true, message: "请输入密码", trigger: "blur" },
			{ validator: validatePass, trigger: "blur" }
			],
			checkPassword: [
			{ required: true, message: "请输入密码", trigger: "blur" },
			{ validator: validatePass2, trigger: "blur" }
			],
			username: [
			{ required: true, message: "请输入联系人姓名", trigger: "blur" },
			{ validator: validateUsername, trigger: "blur" }
			],
			company_name: [
			{ required: true, message: "请输入公司法定名称", trigger: "blur" },
			{ min: 2, max: 4, message: "请输入正确的公司法定名称", trigger: "blur" }
			],
			agree: [
			{ type: "array", required: true, message: "请阅读并勾选注册协议", trigger: "change" }
			]
		}
		};
	},
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
}
</script>

<style lang="less" scoped>
	@import '../style/mixin';
	.login_page{
		background-color: #324057;
	}
	.manage_tip{
		position: absolute;
		width: 100%;
		top: -100px;
		left: 0;
		p{
			font-size: 34px;
			color: #fff;
		}
	}
	.form_contianer{
		.wh(320px, 210px);
		.ctp(320px, 210px);
		padding: 25px;
		border-radius: 5px;
		text-align: center;
		background-color: #fff;
		.submit_btn{
			width: 100%;
			font-size: 16px;
		}
	}
	.tip{
		font-size: 12px;
		color: red;
	}
	.form-fade-enter-active, .form-fade-leave-active {
	  	transition: all 1s;
	}
	.form-fade-enter, .form-fade-leave-active {
	  	transform: translate3d(0, -50px, 0);
	  	opacity: 0;
	}
</style>
