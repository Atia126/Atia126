<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>متجر الأناقة والجمال</title>
    <style>
        /* إعدادات عامة */
        body {
            margin: 0;
            font-family: 'Cairo', sans-serif;
            background-color: #fef5f7;
            color: #333;
        }
        header {
            background-color: #e91e63;
            color: white;
            padding: 20px 10px;
            text-align: center;
        }
        header h1 {
            margin: 0;
            font-size: 36px;
        }
        header p {
            margin: 5px 0 0;
            font-size: 18px;
        }
        nav {
            text-align: center;
            padding: 10px 0;
            background-color: #f8f9fa;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        nav a, nav select {
            text-decoration: none;
            margin: 0 15px;
            font-size: 18px;
            color: #e91e63;
            font-weight: bold;
            cursor: pointer;
            border: none;
            background: none;
        }
        nav a:hover {
            color: #333;
        }
        .products {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 20px;
        }
        .product-card {
            background-color: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            text-align: center;
            transition: transform 0.3s;
        }
        .product-card:hover {
            transform: translateY(-5px);
        }
        .product-card img {
            width: 100%;
            height: 250px;
            object-fit: cover;
        }
        .product-card h3 {
            font-size: 20px;
            margin: 15px 0 5px;
            color: #e91e63;
        }
        .product-card p {
            margin: 0 0 10px;
            font-size: 16px;
            color: #666;
        }
        .product-card button {
            background-color: #e91e63;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-bottom: 10px;
        }
        .product-card button:hover {
            background-color: #c2185b;
        }

        footer {
            background-color: #e91e63;
            color: white;
            text-align: center;
            padding: 10px;
            margin-top: 20px;
        }
        footer p {
            margin: 0;
            font-size: 14px;
        }

        .cart {
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: white;
            border: 1px solid #ddd;
            border-radius: 8px;
            padding: 15px;
            width: 300px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
            display: none;
        }
        .cart h3 {
            margin-top: 0;
            color: #e91e63;
        }
        .cart-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        .cart-total {
            font-weight: bold;
            margin: 15px 0;
            text-align: right;
        }
        .cart button {
            background-color: #e91e63;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        .cart button:hover {
            background-color: #c2185b;
        }
    </style>
</head>
<body>
    <header>
        <h1 id="title">متجر الأناقة والجمال</h1>
        <p id="subtitle">كل ما يخص المرأة في مكان واحد</p>
    </header>
    <nav>
        <a href="#clothes" id="nav-clothes">الملابس</a>
        <a href="#beauty" id="nav-beauty">أدوات التجميل</a>
        <a href="#cart" onclick="toggleCart()">عربة التسوق</a>
        <select id="language-selector" onchange="changeLanguage(this.value)">
            <option value="ar">العربية</option>
            <option value="en">English</option>
            <option value="fr">Français</option>
        </select>
    </nav>
    <section class="products" id="clothes">
        <div class="product-card">
            <img src="https://via.placeholder.com/250x250.png?text=Dress" alt="فستان سهرة">
            <h3 id="product-1-name">فستان سهرة</h3>
            <p id="product-1-price">50 يورو</p>
            <button onclick="addToCart('فستان سهرة', 50)">أضف إلى السلة</button>
        </div>
        <div class="product-card">
            <img src="https://via.placeholder.com/250x250.png?text=Bag" alt="حقيبة يد">
            <h3 id="product-2-name">حقيبة يد</h3>
            <p id="product-2-price">30 يورو</p>
            <button onclick="addToCart('حقيبة يد', 30)">أضف إلى السلة</button>
        </div>
    </section>
    <div class="cart" id="cart">
        <h3 id="cart-title">عربة التسوق</h3>
        <div id="cart-items"></div>
        <p class="cart-total" id="cart-total">المجموع: 0 يورو</p>
        <button onclick="checkout()" id="checkout-button">إتمام الشراء</button>
    </div>
    <footer>
        <p>&copy; 2024 <span id="footer-title">متجر الأناقة والجمال</span> - جميع الحقوق محفوظة</p>
    </footer>
    <script>
        let cart = [];
        const translations = {
            ar: {
                title: "متجر الأناقة والجمال",
                subtitle: "كل ما يخص المرأة في مكان واحد",
                navClothes: "الملابس",
                navBeauty: "أدوات التجميل",
                cartTitle: "عربة التسوق",
                checkout: "إتمام الشراء",
                product1: "فستان سهرة",
                product2: "حقيبة يد",
                footer: "متجر الأناقة والجمال",
            },
            en: {
                title: "Elegance & Beauty Store",
                subtitle: "Everything a woman needs in one place",
                navClothes: "Clothes",
                navBeauty: "Beauty Products",
                cartTitle: "Shopping Cart",
                checkout: "Checkout",
                product1: "Evening Dress",
                product2: "Handbag",
                footer: "Elegance & Beauty Store",
            },
            fr: {
                title: "Boutique Élégance et Beauté",
                subtitle: "Tout ce dont une femme a besoin en un seul endroit",
                navClothes: "Vêtements",
                navBeauty: "Produits de Beauté",
                cartTitle: "Panier",
                checkout: "Paiement",
                product1: "Robe de soirée",
                product2: "Sac à main",
                footer: "Boutique Élégance et Beauté",
            }
        };

        function addToCart(name, price) {
            cart.push({ name, price });
            alert(`${name} تمت إضافته إلى السلة.`);
            updateCart();
        }

        function updateCart() {
            const cartItems = document.getElementById('cart-items');
            const cartTotal = document.getElementById('cart-total');
            cartItems.innerHTML = '';
            let total = 0;
            cart.forEach(item => {
                total += item.price;
                cartItems.innerHTML += `<div class="cart-item"><span>${item.name}</span><span>${item.price} €</span></div>`;
            });
            cartTotal.textContent = `المجموع: ${total} €`;
        }

        function toggleCart() {
            const cartDiv = document.getElementById('cart');
            cartDiv.style.display = cartDiv.style.display === 'none' ? 'block' : 'none';
        }

        function checkout() {
            alert('Merci pour vos achats! Vous serez redirigé vers la page de paiement.');
        }

        function changeLanguage(lang) {
            const t = translations[lang];
            document.getElementById('title').textContent = t.title;
            document.getElementById('subtitle').textContent = t.subtitle;
            document.getElementById('nav-clothes').textContent = t.navClothes;
            document.getElementById('nav-beauty').textContent = t.navBeauty;
            document.getElementById('cart-title').textContent = t.cartTitle;
            document.getElementById('checkout-button').textContent = t.checkout;
            document.getElementById('product-1-name').textContent = t.product1;
            document.getElementById('product-2-name').textContent = t.product2;
            document.getElementById('footer-title').textContent = t.footer;
        }

        // Default to Arabic
        changeLanguage('ar');
    </script>
</body>
</html>
