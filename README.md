<!DOCTYPE html><html>
<head>
<meta charset="UTF-8">
<title>Cat Dodge Game</title><style>
body{
margin:0;
background:linear-gradient(#4facfe,#00f2fe);
font-family:Arial;
text-align:center;
overflow:hidden;
}

h1{
color:white;
}

canvas{
background:white;
border-radius:20px;
box-shadow:0 10px 30px rgba(0,0,0,0.3);
display:block;
margin:auto;
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
border-radius:50%;
border:none;
font-size:28px;
background:white;
box-shadow:0 5px 10px rgba(0,0,0,0.3);
}

button:active{
transform:scale(0.9);
}

#menu{
position:absolute;
top:40%;
left:50%;
transform:translate(-50%,-50%);
background:white;
padding:30px;
border-radius:20px;
box-shadow:0 10px 20px rgba(0,0,0,0.3);
}

#menu button{
width:120px;
height:50px;
border-radius:10px;
font-size:18px;
}

#score{
position:absolute;
top:10px;
left:10px;
background:rgba(0,0,0,0.5);
color:white;
padding:10px;
border-radius:10px;
}
</style></head><body><h1>🐱 Cat Dodge</h1><div id="menu">
<h2>Start Game</h2>
<button onclick="startGame()">PLAY</button>
</div><div id="score">
Score: <span id="s">0</span><br>
Level: <span id="l">1</span><br>
High: <span id="h">0</span>
</div><canvas id="game" width="400" height="500"></canvas>

<div class="controls">
<button onclick="left()">⬅️</button>
<button onclick="right()">➡️</button>
</div><script>

let canvas=document.getElementById("game");
let ctx=canvas.getContext("2d");

let running=false;

let player={x:200,y:450};

let score=0;
let level=1;

let highScore=localStorage.getItem("highscore")||0;

let enemies=[];
let diamonds=[];
let golds=[];

document.getElementById("h").innerText=highScore;

function startGame(){
document.getElementById("menu").style.display="none";
running=true;
}

function left(){
player.x-=30;
if(player.x<20) player.x=20;
}

function right(){
player.x+=30;
if(player.x>380) player.x=380;
}

function drawPlayer(){
ctx.fillStyle="gray";

ctx.beginPath();
ctx.arc(player.x,player.y,20,0,Math.PI*2);
ctx.fill();

ctx.fillStyle="black";

ctx.beginPath();
ctx.arc(player.x-6,player.y-5,3,0,Math.PI*2);
ctx.arc(player.x+6,player.y-5,3,0,Math.PI*2);
ctx.fill();
}

function drawEnemy(x,y){
ctx.fillStyle="red";
ctx.fillRect(x,y,20,20);
}

function drawDiamond(x,y){

ctx.shadowColor="#00e5ff";
ctx.shadowBlur=15;

ctx.fillStyle="#00e5ff";

ctx.beginPath();
ctx.moveTo(x+10,y);
ctx.lineTo(x+20,y+10);
ctx.lineTo(x+10,y+20);
ctx.lineTo(x,y+10);
ctx.closePath();
ctx.fill();

ctx.shadowBlur=0;
}

function drawGold(x,y){
ctx.fillStyle="gold";

ctx.beginPath();
ctx.arc(x+10,y+10,10,0,Math.PI*2);
ctx.fill();
}

function update(){

if(!running) return;

ctx.clearRect(0,0,400,500);

drawPlayer();

if(Math.random()<0.03){
enemies.push({x:Math.random()*380,y:0});
}

if(Math.random()<0.02){
diamonds.push({x:Math.random()*380,y:0});
}

if(Math.random()<0.015){
golds.push({x:Math.random()*380,y:0});
}

for(let i=0;i<enemies.length;i++){

let e=enemies[i];

e.y+=2+level;

drawEnemy(e.x,e.y);

if(player.x<e.x+20 &&
player.x+40>e.x &&
player.y<e.y+20 &&
player.y+40>e.y){

if(score>highScore){
localStorage.setItem("highscore",score);
}

alert("Game Over\nScore: "+score);
location.reload();
}
}

for(let i=0;i<diamonds.length;i++){

let d=diamonds[i];
d.y+=2;

drawDiamond(d.x,d.y);

if(player.x<d.x+20 &&
player.x+40>d.x &&
player.y<d.y+20 &&
player.y+40>d.y){

score+=5;
diamonds.splice(i,1);
}
}

for(let i=0;i<golds.length;i++){

let g=golds[i];
g.y+=2;

drawGold(g.x,g.y);

if(player.x<g.x+20 &&
player.x+40>g.x &&
player.y<g.y+20 &&
player.y+40>g.y){

score+=10;
golds.splice(i,1);
}
}

if(score>20) level=2;
if(score>50) level=3;
if(score>100) level=4;

document.getElementById("s").innerText=score;
document.getElementById("l").innerText=level;

}

setInterval(update,30);

</script></body>
</html> 
