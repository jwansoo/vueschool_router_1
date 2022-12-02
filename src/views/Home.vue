<template>
  <div class="home">
    <h1>All Destinations</h1>
    <button @click="triggerRouterError">Trigger Router Error</button>
    <button @click="addDynamicRoute">Add Dynamic Router</button>
    <router-link to="/dynamic">Visit Dynamic Router</router-link>
    <div class="destinations">
    <router-link
      v-for="destination in destinations"
      :key="destination.id"
      :to="{name:'destination.show', params:{id:destination.id,slug:destination.slug}}"
     >
     <h2>{{destination.name}}</h2>
     <img :src="`/images/${destination.image}`" :alt="destination.name" />
     
     </router-link>
    </div>
  </div>
</template>

<script setup>
import {ref} from 'vue'
import { useRoute,useRouter } from 'vue-router';
import sourceData from '../data.json'
import { isNavigationFailure, NavigationFailureType } from 'vue-router';
const destinations=ref(sourceData.destinations)
const router=useRouter()
const triggerRouterError= async ()=>{
  const navigationFailue=await router.push('/')
  if(isNavigationFailure(navigationFailue, NavigationFailureType.duplicated)){
    console.log(navigationFailue.to)
    console.log(navigationFailue.from);
  }else{

  }
}

const addDynamicRoute=()=>{
  router.addRoute({
    name:'dynamic',
    path:'/dynamic',
    component:()=>import('../views/Login.vue')
  })
  router.removeRoute('dynamic')
}
</script>

<style lang="scss" scoped>

</style>