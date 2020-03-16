<template>
  <div>
    <Form @newData="addData"/>
    <DisplayUrls :shortUrls="shortUrls" @clear="delUrl"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Form from "@/components/Form.vue";
import DisplayUrls from "@/components/DisplayUrls.vue";

export default {
  name: "Home",
  components: {
    Form,
    DisplayUrls
  },
  data(){
    return {
        shortUrls : []
    }
  },
  methods:{
    addData(e){
        this.shortUrls.push(e)
    },
    delUrl(code){
        this.shortUrls = this.shortUrls.filter(shortUrl => shortUrl.code !== code);
    }
  },
  created(){
    if (localStorage.getItem('shorty')){
        this.shortUrls = JSON.parse(localStorage.getItem('shorty'));
    }
  },
  watch: {
    shortUrls: {
        handler() {
            localStorage.setItem('shorty', JSON.stringify(this.shortUrls));
        },
        deep: true,
    },
  },
};
</script>
