<style scoped>
  .login{
         width: 420px;
         height: 420px;
    position: relative;
    margin: 100px auto;
  }

  .header_span{
  	display: inline-block;
    width: 100%;
   
    text-align: center;
    color: #a0a0a0;
   
   
    line-height: 40px;
    height: 40px;
   

    font-size: 30px;
    font-weight: 600;
    letter-spacing: 15px;
    border-bottom: 1px solid #ffe100;
  }


  .user_login_content {
   
    width: 570px;
}

.user_login_content label {
    text-align: center;
    margin: 10px;
    width: 70px;
}

.usermessage {
    margin: 15px 10px;
    width: 325px;
    border-radius: 20px;
    border: 1px solid #6a3906;
    outline: medium;
    
    appearance: none;
    height: 35px;
    padding: 0 10px;
}


.prompt {
    display: inline-block;
    color: red;
    width: 150px;

}

.auto_login_content {
    width: 420px;
    text-align: center;
    margin: 10px;
    font-size: 16px;
}

.auto_login {
    border: 1px solid #6a3906;
    width: 10px;
    height: 10px;
    color: #6a3906;
    border-radius: 20px;
    margin-left: 10px;
}

.font{
	color: #a0a0a0;
    font-size: 14px;
    margin:10px;
}


.login_re {
    width: 420px;
    text-align: center;
}

.login_button {
    display: inline-block;
    text-indent: 0.5em;
    width: 130px;
    height: 35px;
    background-color: #ffe100;
    border: 1px solid #ffe100;
    border-radius: 15px;
    font-size: 20px;
    font-weight: bold;
    color: #6a3906;
    letter-spacing: 10px;
    outline: medium;
    cursor: pointer;
}

.login_re p {
    display: inline-block;
    text-align: center;
    margin: 20px;
    font-size: 16px;
}


</style>


<template>
  
 <div class="login">
 	
			
			<span id="user_login" class="header_span" style="cursor: pointer;">账号登录</span>
			
			<div id="user_login_content" class="user_login_content">
				<label>邮箱</label>
				<input type="text" class="usermessage"  placeholder="请输入邮箱" v-on:blur="user($event.target.value)" ref="email" v-model="userName"><span class="prompt" >{{userTitle}}</span>
				
				<label>密码</label>
				<input type="password" class="usermessage pwd"  placeholder="请输入密码" v-on:blur="pwd($event.target.value)" v-model="password" ref="pwd"><span class="prompt">{{pwdTitle}}</span>

				<div id="auto_login_content" class="auto_login_content">
					<input type="checkbox" name="auto_login" id="auto_login" value="0" class="auto_login" />
					<span>下次自动登录 </span>
					<span class="font">使用公共电脑请谨慎选择</span>

				</div>
				<div id="login_re" class="login_re">
					<input type="button"  id="login_button" value="登录" class="login_button" v-on:click="login()" />
					<p>
						<a href="../resetPassword/resetPassword.html">忘记密码</a>|
						<a href="../register/register.html" class="f_b">免费注册</a>
					</p>

				</div>
				

			</div>


 </div>

</template>

<script>

import axios from 'axios'


export default {
  name: 'login',
  data () {
    return {
      userTitle:"",
      pwdTitle:"",

      userName:"",
      password:""

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
       axios.get("http://m.wishlist1314.com/wishlist_mobile/mobile/getBannerList")
		  .then(function (response) {

		    console.log(response);
           
          
		    that.$router.push({ path: 'Index_login' });

		  })
		  .catch(function (error) {
		    console.log(error);
		  });

    }
  }
}
</script>




