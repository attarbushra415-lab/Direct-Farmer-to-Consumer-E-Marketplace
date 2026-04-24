<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmDirect Pro</title>

<style>
body {
  margin:0;
  font-family: Arial;
  background:#e8f5e9;
}

/* 🌿 HERO LOGIN SCREEN */
.login {
  height:100vh;
  background:
  linear-gradient(rgba(0,0,0,0.6),rgba(0,0,0,0.6)),
  url("https://images.unsplash.com/photo-1500595046743-cd271d694d30?w=1200");
  background-size:cover;
  display:flex;
  justify-content:center;
  align-items:center;
  flex-direction:column;
  color:white;
  text-align:center;
  padding:20px;
}

.login h1 {
  font-size:26px;
  margin-bottom:5px;
}

.login p {
  font-size:13px;
  opacity:0.9;
}

/* LOGIN BOX */
.box {
  background:rgba(255,255,255,0.15);
  backdrop-filter: blur(10px);
  padding:20px;
  border-radius:15px;
  margin-top:15px;
  width:260px;
}

input, select {
  width:100%;
  padding:10px;
  margin:5px 0;
  border:none;
  border-radius:8px;
}

button {
  width:100%;
  padding:10px;
  background:#2e7d32;
  color:white;
  border:none;
  border-radius:8px;
  cursor:pointer;
}

button:hover {
  background:#1b5e20;
}

/* APP */
.app {
  display:none;
}

.header {
  background:#1b5e20;
  color:white;
  padding:12px;
  text-align:center;
}

.grid {
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
  padding:10px;
}

.card {
  background:white;
  border-radius:12px;
  overflow:hidden;
  box-shadow:0 3px 8px rgba(0,0,0,0.2);
  transition:0.3s;
}

.card:hover {
  transform:scale(1.04);
}

.card img {
  width:100%;
  height:110px;
  object-fit:cover;
}

.card-body {
  padding:8px;
}

/* CART */
.cart, .payment, .dashboard {
  margin:10px;
  padding:10px;
  background:white;
  border-radius:10px;
}

</style>
</head>

<body>

<!-- 🌿 LOGIN HERO PAGE -->
<div class="login" id="loginBox">

<h1>🌾 Direct Farmer to Consumer</h1>
<p>Fresh farm produce directly from farmers to your home 🚜</p>

<div class="box">
  <input id="user" placeholder="Enter Name">

  <select id="role">
    <option value="customer">Customer</option>
    <option value="farmer">Farmer</option>
  </select>

  <button onclick="login()">Enter Marketplace</button>
</div>

</div>

<!-- APP -->
<div class="app" id="app">

<div class="header">🌾 FarmDirect Pro</div>

<!-- FARMER DASHBOARD -->
<div class="dashboard" id="dashboard" style="display:none;">
<h3>👨‍🌾 Farmer Dashboard</h3>
<p>Manage your farm products easily</p>
<button onclick="addDummyProduct()">Add Product</button>
</div>

<!-- PRODUCTS -->
<div class="grid" id="products"></div>

<!-- CART -->
<div class="cart">
<h3>🛒 Cart</h3>
<div id="cart"></div>
<p>Total: ₹<span id="total"></span></p>
<button onclick="openPayment()">Checkout</button>
</div>

<!-- PAYMENT -->
<div class="payment" id="payment" style="display:none;">
<h3>💳 Razorpay Payment (UI)</h3>
<input placeholder="Enter UPI ID">
<button onclick="pay()">Pay Now</button>
</div>

</div>

<script>

let user="", role="";
let cart=[];

let products=[
 {name:"Tomato",price:30,img:"https://images.unsplash.com/photo-1607305387299-a3d9611cd469?w=600"},
 {name:"Potato",price:25,img:"https://images.unsplash.com/photo-1518977676601-b53f82aba655?w=600"},
 {name:"Onion",price:20,img:"https://images.unsplash.com/photo-1508747703725-719777637510?w=600"}
];

/* LOGIN */
function login(){
  user=document.getElementById("user").value;
  role=document.getElementById("role").value;

  document.getElementById("loginBox").style.display="none";
  document.getElementById("app").style.display="block";

  if(role==="farmer"){
    document.getElementById("dashboard").style.display="block";
  }

  render();
}

/* PRODUCTS */
function render(){
  let html="";

  products.forEach((p,i)=>{
    html+=`
    <div class="card">
      <img src="${p.img}">
      <div class="card-body">
        <h4>${p.name}</h4>
        <p>₹${p.price}</p>
        <button onclick="addCart(${i})">Add to Cart</button>
      </div>
    </div>`;
  });

  document.getElementById("products").innerHTML=html;
  updateCart();
}

/* CART */
function addCart(i){
  cart.push(products[i]);
  updateCart();
}

function updateCart(){
  let html="";
  let total=0;

  cart.forEach(c=>{
    total+=c.price;
    html+=`<p>${c.name} - ₹${c.price}</p>`;
  });

  document.getElementById("cart").innerHTML=html;
  document.getElementById("total").innerText=total;
}

/* PAYMENT */
function openPayment(){
  document.getElementById("payment").style.display="block";
}

function pay(){
  alert("Payment Successful (Mock Razorpay)");
  cart=[];
  updateCart();
}

/* FARMER ADD */
function addDummyProduct(){
  products.push({
    name:"New Crop",
    price:40,
    img:"https://images.unsplash.com/photo-1501004318641-b39e6451bec6?w=600"
  });
  render();
}

</script>

</body>
</html>

