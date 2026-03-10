<!Xin Chào>
<html>
<head>
<meta charset="UTF-8">
<title>Hunter Game</title>

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

#high{
position:absolute;
top:50px;
left:20px;
font-size:20px;
color:white;
}
</style>
</head>

<body>

<div id="score">Score: 0</div>
<div id="high">High: 0</div>
<div id="startText">Bắt Đầu</div>

<canvas id="game" width="400" height="600"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let birdImg = new Image();
birdImg.src = "raven.png";

let coinImg = new Image();
coinImg.src = "coin.png";

let coinSound = new Audio("coin.wav");
let jumpSound = new Audio("jump.wav");

let bird={
x:80,
y:200,
width:70,
height:70,
gravity:0.5,
lift:-8,
velocity:0
};

let pipes=[];
let coins=[];
let score=0;
let highScore=localStorage.getItem("high") || 0;

document.getElementById("high").innerText="High: "+highScore;

let gameStart=false;

function drawBird(){
ctx.drawImage(birdImg,bird.x,bird.y,bird.width,bird.height);
}

function createPipe(){

let gap=150;
let top=Math.random()*250+50;

pipes.push({
x:400,
top:top,
bottom:top+gap,
width:60
});

coins.push({
x:430,
y:top+gap/2,
size:40,
taken:false
});
}

function drawPipes(){

ctx.fillStyle="green";

for(let i=0;i<pipes.length;i++){

let p=pipes[i];

ctx.fillRect(p.x,0,p.width,p.top);
ctx.fillRect(p.x,p.bottom,p.width,600);

p.x-=2;

if(
bird.x < p.x+p.width &&
bird.x+bird.width > p.x &&
(bird.y<p.top || bird.y+bird.height>p.bottom)
){

gameStart=false;

if(score>highScore){
highScore=score;
localStorage.setItem("high",highScore);
}

document.getElementById("startText").innerText="GAME OVER - TAP";
document.getElementById("startText").style.display="block";
}

}

pipes=pipes.filter(p=>p.x>-60);
}

function drawCoins(){

for(let i=0;i<coins.length;i++){

let c=coins[i];

c.x-=2;

if(!c.taken){
ctx.drawImage(coinImg,c.x,c.y,c.size,c.size);
}

if(
bird.x<c.x+c.size &&
bird.x+bird.width>c.x &&
bird.y<c.y+c.size &&
bird.y+bird.height>c.y &&
!c.taken
){
score+=5;
coinSound.play();
c.taken=true;
document.getElementById("score").innerText="Score: "+score;
}

}

coins=coins.filter(c=>c.x>-20);
}

function updateBird(){

bird.velocity+=bird.gravity;
bird.y+=bird.velocity;

if(bird.y+bird.height>canvas.height){
bird.y=canvas.height-bird.height;
bird.velocity=0;
}

}

function gameLoop(){

ctx.clearRect(0,0,canvas.width,canvas.height);

drawBird();

if(gameStart){
updateBird();
drawPipes();
drawCoins();
}

requestAnimationFrame(gameLoop);
}

setInterval(()=>{
if(gameStart){
createPipe();
}
},2000);

document.addEventListener("click",()=>{

if(!gameStart){

pipes=[];
coins=[];
score=0;

bird.y=200;
bird.velocity=0;

document.getElementById("score").innerText="Score: 0";
document.getElementById("startText").style.display="none";

gameStart=true;

}

bird.velocity=bird.lift;
jumpSound.play();

});

gameLoop();

</script>

</body>
</html>
