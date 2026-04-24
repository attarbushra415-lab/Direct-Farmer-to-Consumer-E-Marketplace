
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Farmer Marketplace</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: #f5f5f5;
}

header {
  background: #2e7d32;
  color: white;
  padding: 15px;
  text-align: center;
}

nav {
  display: flex;
  justify-content: space-between;
  background: #388e3c;
  padding: 0 20px;
}

nav a {
  color: white;
  padding: 14px;
  text-decoration: none;
}

nav a:hover {
  background: #1b5e20;
}

#cart {
  font-weight: bold;
}

.hero {
  text-align: center;
  padding: 40px;
  background: url('https://images.unsplash.com/photo-1500595046743-cd271d694d30') no-repeat center/cover;
  color: white;
}

.search-box {
  text-align: center;
  margin: 20px;
}

.search-box input {
  padding: 10px;
  width: 250px;
}

.products {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: white;
  padding: 15px;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.card img {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 10px;
}

button {
  background: #2e7d32;
  color: white;
  border: none;
  padding: 10px;
  margin-top: 10px;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background: #1b5e20;
}

.cart-box {
  padding: 20px;
  background: white;
  margin: 20px;
  border-radius: 10px;
}

footer {
  background: #2e7d32;
  color: white;
  text-align: center;
  padding: 10px;
}
</style>
</head>

<body>

<header>
  <h2>🌾 Farmer Marketplace</h2>
</header>

<nav>
  <div>
    <a href="#">Home</a>
    <a href="#">Products</a>
  </div>
  <div id="cart">🛒 Cart: 0</div>
</nav>

<section class="hero">
  <h1>Fresh Products Direct from Farmers</h1>
</section>

<div class="search-box">
  <input type="text" id="search" placeholder="Search products..." onkeyup="searchProduct()">
</div>

<section class="products" id="productList">

  <!-- Tomatoes -->
  <div class="card" data-name="tomato">
    <img src="https://upload.wikimedia.org/wikipedia/commons/8/88/Bright_red_tomato_and_cross_section02.jpg">
    <h3>Tomatoes</h3>
    <p>₹30/kg</p>
    <button onclick="addToCart('Tomatoes',30)">Add to Cart</button>
  </div>

  <!-- Potatoes -->
  <div class="card" data-name="potato">
    <img src="https://upload.wikimedia.org/wikipedia/commons/a/ab/Patates.jpg">
    <h3>Potatoes</h3>
    <p>₹20/kg</p>
    <button onclick="addToCart('Potatoes',20)">Add to Cart</button>
  </div>

  <!-- Carrots -->
  <div class="card" data-name="carrot">
    <img src="https://upload.wikimedia.org/wikipedia/commons/7/7e/Carrots_of_many_colors.jpg">
    <h3>Carrots</h3>
    <p>₹40/kg</p>
    <button onclick="addToCart('Carrots',40)">Add to Cart</button>
  </div>

  <!-- Onions -->
  <div class="card" data-name="onion">
    <img src="https://upload.wikimedia.org/wikipedia/commons/2/25/Onions.jpg">
    <h3>Onions</h3>
    <p>₹25/kg</p>
    <button onclick="addToCart('Onions',25)">Add to Cart</button>
  </div>

</section>

<div class="cart-box">
  <h3>🧾 Cart Summary</h3>
  <ul id="cartItems"></ul>
  <h4>Total: ₹<span id="total">0</span></h4>
  <button onclick="checkout()">Checkout</button>
</div>

<footer>
  <p>© 2026 Farmer Marketplace</p>
</footer>

<script>
let cart = [];
let total = 0;

function addToCart(name, price) {
  cart.push({name, price});
  total += price;

  document.getElementById("cart").innerText = "🛒 Cart: " + cart.length;
  updateCart();
}

function updateCart() {
  let list = document.getElementById("cartItems");
  list.innerHTML = "";

  cart.forEach(item => {
    let li = document.createElement("li");
    li.innerText = item.name + " - ₹" + item.price;
    list.appendChild(li);
  });

  document.getElementById("total").innerText = total;
}

function checkout() {
  if(cart.length === 0){
    alert("Cart is empty!");
  } else {
    alert("Order placed successfully!");
    cart = [];
    total = 0;
    updateCart();
    document.getElementById("cart").innerText = "🛒 Cart: 0";
  }
}

function searchProduct() {
  let input = document.getElementById("search").value.toLowerCase();
  let cards = document.querySelectorAll(".card");

  cards.forEach(card => {
    let name = card.getAttribute("data-name");
    if(name.includes(input)){
      card.style.display = "block";
    } else {
      card.style.display = "none";
    }
  });
}
</script>

</body>
</html>
