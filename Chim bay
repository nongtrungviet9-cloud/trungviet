<!Xin Chào >
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

let bird = {
x:80,
y:200,
size:20,
gravity:0.5,
lift:-8,
velocity:0
};

let pipes = [];
let score = 0;
let gameStart = false;

function drawBird(){
ctx.fillStyle="yellow";
ctx.beginPath();
ctx.arc(bird.x,bird.y,bird.size,0,Math.PI*2);
ctx.fill();
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

ctx.fillRect(p.x,0,p.width,p.top);
ctx.fillRect(p.x,p.bottom,p.width,600);

p.x -= 2;

if(p.x + p.width < 0){
pipes.splice(i,1);
score++;
document.getElementById("score").innerText="Score: "+score;
}

if(
bird.x + bird.size > p.x &&
bird.x - bird.size < p.x + p.width &&
(bird.y - bird.size < p.top || bird.y + bird.size > p.bottom)
){
gameOver();
}

}
}

function updateBird(){
bird.velocity += bird.gravity;
bird.y += bird.velocity;

if(bird.y > canvas.height || bird.y < 0){
gameOver();
}
}

function gameLoop(){

ctx.clearRect(0,0,400,600);

drawBird();
drawPipes();

if(gameStart){
updateBird();
}

requestAnimationFrame(gameLoop);
}

function gameOver(){
alert("Game Over! Score: "+score);
location.reload();
}

setInterval(()=>{
if(gameStart){
createPipe();
}
},2000);

canvas.addEventListener("click",()=>{

if(!gameStart){
gameStart=true;
document.getElementById("startText").style.display="none";
}

bird.velocity = bird.lift;

});

gameLoop();

</script>

</body>
</html>
