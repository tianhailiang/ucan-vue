<style scoped>
 
.logo_box{
  width:100%;
  height:100%;
  background:#f76907;
  
} 
  
 .top{
  width:100%;
  height:300px;
 
  box-sizing: border-box;
  font-size:50px;
  color:#fff;
  text-align:center;
  padding-top:180px;
 }



.user_login_content {
   background:#fff;
    width:100%;
    height:252px;
    border-top:10px solid #f7f7f7;
    border-bottom:10px solid #f7f7f7;

    display: flex;
    flex-direction: column;

    align-items: center;
}

.user_login_content label {
    text-align: center;
    margin: 10px;
    width: 70px;
}

.usermessage {
    margin: 50px 10px 0;
    width: 320px;
    border-radius: 20px;
    border: 1px solid #6a3906;
    outline: medium;
    
    appearance: none;
    height: 35px;
    padding: 0 10px;
}

.pwd{
  margin-top:27px;
}


.prompt {
    display: inline-block;
    color: red;
   
   width:150px;
}





.login_button {
    display: inline-block;
    text-indent: 0.5em;
    width: 130px;
    height: 36px;
    background-color: #ff870d;
   
    border-radius: 10px;
    font-size: 20px;
    font-weight: bold;
    color: #fff;
    letter-spacing: 10px;
    outline: medium;
    cursor: pointer;
        margin-top: 37px;
    margin-left: -149px;
}




</style>


<template>
  
 <div class="logo_box">
 	
			
			<div class="top" >
         优看后台管理系统v1.0  
      </div>
			
			<div  class="user_login_content">
        <div>
    				<label>邮箱</label>
    				<input type="text" class="usermessage"  placeholder="请输入邮箱" v-on:blur="user($event.target.value)" ref="email" v-model="userName"><span class="prompt" >{{userTitle}}</span>
				 </div>
         <div>
    				<label>密码</label>
    				<input type="password" class="usermessage pwd"  placeholder="请输入密码" v-on:blur="pwd($event.target.value)" v-model="password" ref="pwd"><span class="prompt">{{pwdTitle}}</span>

			    </div>
				<div  >
					<input type="button"   value="登录" class="login_button" v-on:click="login()" />
				

				</div>
				

			</div>


 </div>

</template>

<script>

import axios from 'axios'

var qs = require('qs');

export default {
  name: 'login',
  data () {
    return {
      userTitle:"",
      pwdTitle:"",

      userName:"",
      password:"",
      checked:true

    }
  },

  methods: {
    user: function (message) {
      if(message==""){
      	this.$refs.email.focus();
        this.$set(this,'userTitle', "用户名不能为空");
      }else{
         //先验证邮箱

         var reg = /^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/;

         if(reg.test(message)){
             
         	  this.$set(this,'userTitle', "");
         }else{
         	//获取元素焦点
         	
         	this.$refs.email.focus();
         	
         	this.$set(this,'userTitle', "邮箱地址不合法！");
         }

      }
    },

    pwd:function(pwd){

       if(pwd==""){
       	     this.$refs.pwd.focus();
            this.$set(this,'pwdTitle', "密码不能为空");
       }else{

       	   this.$set(this,'pwdTitle', "");
       }

    },

    login:function(){
     
       if(this.userName==""){
       		this.$refs.email.focus();
       	    this.$set(this,'userTitle', "用户名不能为空");
       	   return;
       }

       if(this.password==""){
       	    this.$refs.pwd.focus();
            this.$set(this,'pwdTitle', "密码不能为空");   
            return;      
       }
     
       var that = this;
       // http://m.wishlist1314.com/wishlist_mobile/mobile/getBannerList
       // http://localhost:9000/static/mock/login/login.json
         
       
       axios.get("http://localhost:9000/static/mock/login/login.json",{

            params:{
             "name":that.userName,
            "pwd":that.password
          }
          
       })
		  .then(function (response) {

		      console.log(response)
          var result=response.data;
          
          if(result.code==0){
        

             that.$router.push({ path: 'Index_login' });

          }else{

            alert(result.msg)
          } 
          
		      

		  })
		  .catch(function (error) {
		      console.log(error);
		  });


    }
  }
}
</script>




