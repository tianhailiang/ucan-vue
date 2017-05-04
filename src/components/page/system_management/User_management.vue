
<style scoped>

.content_box{
  position:absolute;
  left:200px;
  top:107px;
  border:1px solid #dfe6ec;	
}

.top{
  width:100%;
  height:40px;
  display: flex;
  justify-content: flex-end;

}

.top_nav{
  width:202px;
  height:100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
	
.top_nav span{
  display: inline-block;
  flex:1;
  height:100%;
  text-align:center;
  line-height:40px;
  


}

.active{
  background:#e45f00;
  color:#fff;
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

.deleteAll{
  color:#fff;
  float: right;
  margin-right:5px;
  background:#f39801;
}

</style>

<template>
 <div class="content_box">

    <div class="top">
      
        <div class="top_nav" >
          
           <span class="active">管理员列表</span>
           <span>添加管理员</span>

        </div> 

    </div>
    
    
        <el-table ref="multipleTable" :data="tableData" border tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange" >
          <el-table-column type="selection" width="55" align="center" >
          </el-table-column>

          <el-table-column label="用户名" width="202" align="center">
            <template scope="scope">{{ scope.row.name }}</template>
          </el-table-column>

          <el-table-column  label="登陆时间" width="202" align="center">

               <template scope="scope">{{ scope.row.date }}</template>

          </el-table-column>
          <el-table-column  label="登陆IP"  width="202" align="center">

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

             <el-table-column label="所属角色" width="202" align="center">
                    <template scope="scope">{{ scope.row.role }}</template>

              </el-table-column>  


        </el-table>

        <div style="margin-top: 20px">
           
            <el-button @click="deleteRowAll()" class="deleteAll">批量删除</el-button>
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

      deleteRowAll() {
       

         if(this.multipleSelection.length==0){
            
            return; 

         }else{


             this.multipleSelection.forEach((val) => {
                   
                    this.tableData.forEach((row,index) =>{
                       

                         if(row.id==val.id){
                            //判断是否相等
                           
                            console.log("true")
                            this.tableData.splice(index,1)

                         }

                    });
              });

         }

         
         

      },

      handleSelectionChange(val) {

       this.multipleSelection =val;
       
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