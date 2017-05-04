

<template>
  
  <header class="header">
    <h1>ucan后台管理系统v1.0
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
    height:80px;
    background:green;
    display: flex;

    justify-content: space-between;

  }

.log_right{
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
