<template>
    <div class="app-container">
        <!--顶部header区域-->
        <mt-header title="vue项目">
            <span slot="left" @click="goBack" v-show="flag">
                <mt-button icon="back">返回</mt-button>
            </span>
        </mt-header>
        <!--router路由区域-->

        <transition>
            <router-view></router-view>
        </transition>

        <!--底部tabbar区域-->
        <nav class="mui-bar mui-bar-tab">
            <router-link class="mui-tab-item-my" to="/home">
                <span class="mui-icon mui-icon-home"></span>
                <span class="mui-tab-label">首页</span>
            </router-link>
            <router-link class="mui-tab-item-my" to="/member">
                <span class="mui-icon mui-icon-contact"></span>
                <span class="mui-tab-label">会员</span>
            </router-link>
            <router-link class="mui-tab-item-my" to="/shopcar">
                <span class="mui-icon mui-icon-extra mui-icon-extra-cart">
                    <span class="mui-badge">{{ $store.getters.getAllCount }}</span>
                </span>
                <span class="mui-tab-label">购物车</span>
            </router-link>
            <router-link class="mui-tab-item-my" to="/search">
                <span class="mui-icon mui-icon-search"></span>
                <span class="mui-tab-label">搜索</span>
            </router-link>
        </nav>

    </div>
</template>

<script>

    export default {
        name: "App",
        data(){
            return {
                flag : false
            }
        },
        methods:{
            //点击后退
            goBack(){
                this.$router.go(-1)
            }
        },
        //在页面初始化时判断路由地址
        created(){
            this.flag = this.$route.path === '/home' ? false : true;
        },
        //监听路由地址, 当时首页的时候, 隐藏返回按钮
        watch:{
            '$route.path':function (newVal) {
                if(newVal === '/home'){
                    this.flag = false;
                }else{
                    this.flag = true
                }
            }
        }

    }
</script>

<style scoped lang="scss">
    .app-container {
        padding-top: 40px;
        padding-bottom: 50px;
        overflow-x: hidden;
    }

    .mint-header{
        position: fixed;
        z-index: 999;
        width: 100%;
        top: 0;
    }

    .v-enter {
        opacity: 0;
        transform: translateX(100%);
    }

    .v-leave-to {
        opacity: 0;
        transform: translateX(-100%);
        position: absolute;
    }

    .v-enter-active, .v-leave-active {
        transition: all 1s;
    }

    /*改类名, 解决和js冲突的问题*/
    .mui-bar-tab .mui-tab-item-my {
        display: table-cell;
        overflow: hidden;
        width: 1%;
        height: 50px;
        text-align: center;
        vertical-align: middle;
        white-space: nowrap;
        text-overflow: ellipsis;
        color: #929292;
    }

    .mui-bar-tab .mui-tab-item-my .mui-icon {
        top: 3px;
        width: 24px;
        height: 24px;
        padding-top: 0;
        padding-bottom: 0;
    }

    .mui-bar-tab .mui-tab-item-my .mui-icon ~ .mui-tab-label {
        font-size: 11px;
        display: block;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .mui-bar-tab .mui-tab-item-my.mui-active {
        color: #007aff;
    }

</style>