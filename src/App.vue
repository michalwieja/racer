<template>
  <div class="wrapper">
    <h1>racer</h1>
    <div class="game">
      <div class="left"></div>
      <div class="right"></div>
      <div class="car"></div>
      <div class="rival"></div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    const car = document.querySelector(".car");
    const rival = document.querySelector(".rival");

    function moveLeft() {
      let left = car.offsetLeft;
      left -= 100;
      if (left < 0) {
        left = 0;
      }
      car.style.left = left + "px";
    }
    function moveRight() {
      let left = car.offsetLeft;
      left += 100;
      if (left > 200) {
        left = 200;
      }
      car.style.left = left + "px";
    }

    document.addEventListener("keydown", e => {
      if (e.key === "ArrowLeft") {
        moveLeft();
      } else if (e.key === "ArrowRight") {
        moveRight();
      }
    });

    const left = document.querySelector(".left");
    const right = document.querySelector(".right");
    left.addEventListener("touchstart", moveLeft);
    right.addEventListener("touchstart", moveRight);
    rival.addEventListener("animationiteration", () => {
      let random = Math.floor(Math.random() * 3) * 100;

      rival.style.left = random + "px";
    });
    setInterval(() => {
      let carLeft = car.offsetLeft;
      let rivalLeft = rival.offsetLeft;
      let rivalTop = rival.offsetTop;

      if (carLeft === rivalLeft && rivalTop > 300) {
        alert("ok");
      }
    }, 10);
  }
};
</script>



<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.wrapper {
  height: 100vh;
  background: #333;
  color: white;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  h1 {
    margin: 20px;
  }
}
.game {
  height: 600px;
  width: 300px;
  border: 1px solid white;
  position: relative;
  overflow: hidden;
}
.left,
.right {
  width: 50%;
  position: absolute;
  height: 100%;
}
.right {
  left: 50%;
}
.car {
  position: absolute;
  width: 100px;
  height: 150px;
  background-color: #fff;
  bottom: 0;
  left: 100px;
}

.rival {
  position: absolute;
  width: 100px;
  height: 150px;
  background-color: #fab;
  top: 0;
  left: 0px;
  animation: rivalMove 1s infinite linear;
}

@keyframes rivalMove {
  from {
    top: 0;
  }
  to {
    top: 600px;
  }
}
</style>


