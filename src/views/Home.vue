<template>
    <div>
        <el-container class="home">
            <el-main>
                <p>Here, check your any interests <br/> from everywhere, just at once.</p>
            </el-main>
        </el-container>

    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

    @Component({
        components: {
            HelloWorld
        }
    })
    export default class Home extends Vue {
    }
</script>

<style scoped>
    div {
        width:95%;
        height:1080px;
        background:url("../assets/table.jpeg") no-repeat center;

        margin:0 auto;
    }
    .home p {
        text-align:left;
        padding:100px 200px;
        font-size:60px;
        font-weight:bold;
        color:white;
    }
</style>