<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommand-view :recommends="recommends"></recommand-view>
    <feature-view></feature-view>
    <tab-control class="tab-control" :titles="['流行','新款','精选']"></tab-control>




    <ul>
    <li>列表1</li>
  </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>
    <ul>
      <li>列表1</li>
    </ul>
    <ul>
      <li>列表2</li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul>
    <ul>
      <li></li>
    </ul><ul>
    <li></li>
  </ul>

  </div>
</template>

<script>

  import HomeSwiper from './childComponents/HomeSwiper'
  import RecommandView from './childComponents/RecommandView'
  import FeatureView from './childComponents/FeatureView'

  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'

  import {getHomeMultidata,getHomeGoods} from "../../network/home";

  // import Swiper from 'components/common/swiper/Swiper'


  export default {
        name: "home",
      components:{

        HomeSwiper,
        RecommandView,
        FeatureView,
        NavBar,
        TabControl
      },
    //保存请求的res
    data(){
      return{
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]},
        }
      }
    },
    //发送网络请求
    created(){
    //1.请求多个数据
      this.getHomeMultidata()

    //  2.请求商品数据 传递不同的类型
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods:{
          getHomeMultidata(){
            getHomeMultidata().then(res => {
              this.banners = res.data.banner.list;
              this.recommends = res.data.recommend.list;
              // console.log(res);
            })
          },
      getHomeGoods(type){
        const page = this.goods[type].page + 1;
        getHomeGoods(type, page).then(res =>{
          //console.log(res);
          this.goods[type].list.push(...res.data.list);
          this.goods[type].page += 1;
        })
      }
    }
  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
.home-nav{
  background: var(--color-tint);
  color: #fff;
  position: fixed;
  left: 0;
  right: 0;
  top: 0;
  z-index: 9;
}
  /*实现tab-control的不随之浮动和浮动的转换 根据距离调节*/
  .tab-control{
    /*自动根据top的值设置是fixed或是sticky*/
    position: sticky;
    top: 44px;

  }
</style>
