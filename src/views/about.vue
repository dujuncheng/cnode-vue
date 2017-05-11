<template>
    <div style="height: 100%;">
        <nv-head page-type="关于" :fix-head="true" :need-add="true" ></nv-head>
        <dl class="about-info">

            <dt>关于项目</dt>
            <dd>该项目是基于Cnodejs的api，采用vue2</dd>

            <dt>源码地址</dt>

            <dd>
                <a href="https://github.com/dujuncheng/cnode-vue">
                    https://github.com/dujuncheng/cnode-vue
                </a>
            </dd>

            <dt>小广告</dt>
            <dd>
                求实习
            </dd>

            <dt>当前版本</dt>
            <dd>V2.0</dd>

        </dl>
    </div>
</template>
<script>
    import nvHead from '../components/header.vue';
    export default {
        components: {
            nvHead
        }
    };
</script>
