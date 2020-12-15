<template>
   <table class="table table-striped">
        <thead>
            <tr>
            <th scope="col">#</th>
            <th scope="col">country</th>
            <th scope="col">code</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(value,key) in countries" v-bind:key="key">
            <th scope="row">{{key+1}}</th>
            <td>{{value.name}}</td>
            <td>{{value.alpha3Code}}</td>
            </tr>
        </tbody>
    </table>
</template>

<script>

import ax from 'axios';
const axios = ax;
// import { ValidationProvider, extend } from 'vee-validate';
export default {

data (){
    return{
        countries : [],
    }
},
mounted(){
   
},
methods:{
    getCountry (region){
        if(region == ''){
            this.countries = [];
            return;
        }
       axios.get('https://restcountries.eu/rest/v2/region/'+region).then((response) => {
            console.log(response.data);
              // this.sliders = this.currentShows.sliders;
              this.countries = response.data;
              // this.$refs.carousel.reload()
        });
    }
}
}
</script>

<style>

</style>