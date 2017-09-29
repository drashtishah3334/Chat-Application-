<template>
    <div class="app-messages">
        <h1 class="title" v-if="loading">Loding...</h1>
        <div v-for="(thread,index) in threads" :key="index" >
            <div  style="color:rgb(170,173,204);">
                
                <router-link :to="{ name: 'chat-messages', params: { threadname: thread.threadname } }" style="text-decoration:none;">
                 <div class="thread_section">
                  <b>  {{thread.threadname}} </b>
                  <hr style="border-color: rgba(238, 238, 250, 0.34);"></hr>
                   </div>
                    </router-link>
            </div>
        </div>
    </div>
    
</template>
<script>
import threads from '@/stubs/threads'


export default {
name:'app-messages',

created(){
    this.fetchThreads()
},
watch:{
    channelSlug(){
            this.fetchThreads()
    }
    
},
computed:{
        channelSlug(){
            return this.$route.params.channelname
        }
},
data(){
    return{
        threads:false,
        loading:false
    }
    
},
methods:{
    fetchThreads() {
        this.loading = true
        setTimeout(() => {
          this.loading = false
          this.threads = threads[this.channelSlug]
        }, 2000)
      },
      subscribeForMessages() {
        this.$bus.$on('message-sent:' + this.channelSlug, (message) => {
          this.messages.push(message)
          setTimeout(() => {
            this.$el.scrollTop = this.$el.scrollHeight
          }, 100)
        })
      }
    }
}
</script>

<style lang="scss">
.app-messages{
    position: fixed;
    top:0px;
    botton:0px;
    left:300px;
    width:20%;
    background-color:white;
    color:rgb(95,98,131);
}
.thread_section
{
    text-align:left;
}
</style>
