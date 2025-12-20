# Focus-_-Brand-
http://localhost:7700/index.html
<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>FOCUS | Clothing Brand</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    direction:rtl;
    background:#f4f4f4;
}

/* هيرو */
.hero{
    height:100vh;
    background:black;
    color:white;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    animation:fade 2s;
}
.hero h1{
    font-size:60px;
    letter-spacing:5px;
}
.hero p{
    font-size:20px;
}
.hero button{
    margin-top:20px;
    padding:15px 30px;
    background:white;
    border:none;
    font-size:18px;
    cursor:pointer;
}

@keyframes fade{
    from{opacity:0}
    to{opacity:1}
}

/* بانر */
.banner{
    background:#222;
    color:white;
    text-align:center;
    padding:15px;
    font-size:18px;
}

/* أقسام */
.section{
    max-width:1200px;
    margin:auto;
    padding:40px 20px;
}
.section h2{
    text-align:center;
    margin-bottom:25px;
}

/* منتجات */
.products{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(260px,1fr));
    gap:20px;
}
.product{
    background:white;
    padding:15px;
    border-radius:10px;
    text-align:center;
}
.product img{
    width:100%;
    border-radius:10px;
}
select{
    width:100%;
    padding:8px;
    margin:5px 0;
}
.product button{
    width:100%;
    background:black;
    color:white;
    border:none;
    padding:10px;
    margin-top:10px;
    cursor:pointer;
}

/* العربة */
.cart{
    background:white;
    border-radius:10px;
    padding:20px;
}
.cart-item{
    display:flex;
    justify-content:space-between;
    margin-bottom:10px;
}
.cart-item button{
    background:red;
    color:white;
    border:none;
    padding:5px 10px;
}
.checkout{
    width:100%;
    padding:15px;
    background:green;
    color:white;
    border:none;
    font-size:18px;
    cursor:pointer;
}
</style>
</head>

<body>

<!-- الصفحة الرئيسية -->
<div class="hero">
    <h1>FOCUS</h1>
    <p>Modern Street Wear</p>
    <button onclick="document.getElementById('shop').scrollIntoView({behavior:'smooth'})">
        تسوق الآن
    </button>
</div>

<!-- بانر تخفيض -->
<div class="banner">
🔥 خصم لفترة محدودة – اطلب الآن عبر واتساب 🔥
</div>

<!-- المتجر -->
<div class="section" id="shop">

<h2>هودي Focus</h2>
<div class="products">
<div class="product">
<img src="https://images.unsplash.com/photo-1618354691373-d851c5c3a990">
<h3>هودي Focus</h3>
<p>600 جنيه</p>

<select id="hoodieColor">
<option>أسود</option>
<option>أبيض</option>
<option>رمادي</option>
</select>

<select id="hoodieSize">
<option>S</option>
<option>M</option>
<option>L</option>
<option>XL</option>
</select>

<button onclick="addToCart('هودي Focus',600,hoodieColor.value,hoodieSize.value)">
إضافة للعربة
</button>
</div>
</div>

<h2>سويت بانتس Focus</h2>
<div class="products">
<div class="product">
<img src="https://images.unsplash.com/photo-1624378439575-d8705ad7ae80">
<h3>سويت بانتس Focus</h3>
<p>500 جنيه</p>

<select id="pantsColor">
<option>أسود</option>
<option>رمادي</option>
</select>

<select id="pantsSize">
<option>S</option>
<option>M</option>
<option>L</option>
<option>XL</option>
</select>

<button onclick="addToCart('سويت بانتس Focus',500,pantsColor.value,pantsSize.value)">
إضافة للعربة
</button>
</div>
</div>

</div>

<!-- عربة التسوق -->
<div class="section">
<div class="cart">
<h2>🛒 عربة التسوق</h2>
<div id="cartItems"></div>
<h3 id="total">الإجمالي: 0 جنيه</h3>
<button class="checkout" onclick="checkout()">إتمام الشراء عبر واتساب</button>
</div>
</div>

<script>
let cart=[];
let phoneNumber="201234567890"; // غير الرقم لرقمك

function addToCart(name,price,color,size){
cart.push({name,price,color,size});
renderCart();
}

function removeItem(i){
cart.splice(i,1);
renderCart();
}

function renderCart(){
let box=document.getElementById("cartItems");
let total=0;
box.innerHTML="";
cart.forEach((item,i)=>{
total+=item.price;
box.innerHTML+=`
<div class="cart-item">
<span>${item.name} | لون: ${item.color} | مقاس: ${item.size}</span>
<button onclick="removeItem(${i})">حذف</button>
</div>`;
});
document.getElementById("total").innerText="الإجمالي: "+total+" جنيه";
}

function checkout(){
if(cart.length===0){
alert("العربة فاضية");
return;
}
let msg="طلب جديد من Focus:%0A";
cart.forEach(i=>{
msg+=`- ${i.name} | لون: ${i.color} | مقاس: ${i.size} | ${i.price} جنيه%0A`;
});
let total=cart.reduce((s,i)=>s+i.price,0);
msg+=`%0Aالإجمالي: ${total} جنيه`;
window.open(`https://wa.me/${+201010228751}?text=${msg}`);
}
</script>

</body>
</html>
