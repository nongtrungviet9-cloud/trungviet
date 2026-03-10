<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>BirdyBird</title>

<style>

body{
margin:0;
overflow:hidden;
background:#70c5ce;
}

canvas{
display:block;
margin:auto;
background:#70c5ce;
}

#score{
position:absolute;
top:20px;
left:20px;
font-size:25px;
color:white;
font-weight:bold;
}

</style>

</head>

<body>

<div id="score">Score: 0</div>

<canvas id="game" width="400" height="600"></canvas>

<script>

const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let score = 0;

const birdImg = new Image();
birdImg.src = "bird.png"; // sprite sheet

let frame = 0;

let bird = {
x:80,
y:200,
width:60,
height:60,
gravity:0.5,
velocity:0,
lift:-8
};

let pipes = [];

function createPipe(){

let gap = 150;
let top = Math.random()*250 + 50;

pipes.push({
x:400,
top:top,
bottom:top+gap,
width:60
});

}

function drawBird(){

ctx.drawImage(
birdImg,
frame*60,
0,
60,
60,
bird.x,
bird.y,
60,
60
);

frame++;

if(frame>2){
frame=0;
}

}

function drawPipes(){

ctx.fillStyle="green";

for(let i=0;i<pipes.length;i++){

let p = pipes[i];

ctx.fillRect(p.x,0,p.width,p.top);
ctx.fillRect(p.x,p.bottom,p.width,600);

p.x -= 3;

if(p.x+p.width<0){

pipes.splice(i,1);
score++;

document.getElementById("score").innerText="Score: "+score;

}

if(
bird.x+bird.width > p.x &&
bird.x < p.x+p.width &&
(bird.y < p.top || bird.y+bird.height > p.bottom)
){
gameOver();
}

}

}

function update(){

bird.velocity += bird.gravity;
bird.y += bird.velocity;

if(bird.y>600){
gameOver();
}

}

function gameLoop(){

ctx.clearRect(0,0,400,600);

drawBird();
drawPipes();
update();

requestAnimationFrame(gameLoop);

}

function gameOver(){

alert("Game Over\nScore: "+score);
location.reload();

}

setInterval(createPipe,2000);

canvas.addEventListener("click",()=>{

bird.velocity = bird.lift;

});

gameLoop();

</script>

</body>
</html> 
