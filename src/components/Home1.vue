<template>
	<!-- 页面容器 -->
	<el-container class="home_container">
		<!-- 页面头部 -->
		<el-header>
			<div class="header_title">
				备授课后台管理系统
			</div>
			<el-button
				type="primary"
				@click="handleLogout"
			>退出</el-button>
		</el-header>
		<!-- 页面主体区域 -->
		<el-container>
			<!-- 页面侧边栏 -->
			<el-aside width="200px">
                <!-- 侧边栏菜单区域 -->
				<el-menu
					default-active="2"
                    :collapse="false"
                    :unique-opened="true"
					class="el-menu-vertical-demo"
					@open="handleOpen"
					@close="handleClose"
					background-color="#545c64"
					text-color="#fff"
					active-text-color="#ffd04b"
				>
					<el-submenu index="/home">
						<template slot="title">
							<i class="el-icon-location"></i>
							<span>导航一</span>
						</template>
						<el-menu-item-group>
							<template slot="title">分组一</template>
							<el-menu-item index="/home/1">选项1</el-menu-item>
							<el-menu-item index="1-2">选项2</el-menu-item>
						</el-menu-item-group>
						<el-menu-item-group title="分组2">
							<el-menu-item index="1-3">选项3</el-menu-item>
						</el-menu-item-group>
						<el-submenu index="1-4">
							<template slot="title">选项4</template>
							<el-menu-item index="1-4-1">选项1</el-menu-item>
						</el-submenu>
					</el-submenu>
					<el-menu-item index="2">
						<i class="el-icon-menu"></i>
						<span slot="title">导航二</span>
					</el-menu-item>
					<el-menu-item
						index="3"
						disabled
					>
						<i class="el-icon-document"></i>
						<span slot="title">导航三</span>
					</el-menu-item>
					<el-menu-item index="4">
						<i class="el-icon-setting"></i>
						<span slot="title">导航四</span>
					</el-menu-item>
				</el-menu>
			</el-aside>
			<el-container>
				<el-main>Main</el-main>
				<el-footer>
                    特别鸣谢：张进、高杨
                </el-footer>
			</el-container>
		</el-container>
	</el-container>
</template>

<script>
export default {
	data() {
		return {
			sourceList: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
			activeIndex: 0
		}
	},
	methods: {
		handleLogout() {
			window.sessionStorage.removeItem('token')
			this.$router.push('/login')
		}
	},
	mounted() {}
}
</script>

<style lang="scss" scoped>
.home_container {
	height: 100%;
	.el-header {
		background: #373d41;
		display: flex;
		justify-content: space-between;
		align-items: center;
		.header_title {
			font-size: 20px;
			font-weight: bold;
			color: #fff;
		}
		.el-button {
			height: 60%;
		}
	}
	.el-aside {
		background: #373d41;
	}
	.el-main {
		background: #eaedf1;
	}
	.el-footer {
        background: #373d41;
        font-size: 20px;
        font-weight: bold;
        color: #fff;
        display: flex;
        justify-content: flex-start;
        align-items: center;
	}
}
</style>