<template>
    <el-container>
        <el-aside width="280px" class="aside">
            <div class="aside">
                <side-menu :openList="openList" :siteList="siteList" :siteOpen="siteShow" @onCardClick="onCardClick"
                           @goBackToMain="goBackToMain" @openChange="openChange"></side-menu>
            </div>
        </el-aside>
        <el-main>
            <card-sector v-if="(!siteShow)&(!cardAdd)" :openList="openList" :siteList="siteList"
                         @onCardClick="onCardClick" @addCardClick="addEnd"></card-sector>
            <iframe v-if="siteShow" class="siteView" :src="siteUrl"></iframe>
            <card-add-form v-if="cardAdd" @onAddEnd="addEnd"></card-add-form>
            <router-view/>
        </el-main>
    </el-container>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';
    import SideMenu from './main-page-sub/SideMenu.vue';
    import SiteCard from './main-page-sub/SiteCard.vue';
    import CardSector from './main-page-sub/CardSector.vue';
    import CardAddForm from './main-page-sub/CardAddForm.vue';

    @Component({
        components: {
            SideMenu,
            CardSector,
            CardAddForm
        }
    })
    export default class MainPage extends Vue {
        public activePage: string = "SidePage1";
        public siteUrl: string = "";
        public siteList: SiteCard[] = [];
        public openList: string[] = ["1", "1", "1", "1"];
        public siteShow: boolean = false;
        public cardAdd: boolean = false;
        private list: string[] = [];

        async mounted() {
            this.openList = ["1", "1", "1", "1"];
            let jsonList = await window.$model.getData1();
            this.list = jsonList.data;
            for (let i: number = 0; i < jsonList.data.length; i++) {
                this.siteList.push(jsonList.data[i]);
                console.log(this.siteList[i].siteName);
            }
        }

        onCardClick(eventUrl: string) {
            this.siteUrl = eventUrl;
            this.siteShow = true;
        }

        addEnd() {
            this.cardAdd = !this.cardAdd;
        }

        goBackToMain() {
            this.siteShow = false;
            this.cardAdd = false;
        }

        openChange(list: string[]) {
            this.openList = list;
            console.log(this.openList, "has Changed");
            this.siteList.push(new SiteCard());
            this.siteList.pop();
        }
    }
</script>

<style scoped>
    iframe {
        width: 100%;
        height: 720px;
    }

    .aside {
        background: white;
        height: 800px;
    }
</style>