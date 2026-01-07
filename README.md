<div id="road">
  <div id="car"></div>
  <div class="enemy"></div>
  <div class="enemy"></div>
</div>
.enemy {
  width: 50px;
  height: 90px;
  background: black;
  position: absolute;
  top: -120px;
  border-radius: 8px;
}
const enemies = document.querySelectorAll(".enemy");

enemies.forEach(e => resetEnemy(e));

function resetEnemy(enemy) {
  enemy.style.top = "-120px";
  enemy.style.left = Math.floor(Math.random() * 250) + "px";
}

function checkCollision(enemy) {
  return (
    enemy.offsetTop + 90 > 400 &&
    enemy.offsetLeft < left + 50 &&
    enemy.offsetLeft + 50 > left
  );
}
enemies.forEach(enemy => {
  enemy.style.top = enemy.offsetTop + speed + "px";

  if (checkCollision(enemy)) {
    alert("💥 Crash!");
    location.reload();
  }

  if (enemy.offsetTop > 500) resetEnemy(enemy);
});
.drift-left {
  transform: rotate(-8deg);
}
.drift-right {
  transform: rotate(8deg);
}
document.addEventListener("keydown", e => {
  if (e.key === "ArrowLeft") {
    left -= 20;
    car.className = "drift-left";
  }
  if (e.key === "ArrowRight") {
    left += 20;
    car.className = "drift-right";
  }
});

document.addEventListener("keyup", () => {
  car.className = "";
});
<div id="nitro">
  <div id="nitro-fill"></div>
</div>
#nitro {
  width: 200px;
  height: 10px;
  border: 1px solid white;
  margin: auto;
}
#nitro-fill {
  height: 100%;
  width: 100%;
  background: cyan;
}
let nitro = 100;
const nitroFill = document.getElementById("nitro-fill");

document.addEventListener("keydown", e => {
  if (e.code === "Space" && nitro > 0) {
    speed = 10;
    nitro--;
  }
});

document.addEventListener("keyup", e => {
  if (e.code === "Space") speed = 5;
});

function updateNitro() {
  nitroFill.style.width = nitro + "%";
  if (nitro < 100) nitro += 0.2;
}
updateNitro();
