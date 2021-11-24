<template>
    <div ref="boxCavas">xxx</div>
</template>

<script setup lang="ts">
   import { onMounted, ref } from '@vue/runtime-dom';
   import * as PIXI from 'pixi.js';
   console.log(PIXI);
   const boxCavas = ref<HTMLDivElement | null>(null);
   webGLisCavas();
   //判断支持度
   function webGLisCavas():void{
     let type = "WebGL"
     if(!PIXI.utils.isWebGLSupported()){
       type = "canvas"
     }
     PIXI.utils.sayHello(type);
   };
   //画图
   function drawPIXI ():void{
     let app = new PIXI.Application({width: 256, height: 256});
     boxCavas.value?.appendChild(app.view)
   }
   onMounted(()=>{
     console.log(boxCavas.value);
     drawPIXI();
   })
</script>