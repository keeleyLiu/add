<template>
<div>
  <el-row type="flex" class="row-bg">
    <el-col :span="6" class="my-left">
        <div>
          <el-button type="primary" round size="small" icon="el-icon-plus" @click="add_scenes">新增</el-button>
        </div>
        <el-divider></el-divider>
      <div class="grid-content bg-purple" v-for="(scenes, index) in list" :key="scenes.id">
        <div v-on:click="change_scenes(index)">
          <div class="title_head" >场景 {{index+1}}</div>
          <div class="title_sub">{{scenes.context}}</div>
        </div>
         <el-divider></el-divider>
      </div>
    </el-col>
    <el-col>
    <div v-if="list == undefined ||list == null || list.length <= 0 " style="text-align:center">
        暂无数据
    </div>
      <div class="grid-content bg-purple-light" v-else>
        <el-row type="flex">
            <el-col>
                <div class="content_main_title">场景 {{current_scenes_index+1}}</div>
            </el-col>
            <el-col :span="4">
                <el-button type="danger" icon="el-icon-delete" size="mini" circle @click="remove_scenes"></el-button>
                <el-button type="primary" icon="el-icon-edit" size="mini" circle @click="edit_scenes"></el-button>
            </el-col>
        </el-row>
        <el-divider></el-divider>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">场景描述：</el-col>
            <el-col class="content_main_v">{{current_scenes.context}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">适用范围：</el-col>
            <el-col class="content_main_v">{{current_scenes.scope}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">判断标准：</el-col>
            <el-col class="content_main_v">{{current_scenes.standard}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">解决方案：</el-col>
            <el-col class="content_main_v">{{current_scenes.solution}}</el-col>
        </el-row>
        <el-row class="content_main_detail" type="flex">
            <el-col :span="8" class="content_main_k">应急操作恢复步骤：</el-col>
            <el-col class="content_main_v">
                <div class="block">
                    <el-timeline>
                        <el-timeline-item 
                        v-for="(activity, index) in current_scenes.activities"
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
  <AddScenes ref="addScenesView" @saveScenes='save_scenes'/>
  </div>
</template>
<script>
var json_data = require('../data/date.json')
let id = json_data.length;
function genId() {
    return ++id;
}
import AddScenes from "./AddScenes.vue"

export default {
    components : {AddScenes},
    data() {
        return {
            current_scenes_index:0,
            ...json_data
        };
    },
    computed:{
        current_scenes(){
            return this.list[this.current_scenes_index] || {}
        }
    },
    methods: {
        change_scenes: function(index){
            this.current_scenes_index = index;
        },
        add_scenes: function(){
            this.$refs.addScenesView.showDialog();
        },
        edit_scenes: function(index){
            this.$refs.addScenesView.showDialog(this.current_scenes);
        },
        save_scenes: function(scenes){
            if(!scenes) return;
            if(scenes.id){
                const updatedItems = this.list.map(el => el.id === scenes.id ? scenes : el)
                this.list = updatedItems
            }else{
                scenes.id = genId()
                this.list.push(scenes)
            }
        },
        remove_scenes: function(){
            this.$confirm('确认删除？')
            .then(_ => {
                this.list = [...this.list.filter(it=>it.id!=this.current_scenes.id)]
            }).catch(_ => {});
        }
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