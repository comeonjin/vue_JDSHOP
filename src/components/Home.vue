<template>
	<div class="home_container">
        <el-button type="primary" @click="handleLogout">退出</el-button>
        <div class="content_container">
            <div v-for="item in sourceList" :key="item">
                <h1 :id="item" class="title" >{{item}}</h1>
                <li v-for="id in 10" :key="id" v-text="id"></li>
            </div>
        </div>
        
        <div class="maodian">
            <div class="mdItem" :class="{active:index === activeIndex}"  @click="jumpto(item)" v-for="(item, index) in sourceList" v-text="item" :key="item"></div>
        </div>
	</div>
</template>

<script>
export default {
	data() {
		return {
            sourceList: [1,2,3,4,5,6,7,8,9,10],
            activeIndex: 0
        };
    },
    methods: {
        handleLogout() {
            window.sessionStorage.removeItem('token');
            this.$router.push('/login');
        },
        jumpto(id) {
            document.getElementById(id).scrollIntoView()
            this.activeIndex = id-1
        },
        handleScroll() {
            let scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop // 滚动条偏移量
            // console.log(scrollTop)
            let _article = document.querySelectorAll('.title')
            _article.forEach((item, index) => {
                console.log(scrollTop, item.offsetTop)
                if (scrollTop >= item.offsetTop) {
                    this.activeIndex = index
                    return 
                }
                // console.log(index)
            })
        }
    },
    mounted() {
        window.addEventListener('scroll',this.handleScroll)
    }
};
</script>

<style lang="scss" scoped>
    .content_container{
        background: #808080;
        h1{
            margin: 0;
        }
        li{
            background: yellowgreen;
            text-align: left;
        }  
    }
    

    .maodian{
        width: 50px;
        position: fixed;
        top: 10px;
        left: 50px;
        background: orange;
        .mdItem{
            width: 100%;
            height: 20px;
            font-weight: bold;
            text-align: center;
            border: {
                bottom: 1px solid #333333;
            }
            cursor: pointer;
            &.active{
                background: yellowgreen;
            }
        }
        
    }
</style>