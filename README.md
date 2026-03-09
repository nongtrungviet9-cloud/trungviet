<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Ai Là Triệu Phú</title>

<style>
body{
font-family: Arial;
background:#001f3f;
color:white;
text-align:center;
}

#game{
background:#003366;
width:380px;
margin:auto;
margin-top:60px;
padding:20px;
border-radius:15px;
}

button{
display:block;
width:100%;
margin:10px 0;
padding:12px;
font-size:16px;
border:none;
border-radius:8px;
background:#0074D9;
color:white;
}

button:hover{
background:#005fa3;
}

#money{
font-size:20px;
color:yellow;
}
</style>

</head>

<body>

<h1>💰 Ai Là Triệu Phú</h1>

<div id="game">

<h3 id="question"></h3>

<button onclick="answer(0)" id="a"></button>
<button onclick="answer(1)" id="b"></button>
<button onclick="answer(2)" id="c"></button>
<button onclick="answer(3)" id="d"></button>

<p id="money">Tiền: 0 VNĐ</p>

</div>

<script>

let score = 0
let current = 0

let questions = [

{
q:"Thủ đô Việt Nam là gì?",
a:["Hà Nội","Huế","Đà Nẵng","Sài Gòn"],
correct:0,
money:100000
},

{
q:"5 + 5 = ?",
a:["8","9","10","11"],
correct:2,
money:200000
},

{
q:"Con vật nào bay được?",
a:["Chó","Mèo","Chim","Bò"],
correct:2,
money:500000
},

{
q:"Trái đất quay quanh gì?",
a:["Mặt trời","Mặt trăng","Sao hỏa","Sao kim"],
correct:0,
money:1000000
}

]

function load(){

let q = questions[current]

document.getElementById("question").innerText = q.q
document.getElementById("a").innerText = "A. " + q.a[0]
document.getElementById("b").innerText = "B. " + q.a[1]
document.getElementById("c").innerText = "C. " + q.a[2]
document.getElementById("d").innerText = "D. " + q.a[3]

}

function answer(i){

if(i == questions[current].correct){

score = questions[current].money

document.getElementById("money").innerText =
"Tiền: " + score.toLocaleString() + " VNĐ"

current++

if(current < questions.length){

alert("✅ Đúng!")

load()

}else{

alert("🎉 Bạn đã thắng " + score.toLocaleString() + " VNĐ")

location.reload()

}

}else{

alert("❌ Sai rồi! Bạn ra về với " + score.toLocaleString() + " VNĐ")

location.reload()

}

}

load()

</script>

</body>
</html>
