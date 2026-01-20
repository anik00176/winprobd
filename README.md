# winprobd
this is safe and stable
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>WINPRO</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body{margin:0;font-family:Arial;background:#0f172a;color:#fff}
header{background:#020617;padding:15px;text-align:center;font-size:22px;font-weight:bold;color:#22c55e}
.container{padding:15px}
.card{background:#020617;border-radius:10px;padding:15px;margin-bottom:15px}
input,button{width:100%;padding:10px;margin-top:10px;border:none;border-radius:5px}
input{background:#1e293b;color:#fff}
button{background:#22c55e;color:#000;font-weight:bold}
.hide{display:none}
.row{display:flex;justify-content:space-between;margin-top:10px}
.box{width:48%;padding:15px;text-align:center;border-radius:8px}
.green{background:#16a34a}
.red{background:#dc2626}
.small{font-size:13px;color:#94a3b8}
</style>
</head>
<body>

<header>WINPRO</header>

<div class="container">

<!-- LOGIN -->
<div id="login" class="card">
<h3>Login</h3>
<input id="luser" placeholder="Username">
<input id="lpass" type="password" placeholder="Password">
<button onclick="login()">Login</button>
<p class="small">No account? <a href="#" onclick="showRegister()" style="color:#22c55e">Register</a></p>
</div>

<!-- REGISTER -->
<div id="register" class="card hide">
<h3>Register</h3>
<input id="ruser" placeholder="Username">
<input id="rpass" type="password" placeholder="Password">
<button onclick="register()">Create Account</button>
</div>

<!-- DASHBOARD -->
<div id="dash" class="hide">
<div class="card">
<h3>Dashboard</h3>
<p>Balance: <b id="bal">৳1000</b></p>
<button onclick="logout()">Logout</button>
</div>

<div class="card">
<h3>Color Result (Demo)</h3>
<div class="row">
<div class="box green" onclick="play('GREEN')">GREEN</div>
<div class="box red" onclick="play('RED')">RED</div>
</div>
<p id="result" class="small"></p>
</div>

<div class="card">
<h3>History</h3>
<ul id="history" class="small"></ul>
</div>
</div>

</div>

<script>
let user = localStorage.getItem("user");
let bal = localStorage.getItem("bal") || 1000;

if(user){showDash()}

function showRegister(){
login.classList.add("hide");
register.classList.remove("hide");
}

function register(){
localStorage.setItem("user", ruser.value);
localStorage.setItem("pass", rpass.value);
localStorage.setItem("bal", 1000);
alert("Account Created");
location.reload();
}

function login(){
if(luser.value==localStorage.getItem("user") &&
lpass.value==localStorage.getItem("pass")){
showDash();
}else alert("Wrong login");
}

function showDash(){
login.classList.add("hide");
register.classList.add("hide");
dash.classList.remove("hide");
bal=document.getElementById("bal").innerText="৳"+localStorage.getItem("bal");
}

function play(c){
let res=Math.random()>0.5?"GREEN":"RED";
let b=parseInt(localStorage.getItem("bal"));
if(c==res){b+=100}else{b-=50}
localStorage.setItem("bal",b);
document.getElementById("bal").innerText="৳"+b;
result.innerText="Result: "+res;
let li=document.createElement("li");
li.innerText=c+" → "+res;
history.appendChild(li);
}

function logout(){
localStorage.removeItem("user");
location.reload();
}
</script>

</body>
</html>
