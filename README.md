<! Uy tín s1 Vn html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Tvmember</title>

<style>

body{
font-family:Arial;
background:#0f172a;
color:white;
text-align:center;
}

.box{
background:#1e293b;
padding:20px;
margin:20px auto;
width:330px;
border-radius:10px;
}

input,select,button{
width:90%;
padding:10px;
margin:6px;
border:none;
border-radius:6px;
}

button{
background:#22c55e;
color:white;
font-weight:bold;
}

.order{
background:#334155;
padding:10px;
margin:5px;
border-radius:5px;
}

</style>
</head>

<body>

<h1>⚡ Trung Việt  ⚡</h1>

<div id="register" class="box">

<h2>Đăng ký</h2>

<input id="reguser" placeholder="Tài khoản">
<input id="regpass" type="password" placeholder="Mật khẩu">

<button onclick="register()">Đăng ký</button>

<p>Đã có tài khoản?  
<a onclick="showLogin()">Đăng nhập</a></p>

</div>

<div id="login" class="box" style="display:none">

<h2>Đăng nhập</h2>

<input id="loguser" placeholder="Tài khoản">
<input id="logpass" type="password" placeholder="Mật khẩu">

<button onclick="login()">Đăng nhập</button>

</div>

<div id="panel" class="box" style="display:none">

<h2>User Panel</h2>

<p>Số dư: <span id="balance">0</span> đ</p>

<select id="service">
<option>coment tik tok</option>
<option>Tim TikTok</option>
<option>View Tik tok</option>
</select>

<input id="link" placeholder="Link bài viết">
<input id="amount" type="number" placeholder="Số lượng">

<button onclick="order()">Tạo đơn</button>

<h3>Lịch sử đơn</h3>

<div id="orders"></div>

<button onclick="logout()">Đăng xuất</button>

</div>

<div id="admin" class="box" style="display:none">

<h2>Admin Panel</h2>

<button onclick="showUsers()">Xem Users</button>

<div id="users"></div>

<button onclick="logout()">Đăng xuất</button>

</div>

<script>

let currentUser=""

function register(){

let user=document.getElementById("reguser").value
let pass=document.getElementById("regpass").value

if(user==""||pass==""){
alert("Nhập đầy đủ")
return
}

let data={
pass:pass,
balance:10000
}

localStorage.setItem("user_"+user,JSON.stringify(data))

alert("Đăng ký thành công")

showLogin()

}

function login(){

let user=document.getElementById("loguser").value
let pass=document.getElementById("logpass").value

if(user=="admin" && pass=="admin123"){

document.getElementById("login").style.display="none"
document.getElementById("admin").style.display="block"

return

}

let data=JSON.parse(localStorage.getItem("user_"+user))

if(data && data.pass==pass){

currentUser=user

document.getElementById("login").style.display="none"
document.getElementById("panel").style.display="block"

document.getElementById("balance").innerText=data.balance

loadOrders()

}else{

alert("Sai tài khoản")

}

}

function order(){

let service=document.getElementById("service").value
let link=document.getElementById("link").value
let amount=document.getElementById("amount").value

let orders=JSON.parse(localStorage.getItem("orders_"+currentUser)||"[]")

orders.push({
service:service,
link:link,
amount:amount
})

localStorage.setItem("orders_"+currentUser,JSON.stringify(orders))

loadOrders()

}

function loadOrders(){

let orders=JSON.parse(localStorage.getItem("orders_"+currentUser)||"[]")

let html=""

orders.forEach(o=>{

html+=`<div class="order">
${o.service}<br>
${o.amount}<br>
${o.link}
</div>`

})

document.getElementById("orders").innerHTML=html

}

function showUsers(){

let html=""

for(let i=0;i<localStorage.length;i++){

let key=localStorage.key(i)

if(key.startsWith("user_")){

let user=key.replace("user_","")

html+=`<div class="order">${user}</div>`

}

}

document.getElementById("users").innerHTML=html

}

function logout(){

location.reload()

}

function showLogin(){

document.getElementById("register").style.display="none"
document.getElementById("login").style.display="block"

}

</script>

</body>
</html>
