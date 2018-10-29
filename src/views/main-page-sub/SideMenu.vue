<template>
    <el-menu class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose">
        <el-submenu class="group1" v-for="groupName in groupList" :index="groupList.indexOf(groupName).toString()">
            <template slot="title">
                <span slot="title">{{groupName}}</span>
            </template>
            <el-menu-item v-for="site in siteList" v-if="(site.groupNumber===groupList.indexOf(groupName))"
                          :index="site.index.toString()" @click="onCardClick(site.siteUrl)">{{site.siteName}}
            </el-menu-item>
        </el-submenu>
        <div class="buttonContainer1" v-show="!siteOpen">
            <el-button round @click="addGroup" v-if="!adding">Add Group</el-button>
            <div class="adding" v-if="adding">
                <el-input placeholder="New Group Name" v-model="addingName"></el-input>
                <p></p>
                <el-button type="primary" round size="small" @click="groupAdded">Add</el-button>
                <el-button round size="small" @click="groupAddCancel">Cancel</el-button>
            </div>
        </div>
        <div class="buttonContainer2" v-show="siteOpen">
            <el-button type="primary" round @click="goBack">Go Back</el-button>
        </div>
    </el-menu>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';
    import SiteCard from './SiteCard.vue';

    @Component({})

    export default class SideMenu extends Vue {
        public groupList: string[] = ["University", "Game Patchnote", "Webtoon", "Youtube Channel"];
        @Prop()
        openList!: string[];
        public activePage: string = "SidePage";
        public adding: boolean = false;
        public addingName: string = "";

        @Prop()
        siteList!: SiteCard[];

        @Prop()
        siteOpen!: boolean;

        handleOpen(key: string, keyPath: string) {
            console.log("open", key, keyPath);
            if (this.openList[Number(key)] === "1")
                for (let i: number = 0; i < this.openList.length; i++)
                    this.openList[i] = "0";
            this.openList[Number(key)] = "1";
            this.$emit("openChange", this.openList);
        }

        handleClose(key: string, keyPath: string) {
            console.log("close", key, keyPath);
            this.openList[Number(key)] = "0";
            let temp:number=1;
            for(let i:number=0;i<this.openList.length;i++)
                temp*=(Number(this.openList[i])+1);
            if (temp===1) {
                for(let i:number=0;i<this.openList.length;i++)
                    this.openList[i]="1";
            }
            this.$emit("openChange", this.openList);
        }

        handleSelect(key: string, keyPath: string) {
            console.log("select", key, keyPath);
            this.$router.replace("/sidepage" + key);
        }

        onCardClick(siteUrl: string) {
            this.$emit("onCardClick", siteUrl);
        }

        addGroup() {
            this.adding = true;
        }

        groupAdded() {
            this.groupList.push(this.addingName);
            this.$message({
                type: 'success',
                message: 'Add completed'
            });
            this.adding = false;
        }

        groupAddCancel() {
            this.adding = false;
        }

        goBack() {
            this.$emit("goBackToMain");
        }
    }
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }

    .buttonContainer1 {
        text-align: left;
        padding: 10px 10px 10px 30px;
    }

    .buttonContainer2 {
        text-align: right;
        padding: 10px 30px 10px 10px;
    }

    .adding {
        clear: both;
        text-align: center;
    }
</style>
