<!Xin Chào>
<html>
<head>
<meta charset="UTF-8">
<title>Number Game2D</title>

<style>
body{
margin:0;
background:black;
overflow:hidden;
}

canvas{
display:block;
margin:auto;
background:#111;
}

.controls{
position:fixed;
bottom:20px;
width:100%;
display:flex;
justify-content:space-between;
padding:0 40px;
}

.btn{
width:70px;
height:70px;
background:white;
color:black;
font-size:35px;
border-radius:50%;
display:flex;
align-items:center;
justify-content:center;
user-select:none;
}

</style>
</head>

<body>

<canvas id="game" width="400" height="600"></canvas>

<div class="controls">
<div class="btn" id="left">⬅</div>
<div class="btn" id="right">➡</div>
</div>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let player={
x:200,
y:520,
speed:6
};

let obstacles=[];
let score=0;

let moveLeft=false;
let moveRight=false;

document.getElementById("left").ontouchstart=()=>moveLeft=true;
document.getElementById("left").ontouchend=()=>moveLeft=false;

document.getElementById("right").ontouchstart=()=>moveRight=true;
document.getElementById("right").ontouchend=()=>moveRight=false;

function spawnObstacle(){

obstacles.push({
x:Math.random()*360,
y:-20,
size:20,
speed:3
});

}

setInterval(spawnObstacle,1000);

function drawCat(x,y){

ctx.fillStyle="gray";

ctx.beginPath();
ctx.arc(x,y,20,0,Math.PI*2);
ctx.fill();

ctx.fillStyle="black";

ctx.beginPath();
ctx.arc(x-7,y-5,3,0,Math.PI*2);
ctx.arc(x+7,y-5,3,0,Math.PI*2);
ctx.fill();

ctx.fillStyle="pink";

ctx.beginPath();
ctx.arc(x,y+4,3,0,Math.PI);
ctx.fill();

}

function update(){

ctx.clearRect(0,0,400,600);

if(moveLeft) player.x-=player.speed;
if(moveRight) player.x+=player.speed;

drawCat(player.x,player.y);

ctx.fillStyle="red";

for(let i=0;i<obstacles.length;i++){

let o=obstacles[i];

o.y+=o.speed;

ctx.fillRect(o.x,o.y,o.size,o.size);

if(
o.x < player.x+20 &&
o.x+o.size > player.x-20 &&
o.y < player.y+20 &&
o.y+o.size > player.y-20
){

alert("Game Over\nScore: "+score);
location.reload();

}

if(o.y>600){

score++;
obstacles.splice(i,1);

}

}

ctx.fillStyle="white";
ctx.font="20px Arial";
ctx.fillText("Score: "+score,10,30);

requestAnimationFrame(update);

}

update();

</script>

</body>
</html>
