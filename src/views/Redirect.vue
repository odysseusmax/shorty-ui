<template>
  <div class="text-white text-center p-8 font-serif">
    <div v-if="error">
        <h1 class="text-5xl m-4">Ooops... 404</h1>
        <p class="text-xl m-4">That URL doesn't exists. Go home and shorten your URL's. </p>
        <br/>
        <router-link to="/" class="bg-indigo-500 hover:bg-blue-400 p-5 rounded-md font-bold"> Go Home </router-link>
    </div>
    <div v-else>
        <h1 class="text-5xl m-4">You will be redirected shortly..</h1>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Redirect",
  data(){
    return {
        error:false,
        message:""
    }
  },
  methods:{
    
  },
  async created(){
    var code = this.$route.params.code;
    var endpoint = "https://shortyapi.herokuapp.com/api/v1/url";
    var r = await axios.get(
        endpoint,
        {
            params:{
                code:code
            }
        }
    );
    if(r.data.status == 200){
        window.location.href = r.data.data.url;
    }
    else{
        this.error = true;
        this.message = r.data.message
    }
  }
};
</script>
