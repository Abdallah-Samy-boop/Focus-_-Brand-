<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FOCUS — Modern Street Wear</title>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;700;900&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary: #000000;
            --accent: #555;
            --bg: #ffffff;
            --card-bg: #fdfdfd;
            --transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Cairo', sans-serif;
            background: var(--bg);
            color: var(--primary);
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Navbar */
        nav {
            position: fixed;
            top: 0; width: 100%;
            padding: 20px 5%;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1000;
            border-bottom: 1px solid #eee;
        }

        .logo { font-weight: 900; font-size: 24px; letter-spacing: 4px; }

        /* Hero Section */
        .hero {
            height: 100vh;
            background: #000;
            color: white;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            position: relative;
            background-image: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://images.unsplash.com/photo-1554568218-0f1715e72254?q=80&w=1887&auto=format&fit=crop'); /* صورة خلفية افتراضية */
            background-size: cover;
            background-position: center;
        }

        .hero h1 { 
            font-size: clamp(50px, 10vw, 120px); 
            font-weight: 900; 
            letter-spacing: 20px;
            margin-bottom: 10px;
            text-transform: uppercase;
        }

        .hero p { font-size: 1.2rem; opacity: 0.8; letter-spacing: 2px; }

        .btn-main {
            margin-top: 30px;
            padding: 15px 40px;
            background: white;
            color: black;
            border: none;
            font-weight: bold;
            text-transform: uppercase;
            cursor: pointer;
            transition: var(--transition);
        }

        .btn-main:hover { transform: scale(1.05); background: #eee; }

        /* Section Styling */
        .section { padding: 100px 5%; max-width: 1400px; margin: auto; }
        .section-title { text-align: center; margin-bottom: 60px; font-size: 2rem; letter-spacing: 2px; }

        /* Products Grid */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
        }

        .product-card {
            position: relative;
            overflow: hidden;
            cursor: pointer;
            transition: var(--transition);
        }

        .img-container {
            overflow: hidden;
            background: #f4f4f4;
            aspect-ratio: 3/4;
        }

        .product-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }

        .product-card:hover img { transform: scale(1.1); }

        .product-info { padding: 15px 0; text-align: center; }
        .product-info h3 { font-weight: 400; font-size: 1.1rem; }
        .product-info .price { font-weight: 700; color: var(--accent); margin-top: 5px; }

        /* Product Detail Page */
        #productPage {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: white;
            z-index: 2000;
            overflow-y: auto;
            padding-top: 80px;
        }

        .detail-container {
            display: flex;
            flex-wrap: wrap;
            max-width: 1200px;
            margin: auto;
            padding: 20px;
        }

        .detail-gallery { flex: 1; min-width: 300px; position: relative; }
        .detail-info { flex: 1; min-width: 300px; padding: 40px; }

        .slider { width: 100%; aspect-ratio: 3/4; position: relative; background: #eee; overflow: hidden; }
        .slider img { 
            position: absolute; width: 100%; height: 100%; object-fit: cover; 
            opacity: 0; transition: opacity 0.5s ease;
        }
        .slider img.active { opacity: 1; }

        .controls {
            position: absolute; bottom: 20px; left: 50%; transform: translateX(-50%);
            display: flex; gap: 10px;
        }
        .controls button {
            background: white; border: none; width: 40px; height: 40px; border-radius: 50%;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1); cursor: pointer;
        }

        .detail-info h1 { font-size: 2.5rem; margin-bottom: 10px; }
        .detail-info select {
            width: 100%; padding: 12px; margin: 10px 0;
            border: 1px solid #ddd; outline: none;
        }

        .add-btn {
            background: #000; color: white; width: 100%; padding: 18px;
            border: none; margin-top: 20px; cursor: pointer; font-weight: bold;
        }

        /* Cart Drawer */
        .cart-section {
            background: #f9f9f9;
            padding: 50px 5%;
            border-top: 1px solid #eee;
        }
        .cart-container { max-width: 600px; margin: auto; background: white; padding: 30px; border-radius: 4px; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .cart-item { display: flex; justify-content: space-between; border-bottom: 1px solid #eee; padding: 15px 0; }
        .remove-btn { color: #ff4444; border: none; background: none; cursor: pointer; }

        .whatsapp-btn {
            background: #25D366; color: white; width: 100%; padding: 15px;
            border: none; border-radius: 4px; font-size: 1.1rem; font-weight: bold;
            cursor: pointer; margin-top: 20px;
        }

        @media (max-width: 768px) {
            .detail-info { padding: 20px; }
            .hero h1 { letter-spacing: 10px; }
        }
    </style>
</head>
<body>

    <nav>
        <div class="logo">FOCUS</div>
        <div style="cursor: pointer;" onclick="document.getElementById('cart').scrollIntoView({behavior:'smooth'})">🛒 العربة</div>
    </nav>

    <div id="home">
        <section class="hero">
            <h1>FOCUS</h1>
            <p>STREETWEAR COLLECTION 2024</p>
            <button class="btn-main" onclick="document.getElementById('shop').scrollIntoView({behavior:'smooth'})">اكتشف المجموعة</button>
        </section>

        <section class="section" id="shop">
            <h2 class="section-title">الأكثر مبيعاً</h2>
            <div class="products-grid">
                <div class="product-card" onclick="openProduct('hoodie')">
                    <div class="img-container">
                        <img src="https://images.unsplash.com/photo-1556821840-3a63f95609a7?q=80&w=1887&auto=format&fit=crop" alt="Hoodie">
                    </div>
                    <div class="product-info">
                        <h3>Focus Oversized Hoodie</h3>
                        <p class="price">600 جنيه</p>
                    </div>
                </div>

                <div class="product-card" onclick="openProduct('pants')">
                    <div class="img-container">
                        <img src="https://images.unsplash.com/photo-1542272604-787c3835535d?q=80&w=1926&auto=format&fit=crop" alt="Pants">
                    </div>
                    <div class="product-info">
                        <h3>Urban Cargo Pants</h3>
                        <p class="price">550 جنيه</p>
                    </div>
                </div>
            </div>
        </section>
    </div>

    <div id="productPage">
        <div class="detail-container">
            <div class="detail-gallery">
                <button onclick="goBack()" style="background: none; border: none; cursor: pointer; font-size: 1rem; margin-bottom: 20px;">✕ إغلاق</button>
                <div class="slider" id="slider">
                    </div>
                <div class="controls">
                    <button onclick="move(-1)">❮</button>
                    <button onclick="move(1)">❯</button>
                </div>
            </div>

            <div class="detail-info">
                <h1 id="name">اسم المنتج</h1>
                <p id="price" style="font-size: 1.5rem; font-weight: bold; color: var(--accent);"></p>
                <p style="margin: 20px 0; color: #666;">قطن مصري 100% عالي الجودة، تصميم مريح يناسب الجنسين.</p>
                
                <label>اللون</label>
                <select id="color">
                    <option>أسود ملكي</option>
                    <option>أبيض ناصع</option>
                    <option>رمادي دخاني</option>
                </select>

                <label>المقاس</label>
                <select id="size">
                    <option>Small</option>
                    <option>Medium</option>
                    <option>Large</option>
                    <option>X-Large</option>
                </select>

                <button class="add-btn" onclick="addFromProduct()">إضافة إلى حقيبة التسوق</button>
            </div>
        </div>
    </div>

    <section class="cart-section" id="cart">
        <div class="cart-container">
            <h2 style="margin-bottom: 20px; text-align: center;">حقيبة التسوق</h2>
            <div id="cartItems">
                </div>
            <div style="margin-top: 30px; border-top: 2px solid #000; padding-top: 20px;">
                <div style="display: flex; justify-content: space-between; font-weight: 900; font-size: 1.3rem;">
                    <span>الإجمالي:</span>
                    <span id="total">0 جنيه</span>
                </div>
                <button class="whatsapp-btn" onclick="checkout()">إتمام الطلب عبر واتساب</button>
            </div>
        </div>
    </section>

    <script>
        // هنا يمكنك إضافة روابط صورك الجديدة في الـ Arrays بالترتيب
        const products = {
            hoodie: {
                name: "Focus Oversized Hoodie",
                price: 600,
                imgs: [
                    "https://images.unsplash.com/photo-1556821840-3a63f95609a7?q=80&w=1887&auto=format&fit=crop",
                    "https://images.unsplash.com/photo-1521572267360-ee0c2909d518?q=80&w=1887&auto=format&fit=crop"
                ]
            },
            pants: {
                name: "Urban Cargo Pants",
                price: 550,
                imgs: [
                    "https://images.unsplash.com/photo-1542272604-787c3835535d?q=80&w=1926&auto=format&fit=crop",
                    "https://images.unsplash.com/photo-1594633312681-425c7b97ccd1?q=80&w=1887&auto=format&fit=crop"
                ]
            }
        };

        let cart = JSON.parse(localStorage.getItem("focus_cart")) || [];
        let currentProduct, currentIndex = 0;

        function openProduct(key) {
            currentProduct = products[key];
            document.body.style.overflow = "hidden"; // منع السكرول عند فتح المنتج
            document.getElementById("productPage").style.display = "block";
            document.getElementById("name").innerText = currentProduct.name;
            document.getElementById("price").innerText = currentProduct.price + " جنيه";

            let slider = document.getElementById("slider");
            slider.innerHTML = "";
            currentProduct.imgs.forEach((src, i) => {
                slider.innerHTML += `<img src="${src}" class="${i === 0 ? 'active' : ''}">`;
            });
            currentIndex = 0;
        }

        function move(dir) {
            let imgs = document.querySelectorAll("#slider img");
            if (imgs.length === 0) return;
            imgs[currentIndex].classList.remove("active");
            currentIndex = (currentIndex + dir + imgs.length) % imgs.length;
            imgs[currentIndex].classList.add("active");
        }

        function goBack() {
            document.getElementById("productPage").style.display = "none";
            document.body.style.overflow = "auto";
        }

        function addFromProduct() {
            cart.push({
                name: currentProduct.name,
                price: currentProduct.price,
                color: document.getElementById("color").value,
                size: document.getElementById("size").value
            });
            save(); render();
            goBack();
            document.getElementById('cart').scrollIntoView({behavior:'smooth'});
        }

        function save() { localStorage.setItem("focus_cart", JSON.stringify(cart)); }

        function removeItem(i) {
            cart.splice(i, 1);
            save(); render();
        }

        function render() {
            let box = document.getElementById("cartItems");
            let total = 0; 
            box.innerHTML = cart.length === 0 ? "<p style='text-align:center; color:#888;'>الحقيبة فارغة</p>" : "";
            
            cart.forEach((item, idx) => {
                total += item.price;
                box.innerHTML += `
                    <div class="cart-item">
                        <div>
                            <strong>${item.name}</strong><br>
                            <small>${item.color} | ${item.size}</small>
                        </div>
                        <div>
                            <span>${item.price} ج.م</span>
                            <button class="remove-btn" onclick="removeItem(${idx})"> (إزالة)</button>
                        </div>
                    </div>`;
            });
            document.getElementById("total").innerText = total + " جنيه";
        }

        function checkout() {
            if (cart.length === 0) { alert("الحقيبة فارغة!"); return; }
            let msg = "طلب جديد من FOCUS:%0A------------------%0A";
            cart.forEach((i, idx) => {
                msg += `${idx+1}- ${i.name} (${i.color} - ${i.size}) = ${i.price}ج%0A`;
            });
            msg += "------------------%0Aالإجمالي: " + document.getElementById("total").innerText;
            window.open(`https://wa.me/201010228751?text=${msg}`);
        }

        render();
    </script>
</body>
</html>    
