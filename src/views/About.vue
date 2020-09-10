<template>
  <div class="container-fluid">
    
    <div class="social-section">
      <div class="row">
        <div class="col-12 social-distance">
          <div class="d-flex flex-row bd-highlight pd-10 container">
            <span>to learn more about our social distancingspanolicies,</span>
            <span><a href="#" class="social-policy"> click here</a></span>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <Navbar />
    </div>
    <div class="slide-section">
        <div class="container">
            <div class="row">
                <div class="col-3">

                  <div class="movie-filter">
                      <div class="movie-filter-header">
                        <h4>Buy Tickets</h4>
                      </div>
                      <div class="movie-body">
                          <button type="button" class="list-group-item list-group-item-action">Select Theatre</button>
                          <button type="button" class="list-group-item list-group-item-action">Today August 19th</button>
                          <button type="button" class="list-group-item list-group-item-action">All Movies</button>
                          <button type="button" class="list-group-item list-group-item-action">All showing types</button>
                          <button class="btn btn-block see-show-button">  show tickets </button>
                          
                      </div>
                      
                  </div>
                </div>
                <div class="col-9">
                  <agile  ref="carousel" :navButtons="false" v-if="mainSliders.length>0">
                      <div class="slide-custom" v-for="mainSld in mainSliders" v-bind:key="mainSld">
                        <div class="text-part">
                          <div class="text-body">
                              <div class="title">{{mainSld.title}}</div>
                              <div class="text">{{mainSld.text}}</div>
                              <button class="btn btn-book-now see-show-button">{{mainSld.button_name}}</button>
                          </div>
                        </div>
                        

                          <img :src="mainSld.image" class="slide d-block">
                      </div>
                      <!--<div class="slide-custom">
                          <img src="https://3nmm1b14jyur43hv6x3k103p-wpengine.netdna-ssl.com/wp-content/uploads/2020/08/51863-EMAGINE-Your-Private-Cinema-MN-Homepage-Slider-Revised.jpg"  class="slide d-block">
                      </div> -->
                  </agile>
                      <a class="carousel-control-prev" href="#" @click="$refs.carousel.goToPrev()" role="button" data-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="sr-only">Previous</span>
                      </a>
                      <a class="carousel-control-next" href="#" @click="$refs.carousel.goToNext()" role="button" data-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="sr-only">Next</span>
                      </a>
                  
                </div>
            </div> <!-- row-->
          
        </div><!-- container -->
    </div><!-- main section -->
    <div class="body-section">
        <div class="container">
            <div class="row">
              <div class="col-12">
                  <div class="body-title">
                    <h5>Now showing</h5>
                    <a href="#" class="float-right">see more</a>
                  </div>
              </div>
               
            </div>
            <div class="row">
               <div class="col-3" v-for="sld in sliders" v-bind:key="sld">
                  <div class="card h-150">
                   <!-- <div class="card-body text-center" data-filter="overlay-theme"  :style="'background-image: url('+sld.image+');'">
                      <div class="hovered-item">
                          <div class="card-title hover-p">
                            <h5><a href="javascript:;">{{sld.title}}</a></h5>
                            <span class="rate">{{sld.rating}}</span> <span>|</span> <span class="duration">{{sld.run_time}}</span>
                          </div>
                          <p class=" hover-p">{{sld.text}}</p>
                          <div class="btn-grps mt-auto">
                          
                            <button class="btn btn-block btn-light">Watch trailer</button>
                            <button class="btn btn-block btn-primary">Get Tickets</button>
                          </div>
                        </div>
                    </div> -->
                      <div class="card-body d-flex flex-column" data-filter="overlay-theme" :style="'background-image: url('+sld.image+');'">
                        <div class="card-title hover-p">
                            <h5><a href="javascript:;">{{sld.title}}</a></h5>
                            <span class="rate">{{sld.rating}}</span> <span>|</span> <span class="duration">{{sld.run_time}}</span>
                        </div>
                        <ul class="list-unstyled mt-3 mb-4 hover-p">
                          <li>{{sld.text}}</li>
                        </ul>
                        <div class="btn-group-vertical mt-auto hover-p">
                          <button class="btn btn-block btn-light">Watch trailer</button>
                          <button class="btn btn-block see-show-button">Get Tickets</button>
                        </div>
                      </div>
                  </div>
                </div>
            </div>
        </div>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '@/components/NavBar.vue'
// import { VueFlux, Transitions } from 'vue-flux';

import ax from 'axios';
const axios = ax;

export default {
  name: 'About',
  components: {
    Navbar,
    // VueFlux
  },
   data: () => ({
      slides: 5,
      active: 1,
      currentShows : [],
      sliders : [],
      hoverFlag : false,
      mainSliders : [],
   }),
   mounted () {
      this.getNowShowing();
      this.getSlides();
       
    },
   methods: {
    move(amount) {
      let newActive
      const newIndex = this.active + amount
      if (newIndex > this.slides) newActive = 1
      if (newIndex === 0) newActive = this.slides
      this.active = newActive || newIndex
    },
    jump(index) {
      this.active = index
    },
    addSlide() {
      this.slides = this.slides + 1
    },
    removeSlide() {
      this.slides = this.slides - 1 
    },
    getNowShowing : function(){
       axios.get('http://testvue.thetunagroup.com/?api=now-showing').then((response) => {
            console.log(response.data);
            this.currentShows = response.data;
            if(this.currentShows.sliders){
              // this.sliders = this.currentShows.sliders;
              this.sliders = this.currentShows.sliders.slice(0, 4);
            }
        });
    },
    getSlides : function(){
       axios.get('http://testvue.thetunagroup.com/?api=get-sliders').then((response) => {
            console.log(response.data);
            if(response.data.sliders){
              // this.sliders = this.currentShows.sliders;
              this.mainSliders = response.data.sliders;
              // this.$refs.carousel.reload()
            }
        });
    }
  }
}
</script>

<style lang="scss" >
// @import '../flex.scss';

$primary: #5f285f;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}



.prev,
.next {
  position: absolute;
  top: 50%;
  width: 50px;
  height: 50px;
  border: 2px solid $primary;
  color: $primary;
  border-radius: 50%;
  margin-top: -25px;
  margin-left: 25px;
  cursor: pointer;
  line-height: 48px;
  text-align: center;
  text-indent: -2px;
  transition: all 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  
  &:hover {
    background: $primary;
    color: #fff;
    transform: scale(1.2);
  }
  
  &:active {
    transform: translate(0, 3px) scale(1.2);
  }
}

.next {
  right: 0;
  margin-left: auto;
  margin-right: 25px;
  text-indent: 2px;
}

.dots {
  position: fixed;
  // display: block;
  // width: 100%;
  text-align: center;
  bottom: 20px;
}
.agile__dots li{
    padding-left: 5px;
    &button {
      border-radius: 50px !important;
    }
}
.agile__dots li button{
    
  border-radius: 50px !important;
      background: #313944;
    border: 2px solid;
    color: #fff;
    padding: 5px;
  -webkit-appearance: none;
  color: #313944;
  font-weight: bold;
  font-size: 3px;
  cursor: pointer;
  border: 2px solid white;
}
li.agile__dot.agile__dot--current button {
    background: white;
}

.slides {
  font-size: 40px;
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  
  @media (min-width: 600px) {
    font-size: 80px;
  }
  
  @media (min-width: 900px) {
    font-size: 140px;
  }
  
  .animated {
    transition: all 400ms;
    position: absolute;
    transform: translate(-50%, -50%);
  }
  
  .slide-in {
    opacity: 0;
    transform: translate(-40%, -50%);
  }
  
  .slide-in-active {
    transition-delay: 150ms;
  }
  
  .slide-out {
    opacity: 1;
  }
  
  .slide-out-active {
    opacity: 0;
    transform: translate(-60%, -50%);
  }
}

.buttons {
  position: absolute;
  top: 10px;
  left: 10px;
}

button.agile__nav-button {
    background: none;
    border: none;
    font-size: 20px;
    font-weight: 900;
    color: white;
}
.slide {
    -o-object-fit: cover;
    object-fit: cover;
    height: 420px;
    width: 100%;
    margin-bottom: 10px;
    margin-top: 10px;
}
.movie-filter {
    height: 420px;
    background: white;
    margin-top: 10px;
}
.movie-filter-header{
    // height: 420px;
    background: $primary;
    margin-top: 10px;
    color: #fff;
    padding: 20px;
}
.see-show-button{
    background: $primary;
    margin-top: 10px;
    color: #fff;
}
.movie-body {
  padding: 10px;
}
.text-part{
    width:50%;
    text-align: end;

}
.text-body {
    position: absolute;
    top: 20vh;
    text-align: center;
    width: 100%;
}
.title {
    font-size: 28px;
    color: #fff;
    left:10px;
    font-weight: 800;
}
.text{
  color: #fff;
}

.body-section{
  margin-top: 10px;
  margin-bottom: 20px;
}
.hover-p{
  display: none;
}
.card:hover .hover-p {
  display: block;
  
}
 .card:hover [data-filter="overlay-theme"] {
      &:before {
        background-color: #313944de;
      }
    }
.card-body a {
    transition: .5s ease;
    color: white;
    font-weight: 900;
    text-decoration: none;
}
span.rate {
    border: 2px solid;
    padding: 2px;
}
btn-grps{
  font-weight: 100;
  color: rgba(0, 0, 0, .75);
  background-color: rgba(255, 255, 255, 1);
  padding-top: 1rem;
  padding-bottom: 1rem;
}
li {
    max-height: 120px;
    overflow-y: scroll;
    font-size: 14px;
}
.hide-scrollbar::-webkit-scrollbar {
    display: none;
}
li::-webkit-scrollbar {
    width: .1em;
}
button.btn.btn-block.see-show-button {
    margin-top: 10px;
}
</style>
