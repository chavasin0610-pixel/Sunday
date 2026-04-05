<!DOCTYPE html>
<html>
<head>
<base target="_top">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
<link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;500&display=swap" rel="stylesheet">

<style>

:root{
--bg-dark:#0f0f0f;
--accent-red:#8b0000;
--gold:linear-gradient(45deg,#bf953f,#fcf6ba,#b38728,#fbf5b7,#aa771c);
}

body{
margin:0;
font-family:'Kanit',sans-serif;
background:#0f0f0f;
background-image:radial-gradient(circle at center,#2c0000 0%,#0f0f0f 100%);
height:100vh;
display:flex;
justify-content:center;
align-items:center;
}

.login-container{
background:rgba(0,0,0,0.85);
border:1px solid #333;
padding:40px 30px;
border-radius:15px;
box-shadow:0 10px 30px rgba(0,0,0,0.5),0 0 15px rgba(139,0,0,0.2);
width:350px;
text-align:center;
position:relative;
}

.login-container::before{
content:"";
position:absolute;
top:0;
left:0;
right:0;
height:4px;
background:var(--gold);
border-radius:15px 15px 0 0;
}

h2{
color:#fbf5b7;
letter-spacing:3px;
margin-bottom:30px;
}

.input-group{
margin-bottom:20px;
text-align:left;
}

label{
        color:#bf953f;
        font-size:13px;
        display:block;
        margin-bottom:5px;
}

input { 
      width: 100%;
      padding: 12px;
      background: #1a1a1a;
      border: 1px solid #444;
      border-radius: 5px;
      color: white;
      outline: none;
      box-sizing: border-box;
      transition: 0.3s;
      font-size: 16px;
    }


input:focus{
      border-color:#8b0000;
      box-shadow:0 0 5px rgba(139,0,0,0.5);
}

.password-box{
      position:relative;
}

.showpass{
      position:absolute;
right:10px;
top:10px;
cursor:pointer;
}

button{
width:100%;
padding:12px;
margin-top:10px;
border:none;
border-radius:5px;
background:var(--gold);
color:#000;
font-weight:bold;
font-size:16px;
cursor:pointer;
}

button:hover{
filter:brightness(1.2);
}

button:disabled{
opacity:.6;
cursor:not-allowed;
}

#message{
margin-top:20px;
font-size:14px;
min-height:20px;
}

.error{color:#ff4d4d;}
.success{color:#fcf6ba;}

</style>
</head>

<body>

<div class="login-container">

<img src="https://i.ibb.co/9kHMK8kY/1.png" style="height:130px">

<h2>      </h2>    //ใส่ชื่อ

<div class="input-group">
<label>USERNAME</label>
<input type="text" id="user" placeholder="กรอกชื่อผู้ใช้">
</div>

<div class="input-group password-box">
<label>PASSWORD</label>
<input type="password" id="pass" placeholder="กรอกรหัสผ่าน">
<span class="showpass" onclick="togglePass()"></span>
</div>

<button id="loginBtn" onclick="login()">LOGIN</button>

<div id="message"></div>

</div>

<script>

// รีเฟรชแล้วให้กลับ Login
window.onload = function(){
sessionStorage.clear();
localStorage.clear();
};

// แสดง / ซ่อนรหัสผ่าน
function togglePass(){
const p=document.getElementById("pass");
p.type = p.type==="password" ? "text":"password";
}

// กด Enter เพื่อล็อกอิน
document.addEventListener("keydown",function(e){
if(e.key==="Enter"){
login();
}
});

function login(){

const user=document.getElementById('user').value.trim();
const pass=document.getElementById('pass').value.trim();
const msg=document.getElementById('message');
const btn=document.getElementById('loginBtn');

if(user==="" || pass===""){
msg.className="error";
msg.innerText="กรุณากรอก Username และ Password";
return;
}

msg.className="";
msg.innerText="กำลังตรวจสอบตัวตน...";
btn.disabled=true;
btn.innerText="กำลังเข้าสู่ระบบ...";

google.script.run.withSuccessHandler(function(res){

btn.disabled=false;
btn.innerText="LOGIN";

if(res.status==="success"){

msg.className="success";
msg.innerText=res.msg;

setTimeout(function(){

window.location.href="https://script.google.com/macros/s/AKfycbzROLbVKRIfHM9yqxcmM7p--OB13uxoNea1XkewXiUmLVoR-8X0n1dlkG1MXr-HrRH2/exec";

},1000);

}else{

msg.className="error";
msg.innerText=res.msg;

}

}).checkAccess(user,pass);

}

</script>

</body>
</html>
