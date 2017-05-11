<template>
    <div class="login-page">
        <nv-head page-type="登录">
        </nv-head>
        <section class="page-body">
            <div class="label">
                <el-input v-model="token" placeholder="请输入用户名，可以用‘alsotang’测试哦"></el-input>
            </div>
            <div class="label">
                <el-button type="primary" @click="logon" class="login-btn">登陆</el-button>
            </div>
        </section>
    </div>
</template>

<script>
    import $ from 'webpack-zepto';
    import nvHead from '../components/header.vue';

    export default {
        data() {
            return {
                token: ''
            };
        },
        methods: {
            logon() {
                if (this.token === '') {
                    this.$alert('令牌格式错误,应为36位UUID字符串');
                    return false;
                }
                $.ajax({
                    type: 'GET',
                    url: 'https://cnodejs.org/api/v1/user/' + this.token,
                    success: (res) => {
                        console.log(res);
                        let user = {
                            loginname: res.data.loginname,
                            avatar_url: res.data.avatar_url
                        };
//                        先存到sessionStorage里面
                        window.window.sessionStorage.user = JSON.stringify(user);
//                        然后在放进vuex 里面
                        this.$store.dispatch('setUserInfo', user);
//                        回退到之前的页面
                        let redirect = decodeURIComponent(this.$route.query.redirect || '/');
                        this.$router.push({
                            path: redirect
                        });
                    },
                    error: (res) => {
                        var error = JSON.parse(res.responseText);
                        this.$alert(error.error_msg);
                    }
                });
            }
        },
        mounted () {
            console.log(this.$route);
        },
        components: {
            nvHead
        }
    };
</script>
<style lang="scss">
    .page-body {
        padding: 50px 15px;
        min-height: 400px;
        background-color: #fff;
        .label {
            display: inline-block;
            width: 100%;
            margin-top: 15px;
            position: relative;
            left: 0;
            top: 0;
            .txt {
                padding: 12px 0;
                border: none;
                border-bottom: 1px solid #4fc08d;
                background-color: transparent;
                width: 100%;
                font-size: 14px;
                color: #313131;
            }
            .button {
                display: inline-block;
                width: 99%;
                height: 42px;
                line-height: 42px;
                border-radius: 3px;
                color: #fff;
                font-size: 16px;
                background-color: #4fc08d;
                border: none;
                border-bottom: 2px solid #3aa373;
                text-align: center;
                vertical-align: middle;
            }
            .login-btn {
                display: inline-block;
                width: 99%;
            }
            .file {
                position: absolute;
                top: 0;
                left: 0;
                height: 42px;
                width: 48%;
                outline: medium none;
                opacity: 0;
            }
        }
    }
</style>
