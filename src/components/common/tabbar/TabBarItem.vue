<template>
  <div class="tab-bar-item" @click="itemClick">
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
    name: "TabBarItem",
    //此处接收的path并不是App中data中传出来的 所以不用加： 正常在data中传出来的需要加： 这个path是子组件本身的path
    //本身传给本身不需要冒号，组件传给组件需要冒号
    props:{
      path:{
        type:String
      },
      activeColor:{
        type: String,
        default:'red'
      }
    },
    data(){
      return {

      }
    },
    computed:{
      isActive(){
        return this.$route.path.indexOf(this.path) !== -1
      },
      activeStyle() {
        return this.isActive ? {color:this.activeColor} : {}
      }
    },
    methods:{
      itemClick() {
       this.$router.replace(this.path)
      }
    }
  }
</script>

<style scoped>
  .tab-bar-item{
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    font-size: 14px;
    padding-top: 3px;
    box-sizing: border-box;
  }
  .tab-bar-item img{
    width: 24px;
    height: 24px;
  }
  .active{
    color:red;
  }
</style>
