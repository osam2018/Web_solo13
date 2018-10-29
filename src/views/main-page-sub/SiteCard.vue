<template>
    <div class="card" @click="onCardClick">
        <el-card :body-style="{ padding: '0px' }">
            <div class="cardInner">
                <img :src="'./icons/'+imgSrc" class="image">
                <h3>{{siteName}}</h3><br/>
                <div class="cardContent">
                    <span>검색어: {{searchPhrase}}</span><br/>
                    <span>새 글: {{newArtNum}}</span>
                </div>
            </div>
            <div class="bottom">
                <span>최신 확인: {{latestCheckDate}}</span>
            </div>
        </el-card>
    </div>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component
    export default class SiteCard extends Vue {
        @Prop() siteName!: string;
        @Prop() siteUrl!: string;
        @Prop() newArtNum!: number;
        @Prop() imgSrc!: string;
        @Prop() searchPhrase!: string;
        @Prop() latestCheckDate!: string;
        @Prop() groupNumber!: number;
        @Prop() index!: number;

        onCardClick() {
            this.$emit("onCardClick", this.siteUrl);
        }
    }
</script>

<style scoped>
    .card {
        width: 300px;
        margin: 10px;
        display: inline-block;
        float: left;
    }

    .card .image {
        position: relative;
        top: -10px;
        width: 100px;
        height: 100px;
        float: left;
    }

    .cardInner {
        height: 100px;
    }

    .cardContent{
        font-size:13px;
        font-weight:bold;
    }
    .bottom {
        background: #efefef;
        text-align: right;
        padding-right: 10px;
        font-size:12px;
        font-weight:bold;
    }
</style>
