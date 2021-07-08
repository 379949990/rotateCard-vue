<template>
  <div id="ROTATE-CARD-Box-BKBHKNASDUHWQBHKLDKA" :style="scssValues" ref="rotateCardBox">
    <div class="rotate-card-content" :class="['']" @click="handleCardRotate" @mouseleave="handleCardRotate">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "RotateCard",
  data() {
    return {
      rotateAble: true,
      scssValues: {
        "--width": "",
        "--height": "",
        "--rotate": "",
      },
    };
  },
  props: {
    rotate: {
      type: String,
      default: "Y",
    },
  },
  computed: {
    randomString() {
      const abcLib = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
      let randomString = "";
      for (let i = 0; i < 8; i++) {
        console.log("i", i);
        randomString += abcLib[Math.round(Math.random() * abcLib.length)];
      }
      return randomString;
    },
  },
  mounted() {
    this.setClassName();
    this.setStyle();
  },
  methods: {
    setClassName() {
      const frontItems = document.getElementsByTagName("rotate-item-front");
      const backItems = document.getElementsByTagName("rotate-item-back");
      if (frontItems.length === 0 || frontItems.length > 1) console.error('rotateCard ERROR: 请设置一个"<rotate-item-front></rotate-item-front>"元素');
      if (backItems.length === 0 || backItems.length > 1) console.error('rotateCard ERROR: 请设置一个"<rotate-item-back></rotate-item-back>"元素');
      frontItems[0].className += "front-side";
      backItems[0].className += "back-side";
      console.log("frontItem", frontItems, backItems);
    },
    setStyle() {
      this.scssValues["--width"] = this.$refs.rotateCardBox.parentElement.offsetWidth + "px";
      this.scssValues["--height"] = this.$refs.rotateCardBox.parentElement.offsetHeight + "px";
      this.scssValues["--rotate"] = this.rotate === "x" || this.rotate === "X" ? "rotateX(180deg)" : "rotateY(180deg)";
      console.log("scssValues", this.scssValues);
    },
    handleCardRotate($event) {
      console.log("$event", this.rotateAble, $event);
      if ($event.type === "click" && this.rotateAble) {
        this.rotateAble = false;
        $event.currentTarget.className = $event.currentTarget.className.indexOf("flipped") > -1 ? "rotate-card-content" : "rotate-card-content flipped";
        setTimeout(() => {
          this.rotateAble = true;
        }, 1000);
      } else if ($event.type === "mouseleave" && this.rotateAble) {
        $event.currentTarget.className = " rotate-card-content";
      }
    },
  },
};
</script>

<style lang="scss" scoped>
#ROTATE-CARD-Box-BKBHKNASDUHWQBHKLDKA {
  $width: var(--width);
  $height: var(--height);
  $rotate: var(--rotate);

  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-size: 13px;
    color: #07070770;
  }
  width: $width;
  height: $height;
  position: relative;
  perspective: 1000px;
  .rotate-card-content {
    width: $width;
    height: $height;
    position: absolute;
    transform-style: preserve-3d;
    transition: transform 1s;
    .front-side,
    .back-side {
      display: block;
      position: absolute;
      width: $width;
      height: $height;
      backface-visibility: hidden;
      border-radius: calc((var(--width) + var(--height)) * 0.02);
      padding: calc((var(--width) + var(--height)) * 0.03);
    }
    .front-side {
      overflow: hidden;
      background: rgb(240, 240, 240);
    }
    .back-side {
      transform: $rotate;
      background-color: #bbbbbb;
    }
  }
  .flipped {
    transform: $rotate;
  }
}
</style>
