<template>
    <el-container>
        <el-header>
            <div class="sys-title">jians后台管理系统</div>
            <div class="header-right">
                <span @click="goWeb()">首页</span>
                <i class="el-icon-location"></i>
                <span>admin</span>
                <span @click="exit()">退出</span>
            </div>
        </el-header>
        <el-container>
            <el-aside width="200px">
                <el-menu background-color="#40454b" text-color="#fff" active-text-color="#ffd04b" router>
                    <el-submenu index="/admin/user">
                        <template slot="title">
                            <i class="el-icon-s-custom"></i>
                            <span>个人中心</span>
                        </template>
                        <el-menu-item index="/admin/user/personal">修改资料</el-menu-item>
                        <!-- <el-menu-item index="/admin/user/password">修改密码</el-menu-item> -->
                    </el-submenu>
                    <el-menu-item index="/admin/userManage">
                        <template slot="title">
                            <i class="el-icon-star-on"></i>
                            <span>用户管理</span>
                        </template>
                    </el-menu-item>
                    <el-submenu index="/admin/article">
                        <template slot="title">
                            <i class="el-icon-document"></i>
                            <span>文章管理</span>
                        </template>
                        <el-menu-item index="/admin/article">文章列表</el-menu-item>
                        <el-menu-item index="/admin/article/add">发布文章</el-menu-item>
                        <!-- <el-menu-item index="/admin/article/update">更新文章</el-menu-item> -->
                    </el-submenu>

                    <el-submenu index="/admin/comment">
                        <template slot="title">
                            <i class="el-icon-more"></i>
                            <span>评论管理</span>
                        </template>
                        <el-menu-item index="/admin/comment">评论列表</el-menu-item>
                        <!-- <el-menu-item index="/admin/comment/add">添加评论</el-menu-item> -->
                        <!-- <el-menu-item index="/admin/comment/update">更新评论</el-menu-item> -->
                    </el-submenu>

                    <el-menu-item index="/admin/fans">
                        <template slot="title">
                            <i class="el-icon-news"></i>
                            <span>粉丝管理</span>
                        </template>
                    </el-menu-item>

                    <el-menu-item index="/admin/star">
                        <template slot="title">
                            <i class="el-icon-star-on"></i>
                            <span>点赞管理</span>
                        </template>
                    </el-menu-item>
                </el-menu>
            </el-aside>

            <el-container>
                <el-main>
                    <router-view></router-view>
                </el-main>
                <el-footer><div class="foot">Form: https://github.com/ewrfli/vue-jians-views</div></el-footer>
            </el-container>
        </el-container>
    </el-container>
</template>

<script>
export default {
    data() {
        return {};
    },
    methods: {
        exit() {
            //退出系统
            localStorage.clear();
            this.$router.push({
                path: "/login",
            });
        },
        goWeb() {
            this.$router.push({
                path: "/",
            });
        }
    }

  
};
</script>

<style lang="less" scoped>
.el-container {
    width: 100%;
    height: 100%;
    .el-aside {
        background-color: #545c64;
        .el-menu {
          border-right: 0px;
        }
    }
    .el-header {
        background-color: #545c64;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        color: #ffffff;

    }
    .el-main {
        background-color: #ffffff;
    }
    .el-footer {
        background-color: #545c64;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
    }
    .foot {
        color: #fff;
    }
}
</style>
