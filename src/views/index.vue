<template>
  <div class="index">
    <div class="block" style="width:400px">
      <span class="demonstration">视角x</span>
      <el-slider v-model="view.x" :max="180" :min="-180"></el-slider>
    </div>
    <div class="block" style="width:400px">
      <span class="demonstration">视角y</span>
      <el-slider v-model="view.y" :max="180" :min="-180"></el-slider>
    </div>
    <div class="block" style="width:400px">
      <span class="demonstration">视角z</span>
      <el-slider v-model="view.z" :max="180" :min="-180"></el-slider>
    </div>
    <div class="block" style="width:400px">
      <span class="demonstration">视距</span>
      <el-slider v-model="size" :step="0.1" :max="2" :min="0.5"></el-slider>
    </div>
    <plugin3D :data="data" :size="size" :view="view" :step="step"></plugin3D>
  </div>
</template>

<script>
import plugin3D from './Home';
export default {
  name: 'index',
  components: {
    plugin3D,
  },
  data () {
    return {
      data: [
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
      size: 1,
      view: {
        x: -8,
        y: -28,
        z: 3,
      },
      step: 0,
      maxstep: 0,
    };
  },
  mounted() {
    this.maxstep = this.data.length + 1;
  },
};
</script>

<style>

</style>
