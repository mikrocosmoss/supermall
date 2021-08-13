<template>
  <!--所有的item都展示同一个图片，同一个文字-->
<div class="tab-bar-item" @click="itemClick">
 <!--<img src="../../assets/img/tabbar/home.svg"/>-->
  <!--<div>首页</div>-->
  <div v-if="!isActive">
    <slot name="item-icon"></slot>
  </div>
  <div v-else>
    <slot name="item-icon-active"></slot>
  </div>

 <div :style="activeStyle">
  <slot name="item-text"></slot>
 </div>
</div>
</template>

<script>
    export default {
        name: "tab-bar-item",
        props:{
            path:String,
          activeColor:{
              type:String,
            default:'red'
          }
        },
        data(){
          return{
            // isActive:true,

          }
        },
      computed:{
        isActive(){
          //找到path相同
          return this.$route.path.indexOf(this.path) !== -1
        },
        activeStyle(){
          return this.isActive ? {color:this.activeColor}:{}
        }
      },
      methods:{
          itemClick(){
            this.$router.replace(this.path)
          }
      }

    }
</script>

<style scoped>

  .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }
  .tab-bar-item img{
    margin-top: 3px;
    width: 24px;
    height: 24px;
    /*图片与文字之间消除空间 消除默认3像素*/
    vertical-align: middle;
    margin-bottom: 2px;
  }
  .active{
    color: red;
  }

</style>
