
<style scoped>

.Sidebar_tree{
  width:420px;
}

</style>

<template>
  
  <div >

    <Top></Top>
    <div class="Sidebar_tree">
      
      <SidebarTree></SidebarTree>

    </div>

    <router-view></router-view>
        
  </div>

</template>

<script>
	
import Top from './Header';
import SidebarTree from './Sidebar_tree'

export default {
  name: 'Index_login',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    Top,SidebarTree
  }
}

</script>