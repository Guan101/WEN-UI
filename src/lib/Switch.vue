<template>
  <button @click="toggle" :class="{checked:value}"> <span></span></button>
</template>
<script lang="ts">
import { ref } from 'vue'
export default {
    props: {
    value: Boolean,
  },
  setup(props, context){
    const toggle = ()=>{
      context.emit('update:value', !props.value)
    }
    return { toggle}
  } 
}
</script>
<style lang="scss" scoped>
button {
  height: 22px; 
  width: 44px;
  border: none;
  background: #bfbfbf;
  border-radius: 11px; 
  position: relative;
  > span {
    position: absolute; 
    top: 2px; 
    left: 2px; 
    height: 18px; 
    width: 18px;
    background: white; 
    border-radius: 9px;
    transition: all 250ms;
    caret-color: transparent;
  }
  &.checked { background: #1890ff;
    > span { left: calc(100% - 19px)}
  }
  &:focus{outline: none;}
  &:active{
    > span {width: 22px;}
  }
 &.checked:active{
    > span {width: 22px; margin-left: -4px;}
  }
}
</style> 