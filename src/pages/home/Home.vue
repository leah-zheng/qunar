<template>
    <div class="main">
        <home-header></home-header>
        <home-swiper :swiper-list="swiperList"></home-swiper>
        <home-icons :icons-list="iconsList"></home-icons>
        <home-recommend :recommend-list="recommendList"></home-recommend>
        <home-weekend :weekend-list="weekendList"></home-weekend>
    </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
export default {
    name:'Home',
    components:{
        "home-header" : HomeHeader,
        "home-swiper" : HomeSwiper,
        "home-icons":HomeIcons,
        'home-recommend':HomeRecommend,
        'home-weekend':HomeWeekend
    },
    data:function(){
        return{
            swiperList:[],
            iconsList:[],
            recommendList:[],
            weekendList:[]
        }
    },
    methods:{
        getHomeInfo:function(){
            axios.get('/api/index.json')
            // axios.get('/qunar_dist/static/mock/index.json')
            .then(this.getHomeInfoSuccess)
        },
        getHomeInfoSuccess:function(res){
            if(res.data.ret && res.data.data){
                var data = res.data.data;
                this.swiperList = data.swiperList;
                this.iconsList = data.iconsList;
                this.recommendList = data.recommendList;
                this.weekendList = data.weekendList;
            }
        }
    },
    mounted:function(){
        this.getHomeInfo()
    }
}
</script>

<style scoped>
.main{
    background-color: #eee;
}
</style>