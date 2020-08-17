<template>
  <div class="screen" @mousedown="startDrag" @mousemove="doDrag">
    <div class="row" v-for="(ix, x) in xx" :key="ix">
      <div class="box" v-for="(iy, y) in yy" :key="iy">
        {{`${x},${y}`}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted () {
    window.addEventListener('mouseup', this.stopDrag);
  },
  data () {
    return {
      xx: 10,
      yy: 10,
      dragging: false,
      x: 'no',
      y: 'no',
      startPoint: {x: 0, y: 0},
      endPoint: {x: 0, y: 0}
    }
  },
  methods: {
    startDrag(e) {
      let [x, y] = e.path[0].innerHTML.trim().split(',')
      console.log('start: ', x, y)
      this.startPoint = {x, y},
      this.dragging = true;
      this.x = this.y = 0;
    },
    stopDrag(e) {
      let [x, y] = e.path[0].innerHTML.trim().split(',')
      console.log('end: ', x, y)
      this.endPoint = {x, y}
      this.dragging = false;
      this.x = this.y = 'no';
    },
    doDrag(event) {
      let classList = event.path[0].classList
      if (this.dragging) {
        if (!['hover'].includes(classList)){
          classList.toggle('hover')
        }
        console.log('doDrag')
        console.log(classList)
        this.x = event.clientX;
        this.y = event.clientY;
      }
    }
  },
  props: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
  user-select: none;  
  box-sizing: border-box;
}
.screen {
  width: 500px;
  height: 500px;
  background-color: #f1f1f1
}
.row {
  height: 50px;
}
.box {
  color: transparent;
  width: 50px;
  height: 50px;
  display: inline-block;
  border: 1px solid #000;
}
.hover {
  background-color: red;
}
</style>
