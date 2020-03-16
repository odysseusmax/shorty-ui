<template>
  <div class="container p-6">
    <div v-for="shortUrl in shortUrls" :key="shortUrl.code" class="bg-gray-200 my-4 p-4 border-2 border-solid border-gray-600 rounded-lg">
        <div class="border-2 hover:border-6 border-solid border-gray-600 rounded-md text-center w-full sm:w-1/4 p-1 "> {{shortUrl.created_on}}</div>
        <br/>
        <a :href="shortUrl.url" class="m-2 p-2 text-center text-gray-600 w-full"> {{shortUrl.url}} </a>
        <br/>
        <router-link :to="'/'+shortUrl.code" class="m-4 p-2 text-center text-red-500"> {{currentUrl}}/{{shortUrl.code}}</router-link>
        <br/>
        <button class="p-3 m-2 text-red-600 hover:bg-red-600 hover:text-white border-2 border-solid border-red-600 rounded-md" @click="copyClipboard(shortUrl.code)"> Copy</button>
        <button class="p-3 m-2 text-red-600 hover:bg-red-600 hover:text-white border-2 border-solid border-red-600 rounded-md" @click="clear(shortUrl.code)"> Clear!</button>
    </div>
    <div id="qr_code"></div>
  </div>
</template>

<script>

export default {
  name: "DisplayUrls",
  props : ["shortUrls"],
  data(){
    return {
        currentUrl : window.location.host
    }
  },
  methods:{
    copyClipboard(code){
        const el = document.createElement('textarea');
        el.value = this.currentUrl +'/' + code
        document.body.appendChild(el);
        el.select();
        document.execCommand('copy');
        document.body.removeChild(el);
    },
    clear(code){
        this.$emit('clear', code)
    }
  }
};
</script>
