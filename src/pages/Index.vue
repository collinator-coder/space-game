<template>
  <q-page class="flex flex-center" id="space" :style="styleObject">
    <img :style="rotated" class="spaceShip" src="~assets/ship_01.svg">
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data: function() {
    return {
      rotation: 0,
      direction: 1,
      velocity: 0.5,
      styleObject: {
        backgroundPosition: 0
      }
    };
  },
  computed: {
    rotated() {
      return { transform: "rotate(" + this.rotation + "deg)" };
    }
  },
  methods: {
    rotateMore: function() {
      this.rotation += this.direction * this.velocity;
      if (this.rotation >= 360) {
        this.rotation = 0;
      }
      if (this.rotation < 0) {
        this.rotation = 360;
      }
      this.styleObject.backgroundPosition += 50;
    },
    rotateLeft: function() {
      this.direction = -1;
    },
    rotateRight: function() {
      this.direction = 1;
    },
    setInterval: function() {
      window.setInterval(() => {
        this.rotateMore();
      }, 10);
    },
    increaseSpeed: function() {
      this.velocity += 0.5;
    },
    decreaseSpeed: function() {
      this.velocity -= 0.5;
    },
    shoot: function() {
      console.log("Fire!");
    }
  },
  mounted() {
    this.setInterval();
    document.addEventListener('keydown', (event) => {
      switch(event.keyCode) {
        case 37:
          this.rotateLeft();
          break;;
        case 39:
          this.rotateRight();
          break;;
        case 38:
          this.increaseSpeed();
          break;;
        case 40:
          this.decreaseSpeed();
          break;;
        case 32:
          this.shoot();
          break;;
        default:
          break;;
      }
    }, false);
  }
};
</script>
<style scoped>
.spaceShip {
  width: 200px;
  height: auto;
}

#space {
  background-color: black;
    background-image:
    radial-gradient(2px 2px at 20px 30px, #eee, rgba(0,0,0,0)),
    radial-gradient(2px 2px at 40px 70px, #fff, rgba(0,0,0,0)),
    radial-gradient(2px 2px at 50px 160px, #ddd, rgba(0,0,0,0)),
    radial-gradient(2px 2px at 90px 40px, #fff, rgba(0,0,0,0)),
    radial-gradient(2px 2px at 130px 80px, #fff, rgba(0,0,0,0)),
    radial-gradient(2px 2px at 160px 120px, #ddd, rgba(0,0,0,0));
  /* opacity: 0; */
  background-repeat: repeat;
  background-size: 200px 200px;
}
</style>
