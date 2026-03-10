<!PAKOUR 3D>
<html>
<head>
<meta charset="UTF-8">
<title>Parkour 3D Full</title>

<style>
body{margin:0;overflow:hidden}

#jump{
position:absolute;
bottom:40px;
right:40px;
width:90px;
height:90px;
border-radius:50%;
border:none;
font-size:20px;
background:white;
}

#score{
position:absolute;
top:10px;
left:20px;
font-size:25px;
color:white;
font-family:Arial;
}

#level{
position:absolute;
top:10px;
right:20px;
font-size:25px;
color:white;
font-family:Arial;
}
</style>
</head>

<body>

<div id="score">Coin: 0</div>
<div id="level">Level 1</div>
<button id="jump">JUMP</button>

<script src="https://cdn.jsdelivr.net/npm/three@0.158.0/build/three.min.js"></script>

<script>

let scene=new THREE.Scene()
scene.background=new THREE.Color(0x87CEEB)

let camera=new THREE.PerspectiveCamera(75,innerWidth/innerHeight,0.1,5000)

let renderer=new THREE.WebGLRenderer({antialias:true})
renderer.setSize(innerWidth,innerHeight)
document.body.appendChild(renderer.domElement)

let light=new THREE.DirectionalLight(0xffffff,1)
light.position.set(10,20,10)
scene.add(light)

let playerGeo=new THREE.BoxGeometry(1,2,1)
let playerMat=new THREE.MeshStandardMaterial({color:0xff8800})
let player=new THREE.Mesh(playerGeo,playerMat)
scene.add(player)

player.position.set(0,2,0)

let velocityY=0
let gravity=-0.02

function jump(){
if(player.position.y<=2.1){
velocityY=0.4
}
}

document.getElementById("jump").onclick=jump

let platforms=[]
let coins=[]

function platform(x,y,z){

let g=new THREE.BoxGeometry(4,1,4)
let m=new THREE.MeshStandardMaterial({color:0x8B4513})
let p=new THREE.Mesh(g,m)

p.position.set(x,y,z)

scene.add(p)
platforms.push(p)

}

function coin(x,y,z){

let g=new THREE.CylinderGeometry(0.5,0.5,0.2,32)
let m=new THREE.MeshStandardMaterial({color:0xFFD700})

let c=new THREE.Mesh(g,m)
c.rotation.x=Math.PI/2

c.position.set(x,y,z)

scene.add(c)
coins.push(c)

}

for(let i=0;i<200;i++){

let x=Math.random()*20-10
let y=Math.random()*8
let z=-i*8

platform(x,y,z)

if(Math.random()<0.3){
coin(x,y+2,z)
}

}

let speed=0.25
let score=0
let level=1

function animate(){

requestAnimationFrame(animate)

velocityY+=gravity
player.position.y+=velocityY

if(player.position.y<2){
player.position.y=2
velocityY=0
}

player.position.z-=speed

coins.forEach((c,index)=>{

if(player.position.distanceTo(c.position)<1.5){

scene.remove(c)
coins.splice(index,1)

score++
document.getElementById("score").innerText="Coin:
