<template>
  <div class="home">
    <div id="bigbox" :style="`transform-style: preserve-3d;position: relative;transform: rotateY(${view.y}deg) rotateX(${view.x}deg) rotateZ(${view.z}deg);`">
      <!--<div class="backW" style="font-size: 50px;color: #fff;">back</div>-->
      <div class="bottomW"></div>
      <div class="leftW"></div>
      <div class="3d-content" v-html="box3D">

      </div>
      <!--<div class="box" style="transform: rotateY(-0deg) rotateX(-0deg) translateX(00px) translateY(00px) translateZ(00px)">-->
        <!--<div class="aop up" >up</div>-->
        <!--<div class="aop down" >down</div>-->
        <!--<div class="aop left" >left</div>-->
        <!--<div class="aop right">right</div>-->
        <!--<div class="aop after">after</div>-->
        <!--<div class="aop before">before1</div>-->
      <!--</div>-->
      <!--<div class="box" style="transform: rotateY(-0deg) rotateX(-0deg) translateX(100px) translateY(-200px)">-->
        <!--<div class="aop up" >up</div>-->
        <!--<div class="aop down" >down</div>-->
        <!--<div class="aop left" >left</div>-->
        <!--<div class="aop right">right</div>-->
        <!--<div class="aop after">after</div>-->
        <!--<div class="aop before">before2</div>-->
        <!--<div class="aop charu1">charu1</div>-->
        <!--<div class="aop charu2">charu1</div>-->
      <!--</div>-->
      <!--<div class="box" style="transform: rotateY(-0deg) rotateX(-0deg) translateX(100px) translateY(-300px)">-->
        <!--<div class="aop up" >up</div>-->
        <!--<div class="aop down" >down</div>-->
        <!--<div class="aop left" >left</div>-->
        <!--<div class="aop right">right</div>-->
        <!--<div class="aop after">after</div>-->
        <!--<div class="aop before">before2</div>-->
        <!--<div class="aop charu1">charu1</div>-->
        <!--<div class="aop charu2">charu1</div>-->
      <!--</div>-->
      <!--<div class="box" style="transform: rotateY(-0deg) rotateX(-0deg) ">-->
      <!--<div class="aop up" >up</div>-->
      <!--<div class="aop down" >down</div>-->
      <!--<div class="aop left" >left</div>-->
      <!--<div class="aop right">right</div>-->
      <!--<div class="aop after">after</div>-->
      <!--<div class="aop before">before2</div>-->
      <!--<div class="aop charu1">charu1</div>-->
      <!--<div class="aop charu2">charu1</div>-->
      <!--</div>-->
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import * as THREE from 'three';

export default {
  name: 'home',
  props: ['data', 'size', 'view'],
  data() {
    return {
      dat: [
        {
          step: 1,
          QUANTITY: 60,
          ROW: 3,
          COLUMN: 2,
          LAYER: 3,
          LENGTH_POSITION: 0,
          WIDTH_POSITION: 0,
          HEIGHT_POSITION: 0,
          LENGTH: 200,
          WIDTH: 200,
          HEIGHT: 200,
        },
        {
          step: 2,
          QUANTITY: 5,
          ROW: 2,
          COLUMN: 5,
          LAYER: 2,
          LENGTH_POSITION: 0,
          WIDTH_POSITION: 200,
          HEIGHT_POSITION: 0,
          LENGTH: 200,
          WIDTH: 100,
          HEIGHT: 100,
        },
      ],
      box3D: '',
      data2: [],
    };
  },
  methods: {
    renderBox() {
      this.box3D = '';
      for (let i = 0; i < this.data2.length; i++) {
        const item = this.data2[i];
        console.log(item,'1')
        // ------UP
        const box = `<div class="box" style="transform:translateX(${item.WIDTH_POSITION}px) translateY(-${(item.HEIGHT)+item.HEIGHT_POSITION}px) translateZ(${(item.LENGTH/2) + item.LENGTH_POSITION}px)">`;
        const aopCLOSE = `</div>`;
        const aopUP1 = `<div style="top: ${(item.HEIGHT - item.LENGTH) / 2}px;width: ${item.WIDTH}px;height: ${item.LENGTH}px; transform: rotateX(90deg) translateZ(${item.HEIGHT/2}px);" class="aop up" >`;
        const aopDOWN1 = `<div style="top: ${(item.HEIGHT - item.LENGTH) / 2}px;width: ${item.WIDTH}px;height: ${item.LENGTH}px; transform: rotateX(270deg) translateZ(${item.HEIGHT/2}px);" class="aop up" >`;
        const aopLEFT1 = `<div style="left: ${(item.WIDTH - item.LENGTH) / 2}px;width: ${item.LENGTH}px;height: ${item.HEIGHT}px; transform: rotateY(90deg) translateZ(${-item.WIDTH/2}px);" class="aop left" >`;
        const aopRIGHT1 = `<div style="left: ${(item.WIDTH - item.LENGTH) / 2}px;width: ${item.LENGTH}px;height: ${item.HEIGHT}px; transform: rotateY(90deg) translateZ(${item.WIDTH/2}px);" class="aop right">`;
        const aopBEFORE1 = `<div style="width: ${item.WIDTH}px;height: ${item.HEIGHT}px; transform: rotateZ(0deg) translateZ(${item.LENGTH/2}px);" class="aop before">`;
        const aopAFTER1 = `<div style="width: ${item.WIDTH}px;height: ${item.HEIGHT}px; transform: rotateZ(0deg) translateZ(${-item.LENGTH/2}px);" class="aop after">`;
        let aopROW = '';
        let aopROW2 = '';
        let aopCOLUMN = '';
        let aopCOLUMN2 = '';
        let aopLAYER = '';
        let aopLAYER2 = '';
        if (item.ROW > 1) {
          for (let i = 0; i < item.ROW; i++) {
            const heightItem = item.LENGTH / (item.ROW) * i;
            aopROW += `<div class="linelap" style="bottom: ${heightItem}px;"></div>`;
            aopROW2 += `<div class="linelap2" style="left: ${heightItem}px;"></div>`;
          };
        };
        if (item.COLUMN > 1) {
          for (let i = 1; i < item.COLUMN; i++) {
            const heightItem = item.WIDTH / (item.COLUMN) * i;
            aopCOLUMN += `<div class="linelap" style="bottom: ${heightItem}px;"></div>`;
            aopCOLUMN2 += `<div class="linelap2" style="left: ${heightItem}px;"></div>`;
          };
        };
        if (item.LAYER > 1) {
          for (let i = 1; i < item.LAYER; i++) {
            const heightItem = item.HEIGHT / (item.LAYER) * i;
            aopLAYER += `<div class="linelap" style="bottom: ${heightItem}px;"></div>`;
            aopLAYER2 += `<div class="linelap2" style="left: ${heightItem}px;"></div>`;
          };
        };
        // ------UP
        const aopUP = aopUP1 + aopROW + aopCOLUMN2 + aopCLOSE;
        const aopDOWN = aopDOWN1 + aopROW + aopCOLUMN2 + aopCLOSE;
        const aopLEFT = aopLEFT1 + aopROW2 + aopLAYER + aopCLOSE;
        const aopRIGHT = aopRIGHT1 + aopROW2 + aopLAYER + aopCLOSE;
        const aopBEFORE = aopBEFORE1 + aopCOLUMN2 + aopLAYER + aopCLOSE;
        const aopAFTER = aopAFTER1 + aopCOLUMN2 + aopLAYER + aopCLOSE;
        this.box3D += box + aopUP + aopDOWN + aopLEFT + aopRIGHT + aopBEFORE + aopAFTER + aopCLOSE;
      };
    },
    renderBoxLOSER1() {
      for (let i = 0; i < this.data2.length; i++) {
        const item = this.data2[i];
        console.log(item,'1')
        const lump1 = `<div class="box" style="transform:translateX(${item.WIDTH_POSITION}px) translateY(-${(item.HEIGHT)+item.HEIGHT_POSITION}px) translateZ(${(item.LENGTH/2) + item.LENGTH_POSITION}px)">
                        <div style="top: ${(item.HEIGHT - item.LENGTH) / 2}px;width: ${item.WIDTH}px;height: ${item.LENGTH}px; transform: rotateX(90deg) translateZ(${item.HEIGHT/2}px);" class="aop up" ></div>
                        <div style="top: ${(item.HEIGHT - item.LENGTH) / 2}px;width: ${item.WIDTH}px;height: ${item.LENGTH}px; transform: rotateX(90deg) translateZ(${-item.HEIGHT/2}px);" class="aop down" ></div>
                        <div style="left: ${(item.WIDTH - item.LENGTH) / 2}px;width: ${item.LENGTH}px;height: ${item.HEIGHT}px; transform: rotateY(90deg) translateZ(${-item.WIDTH/2}px);" class="aop left" ></div>
                        <div style="left: ${(item.WIDTH - item.LENGTH) / 2}px;width: ${item.LENGTH}px;height: ${item.HEIGHT}px; transform: rotateY(90deg) translateZ(${item.WIDTH/2}px);" class="aop right"></div>
                        <div style="width: ${item.WIDTH}px;height: ${item.HEIGHT}px; transform: rotateZ(0deg) translateZ(${-item.LENGTH/2}px);" class="aop after"></div>
                        <div style="width: ${item.WIDTH}px;height: ${item.HEIGHT}px; transform: rotateZ(0deg) translateZ(${item.LENGTH/2}px);" class="aop before"></div>
                      `;
        let lumpLayer = '';
        if (item.LAYER > 0) {
          let layerItem = '';
          for (let i = 0; i < item.LAYER; i++) {
            const heightItem = item.HEIGHT / (item.LAYER) * i;
            console.log(item.HEIGHT,'2222')
            layerItem += `<div style="top: ${(item.HEIGHT - item.LENGTH) / 2}px;width: ${item.WIDTH}px;height: ${item.LENGTH}px; transform: rotateX(90deg) translateZ(${-item.HEIGHT / 2 + heightItem}px);" class="aop up aop2" >charu</div>`;
          };
          lumpLayer = layerItem;
          console.log(lumpLayer,'lumpLayer');
        }
        const lumpCharu = lumpLayer;
        const lump2 = '`</div>`';
        const lump = lump1 + lumpCharu + lump2;
        this.box3D += lump;
      };
    },
    copyArr(arr) {
      let res = []
      for (let i = 0; i < arr.length; i++) {
        res.push(arr[i]);
      }
      return res;
    },
    getdata2(num) {
      // this.data2 = [...this.data];
      // for (let item in this.data) {
      //   this.data2[item] = this.data[item];
      // }
      // this.data2 = this.copyArr(this.data);

      this.data2 = JSON.parse(JSON.stringify(this.data));

      for (let i = 0; i < this.data2.length; i++) {
        this.data2[i].LENGTH_POSITION = this.data2[i].LENGTH_POSITION / num;
        this.data2[i].WIDTH_POSITION = this.data2[i].WIDTH_POSITION / num;
        this.data2[i].HEIGHT_POSITION = this.data2[i].HEIGHT_POSITION / num;
        this.data2[i].LENGTH = this.data2[i].LENGTH / num;
        this.data2[i].WIDTH = this.data2[i].WIDTH / num;
        this.data2[i].HEIGHT = this.data2[i].HEIGHT / num;
      };
      console.log(this.data[0].HEIGHT);
    },
  },
  mounted() {
    this.getdata2(this.size);
    this.renderBox();
  },
  watch: {
    size() {
      this.getdata2(this.size);
      this.renderBox();
      console.log('123',this.size)
    },
  },
};
</script>

<style lang="less">
  @mromalwidth: 200px;
  #bigbox{
    margin-left: 800px;
    margin-top: 500px;
    .linelap{
      height: 0px;
      width: 100%;
      border: 1px solid #000;
      position: absolute;
    }
    .linelap2{
      width: 0px;
      height: 100%;
      border: 1px solid #000;
      position: absolute;
    }
  }
  .backW{
    width: 600px;
    height:600px;
    background: blue;
    position: absolute;
    transform: translateZ(-110px) translateY(0px);
  }
  /*.leftW{*/
  /*width: 600px;*/
  /*height:600px;*/
  /*background: blue;*/
  /*position: absolute;*/
  /*transform:rotateX(90deg);*/
  /*}*/
  .box{

    transform-style: preserve-3d;
    position: absolute;

  }
  .box>div{
    position: absolute;
    font-size: 38px;
  }
  .aop{
    border: 1px solid #000;
    background: red;
    position: absolute;
  }
  .aop2{
    border: 2px solid #000;
  }
</style>
