<!Hunter game>
<html>
<head>
<meta charset="UTF-8">
<title>Hunter Game</title>

<style>
body{
margin:0;
overflow:hidden;
background:#87CEEB;
font-family:Arial;
}

canvas{
display:block;
margin:auto;
background:#87CEEB;
}

#info{
position:fixed;
top:10px;
left:10px;
color:white;
font-size:20px;
font-weight:bold;
}

.controls{
position:fixed;
bottom:20px;
width:100%;
display:flex;
justify-content:space-between;
padding:0 40px;
}

button{
width:70px;
height:70px;
font-size:30px;
border:none;
border-radius:50%;
background:white;
}
</style>
</head>

<body>

<div id="info">Map:1 Score:0</div>

<canvas id="game" width="900" height="400"></canvas>

<div class="controls">
<div>
<button id="left">◀</button>
<button id="right">▶</button>
</div>
<button id="jump">⬆</button>
</div>

<script>

const canvas=document.getElementById("game");
const ctx=canvas.getContext("2d");

let gravity=0.6;
let map=1;
let score=0;
let camera=0;

let player={
x:100,
y:300,
w:40,
h:40,
dy:0,
jump:false
};

let coins=[];
let spikes=[];
let pipes=[];
let plants=[];
let enemies=[];
let blocks=[];

let flag={x:1500,y:260};

function loadMap(){

coins=[];
spikes=[];
pipes=[];
plants=[];
enemies=[];
blocks=[];

let base=map*200;

coins=[
{x:400+base,y:280},
{x:450+base,y:280},
{x:500+base,y:260}
];

spikes=[
{x:600+base,y:330},
{x:640+base,y:330}
];

pipes=[
{x:700+base,y:300}
];

plants=[
{x:720+base,y:270}
];

enemies=[
{x:900+base,y:300,dir:1}
];

blocks=[
{x:550+base,y:250,hit:false}
];

player.x=100;

}

loadMap();

let left=false;
let right=false;

function drawPlayer(){
ctx.fillStyle="red";
ctx.fillRect(player.x-camera,player.y,player.w,player.h);
}

function drawGround(){
ctx.fillStyle="#8B4513";
ctx.fillRect(0,340,900,60);
}

function drawCoins(){
ctx.fillStyle="gold";

coins.forEach((c,i)=>{

ctx.beginPath();
ctx.arc(c.x-camera,c.y,10,0,Math.PI*2);
ctx.fill();

if(Math.abs(player.x-c.x)<25 && Math.abs(player.y-c.y)<25){
coins.splice(i,1);
score+=10;
}

});
}

function drawSpikes(){

ctx.fillStyle="silver";

spikes.forEach(s=>{

ctx.beginPath();
ctx.moveTo(s.x-camera,340);
ctx.lineTo(s.x+20-camera,320);
ctx.lineTo(s.x+40-camera,340);
ctx.fill();

if(player.x>s.x-20 && player.x<s.x+40 && player.y>300){
gameOver();
}

});
}

function drawPipes(){
ctx.fillStyle="green";

pipes.forEach(p=>{
ctx.fillRect(p.x-camera,300,60,40);
});
}

function drawPlants(){

ctx.fillStyle="purple";

plants.forEach(pl=>{

ctx.fillRect(pl.x-camera,270,30,30);

if(player.x<
