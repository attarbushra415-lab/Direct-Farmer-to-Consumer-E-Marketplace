
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmDirect Pro</title>

<style>
body{
  margin:0;
  font-family:Arial;
  overflow:hidden;
  background:#e8f5e9;
}

/* LOGIN */
.screen{
  position:absolute;
  width:100%;
  height:100vh;
  transition:0.5s;
}

.login{
  background:
  linear-gradient(rgba(0,0,0,0.6),rgba(0,0,0,0.6)),
  url("https://images.unsplash.com/photo-1501004318641-b39e6451bec6?w=1200");
  background-size:cover;
  color:white;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  text-align:center;
}

.box{
  background:rgba(255,255,255,0.15);
  padding:20px;
  border-radius:15px;
  width:270px;
  backdrop-filter:blur(10px);
}

input,select{
  width:100%;
  padding:10px;
  margin:5px 0;
  border:none;
  border-radius:8px;
}

button{
  width:100%;
  padding:10px;
  background:#2e7d32;
  color:white;
  border:none;
  border-radius:8px;
  cursor:pointer;
}

button:hover{
  background:#1b5e20;
}

/* APP */
.app{
  background:#f1f8e9;
  transform:translateX(100%);
}

.show{
  transform:translateX(0);
}

/* HEADER */
.header{
  background:#1b5e20;
  color:white;
  padding:12px;
  text-align:center;
}

/* PAGE */
.page{
  display:none;
  height:100vh;
  overflow:auto;
  padding-bottom:60px;
}

.active{
  display:block;
  animation:slide .4s ease;
}

@keyframes slide{
  from{transform:translateX(50px);opacity:0}
  to{transform:translateX(0);opacity:1}
}

/* GRID */
.grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  padding:10px;
}

/* CARD */
.card{
  background:white;
  border-radius:12px;
  overflow:hidden;
  box-shadow:0 3px 8px rgba(0,0,0,0.2);
  transition:0.3s;
  animation:fade 0.4s ease;
}

.card:hover{
  transform:scale(1.05);
}

@keyframes fade{
  from{opacity:0}
  to{opacity:1}
}

.card img{
  width:100%;
  height:110px;
  object-fit:cover;
}

/* CART / PANEL */
.panel{
  background:white;
  margin:10px;
  padding:10px;
  border-radius:10px;
}

/* PAYMENT */
.payment{
  background:white;
  padding:15px;
  margin:10px;
  border-radius:10px;
}

/* TRACK */
.track{
  background:white;
  margin:10px;
  padding:10px;
  border-radius:10px;
  font-size:13px;
}

/* NAV */
.nav{
  position:fixed;
  bottom:0;
  width:100%;
  display:flex;
  justify-content:space-around;
  background:white;
  padding:10px;
  border-top:1px solid #ccc;
}

.nav div{
  cursor:pointer;
  font-size:13px;
}

.nav .activeTab{
  color:#2e7d32;
  font-weight:bold;
}
</style>
</head>

<body>

<!-- LOGIN -->
<div class="screen login" id="login">
<h1>🌾 FarmDirect</h1>
<p>Fresh Fruits & Vegetables from Farmers 🚜</p>

<div class="box">
<input id="user" placeholder="Name">
<select id="role">
<option value="customer">Customer</option>
<option value="farmer">Farmer</option>
</select>
<button onclick="enterApp()">Enter</button>
</div>
</div>

<!-- APP -->
<div class="screen app" id="app">

<div class="header">🌾 FarmDirect Pro</div>

<!-- HOME -->
<div class="page active" id="home">
<div class="grid" id="products"></div>
</div>

<!-- FARMER -->
<div class="page" id="farmer">
<div class="panel">
<h3>👨‍🌾 Farmer Dashboard</h3>
<input id="pname" placeholder="Product Name">
<input id="pprice" placeholder="Price">
<button onclick="addProduct()">Upload Product</button>

<h4>Your Products</h4>
<div id="myproducts"></div>
</div>
</div>

<!-- CART -->
<div class="page" id="cartPage">
<div class="panel" id="cart"></div>
<p>Total: ₹<span id="total">0</span></p>
<button onclick="openPay()">Checkout</button>
</div>

<!-- PAYMENT -->
<div class="page" id="payPage">
<div class="payment">
<h3>💳 Razorpay Checkout (Mock UI)</h3>
<input placeholder="Enter UPI ID">
<button onclick="pay()">Pay Now</button>
</div>

<div class="track" id="track"></div>
</div>

<!-- NAV -->
<div class="nav">
<div onclick="openPage('home')" id="navHome">🏠 Home</div>
<div onclick="openPage('cartPage')" id="navCart">🛒 Cart</div>
<div onclick="openPage('farmer')" id="navFarmer">👨‍🌾 Farmer</div>
</div>

</div>

<script>

let products = [

/* 🌿 VEGETABLES */
{name:"Tomato",price:30,img:"https://images.unsplash.com/photo-1607305387299-a3d9611cd469?w=600"},
{name:"Potato",price:25,img:"https://images.unsplash.com/photo-1518977676601-b53f82aba655?w=600"},
{name:"Onion",price:20,img:"https://images.unsplash.com/photo-1508747703725-719777637510?w=600"},
{name:"Carrot",price:35,img:"https://images.unsplash.com/photo-1447175008436-054170c2e979?w=600"},

/* 🍎 FRUITS */
{name:"Apple",price:120,img:"https://images.unsplash.com/photo-1567306226416-28f0efdc88ce?w=600"},
{name:"Banana",price:40,img:"https://images.unsplash.com/photo-1571771894821-ce9b6c11b08e?w=600"},
{name:"Orange",price:60,img:"https://images.unsplash.com/photo-1580910051074-3eb694886505?w=600"},
{name:"Grapes",price:80,img:"https://images.unsplash.com/photo-1537640538966-79f369143f8f?w=600"}

];

let cart=[];

/* LOGIN */
function enterApp(){
  document.getElementById("login").style.display="none";
  document.getElementById("app").classList.add("show");
  render();
}

/* NAV */
function openPage(id){
  document.querySelectorAll(".page").forEach(p=>p.classList.remove("active"));
  document.getElementById(id).classList.add("active");

  document.querySelectorAll(".nav div").forEach(n=>n.classList.remove("activeTab"));
  if(id=="home") document.getElementById("navHome").classList.add("activeTab");
  if(id=="cartPage") document.getElementById("navCart").classList.add("activeTab");
  if(id=="farmer") document.getElementById("navFarmer").classList.add("activeTab");
}

/* PRODUCTS */
function render(){
  let html="";
  products.forEach((p,i)=>{
    html+=`
    <div class="card">
      <img src="${p.img}">
      <div style="padding:8px">
        <h4>${p.name}</h4>
        <p>₹${p.price}</p>
        <button onclick="add(${i})">Add</button>
      </div>
    </div>`;
  });
  document.getElementById("products").innerHTML=html;
}

/* CART */
function add(i){
  cart.push(products[i]);
  updateCart();
}

function updateCart(){
  let html="";
  let total=0;

  cart.forEach(c=>{
    total+=Number(c.price);
    html+=`<p>${c.name} - ₹${c.price}</p>`;
  });

  document.getElementById("cart").innerHTML=html;
  document.getElementById("total").innerText=total;
}

/* FARMER */
function addProduct(){
  let n=document.getElementById("pname").value;
  let p=document.getElementById("pprice").value;

  let obj={
    name:n,
    price:p,
    img:"https://images.unsplash.com/photo-1501004318641-b39e6451bec6?w=600"
  };

  products.push(obj);
  render();

  document.getElementById("myproducts").innerHTML+=
  `<p>${n} - ₹${p}</p>`;
}

/* PAYMENT */
function openPay(){
  openPage("payPage");
  document.getElementById("track").innerHTML=
  "🟡 Ordered → 🟠 Packed → 🔵 Out for Delivery → 🟢 Delivered";
}

function pay(){
  alert("Payment Successful (Mock Razorpay)");
  cart=[];
  updateCart();
}

</script>

</body>
</html>
