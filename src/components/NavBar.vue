<template>
  <nav class="navbar navbar-expand-lg navbar-tuna ">
      <a class="navbar-brand" href="#">
        <img src="https://thetunagroup.com/storage/settings/Tuna1559538115.svg" width="200" height="30" class="d-inline-block align-top" alt="" loading="lazy">
      </a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
        
          <li class="nav-item active" v-for="menu in menus" v-bind:key="menu">
            <a class="nav-link tuna-a" href="/">{{menu.menuname}} <span class="sr-only">(current)</span></a>
          </li>
          <!--<li class="nav-item">
            <a class="nav-link tuna-a" href="#">Our Teaters</a>
          </li>
          <li class="nav-item">
            <a class="nav-link tuna-a" href="#">Food & drinks</a>
          </li>
          <li class="nav-item">
            <a class="nav-link tuna-a" href="#">Host Events</a>
          </li>
          <li class="nav-item">
            <a class="nav-link tuna-a" href="#">Gift card</a>
          </li>-->
          
          
        </ul>
        <span class="navbar-text">
          <a href="#" class="btn btn-warning">
          Show time
          </a>
        </span>
      </div>
    </nav>
</template>

<script>
import ax from 'axios';
const axios = ax;
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => ({
      menus : [],
   }),
   mounted () {
      this.getSlides();
       
    },
  methods:{
    getSlides : function(){
       axios.get('http://testvue.thetunagroup.com/?api=menus').then((response) => {
            console.log(response.data);
            if(response.data.menus){
              // this.sliders = this.currentShows.sliders;
              this.menus = response.data.menus;
              // this.$refs.carousel.reload()
            }
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
 color:#313944
}
a.nav-link.tuna-a {
    font-size: 13px;
}
</style>
