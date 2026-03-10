<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Raven Bird Game</title>

<style>
body{
margin:0;
background:#70c5ce;
overflow:hidden;
font-family:Arial;
text-align:center;
}

canvas{
display:block;
margin:auto;
background:#70c5ce;
}

#startText{
position:absolute;
top:40%;
width:100%;
font-size:30px;
color:white;
font-weight:bold;
}

#score{
position:absolute;
top:20px;
left:20px;
font-size:25px;
color:white;
}
</style>
</head>

<body>

<div id="startText">Bắt Đầu</div>
<div id="score">0</div>

<canvas id="game" width="400" height="600"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let gameStart=false;
let score=0;

let bird={
x:80,
y:200,
width:60,
height:45,
gravity:0.6,
lift:-10,
velocity:0
};

const birdImg=new Image();
birdImg.src="raven.png";

let pipes=[];
let pipeWidth=70;
let gap=170;

document.addEventListener("click",jump);

function jump(){

if(!gameStart){
gameStart=true;
document.getElementById("startText").style.display="none";
}

bird.velocity=bird.lift;

}

function createPipe(){

let topHeight=Math.random()*300+50;

pipes.push({
x:canvas.width,
top:topHeight,
bottom:canvas.height-topHeight-gap
});

}

setInterval(createPipe,2000);

function update(){

ctx.clearRect(0,0,canvas.width,canvas.height);

if(gameStart){

bird.velocity+=bird.gravity;
bird.y+=bird.velocity;

}

ctx.drawImage(birdImg,bird.x,bird.y,bird.width,bird.height);

pipes.forEach(pipe=>{

pipe.x-=3;

ctx.fillStyle="green";

ctx.fillRect(pipe.x,0,pipeWidth,pipe.top);

ctx.fillRect(pipe.x,canvas.height-pipe.bottom,pipeWidth,pipe.bottom);

if(
bird.x < pipe.x + pipeWidth &&
bird.x + bird.width > pipe.x &&
(bird.y < pipe.top || bird.y + bird.height > canvas.height - pipe.bottom)
){
resetGame();
}

if(pipe.x+pipeWidth==bird.x){

score++;
document.getElementById("score").innerText=score;

}

});

requestAnimationFrame(update);

}

function resetGame(){

pipes=[];
bird.y=200;
bird.velocity=0;
score=0;
gameStart=false;
document.getElementById("score").innerText=score;
document.getElementById("startText").style.display="block";

}

update();

</script>

</body>
</html>
