<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Farmer Cart</title>

<style>
body {
  margin: 0;
  font-family: Arial;
  background: #f4f4f4;
}

/* Screens */
.screen {
  display: none;
  padding: 20px;
  text-align: center;
}

.active {
  display: block;
}

/* Splash */
#splash {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: green;
  color: white;
  font-size: 24px;
}

/* Buttons */
button {
  padding: 10px;
  margin: 10px;
  background: green;
  color: white;
  border: none;
  border-radius: 5px;
}

/* Inputs */
input {
  padding: 10px;
  margin: 8px;
  width: 80%;
}

/* Product List */
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: white;
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
}

.cart-box {
  background: #fff;
  padding: 10px;
  margin-top: 15px;
  border-radius: 5px;
}
</style>

</head>

<body>

<!-- Splash Screen -->
<div id="splash" class="screen active">
  🛒 Farmer Cart
</div>

<!-- Language Screen -->
<div id="language" class="screen">
  <h2>Select Language</h2>
  <p>English</p>
  <p>Hindi (हिंदी)</p>
  <p>Marathi (मराठी)</p>
  <button onclick="nextScreen('signup')">Continue</button>
</div>

<!-- Signup Screen -->
<div id="signup" class="screen">
  <h2>Create Account</h2>
  <input type="text" placeholder="Name">
  <input type="password" placeholder="Password">
  <br>
  <button onclick="nextScreen('home')">Continue</button>
</div>

<!-- Home Screen -->
<div id="home" class="screen">
  <h2>Products</h2>

  <div class="item">
    🍅 Tomato ₹40
    <button onclick="addCart('Tomato',40)">Add</button>
  </div>

  <div class="item">
    🥭 Mango ₹80
    <button onclick="addCart('Mango',80)">Add</button>
  </div>

  <div class="item">
    🍌 Banana ₹30
    <button onclick="addCart('Banana',30)">Add</button>
  </div>

  <div class="item">
    🍇 Grapes ₹60
    <button onclick="addCart('Grapes',60)">Add</button>
  </div>

  <button onclick="showCart()">View Cart</button>

  <div id="cart" class="cart-box"></div>
</div>

<script>
let cart = [];
let total = 0;

/* Switch Screens */
function nextScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

/* Splash Auto Next */
setTimeout(() => {
  nextScreen('language');
}, 2000);

/* Add to Cart */
function addCart(item, price) {
  cart.push(item + " ₹" + price);
  total += price;
  alert(item + " added to cart");
}

/* Show Cart */
function showCart() {
  let cartDiv = document.getElementById("cart");

  if(cart.length === 0){
    cartDiv.innerHTML = "Cart is empty";
    return;
  }

  cartDiv.innerHTML =
    "<h3>Cart Items:</h3>" +
    cart.join("<br>") +
    "<br><br><b>Total: ₹" + total + "</b>";
}
</script>

</body>
</html>


