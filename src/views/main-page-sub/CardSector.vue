<template>
    <div>
        <site-card v-for="site in siteList" v-if="openList[site.groupNumber]==='1'"
                   :siteName="site.siteName" :siteUrl="site.siteUrl"
                   :newArtNum="site.newArtNum" :imgSrc="site.imgSrc" :searchPhrase="site.searchPhrase"
                   :index="site.index"
                   :latestCheckDate="site.latestCheckDate" :groupNumber="site.groupNumber"
                   @onCardClick="onCardClick"></site-card>
        <add-card @addCardClick="addCardClick"></add-card>
    </div>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';
    import SiteCard from './SiteCard.vue';
    import AddCard from './AddCard.vue';
    import SideMenu from './SideMenu.vue';

    @Component({
        components: {
            SiteCard,
            AddCard,
            SideMenu
        }
    })
    export default class CardSector extends Vue {
        @Prop()
        siteList!: SiteCard[];
        @Prop()
        openList!: string[];

        onCardClick(event: string) {
            this.$emit("onCardClick", event);
        }

        addCardClick() {
            this.$emit("addCardClick");
        }
    }
</script>

<style>

</style>