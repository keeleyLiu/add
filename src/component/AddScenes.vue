<template>
    <el-dialog :title="dialogTitle" :visible.sync="dialogVisible" width="80%" :before-close="handleClose">
        <div>
            <el-row type="flex">
                <el-col :span="4">场景描述</el-col>
                <el-col><el-input v-model="scenes.context" placeholder="请输入场景描述"></el-input></el-col>
            </el-row>
            <el-row type="flex">
                <el-col :span="4">适应范围</el-col>
                <el-col ><el-input v-model="scenes.scope" placeholder="请输入场景描述"></el-input></el-col>
            </el-row>
            <el-row type="flex">
                <el-col :span="4">判断标准</el-col>
                <el-col  ><el-input  v-model="scenes.standard" placeholder="请输入判断标准"></el-input></el-col>
            </el-row>
            <el-row type="flex">
                <el-col :span="4">解决方案</el-col>
                <el-col ><el-input v-model="scenes.solution" placeholder="请输入解决方案"></el-input></el-col>
            </el-row>
        </div>
        <div>应急恢复步骤</div>
        <el-row type="flex" v-for="(activity, index) in scenes.activities" :key="index">
            <el-col :span="4">
                步骤 {{index+1}}
            </el-col>
            <el-col>
                <el-row type="flex">
                    <el-col :span="4">耗时/min</el-col>
                    <el-col><el-input v-model="activity.time" auto-complete="" placeholder="请输入耗时"></el-input></el-col>
                </el-row>
                <el-row type="flex">
                    <el-col :span="4">操作内容及目标</el-col>
                    <el-col ><el-input v-model="activity.target"  placeholder="请输入操作内容及目标"></el-input></el-col>
                </el-row>
                <el-row type="flex">
                    <el-col :span="4">执行动作/命令</el-col>
                    <el-col ><el-input v-model="activity.content" placeholder="请输入执行动作/命令"></el-input></el-col>
                </el-row>
            </el-col>
        </el-row>
        <div style="padding:10px;background:#ccf2ff;text-align:center;" @click="add_step"><el-link icon="el-icon-plus">添加步骤</el-link></div>
        <span slot="footer" class="dialog-footer">
            <el-button @click="dialogVisible = false">取 消</el-button>
            <el-button type="primary" @click="commit">提 交</el-button>
        </span>
    </el-dialog>
    
</template>

<script>
  export default {
    data() {
      return {
        dialogVisible: false,
        scenes: {activities:[]},
      };
    },
    computed:{
        dialogTitle(){
            return this.scenes.id ? "修改场景": "新增场景"
        }
    },
    methods: {
      showDialog(payload){
          this.dialogVisible = true;
          if(payload) this.scenes = {...payload}
      },
      add_step(){
          this.scenes.activities.push({})
      },
      handleClose(done){
          done()
          this.scenes = {activities:[]}
      },
      commit(){
          this.dialogVisible = false
          this.$emit("saveScenes",this.scenes)
      }
    }
  };
</script>
<style scoped>
.el-row{
    margin: 20px 10px;
}
</style>