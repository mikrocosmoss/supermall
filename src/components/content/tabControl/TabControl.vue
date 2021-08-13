<template>
  <div class="tab-control">
    <div v-for="(item,index) in titles"
         class="tab-control-item" :class="{active:index === currentIndex}"
         @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
    export default {
        name: "tab-control",
      props:{
        titles:{
            type:Array,
            default(){
              return []
            }
          }
      },
      //点击变active
      data(){
          return{
            currentIndex:0
          }
      },
      methods:{
        itemClick(index){
          this.currentIndex = index
        }
      }
    }
</script>

<style scoped>
.tab-control{
  display: flex;
  text-align: center;
  font-size: 16px;
  background: #ffffff;
}
  .tab-control-item{
    flex: 1;
    height: 40px;
    line-height: 40px;
  }
  .tab-control-item span{
    padding: 5px;
  }
  .active{
    color: var(--color-high-text);

  }
  .active span{
    border-bottom: 3px solid var(--color-high-text);
  }
</style>
