<template>
        <div class="card-header">
            <h5 class="mb-0">Personal Information</h5>
            <p class="text-muted mb-0">please fill the form.</p>
        </div>
        <div class="card-body">
            <div class="form-row">
                <div class="form-group col-md-6">
                        <label for="first-name">Full name *</label>
                        <input type="text" v-model="formOb.fname"  class="form-control" :class="error.fname? 'is-invalid':''" name="first-name" id="first-name">
                        <div class="invalid-feedback" v-if="error.fname">
                            {{error.fname}}
                        </div>

                </div>
                <div class="form-group col-md-6">
                <label for="last-name">Email *</label>
                <input type="text" v-model="formOb.email" class="form-control" :class="error.email? 'is-invalid':''" name="email" id="email">
                <div class="invalid-feedback" v-if="error.email">
                        {{error.email}}
                    </div>
                </div>
            </div>
            <div class="form-row">
                
                <div class="form-group col-md-6">
                    <label for="state">Region *</label>
                    <select name="state" id="state" class="form-control" :class="error.region? 'is-invalid':''" v-model="formOb.region">
                        <option value="Africa">Africa</option>
                        <option value="Americas">Americas</option>
                        <option value="Asia">Asia</option>
                        <option value="Europe">Europe</option>
                        <option value="Oceania">Oceania</option>
                    </select>
                    <div class="invalid-feedback" v-if="error.region">
                        {{error.region}}
                    </div>
                </div>
                <div class="form-group col-md-6">
                    <label for="city">DOB *</label>
                    <input type="date" class="form-control " name="city" :class="error.dob? 'is-invalid':''" id="city" v-model="formOb.dob">
                    <div class="invalid-feedback" v-if="error.dob">
                        {{error.dob}}
                    </div>
                </div>
            </div>
            <div class="form-group form-check">
                <input type="checkbox" class="form-check-input" id="exampleCheck1" value="1" v-model="formOb.terms">
                <label class="form-check-label" for="exampleCheck1">I agree to Terms and Conditions</label>
            </div>
        </div>
        <div class="card-footer text-muted d-flex align-items-center">
            <button type="submit" class="btn btn-primary mr-3" @click="handleSubmit()">Submit</button>
            <small v-if="error.terms" class="text-danger">{{error.terms}}</small>
        </div>
</template>

<script>


// import { ValidationProvider, extend } from 'vee-validate';
var validator = require('validator');
export default {

data (){
    return{
        formOb : {},
        error : {},
        error_flag : false,
    }
},
mounted(){
   
},
methods:{
    handleSubmit (){
        console.log(this.formOb);
        this.error = {};
        this.error_flag = false;
        if(!this.formOb.email || !validator.isEmail(this.formOb.email)){
            this.error.email = 'please provide a valid email';
            this.error_flag = true;
        }
        if(!this.formOb.fname || this.formOb.fname == ''){
            this.error.fname = 'please provide a valid full name';
            this.error_flag = true;
        }
        
        if(!this.formOb.region || this.formOb.region == ''){
            this.error.region = 'please provide a valid region';
            this.error_flag = true;
        }
        if(!this.formOb.terms || this.formOb.terms==false){
            this.error.terms = 'please check the terms & conditions';
            this.error_flag = true;
        }
        if(!this.formOb.dob || this.formOb.dob == ''){
            this.error.dob = 'please fill date of birth ';
            this.error_flag = true;
        }
        if(this.formOb.dob && this.calculate_age(this.formOb.dob) < 18 ){
            this.error.dob = 'provided age is less than 18 ';
            this.error_flag = true;
        }
        if(this.error_flag){
            return;
        }
        console.log(this.formOb);
        this.$parent.$refs.countryList.getCountry(this.formOb.region);

    },
    calculate_age(dt) {
        var dob = new Date(dt); 
        var diff_ms = Date.now() - dob.getTime();
        var age_dt = new Date(diff_ms); 
    
        return Math.abs(age_dt.getUTCFullYear() - 1970);
    }
}
}
</script>

<style>

</style>