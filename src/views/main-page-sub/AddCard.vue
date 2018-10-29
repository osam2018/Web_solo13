<template>
    <div class="addCard" @click="OnAddCardClick">
        <div class="plusIcon">+</div>
    </div>
</template>

<script lang="ts">
    import {Component, Vue} from 'vue-property-decorator';

    @Component({})
    export default class AddCard extends Vue {
        OnAddCardClick() {
            this.$emit("addCardClick");
        }
    }
</script>

<style>
    div.addCard {
        width: 296px;
        height: 130px;
        border-radius: 25px;
        border: 2px dotted;
        display: inline-block;
        float: left;
        margin: 10px;
    }

    div.plusIcon {
        position: relative;
        background: #ffffff;
        left: 130px;
        top: 24px;
        font-size: 70px;
        vertical-align: center;
        text-align: center;
        width: 32px;
        height: 32px;
        border-radius: 20px;
        border: none;
        z-index: 100;
    }
</style>