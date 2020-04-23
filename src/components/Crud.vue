<template>
<div class="crud">

  <div class="crudHeader">
  <el-button type="primary" icon="el-icon-s-operation" circle @click.native="Filter"></el-button>
  <el-button icon="el-icon-refresh-left" circle ></el-button>
  </div>

    <el-table
    :data="tableData"
    border
    style="width: 100%"
    :row-class-name="tableRowClassName">

    <el-table-column
    v-for="(item,index) in checkedCities" :key="index"
      :resizable="false"
      :prop= Object.keys(tableData[0])[index] 
      :label= item
      :width= w[index]>
    </el-table-column>

    <el-table-column
      :resizable="false"
      label="操作"
      width="200">
      <template slot-scope="scope">
        <el-button type="text" size="small" @click="View(scope)"><i class="el-icon-zoom-in"></i><span>查看</span></el-button>
        <el-button type="text" size="small" @click="Edit(scope)"><i class="el-icon-edit"></i><span>编辑</span></el-button>
        <el-button type="text" size="small" @click="Del(scope)"><i class="el-icon-delete"></i><span>删除</span></el-button>
      </template>
    </el-table-column>
  </el-table>



    <el-dialog
    :title = title
    :visible.sync="dialogVisible"
    width="50%" 
    :before-close="handleClose">
    <div class="viewLists" v-if="EW==1">
      <div class="viewList" v-for="(item,items,index) in tableData[view.$index]" :key="index">
        <span>{{titleList[index]}}：</span>
        <el-input
          placeholder="请输入内容"
          :disabled = disabled
          v-model="viewData[index]"
          clearable>
        </el-input>
      </div>
    </div>
    <div class="viewLists" v-if="EW==2">
      <!-- <el-checkbox-group v-model="label" >
        <el-checkbox v-for="(item,index) in label " :key="index" :label="index">{{item}}</el-checkbox>
      </el-checkbox-group> -->
        <el-checkbox-group v-model="checkedCities" @change="handleCheckedCitiesChange">
    <el-checkbox v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
  </el-checkbox-group>
    </div>
    <span slot="footer" class="dialog-footer">
      <el-button @click="dialogVisible = false">取消</el-button>
      <el-button type="primary" @click="addSure">确定</el-button>
    </span>
  </el-dialog>

</div>
</template>



<script>
  export default {
    props:{
      tableData:{           //这个就是父组件中子标签自定义名字
        type:Array,
      },
      titleList:{
        type:Array,
      },
      w:{
        type:Array,
      },
    },
    methods: {
      tableRowClassName({row, rowIndex}) {
        if (rowIndex === 1) {
          return 'warning-row';
        } else if (rowIndex === 3) {
          return 'success-row';
        }
        return '';
      },
      handleClose(done) {
        
        done();
      },
      View(data){
        this.viewData=[]
        console.log(data.row)
        Object.values(data.row).forEach((item,index)=>{
          this.viewData.push(item)
        })
        this.view = data
        this.dialogVisible=true
        this.disabled = true
        this.title = '查看'
        this.EW=1
      },
      Edit(data){
        this.viewData=[]
        Object.values(data.row).forEach((item,index)=>{
          this.viewData.push(item)
        })
        this.view = data
        this.dialogVisible=true
        this.disabled = false
        this.title = '编辑'
        this.EW=1
      },
      addSure(){
        this.dialogVisible = false
        if(this.EW==1){
          var kkk = Object.keys(this.tableData[this.view.$index])
          kkk.forEach((item,index)=>{
            this.viewData.forEach((item2,index2)=>{
              if(index==index2){
                  this.tableData[this.view.$index][kkk[index]] =this.viewData[index]
              }
            })
          })
        }else if(this.EW==2){
          console.log(this.checkedCities)
        }
        this.EW=0
      },
      Del(data){
        this.tableData.splice(data.$index,1)
      },
      Filter(){
        console.log(111)
        this.dialogVisible=true
        this.title = '多选'
        this.EW=2
      },
      handleCheckedCitiesChange(value) {

        this.titleList=value
        // let checkedCount = value.length;
        // this.checkAll = checkedCount === this.cities.length;
        // this.isIndeterminate = checkedCount > 0 && checkedCount < this.cities.length;
      }

    },
    data() {
      return {
        aa:0,
        dialogVisible: false,
        view:{},
        viewData:[],
        disabled:"",
        title:"",
        EW:0,
        checkAll: false,
        checkedCities: this.titleList,
        cities:this.titleList,
        isIndeterminate: true
      }
    }
  }
</script>

<style rel="stylesheet/stylus" lang="stylus">
.crud
  width: 1200px;
  height: 500px;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  margin: auto;
  padding 10px
  box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04)
  .crudHeader
    height: 50px;
    .el-button
      width 30px
      height 30px
      padding 8px
      float right
      margin 10px 5px
  .viewList
    height 50px
    width 50%
    display inline-block
    .el-input
      width 80%
      margin-top 5px

  .el-table .warning-row {
    background: oldlace;
  }

  .el-table .success-row {
    background: #f0f9eb;
  }
</style>