<template>
    <el-form ref="form" :model="form" label-width="120px">
        <el-form-item label="Website name">
            <el-input v-model="form.name" placeholder="Title of the page"></el-input>
        </el-form-item>
        <el-form-item label="Website Url">
            <el-input v-model="form.url" placeholder="http://www.example.com"></el-input>
        </el-form-item>
        <el-form-item label="Group">
            <el-select v-model="form.region" placeholder="Group">
                <el-option label="University" value="1"></el-option>
                <el-option label="Game Patchnote" value="2"></el-option>
                <el-option label="Webtoon" value="3"></el-option>
                <el-option label="Youtube" value="4"></el-option>
            </el-select>
        </el-form-item>
        <el-form-item label="Search Phrase">
            <el-input v-model="form.searchPhrase"
                      placeholder="New contents which don't include this in their title won't be counted"></el-input>
        </el-form-item>
        <el-form-item>
            <el-button type="primary" @click="onSubmit">Create</el-button>
            <el-button v-on:click="onAddCancel">Cancel</el-button>
        </el-form-item>
    </el-form>
</template>

<script lnag="ts">
    export default {
        data() {
            return {
                form: {
                    name: '',
                    url: '',
                    region: '',
                    searchPhrase: ''
                }
            }
        },
        methods: {
            onSubmit() {
                alert('Submit! 하지만 서버사이드 구현은 하지 않아 실제론 추가되지 않습니다.');
                this.$emit("onAddEnd");
            },
            onAddCancel() {
                this.$confirm('입력한 내용은 저장되지 않습니다. 계속하시겠습니까?', 'Warning', {
                    confirmButtonText: 'OK',
                    cancelButtonText: 'Cancel',
                    type: 'warning'
                }).then(() => {
                    this.$message({
                        type: 'info',
                        message: '추가 취소'
                    });
                    this.$emit("onAddEnd");
                });
            }
        }
    }
</script>

<style scoped>

</style>