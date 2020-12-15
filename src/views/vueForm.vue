<template>
<div class="content">
    <div class="container">
        <ul class="nav justify-content-center">
            <li class="nav-item">
                <a class="nav-link " href="#">Home</a>
            </li>
            <li class="nav-item">
                <a class="nav-link active" href="#">Form</a>
            </li>
            
        </ul>
        <div class="home">
            <div class="mt-5">
                <div class="container">
                    <div class="row">
                        
                        
                        <div class="col-6">
                            <div class="card">
                                <Form/>
                            </div>
                        </div>
                        <div class="col-6">
                            <div class="card">
                                
                                <div class="card-body">
                                   <CountryList ref="countryList"/>
                                </div>
                                    
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

import Form from '@/components/Form.vue'
import CountryList from '@/components/CountryList.vue'
export default {
  name: 'Home',
  components: {
    Form,
    CountryList
  }
}
</script>