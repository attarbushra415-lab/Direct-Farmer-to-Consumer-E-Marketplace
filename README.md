<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FarmFresh | Direct from Farm to Table</title>
    <script src="https://tailwindcss.com"></script>
    <link href="https://cloudflare.com" rel="stylesheet">
    <style>
        @import url('https://googleapis.com');
        body { font-family: 'Poppins', sans-serif; }
    </style>
</head>
<body class="bg-gray-50">

    <!-- Navigation -->
    <nav class="bg-white shadow-md sticky top-0 z-50">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold text-green-600 flex items-center">
                <i class="fas fa-leaf mr-2"></i>FarmFresh
            </a>
            <div class="hidden md:flex space-x-8 font-medium">
                <a href="#home" class="hover:text-green-600 transition">Home</a>
                <a href="#products" class="hover:text-green-600 transition">Shop</a>
                <a href="#farmers" class="hover:text-green-600 transition">Our Farmers</a>
                <a href="#" class="hover:text-green-600 transition">About</a>
            </div>
            <div class="flex items-center space-x-4">
                <button class="relative">
                    <i class="fas fa-shopping-basket text-xl text-gray-700"></i>
                    <span class="absolute -top-2 -right-2 bg-green-500 text-white text-xs rounded-full px-1.5">3</span>
                </button>
                <button class="bg-green-600 text-white px-5 py-2 rounded-full hover:bg-green-700 transition">Login</button>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <header id="home" class="relative h-[500px] flex items-center justify-center text-white">
        <img src="https://unsplash.com" 
             class="absolute inset-0 w-full h-full object-cover brightness-50" alt="Farm land">
        <div class="relative z-10 text-center px-4">
            <h1 class="text-4xl md:text-6xl font-bold mb-4">Freshness Delivered <br> Directly from the Soil</h1>
            <p class="text-lg md:text-xl mb-8">Support local farmers and get 100% organic produce at your doorstep.</p>
            <a href="#products" class="bg-orange-500 hover:bg-orange-600 text-white px-8 py-3 rounded-lg font-semibold text-lg transition">Shop Fresh Produce</a>
        </div>
    </header>

    <!-- Product Section -->
    <section id="products" class="container mx-auto px-6 py-16">
        <div class="flex justify-between items-end mb-12">
            <div>
                <h2 class="text-3xl font-bold text-gray-800">Season's Best</h2>
                <p class="text-gray-600">Harvested today, delivered tomorrow.</p>
            </div>
            <button class="text-green-600 font-semibold border-b-2 border-green-600">View All</button>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
            <!-- Product 1 -->
            <div class="bg-white rounded-xl shadow-sm hover:shadow-xl transition p-4 border">
                <img src="https://unsplash.com" alt="Tomatoes" class="w-full h-48 object-cover rounded-lg mb-4">
                <span class="text-xs font-bold text-green-600 uppercase tracking-widest">Organic</span>
                <h3 class="text-lg font-bold text-gray-800">Fresh Cherry Tomatoes</h3>
                <p class="text-sm text-gray-500 mb-4">Grown by: Green Valley Farm</p>
                <div class="flex justify-between items-center">
                    <span class="text-xl font-bold text-gray-900">$4.50 / kg</span>
                    <button class="bg-green-100 p-2 rounded-full text-green-600 hover:bg-green-600 hover:text-white transition">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
            </div>

            <!-- Product 2 -->
            <div class="bg-white rounded-xl shadow-sm hover:shadow-xl transition p-4 border">
                <img src="https://unsplash.com" alt="Carrots" class="w-full h-48 object-cover rounded-lg mb-4">
                <span class="text-xs font-bold text-green-600 uppercase tracking-widest">Pesticide Free</span>
                <h3 class="text-lg font-bold text-gray-800">Mountain Carrots</h3>
                <p class="text-sm text-gray-500 mb-4">Grown by: John's Organic Acres</p>
                <div class="flex justify-between items-center">
                    <span class="text-xl font-bold text-gray-900">$3.20 / kg</span>
                    <button class="bg-green-100 p-2 rounded-full text-green-600 hover:bg-green-600 hover:text-white transition">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
            </div>

            <!-- Product 3 -->
            <div class="bg-white rounded-xl shadow-sm hover:shadow-xl transition p-4 border">
                <img src="https://unsplash.com" alt="Avocado" class="w-full h-48 object-cover rounded-lg mb-4">
                <span class="text-xs font-bold text-green-600 uppercase tracking-widest">Premium</span>
                <h3 class="text-lg font-bold text-gray-800">Hass Avocado</h3>
                <p class="text-sm text-gray-500 mb-4">Grown by: Sun-Kissed Orchards</p>
                <div class="flex justify-between items-center">
                    <span class="text-xl font-bold text-gray-900">$2.00 / pc</span>
                    <button class="bg-green-100 p-2 rounded-full text-green-600 hover:bg-green-600 hover:text-white transition">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
            </div>

            <!-- Product 4 -->
            <div class="bg-white rounded-xl shadow-sm hover:shadow-xl transition p-4 border">
                <img src="https://unsplash.com" alt="Spinach" class="w-full h-48 object-cover rounded-lg mb-4">
                <span class="text-xs font-bold text-green-600 uppercase tracking-widest">Local</span>
                <h3 class="text-lg font-bold text-gray-800">Baby Spinach</h3>
                <p class="text-sm text-gray-500 mb-4">Grown by: Rooted Family Farm</p>
                <div class="flex justify-between items-center">
                    <span class="text-xl font-bold text-gray-900">$2.50 / bag</span>
                    <button class="bg-green-100 p-2 rounded-full text-green-600 hover:bg-green-600 hover:text-white transition">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Meet the Farmers -->
    <section id="farmers" class="bg-green-50 py-16">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl font-bold text-center mb-12 text-gray-800">Know Your Farmer</h2>
            <div class="grid grid-cols-1 md:grid-cols-3 gap-12">
                <div class="text-center">
                    <img src="https://unsplash.com" class="w-32 h-32 rounded-full mx-auto mb-4 border-4 border-white shadow-lg object-cover">
                    <h4 class="text-xl font-bold">Farmer Robert</h4>
                    <p class="text-gray-600 italic">"30 years of growing organic berries in Oregon."</p>
                </div>
                <div class="text-center">
                    <img src="https://unsplash.com" class="w-32 h-32 rounded-full mx-auto mb-4 border-4 border-white shadow-lg object-cover">
                    <h4 class="text-xl font-bold">Farmer Maria</h4>
                    <p class="text-gray-600 italic">"Specializes in heritage vegetables and soil health."</p>
                </div>
                <div class="text-center">
                    <img src="https://unsplash.com" class="w-32 h-32 rounded-full mx-auto mb-4 border-4 border-white shadow-lg object-cover">
                    <h4 class="text-xl font-bold">The Patel Family</h4>
                    <p class="text-gray-600 italic">"Providing pesticide-free greens to the community."</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-gray-300 py-12 px-6">
        <div class="container mx-auto grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
                <h3 class="text-2xl font-bold text-white mb-4">FarmFresh</h3>
                <p>Empowering local farmers by connecting them directly with you.</p>
            </div>
            <div>
                <h4 class="text-white font-bold mb-4">Company</h4>
                <ul>
                    <li><a href="#" class="hover:text-green-400">Our Story</a></li>
                    <li><a href="#" class="hover:text-green-400">Privacy Policy</a></li>
                    <li><a href="#" class="hover:text-green-400">Terms of Service</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-white font-bold mb-4">Support</h4>
                <ul>
                    <li><a href="#" class="hover:text-green-400">FAQs</a></li>
                    <li><a href="#" class="hover:text-green-400">Shipping Info</a></li>
                    <li><a href="#" class="hover:text-green-400">Contact Us</a></li>
                </ul>
            </div>
            <div>
                <h4 class="text-white font-bold mb-4">Newsletter</h4>
                <div class="flex">
                    <input type="email" placeholder="Email" class="p-2 rounded-l-md w-full text-gray-800">
                    <button class="bg-green-600 px-4 py-2 rounded-r-md hover:bg-green-700">Join</button>
                </div>
            </div>
        </div>
        <div class="text-center mt-12 border-t border-gray-700 pt-8">
            <p>&copy; 2023 FarmFresh Marketplace. All rights reserved.</p>
        </div>
    </footer>

</body>
</html>



