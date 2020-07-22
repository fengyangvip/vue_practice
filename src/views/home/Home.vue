<template>
 <div id="home">
  <nav-bar class="home-nav">
     <div slot="center">购物街</div>
  </nav-bar>
  <home-swiper :banners="banners"></home-swiper>
  <recommend-view :recommends="recommends"></recommend-view>
  <feature-view></feature-view>
  <tab-control :titles="titles"　></tab-control>


  <ul>
   <li>列表1</li>
   <li>列表2</li>
   <li>列表3</li>
   <li>列表4</li>
   <li>列表5</li>
   <li>列表6</li>
   <li>列表7</li>
   <li>列表8</li>
   <li>列表9</li>
   <li>列表10</li>
   <li>列表1</li>
   <li>列表2</li>
   <li>列表3</li>
   <li>列表4</li>
   <li>列表5</li>
   <li>列表6</li>
   <li>列表7</li>
   <li>列表8</li>
   <li>列表9</li>
   <li>列表10</li>
   <li>列表1</li>
   <li>列表2</li>
   <li>列表3</li>
   <li>列表4</li>
   <li>列表5</li>
   <li>列表6</li>
   <li>列表7</li>
   <li>列表8</li>
   <li>列表9</li>
   <li>列表10</li>
   <li>列表1</li>
   <li>列表2</li>
   <li>列表3</li>
   <li>列表4</li>
   <li>列表5</li>
   <li>列表6</li>
   <li>列表7</li>
   <li>列表8</li>
   <li>列表9</li>
   <li>列表10</li>
   <li>列表88</li>
  </ul>


 </div>
</template>

<script>

import HomeSwiper from './childComps/HomeSwiper'
import RecommendView from './childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'

import {getHomeMultidata,getHomeGoods} from 'network/home'

export default {
    name:'Home',
    components:{
        NavBar,
        HomeSwiper,
        RecommendView,
        FeatureView,
        TabControl
    },
    data(){
      return {
          banners:[],
          recommends:[],
          titles:['流行','新款','精选'],
          goods:{
              'pop':{page:0,list:[]},
          }
      }
    },
    created(){
        this.getHomeMultidata();
        this.getHomeGoods('pop');
    },
    methods:{
        getHomeGoods(type){
            const page = this.goods[type].page + 1;
            getHomeGoods(type,page).then(res =>{
                this.goods[type].list.push(...res.data.list);
                this.goods[type].page++;
            })
        },
        getHomeMultidata(){
            getHomeMultidata().then(res => {
                    this.banners = res.data.banner.list;
                    this.recommends = res.data.recommend.list;
                }
            )
        },

    }
}

</script>

<style scoped>
  #home {
    padding-top: 44px;
   /* height: 100vh;
    position: relative;*/
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }

  .tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

  /*.content {*/
    /*height: calc(100% - 93px);*/
    /*overflow: hidden;*/
    /*margin-top: 44px;*/
  /*}*/
</style>
