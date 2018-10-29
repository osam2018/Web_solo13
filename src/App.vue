<template>
    <el-container id="app">
        <el-header class="header">
            <div id="nav">
                <el-menu :default-active="activePage" class="el-menu-demo" mode="horizontal" @select="handleSelect">
                    <el-menu-item index="home">HOME</el-menu-item>
                    <el-menu-item index="mainpage">MAIN</el-menu-item>
                </el-menu>
            </div>
        </el-header>
        <router-view/>
    </el-container>
</template>
<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';

    @Component({})
    export default class Home extends Vue {
        public activePage: string = "home";
        handleSelect(key: string, keyPath: string) {
            this.$router.replace("/" + key);
        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        color: #2c3e50;
    }

    .el-header, .el-footer {
        background-color: #B3C0D1;
        color: #333;
        text-align: center;
        line-height: 60px;
    }

    .el-aside {
        background-color: #D3DCE6;
        color: #333;
    }

    .el-main {
        color: #333;
        text-align: center;
    }

    body > .el-container {
        margin-bottom: 40px;
    }

</style>
