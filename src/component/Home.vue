<template>
  <el-row type="flex" class="row-bg">
    <el-col :span="6" class="my-left">
      <div class="grid-content bg-purple">
        <div>
          <el-button type="primary" round size="small" icon="el-icon-plus">新增</el-button>
        </div>
        <el-divider></el-divider>
        <div>
          <div class="title_head">场景1</div>
          <div class="title_sub">场景1描述</div>
        </div>
      </div>
    </el-col>
    <el-col>
      <div class="grid-content bg-purple-light">
        <el-row type="flex">
            <el-col>
                <div class="content_main_title">场景1</div>
            </el-col>
            <el-col :span="4">
                <el-button type="danger" icon="el-icon-delete" size="mini" circle></el-button>
                <el-button type="primary" icon="el-icon-edit" size="mini" circle></el-button>
            </el-col>
        </el-row>
        <el-divider></el-divider>

        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">场景描述：</el-col>
            <el-col class="content_main_v">{{list[0].context}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">适用范围：</el-col>
            <el-col class="content_main_v">{{list[0].scope}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">判断标准：</el-col>
            <el-col class="content_main_v">{{list[0].standard}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">解决方案：</el-col>
            <el-col class="content_main_v">{{list[0].solution}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">应急操作恢复步骤：</el-col>
            <el-col class="content_main_v">
                <div class="block">
                    <el-timeline>
                        <el-timeline-item 
                        v-for="(activity, index) in list[0].activities"
                        :key="index"
                        :hide-timestamp=true>
                        <div>步骤{{index+1}}</div>
                        <div>点击展示当前步骤</div>
                        </el-timeline-item>
                    </el-timeline>
                </div>
            </el-col>
        </el-row>
      </div>
    </el-col>
  </el-row>
</template>
<script>
var json_data = require('../data/date.json')
console.log(json_data)
export default {
    data() {
        return json_data;
    }
};
</script>
<style scoped>
.my-left {
  padding: 0px 10px;
  text-align: left;
  border-right: solid 1px #acc0d8;
}
.link_top {
  height: 1px;
  border-top: solid #acc0d8 1px;
  margin: 10px 0px;
}
.content_main_title{
    text-align: left;
    padding: 10px 5px;
}
.content_main_detail{
    margin: 1.5em 0px;
}
.content_main_k{
    text-align: right;
    margin-left: 10px;
}
.content_main_v{
    padding: 0px 10px;
}
</style>