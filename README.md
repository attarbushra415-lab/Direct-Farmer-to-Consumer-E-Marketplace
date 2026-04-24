
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmDirect Pro</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: #f5f5f5;
}

/* NAVBAR */
nav {
  position: sticky;
  top: 0;
  background: #2e7d32;
  color: white;
  padding: 12px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.search-box {
  padding: 6px;
  border-radius: 5px;
  border: none;
}

.cart {
  cursor: pointer;
  font-size: 18px;
}

/* HERO */
.hero {
  background: url('https://images.unsplash.com/photo-1606787366850-de6330128bfc') center/cover;
  color: white;
  padding: 70px 20px;
  text-align: center;
}

/* CATEGORY FILTER */
.filters {
  display: flex;
  gap: 10px;
  padding: 10px;
  overflow-x: auto;
}

.filters button {
  background: white;
  color: #2e7d32;
  border: 1px solid #2e7d32;
  padding: 6px 10px;
  border-radius: 20px;
  cursor: pointer;
}

/* PRODUCTS */
.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px,1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  padding: 10px;
  border-radius: 10px;
  text-align: center;
  transition: 0.3s;
}

.card:hover {
  transform: scale(1.05);
}

.card img {
  width: 100%;
  height: 150px;
  object-fit: cover;
}

/* Quantity */
.qty {
  display: flex;
  justify-content: center;
  gap: 5px;
  margin-top: 5px;
}

/* CART DRAWER */
.cart-drawer {
  position: fixed;
  right: -350px;
  top: 0;
  width: 300px;
  height: 100%;
  background: white;
  box-shadow: -2px 0 5px rgba(0,0,0,0.2);
  padding: 20px;
  transition: 0.3s;
  overflow-y: auto;
}

.cart-drawer.open {
  right: 0;
}

/* BUTTON */
button {
  background: #2e7d32;
  color: white;
  border: none;
  padding: 6px 10px;
  cursor: pointer;
  border-radius: 5px;
}

/* TOAST */
.toast {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: black;
  color: white;
  padding: 10px;
  display: none;
  border-radius: 5px;
}

/* FOOTER */
footer {
  background: #222;
  color: white;
  padding: 20px;
  text-align: center;
}
</style>
</head>

<body>

<!-- NAV -->
<nav>
  <h2>FarmDirect</h2>
  <input type="text" class="search-box" placeholder="Search..." onkeyup="searchProduct(this.value)">
  <div class="cart" onclick="toggleCart()">🛒 <span id="count">0</span></div>
</nav>

<!-- HERO -->
<div class="hero">
  <h1>Fresh From Farmers</h1>
  <p>Healthy • Organic • Direct</p>
</div>

<!-- FILTERS -->
<div class="filters">
  <button onclick="filter('all')">All</button>
  <button onclick="filter('vegetable')">Vegetables</button>
  <button onclick="filter('fruit')">Fruits</button>
</div>

<!-- PRODUCTS -->
<div class="products" id="productList"></div>

<!-- CART -->
<div class="cart-drawer" id="cart">
  <h3>Your Cart</h3>
  <div id="cartItems"></div>
  <h4>Total: ₹<span id="total">0</span></h4>
  <button onclick="checkout()">Checkout</button>
</div>

<!-- TOAST -->
<div class="toast" id="toast">Added to Cart</div>

<!-- FOOTER -->
<footer>
  <p>© 2026 FarmDirect Pro</p>
</footer>

<script>
const products = [
  {name:"Tomato",price:30,cat:"vegetable",img:"https://images.unsplash.com/photo-1567306226416-28f0efdc88ce"},
  {name:"Potato",price:25,cat:"vegetable",img:"https://images.unsplash.com/photo-1582515073490-dc0a1d0b36a5"},
  {name:"Carrot",price:40,cat:"vegetable",img:"https://images.unsplash.com/photo-1582515073490-dc0a1d0b36a5"},
  {name:"Onion",price:35,cat:"vegetable",img:"https://images.unsplash.com/photo-1587049352851-8d4e89133924"},
  {name:"Apple",price:120,cat:"fruit",img:"https://images.unsplash.com/photo-1560806887-1e4cd0b6cbd6"},
  {name:"Banana",price:50,cat:"fruit",img:"https://images.unsplash.com/photo-1574226516831-e1dff420e37d"},
  {name:"Spinach",price:20,cat:"vegetable",img:"https://images.unsplash.com/photo-1576045057995-568f588f82fb"},
  {name:"Mango",price:150,cat:"fruit",img:"https://images.unsplash.com/photo-1550258987-190a2d41a8ba"}
];

let cart = [];

function displayProducts(list = products) {
  const box = document.getElementById("productList");
  box.innerHTML = "";
  list.forEach((p,i)=>{
    box.innerHTML += `
      <div class="card">
        <img src="${p.img}">
        <h3>${p.name}</h3>
        <p>₹${p.price}</p>
        <button onclick="addToCart(${i})">Add</button>
      </div>`;
  });
}

function addToCart(i){
  cart.push(products[i]);
  updateCart();
  showToast();
}

function updateCart(){
  let items = document.getElementById("cartItems");
  items.innerHTML="";
  let total=0;

  cart.forEach((item,i)=>{
    total+=item.price;
    items.innerHTML+=`
    <div>
      ${item.name} ₹${item.price}
      <button onclick="removeItem(${i})">❌</button>
    </div>`;
  });

  document.getElementById("total").innerText=total;
  document.getElementById("count").innerText=cart.length;
}

function removeItem(i){
  cart.splice(i,1);
  updateCart();
}

function toggleCart(){
  document.getElementById("cart").classList.toggle("open");
}

function showToast(){
  let t=document.getElementById("toast");
  t.style.display="block";
  setTimeout(()=>t.style.display="none",1500);
}

function searchProduct(q){
  let res=products.filter(p=>p.name.toLowerCase().includes(q.toLowerCase()));
  displayProducts(res);
}

function filter(cat){
  if(cat==="all") displayProducts();
  else displayProducts(products.filter(p=>p.cat===cat));
}

function checkout(){
  if(cart.length===0) alert("Cart empty");
  else alert("Order placed!");
}

displayProducts();
</script>

</body>
</html>
