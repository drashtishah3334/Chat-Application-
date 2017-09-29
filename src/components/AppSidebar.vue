<template>
<div >
<div class="abc" >
    <h4>Department</h4>
    <br>
    <br>
<div v-if="loading">
    Loading...
</div>
<aside>
   <!-- <ul class="menu-list">
        <li v-for="(chan, index) in chans" :key="index">
            <div style="color:rgb(170,173,204);">
            <router-link :to="{ name: 'app-messages', params: { channelname: index } }" style="text-decoration:none;">
               <div  class="sidebar" style="color:rgb(170,173,204);"> {{chan.name}}</div>
             </router-link>
             <br>
             </div>
        </li>
    </ul>-->
    <table>
    <div class="menu-list">
        <tr v-for="(chan, index) in chans" :key="index">
            <div style="color:rgb(170,173,204);">
            <router-link :to="{ name: 'app-messages', params: { channelname: index } }" style="text-decoration:none;">
               <div  class="sidebar" style="color:rgb(170,173,204);"> {{chan.name}}</div>
             </router-link>
             <br>
             </div>
        </tr>
    </div>
    </table>
</aside>
</div>
</div>
</template>



<script>
import channel from '@/components/channels';
//import ChatMessages from '@/components/ChatMessages';
export default {
    name: 'AppSidebar',    
   /* components:{
        ChatMessages
    },*/

created (){
    this.fetchAllChannels()
},


data() {
      return {
        loading:false, 
        chans: false
      }
},


methods: {
    fetchAllChannels(){
        this.loading=true
        setTimeout(()=>{
            this.loading=false
            this.chans=channel
        },2000)
        
        
    
    }
}

}


</script>



<style lang="scss">
.abc{
    position: fixed;
    background-color:rgb(49,47,74);
    //padding:12px;
    top:0;
    bottom:0;
    left:0px;
    width:300px;
    color:rgb(170,173,204);
}
tr{
    padding-left: 0px;
    border-radius: 2px;
   color:rgb(170,173,204);
      text-align: left;
      //background-color:rgb(238,238,250);

}
.menu-list{
    list-style-type:none;
    color:rgb(238,238,250);
    position:fixed;
    left:30px;
}
.slidebar{
    color:rgb(170,173,204);
    align:left;
}
h4 {
      font-size: 1.1rem;
      font-weight: lighter;
    }
</style>