<template>
<div>
  <div class="w-full flex flex-col items-center pt-10">
    <ul class="flex w-[30%] justify-between">
      <li @click="changeDisplay('login')" :class="{'active':activeDispaly === 'login'}"  class="text-[22px] font-bold text-white cursor-pointer hover:text-rose-400 border-sky-300 hover:border-b-2">ورود</li>
      <li @click="changeDisplay('register')" :class="{'active':activeDispaly === 'register'}" class="text-[22px] font-bold text-white cursor-pointer hover:text-rose-400 border-sky-300 hover:border-b-2">ثبت نام</li>
    </ul>
    <login v-show="activeDispaly == 'login'"/>
    <Register v-show="activeDispaly == 'register'"/>
  </div>
</div>
</template>



<script setup>
import { ref } from 'vue';
import Login from './components/Login.vue';
import Register from './components/register.vue';


components:{
  Login;
  Register;
};

let activeDispaly = ref("login") 
function changeDisplay(display_name){
    activeDispaly.value = display_name
}
</script>



<style scoped>
.active{
  color: rgb(251 113 133);
  border-bottom: 2px solid #07afff;
}
</style>
