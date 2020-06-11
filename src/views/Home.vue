<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    
  </div>
</template>

<script>


export default {
  name: 'Home',
  data(){
    return{
    cookieObj: null,
    cookieLang:null
    }

  },
  mounted(){
    this.cookieObj = new this.$cookie;
    this.cookieLang = this.cookieObj.read('language');
    if(this.cookieLang){
      this.$router.push('/' + this.cookieLang + '/videos')
      
    }

  }

}
</script>
