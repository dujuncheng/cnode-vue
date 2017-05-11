<template>
    <div>
        <!--page-cover是遮罩层-->
        <div class="page-cover" v-if="show&&fixHead" @click="showMenus"></div>

        <header :class="{'show': show&&fixHead,'fix-header': fixHead,'no-fix': !fixHead}" id="hd">
            <div class="nv-toolbar">
               <div class="item item-goback">
                   <i class="el-icon-arrow-left btn-goback" @click="goBack()" v-if="cangoback"></i>
               </div>
               <div class="item"><el-button type="primary" size="mini" class="title">{{pageType}}</el-button></div>
               <div class="item"><div class="toolbar-nav" @click="openMenu" v-if="fixHead"></div></div>
            </div>
        </header>
        <nv-menu :show-menu="show" :page-type="pageType" :nick-name="nickname" :profile-url="profileimgurl" v-if="fixHead" ></nv-menu>
    </div>
</template>

<script>
    import $ from 'webpack-zepto';

    export default {
        watch: {

        },
        computed: {
            canback () {
                if (window.location.pathname === '/list') {
                    return true;
                }
            }
        },
        replace: true,
        props: {
            pageType: String,
            fixHead: Boolean,
            messageCount: Number,
            needAdd: {
                type: Boolean,
                default: true
            }
        },
        data() {
            return {
                nickname: '',
                profileimgurl: '',
                show: false,
                cangoback: true
            };
        },
        methods: {
            goBack () {
                this.$router.go(-1);
                if (window.location.pathname === '/list') {
                    this.cangoback = false;
                } else {
                    this.cangoback = true;
                }
            },
            openMenu() {
                $('html, body, #page').addClass('scroll-hide');
                this.show = !this.show;
            },
//           切换左侧的侧边栏
            showMenus() {
//              这句是toggle
                this.show = !this.show;
                $('html, body, #page').removeClass('scroll-hide');
            }
        },
        components: {
            'nvMenu': require('./menu.vue')
        }
    };
</script>
<style lang="css">
    .title{
        margin: 0 auto;
        text-align: center;
        color: white;
    }
    .nv-toolbar{
        width: 100vw;
        display: flex;
        align-items: stretch;
    }
    .item{
        flex: 1;
        text-align: center;
        line-height: 44px;
    }
    .item-goback{
        text-align: left;
        padding-left: 20px;
    }
    .btn-goback{
      width: 50%;
      height: 100%;
      display: block;
      padding: 15px;
    }
</style>
