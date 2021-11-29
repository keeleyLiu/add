<template>
    <el-row type="flex" class="row-bg">
    <el-col :span="6" class="my-left">
        <div class="grid-content bg-purple">
            <div><el-button type="primary" round size="small" icon="el-icon-plus">新增</el-button></div>
            <el-divider></el-divider>
            <div>
                <div class="title_head">场景1</div>
                <div class="title_sub">场景1描述</div>
            </div>
        </div>
    </el-col>
    <el-col :span="18">
        <div class="grid-content bg-purple-light">
            
        </div></el-col>
    </el-row>
</template>
<script>
export default {
}
</script>
<style scoped>
    .my-left{
        padding: 0px 10px;
        text-align: left;
        border-right: solid 1px #ACC0D8;
    }
    .link_top{
        height: 1px;
        border-top: solid #ACC0D8 1px;
        margin: 10px 0px;
    }
</style>