<template>
    <div ref="boxCavas"></div>
     <button @click="onStart">
         {{start ? '停止' : '开始'}}
     </button>
    <div>cavas 宽{{cavasWidth}}</div>
    <div>cavas 高{{cavasHeight}}</div>
    <!-- <img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fdata.apkshub.com%2F5e%2Fcom.hiapk.hidict%2Fscreenhost%2Ficon.png&refer=http%3A%2F%2Fdata.apkshub.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640502470&t=a506c4f890f58cd76e8b15a95d6bee3f" alt=""> -->
</template>

<script setup lang="ts">
import { ref } from "@vue/runtime-dom";

  //Aliases
  let Application = PIXI.Application,
  loader = PIXI.loader,
  resources = PIXI.loader.resources,
  Sprite = PIXI.Sprite;
  //Create a Pixi Application
  let app = new Application({ 
    width: 500, 
    height: 500,                       
    antialias: true, 
    transparent: false, 
    resolution: 1
    }
  );
  let cavasWidth = [app.view][0].width;
  let cavasHeight = [app.view][0].height;
  let start = ref(false)
  //Add the canvas that Pixi automatically created for you to the HTML document
  console.log([app.view],'app.view');
  
  document.body.appendChild(app.view);

//load an image and run the `setup` function when it's done
loader
  .add("ball_1.png")
  .add('https://ourydcimage.ourydc.cn/giftImage/gift/101_10000_23.png')
  .load(setup);
//This `setup` function will run when the image has loaded
function setup() {
  //Create the cat sprite
  let cat = new Sprite(resources["ball_1.png"].texture);
  cat.x = 0;
  cat.y = cavasHeight - 100;
  cat.width =100;
  cat.height = 100;
  cat.rotation = 0.5;
  cat.anchor.x = 0.5;
  (cat as any).vx = 1;
  (cat as any).vy = 1;
  //Add the cat to the stage
  app.stage.addChild(cat);
  app.ticker.add(function gameLoop (delta){
    //   console.log(delta,'delta');
    //  requestAnimationFrame(gameLoop);
    //  (cat as any).vx = 1;
    //  (cat as any).vy = 1;
     
     //Apply the velocity values to the cat's 
     //position to make it move
     if (start.value) {
         cat.x += (cat as any).vx;
         if (cavasWidth <= cat.x) {
             (cat as any).vx = -1;
         }else if (0 == cat.x) {
             (cat as any).vx = +1;
         }   
     }
    //  cat.y += (cat as any).vy;
  });
}
function onStart(){
    start.value = !start.value;
}
// function gameLoop(){

//   //Move the cat 1 pixel 
//   cat.x += 1;
// }
</script>