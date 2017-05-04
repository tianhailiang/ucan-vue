

<template>
  
  <header class="header">
    <h1 class="logo">优看后台管理系统v1.0
    </h1>
    
    <div class="log_right" >
      
       <!--  <img src="../../assets/logo.png" class="person_logo"> -->

        <div class="person_right">
          <router-link to="/Login" tag="span">进入网站</router-link>
         
          <span>修改个人信息</span>
          <span>退出</span>

        </div>

    </div>

  </header>
</template>

<script>

export default {
  name: 'top',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  header{
    width:100%;
    height:105px;
    background:#eee;
   
    border-bottom:2px solid #ffaf00;
    position:relative;

  }

.logo{
  position:absolute;
  left:0;
  top:0;
  width:100%;
  height:100%;
  text-align:center;
  line-height: 105px;
  font-size:55px;
  color:#f09900;
}
.log_right{
  position: absolute;
  right:0;
  top:0;
  display: flex;


}

.person_right{
  margin-right:20px;
}

.person_logo{
  width:40px;
  height:60px;
  border:10px solid #333;
  margin-right:10px;
}

span{
  display:block;
}


</style>
