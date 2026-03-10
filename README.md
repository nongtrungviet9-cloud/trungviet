<!Hunter Game>
<html>
<head>
<meta charset="UTF-8">
<title>BirdyBird Game</title>

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

<div id="score">Score: 0</div>
<div id="startText">TAP TO START</div>

<canvas id="game" width="400" height="600"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let birdImg = new Image();
birdImg.src = "bird.png";   // ảnh con chim

let bird = {
x:80,
y:200,
width:50,
height:50,
gravity:0.5,
lift:-8,
velocity:0
};

let pipes = [];
let score = 0;
let gameStart = false;

function drawBird(){
ctx.drawImage(birdImg,bird.x,bird.y,bird.width,bird.height);
}

function createPipe(){
let gap = 150;
let top = Math.random()*250+50;

pipes.push({
x:400,
top:top,
bottom:top+gap,
width:50
});
}

function drawPipes(){

ctx.fillStyle="green";

for(let i=0;i<pipes.length;i++){

let p = pipes[i];

ctx.fillRect
