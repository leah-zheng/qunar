<template>
    <div>
        <city-header></city-header>
        <city-list :hot-cities="hotCities" :cities="cities"></city-list>
    </div>
    
</template>



<script>
import axios from 'axios'
import CityHeader from './components/Header'
import CityList from './components/List'
export default {
    name:'City',
    data:function(){
        return {
            hotCities:[],
            cities:{}
        }
    },
    components:{
        'city-header':CityHeader,
        'city-list':CityList
    },
    methods:{
        getCityInfo:function(){
            // axios.get('/qunar_dist/static/mock/city.json')
            axios.get('/api/city.json')
            .then(this.getCityInfoSuccess)
        },
        getCityInfoSuccess:function(res){
            var data = res.data.data;
            this.hotCities = data.hotCities;
            this.cities = data.cities;
        }
    },
    mounted:function(){
        this.getCityInfo();
    }
}
</script>