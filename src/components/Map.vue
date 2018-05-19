<template>
  <div id="map_component">
    <canvas id="map" width="640" height="480">
    </canvas>
    <div class="data">{{this.player}}</div>
  </div>
</template>

<script>
export default {
  name: 'Map',
  data () {
    return {
      player: {},
      map: {},
    }
  },
  mounted () {
    var canvas = document.getElementById("map");
    var context = canvas.getContext("2d");
    this.initMap(canvas,context)
    this.map.generate()
    this.renderMap()
    this.initPlayer()
    this.player.update()
  },
  methods: {
    initMap: function (canvas, context) {
      this.map = {
        canvas: canvas,
        context: context,
        generate: function() {
          var mapArray = new Array(32)
          for (var i = 0; i < 32; i++) {
            mapArray[i] = new Array(24)
          }
          for (i = 0; i < 32; i++) {
            for (var j = 0; j < 24; j++) {
              mapArray[i][j] = Math.floor(Math.random() * 2)
            }
          }
          return mapArray
        },
        mapArray: generate(),
      }
    },
    renderMap: function(){
      var canvas = document.getElementById('map')
      var context = canvas.getContext('2d')
      for (var i = 0; i<32; i++){
        for (var j = 0; j<24; j++){
          if (this.mapArray[i][j]){
              context.fillStyle = "blue";
              context.fillRect(i*20, j*20, 20, 20);
          }
          else{
              context.fillStyle = "black";
              context.fillRect(i*20, j*20, 20, 20);
          }
        }
      }
    },
    updateMap: function() {
    },
    initPlayer: function(){
      this.player = {
        width: 20,
        height: 20,
        color: "red",
        speed: {
          x: 0,
          y: 0
        },
        position: {
          x:0,
          y:0
        },
        aPos: {
          x:0,
          y:0
        },
        update: function() {
          map.context.fillStyle = this.color;
          ctx.fillRect(this.x, this.y, this.width, this.height);
        }
      }
    },
    renderPlayer: function(){

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
