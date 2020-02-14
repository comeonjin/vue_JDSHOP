<template>
	<div class="login_container">
		<div class="login_box">
			<!-- 头像区域 -->
			<div class="avatar_box">
				<img
					src="../assets/logo.png"
					alt
				/>
			</div>
			<!-- 登陆标签区域 -->
			<el-form
				ref="loginFormRef"
				label-width="0px"
				:model="loginForm"
				:rules="loginRules"
				class="login_form"
			>
				<el-form-item prop="username">
					<el-input
						v-model="loginForm.username"
						prefix-icon="el-icon-user"
						placeholder="请输入用户名"
					></el-input>
				</el-form-item>
				<el-form-item prop="password">
					<el-input
						v-model="loginForm.password"
						type="password"
						prefix-icon="el-icon-lock"
						placeholder="请输入密码"
					></el-input>
				</el-form-item>
				<el-form-item class="button_box">
					<el-button
						@click="handleSubmit"
						type="primary"
					>登录</el-button>
					<el-button
						@click="handleReset"
						type="info"
					>重置</el-button>
				</el-form-item>
			</el-form>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			loginForm: {
				username: 'admin',
				password: '123456'
			},
			loginRules: {
				username: [
					{
						required: true,
						message: '请输入用户名',
						trigger: 'blur'
					},
					{
						min: 3,
						max: 5,
						message: '长度在 3 到 5 个字符',
						trigger: 'blur'
					}
				],
				password: [
					{ required: true, message: '请输入密码', trigger: 'blur' }
				]
			}
		}
	},
	methods: {
		handleSubmit() {
			this.$refs.loginFormRef.validate(async (STATUS, object) => {
				if (!STATUS) {
					return
				}
				const { status, token } = await this.sendApi(this.loginForm)
				if (status === 200) {
					this.$message.success('登录成功!')
					window.sessionStorage.setItem('token', token)
					this.handleReset()
					this.$router.push('/home')
				} else {
					this.$message.error('账号或密码错误!')
				}
			})
		},
		sendApi(params) {
			// const someParamVoid = Object.keys(params).some((param) => {
			// 	return params[param] === ''
			// })
			return new Promise((resolve, reject) => {
				if (
					params.username === 'admin' &&
					params.password === '123456'
				) {
					resolve({
						status: 200,
						token: 'QWE!@#WSADAS!@#!@SAXDASD!Q@!#!'
					})
				} else {
					resolve({ status: 404 })
				}
			})
		},
		handleReset() {
			this.$refs.loginFormRef.resetFields()
		}
	}
}
</script>

<style lang="scss" scoped>
@mixin center {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
}
.login_container {
	background: #2b4b6b;
	height: 100%;
	.login_box {
		width: 450px;
		height: 300px;
		background: #fff;
		border-radius: 3px;
		@include center;
	}
	.avatar_box {
		width: 130px;
		height: 130px;
		border-radius: 50%;
		border: 1px solid #eee;
		padding: 10px;
		margin: -55px auto;
		box-shadow: 0 0 10px #ddd;
		background: #fff;

		img {
			display: block;
			width: 100%;
			height: 100%;
			border-radius: 50%;
			background: #eee;
		}
	}
	.login_form {
		position: absolute;
		bottom: 0;
		width: 100%;
		box-sizing: border-box;
		padding: 0 20px;
		.button_box {
			display: flex;
			flex-direction: row;
			justify-content: flex-end;
		}
	}
}
</style>
