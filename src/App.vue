
<template>
  <div class="table-box">
    <!--标题-->
    <div class="title">
      <h2>CURD Demo</h2>
    </div>
    <!--查询框-->
    <div class="query-box">
      <el-input class="query-input" v-model="queryInput" placeholder="按姓名搜索" />
      <div class="btnList">
        <el-button type="primary" @click="handleAdd">增加</el-button>
      <el-button type="danger" @click="handleDelList" v-if="multipleSelection.length>0" >删除多条</el-button>
      </div>
    </div>
    <!--表格-->
    <el-table 
    :data="tableData"
     style="width: 100%"
     border="200px"
     ref="multipleTableRef"
     @selection-change="handleSelectionChange"
    >
    <el-table-column type="selection" width="55" />
    <el-table-column prop="name" label="姓名" width="120" />
    <el-table-column prop="email" label="邮箱" width="125" />
    <el-table-column prop="phone" label="电话" width="120" />
    <el-table-column prop="state" label="状态" width="120" />
    <el-table-column prop="address" label="地址" width="300" />
    <el-table-column fixed="right" label="操作" width="140">
      <template #default="scope">
        <el-button link type="primary" size="small" @click="handleRowDel(scope.row)">删除</el-button>
        <el-button link type="primary" size="small">编辑</el-button>
      </template>
    </el-table-column>
  </el-table>
  <!--dialog弹窗-->
  <el-dialog v-model="dialogFormVisible" :title="dialogType === 'add' ?'新增':'编辑'">
    <el-form :model="tableForm">
      <el-form-item label="请输入姓名" :label-width="100">
        <el-input v-model="tableForm.name" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入邮箱" :label-width="100">
        <el-input v-model="tableForm.email" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入手机" :label-width="100">
        <el-input v-model="tableForm.phone" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入状态" :label-width="100">
        <el-input v-model="tableForm.state" autocomplete="off" />
      </el-form-item>
      <el-form-item label="请输入地址" :label-width="100">
        <el-input v-model="tableForm.address" autocomplete="off" />
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button type="primary" @click="dialogConfirm">
          确认
        </el-button>
      </span>
    </template>
  </el-dialog>
  </div>
</template>
<script setup>
import { ref } from 'vue';


let queryInput = ref('')
let tableData = ref([
   {
    id:'1',
    name: 'Tom',
    email:'2131@qq.com',
    state: '在职',
    address: 'No. 189, Grove St, Los Angeles',
    phone:'12343534',
  },
  {
    id:'2',
    name: 'Tom',
    email:'2131@qq.com',
    state: '在职',
    address: 'No. 189, Grove St, Los Angeles',
    phone:'12343534',
  },
  {
    id:'3',
    name: 'Tom',
    email:'2131@qq.com',
    state: '在职',
    address: 'No. 189, Grove St, Los Angeles',
    phone:'12343534',
  },
  {
    id:'4',
    name: 'Tom',
    email:'2131@qq.com',
    state: '在职',
    address: 'No. 189, Grove St, Los Angeles',
    phone:'12343534',
  }
])
let multipleSelection = ref([])
let dialogFormVisible = ref(false)
let tableForm = ref({
  name:'许志涛',
  email:'2314@qq.com',
  state:'在职',
  address:'湖南省',
  phone:'123435342',

 

})
let dialogType = ref('add')
//删除一条信息
const handleRowDel = ({id})=>{
  //通过id，获取要删除信息的索引值
  let index = tableData.value.findIndex(item=>item.id === id)
  
  //通过索引值删除信息
  tableData.value.splice(index,1)
}
//选中
const handleSelectionChange = (val) => {
  multipleSelection.value = []

  val.forEach(item => {
    multipleSelection.value.push(item.id)
  });
  
}
//弹窗
const handleAdd = ()=>{
  dialogFormVisible.value = true 
  tableForm.value = {}
}
const handleDelList = ()=>{
  multipleSelection.value.forEach((id)=>{
    handleRowDel(id)
  })
}
const dialogConfirm = ()=>{
  dialogFormVisible.value = false
 //拿到数据


 //添加到table
 tableData.value.push({
  id: (tableData.value.length+1).toString(),
  ...tableForm.value
 })

}




</script >


<style >
.table-box{
  width: 800px;
  margin: 200px auto;
}
.title{
  text-align: center;
}
.query-box{
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.query-input{
  width: 200px;
}
</style>
