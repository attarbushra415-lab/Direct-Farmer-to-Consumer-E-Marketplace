
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FarmDirect</title>

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
  padding: 10px;
  display: flex;
  justify-content: space-between;
}

/* HERO */
.hero {
  background: url('https://images.unsplash.com/photo-1606787366850-de6330128bfc') center/cover;
  color: white;
  padding: 80px 20px;
  text-align: center;
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
}

.card img {
  width: 100%;
  height: 150px;
  object-fit: cover;
}

/* CART */
.cart-drawer {
  position: fixed;
  right: -320px;
  top: 0;
  width: 300px;
  height: 100%;
  background: white;
  padding: 20px;
  transition: 0.3s;
}

.cart-drawer.open {
  right: 0;
}

/* BUTTON */
button {
  background: #2e7d32;
  color: white;
  border: none;
  padding: 8px;
  margin-top: 5px;
  cursor: pointer;
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

<nav>
  <h2>FarmDirect</h2>
  <div onclick="toggleCart()">🛒 <span id="count">0</span></div>
</nav>

<div class="hero">
  <h1>Fresh From Farmers</h1>
  <p>Directly to Your Home</p>
</div>

<div class="products" id="productList"></div>

<div class="cart-drawer" id="cart">
  <h3>Your Cart</h3>
  <div id="cartItems"></div>
  <h4>Total: ₹<span id="total">0</span></h4>
</div>

<div class="toast" id="toast">Added to Cart</div>

<footer>© 2026 FarmDirect</footer>

<script>
const products = [
  {name:"Tomato",price:30,img:"https://images.unsplash.com/photo-1567306226416-28f0efdc88ce"},
  {name:"Potato",price:25,img:"https://images.unsplash.com/photo-1582515073490-dc0a1d0b36a5"},
  {name:"Carrot",price:40,img:"https://images.unsplash.com/photo-1592928302636-c83cfedb5d3c"},
  {name:"Onion",price:35,img:"https://images.unsplash.com/photo-1587049352851-8d4e89133924"}
];

let cart = [];

/* SHOW PRODUCTS */
function displayProducts() {
  let html = "";
  products.forEach((p,i)=>{
    html += `
      <div class="card">
        <img src="${p.img}">
        <h3>${p.name}</h3>
        <p>₹${p.price}</p>
        <button onclick="addToCart(${i})">Add</button>
      </div>
    `;
  });
  document.getElementById("productList").innerHTML = html;
}

/* ADD */
function addToCart(i) {
  cart.push(products[i]);
  updateCart();
  showToast();
}

/* UPDATE CART */
function updateCart() {
  let html = "";
  let total = 0;

  if(cart.length === 0){
    html = "Cart is empty";
  }

  cart.forEach((item,index)=>{
    total += item.price;
    html += `
      <div>
        ${item.name} ₹${item.price}
        <button onclick="removeItem(${index})">❌</button>
      </div>
    `;
  });

  document.getElementById("cartItems").innerHTML = html;
  document.getElementById("total").innerText = total;
  document.getElementById("count").innerText = cart.length;
}

/* REMOVE */
function removeItem(i) {
  cart.splice(i,1);
  updateCart();
}

/* CART TOGGLE */
function toggleCart() {
  document.getElementById("cart").classList.toggle("open");
}

/* TOAST */
function showToast() {
  let t = document.getElementById("toast");
  t.style.display = "block";
  setTimeout(()=>t.style.display="none",1500);
}

displayProducts();
</script>

</body>
</html>
