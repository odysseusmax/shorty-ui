<template>
  <div class="text-white text-center p-8">
    <h1 class="font-serif text-3xl lg:text-4xl xl:text-5xl"> Shorty, The Url Shortener </h1>
    <form @submit="submit">
        <input class="flex-auto bg-blue-600 hover:bg-white hover:text-black border-2 border-solid rounded-md border-blue-900 w-1/2 sm:w-3/4 h-12 font-mono text-center text-sm p-2" type="text" placeholder="Paste the URL you want to shorten" v-model="inputUrl" required/>
        <button class="flex-auto bg-blue-400 hover:bg-green-400 text-base md:text-lg w-1/2 sm:w-1/4 h-12 p-1 font-mono text-center rounded-md" type="submit"> shorten!</button>
    </form>
    <div class="bg-red-600 w-full text-center my-4 p-3 rounded-md" v-if="error">
        {{ errorMessage }}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Form",
  data(){
    return {
        inputUrl:"",
        error : null,
        errorMessage:""
    }
  },
  methods : {
    async submit(e){
        this.error = false;
        e.preventDefault();
        var endpoint = "https://shortyapi.herokuapp.com/api/v1/url";
        var data = new FormData();
        data.set('url', this.inputUrl);
        var r = await axios.post(
            endpoint,
            data
        );
        if(r.data.status == 201){
            this.$emit('newData', r.data.data)
        }
        else{
            console.log(r.data.message);
            this.error = true;
            this.errorMessage = r.data.message;
        }
    }
  }
};
</script>
