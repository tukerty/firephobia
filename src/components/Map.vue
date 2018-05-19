<template>
<div id="map_component">
    <canvas id="map" width="640" height="480">
    </canvas>
    <div class="data">{{this.player}}</div>
    <button @click="movePlayer(1)">top</button>
    <button @click="movePlayer(2)">top-right</button>
    <button @click="movePlayer(5)">right</button>
    <button @click="movePlayer(7)">bot</button>
    <button @click="movePlayer(3)">left</button>
  </div>
</template>

<script>
export default {
  name: 'Map',
  data () {
    return {
      mapArray: new Array(32),
      player: {
        width: 20,
        height: 20,
        color: 'red',
        isWalk: false,
        speed: {
          x: 0,
          y: 0
        },
        position: {
          x: 0,
          y: 0
        },
        aPos: {
          x: 0,
          y: 0
        }
      }
    }
  },
  mounted () {
    this.initMap()
    this.generateMap()
    this.renderMap()
    this.renderPlayer()
  },
  methods: {
    /**
     * Initializes map with canvas DOM element and starts update with 20ms interval
     * @returns {void}
     */
    initMap: function () {
      this.canvas = document.getElementById('map')
      this.context = this.canvas.getContext('2d')
      this.interval = setInterval(this.updateMap, 20)
    },
    generateMap: function () {
      for (var i = 0; i < 32; i++) {
        this.mapArray[i] = new Array(24)
      }
      for (i = 0; i < 32; i++) {
        for (var j = 0; j < 24; j++) {
          this.mapArray[i][j] = Math.floor(Math.random() * 2)
        }
      }
    },
    renderMap: function () {
      for (var i = 0; i < 32; i++) {
        for (var j = 0; j < 24; j++) {
          if (this.mapArray[i][j]) {
            this.context.fillStyle = 'blue'
            this.context.fillRect(i * 20, j * 20, 20, 20)
          } else {
            this.context.fillStyle = 'black'
            this.context.fillRect(i * 20, j * 20, 20, 20)
          }
        }
      }
    },
    clearMap: function () {
      this.context.clearRect(0, 0, this.canvas.width, this.canvas.height)
    },
    updateMap: function () {
      this.clearMap()
      this.renderMap()
      this.updatePlayer()
      this.renderPlayer()
    },
    renderPlayer: function () {
      this.context.fillStyle = this.player.color
      this.context.fillRect(this.player.position.x, this.player.position.y, this.player.width, this.player.height)
    },
    movePlayer: function (direction) {
      if (!this.player.isWalk) {
        this.player.isWalk = true
        var n = direction.toString(3)
        if (n.length === 1) { n = '0' + n }
        this.player.speed.y = (n[0] - 1)
        this.player.speed.x = (n[1] - 1)
      }
    },
    updatePlayer: function () {
      this.player.position.x += this.player.speed.x
      this.player.position.y += this.player.speed.y

      if ((Math.abs(this.player.aPos.x - this.player.position.x) === 20) || (Math.abs(this.player.aPos.y - this.player.position.y) === 20)) {
        this.player.isWalk = false
        this.movePlayer(4)
        console.log(this.player.isWalk)
        this.player.aPos.x = this.player.position.x
        this.player.aPos.y = this.player.position.y
        this.player.isWalk = false
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
