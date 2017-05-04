
<style scoped>
.content_box{
  position:absolute;
  left:200px;
  top:107px;	
}


	
</style>

<style type="text/css" media="screen">
  
.el-table th{
  background:#f39801;

}

 .el-table__header-wrapper thead div{
  background:#f39801;
  color:#fff;
  
 }


 .el-table .cell, .el-table th>div {
    padding-left: 0px; 
    padding-right: 0px; 
    box-sizing: border-box;
    text-overflow: ellipsis;
}

.el-button--small {
    padding: 7px 20px;
    font-size: 12px;
    border-radius: 4px;
    background: #ff7b0f;
    color: #fff;
}


</style>

<template>
 <div class="content_box">

		<el-table
    ref="multipleTable"
    :data="tableData"
    border
   
    style="width: 100%;"
    @selection-change="handleSelectionChange">
      <el-table-column
        type="selection"
        width="55" align="center">
      </el-table-column>

      <el-table-column
        label="用户名"
        align="center" width="202" >
        <template scope="scope">{{ scope.row.name }}</template>
      </el-table-column>

    <el-table-column
      label="登陆时间"
      width="202" align="center">
       <template scope="scope">{{ scope.row.date }}</template>

    </el-table-column>
     
      <el-table-column
        label="登陆IP"
        show-overflow-tooltip width="202" align="center">
         <template scope="scope">{{ scope.row.ip }}</template>
      </el-table-column>

      <el-table-column  label="操作" width="202" align="center">

                <template scope="scope">
                    <el-button size="small" @click="handleEdit(scope.$index, scope.row)">修改</el-button>
                    <el-button @click.native.prevent="deleteRow(scope.$index, tableData)" type="text" size="small">
                      移除
                    </el-button>
                </template>
      </el-table-column>

      <el-table-column
      label="所属角色"
      width="202" align="center">
       <template scope="scope">{{ scope.row.role }}</template>

      </el-table-column>


  </el-table>

  <div style="margin-top: 20px">
    <el-button @click="toggleSelection([tableData[1], tableData[2]])">切换第二、第三行的选中状态</el-button>
    <el-button @click="toggleSelection()">取消选择</el-button>
  </div>

  <div>
    <ProgressBar :tot="total" v-on:handleCurrentChange="getPagedata"></ProgressBar>

  </div>

</div>

</template>


<script>

import axios from 'axios';

import ProgressBar from '../progress_bar/Progress_bar';

  export default {
    data() {
      return {

        tableData:[],
        multipleSelection: [],
        total:0 
      }
    },
    created:function(){
    
    },
     components: {
       ProgressBar
    },

    methods: {

      getPagedata(data){
        //接受子元素传来的值
         console.log(data)
          //http://m.wishlist1314.com/wishlist_mobile/mobile/getBannerList
             axios.get("http://localhost:9000/static/mock/user_admain/user_admain1.json",{
              
               params:{
                 pageSize:data
               }
             })
            .then(function (response) {

                
                var result=response.data;
                
                if(result.code==0){     
                 
                   this.$set(this,"tableData",result.data.rows);
                         

                }else{

                  console.log(result.msg)
                } 
                
                

            }.bind(this))
            .catch(function (error) {
                console.log(error);
            });

      },

      toggleSelection(rows) {
       
        console.log(rows)
        if (rows) {
          rows.forEach(row => {
            this.$refs.multipleTable.toggleRowSelection(row);
          });
        } else {

          this.$refs.multipleTable.clearSelection();
           console.log(this.multipleSelection)
        }
      },
      handleSelectionChange(val) {
        console.log(val)
        this.multipleSelection = val;
        console.log(this.multipleSelection)
      },

       deleteRow(index, rows) {
          //删除
          rows.splice(index, 1);
      },

      handleEdit(index,rows){

        console.log("bianji")
      }

    },

     mounted: function () {

          //http://m.wishlist1314.com/wishlist_mobile/mobile/getBannerList
             axios.get("http://localhost:9000/static/mock/user_admain/user_admain.json",{
              
             })
            .then(function (response) {

                
                var result=response.data;
                
                if(result.code==0){
              
                 
                   this.$set(this,"tableData",result.data.rows);
                   this.$set(this,"total",result.data.total);
                 

                }else{

                  console.log(result.msg)
                } 
                
                

            }.bind(this))
            .catch(function (error) {
                console.log(error);
            });

     }  


  }
</script>