<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Game Đố Vui 100 Câu</title>

<style>
body{
font-family: Arial;
background:#222;
color:white;
text-align:center;
}

#game{
background:#333;
width:350px;
margin:auto;
margin-top:60px;
padding:20px;
border-radius:10px;
}

button{
width:100%;
padding:10px;
margin:8px 0;
font-size:16px;
border:none;
border-radius:6px;
background:#00aaff;
color:white;
}

button:hover{
background:#0088cc;
}
</style>

</head>

<body>

<h1>🎮 Game Đố Vui</h1>

<div id="game">

<h3 id="question"></h3>

<button onclick="answer(0)" id="a"></button>
<button onclick="answer(1)" id="b"></button>
<button onclick="answer(2)" id="c"></button>
<button onclick="answer(3)" id="d"></button>

<p>⭐ Điểm: <span id="score">0</span></p>
<p>📊 Câu: <span id="number">1</span>/100</p>

</div>

<script>

let score = 0
let current = 0

let questions = []

// tạo 100 câu hỏi tự động
for(let i=1;i<=100;i++){

questions.push({
q:"Câu hỏi số " + i + ": 5 + 5 = ?",
a:["8","9","10","11"],
correct:2
})

}

function load(){

let q = questions[current]

document.getElementById("question").innerText = q.q
document.getElementById("a").innerText = q.a[0]
document.getElementById("b").innerText = q.a[1]
document.getElementById("c").innerText = q.a[2]
document.getElementById("d").innerText = q.a[3]

document.getElementById("number").innerText = current+1

}

function answer(i){

if(i == questions[current].correct){
score++
document.getElementById("score").innerText = score
}

current++

if(current < questions.length){
load()
}else{
alert("Game kết thúc! Điểm: "+score)
location.reload()
}

}

load()

</script>

</body>
</html>
