# Nguyen-Thi-Ngoc-Huong.
<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YSL Beauty - Editorial Edition</title>
    <link rel="preconnect" href="https://googleapis.com">
    <link rel="preconnect" href="https://gstatic.com" crossorigin>
    <link href="https://googleapis.com/css2?family=Inter:wght@300;400;500&family=Playfair+Display:ital,wght@0,400;0,500;0,600;1,400;1,500&display=swap" rel="stylesheet">
    <style>
        :root {
            --ysl-black: #000000;
            --ysl-dark-gray: #111111;
            --ysl-mid-gray: #888888;
            --ysl-white: #ffffff;
            --transition-medium: 0.4s ease;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background-color: var(--ysl-black); color: var(--ysl-white); line-height: 1.6; overflow-x: hidden; }
        h1, h2, h3, h4, .logo { font-family: 'Playfair Display', serif; font-weight: 400; }
        .container { max-width: 1300px; margin: 0 auto; padding: 0 40px; }
        header { padding: 22px 0; border-bottom: 1px solid rgba(255,255,255,0.1); position: fixed; width: 100%; top: 0; background: rgba(0,0,0,0.85); backdrop-filter: blur(10px); z-index: 1000; }
        .header-inner { display: flex; justify-content: space-between; align-items: center; }
        .nav-btn { background: transparent; border: none; color: var(--ysl-white); text-transform: uppercase; letter-spacing: 2px; font-size: 0.8rem; cursor: pointer; }
        .logo { font-size: 2.2rem; letter-spacing: 6px; color: var(--ysl-white); text-decoration: none; text-transform: uppercase; }
        .header-right { display: flex; gap: 25px; align-items: center; }
        .btn-outline { padding: 11px 24px; border: 1px solid var(--ysl-white); color: var(--ysl-white); background: transparent; text-transform: uppercase; letter-spacing: 2px; font-size: 0.75rem; cursor: pointer; transition: var(--transition-medium); display: inline-block; text-decoration: none; }
        .btn-outline:hover { background: var(--ysl-white); color: var(--ysl-black); }
        .btn-solid { padding: 12px 24px; border: 1px solid var(--ysl-white); color: var(--ysl-black); background: var(--ysl-white); text-transform: uppercase; letter-spacing: 2px; font-size: 0.75rem; cursor: pointer; width: 100%; font-weight: 500; }
        .sidebar-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.75); z-index: 1999; opacity: 0; visibility: hidden; transition: 0.4s; }
        .sidebar { position: fixed; top: 0; height: 100vh; width: 420px; max-width: 100%; background: var(--ysl-black); border: 1px solid #222; z-index: 2000; transition: transform 0.5s ease; padding: 40px; overflow-y: auto; }
        .sidebar.left { left: 0; transform: translateX(-100%); }
        .sidebar.right { right: 0; transform: translateX(100%); }
        .sidebar.active { transform: translateX(0); }
        .sidebar-overlay.active { opacity: 1; visibility: visible; }
        .close-sidebar { position: absolute; top: 20px; right: 25px; background: transparent; border: none; color: var(--ysl-white); font-size: 2rem; cursor: pointer; }
        .sidebar-title { font-size: 1.8rem; border-bottom: 1px solid rgba(255,255,255,0.2); padding-bottom: 18px; margin-bottom: 28px; font-style: italic; }
        .col-item, .cart-item { display: flex; align-items: center; gap: 18px; margin-bottom: 22px; padding-bottom: 18px; border-bottom: 1px solid rgba(255,255,255,0.1); }
        .col-item img, .cart-item img { width: 70px; height: 80px; object-fit: contain; background: #fff; padding: 4px; }
        .hero { position: relative; width: 100%; min-height: 85vh; display: flex; align-items: center; justify-content: center; padding-top: 85px; overflow: hidden; }
        .hero-img { width: 100%; max-height: 80vh; object-fit: contain; opacity: 0.45; }
        .hero-overlay { position: absolute; inset: 0; background: radial-gradient(circle, rgba(0,0,0,0.3) 0%, rgba(0,0,0,0.85) 100%); }
        .hero-content { position: absolute; z-index: 2; text-align: center; width: 100%; padding: 0 20px; }
        .hero-content h1 { font-size: 4.2rem; text-transform: uppercase; letter-spacing: 10px; margin-bottom: 18px; }
        .hero-content p { font-size: 0.95rem; max-width: 600px; margin: 0 auto 35px; letter-spacing: 3px; text-transform: uppercase; color: #e0e0e0; }
        .promo-banner { border-top: 1px solid rgba(255,255,255,0.12); border-bottom: 1px solid rgba(255,255,255,0.12); padding: 25px 0; background: var(--ysl-dark-gray); }
        .promo-inner { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 20px; }
        .timer-box { font-family: 'Playfair Display', serif; font-size: 1.8rem; letter-spacing: 4px; }
        .section { padding: 90px 0; }
        .section-header { text-align: center; margin-bottom: 60px; }
        .section-header h2 { font-size: 2.8rem; letter-spacing: 4px; text-transform: uppercase; margin-bottom: 10px; }
        .product-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 30px; }
        .product-card { border: 1px solid rgba(255,255,255,0.12); background: var(--ysl-dark-gray); padding: 26px; text-align: center; position: relative; display: flex; flex-direction: column; justify-content: space-between; }
        .badge { position: absolute; top: 16px; right: 16px; background: var(--ysl-white); color: var(--ysl-black); padding: 4px 12px; font-size: 0.7rem; letter-spacing: 2px; text-transform: uppercase; }
        .product-img-box { width: 100%; height: 260px; background: #fff; display: flex; align-items: center; justify-content: center; margin-bottom: 20px; padding: 15px; }
        .product-img-box img { max-width: 100%; max-height: 100%; object-fit: contain; }
        .product-price { font-size: 1.15rem; margin: 15px 0 20px; font-style: italic; }
        .old-price { text-decoration: line-through; color: var(--ysl-mid-gray); font-size: 0.9rem; margin-left: 8px; }
        .modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 2500; display: flex; align-items: center; justify-content: center; opacity: 0; visibility: hidden; transition: 0.4s; padding: 20px; }
        .modal-overlay.active { opacity: 1; visibility: visible; }
        .modal-box { background: var(--ysl-black); width: 100%; max-width: 800px; padding: 40px; border: 1px solid rgba(255,255,255,0.25); position: relative; }
        .sale-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 25px; margin-top: 25px; }
        .sale-item { border: 1px solid rgba(255,255,255,0.15); padding: 20px; text-align: center; }
        .sale-item img { width: 130px; height: 150px; object-fit: contain; background: #fff; padding: 8px; margin-bottom: 14px; }
        .footer-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 45px; margin-bottom: 50px; }
        .footer-col h4 { font-size: 1.3rem; margin-bottom: 18px; letter-spacing: 2px; font-style: italic; text-transform: uppercase; }
        .footer-col p { color: #ccc; margin-bottom: 10px; font-size: 0.95rem; }
        .footer-col a { color: var(--ysl-white); text-decoration: none; }
        .consult-form input { width: 100%; padding: 13px 15px; background: transparent; border: 1px solid rgba(255,255,255,0.3); color: var(--ysl-white); margin-bottom: 14px; }
        .copyright { text-align: center; padding-top: 25px; border-top: 1px solid rgba(255,255,255,0.1); color: var(--ysl-mid-gray); font-size: 0.8rem; letter-spacing: 2px; }
    </style>
</head>
<body>
    <div class="sidebar-overlay" id="overlay" onclick="closeAll()"></div>
    <header>
        <div class="container header-inner">
            <button class="nav-btn" onclick="openSidebar('leftSidebar')">Khám Phá</button>
            <a href="#" class="logo">YSL</a>
            <div class="header-right">
                <button class="nav-btn" onclick="openSidebar('rightSidebar')">Giỏ Hàng (<span id="cartCount">1</span>)</button>
                <a href="#contact" class="btn-outline">Đặt Ngay</a>
            </div>
        </div>
    </header>
    <aside class="sidebar left" id="leftSidebar">
        <button class="close-sidebar" onclick="closeAll()">&times;</button>
        <h2 class="sidebar-title">Bộ Sưu Tập Theo Mùa</h2>
        <div class="col-item"><img src="rouge-pur-couture.png"><div><h4>Rouge Pur Couture</h4><p style="font-size:0.8rem;color:#888;">The Iconic Classic</p></div></div>
        <div class="col-item"><img src="the-bold.png"><div><h4>The Bold</h4><p style="font-size:0.8rem;color:#888;">Phiên Bản Giới Hạn</p></div></div>
        <div class="col-item"><img src="candy-glaze.png"><div><h4>Candy Glaze</h4><p style="font-size:0.8rem;color:#888;">Chăm Sóc Độc Quyền</p></div></div>
        <div class="col-item"><img src="water-stain.png"><div><h4>Water Stain</h4><p style="font-size:0.8rem;color:#888;">Vernis À Lèvres</p></div></div>
        <div class="col-item"><img src="rouge-volupte.png"><div><h4>Rouge Volupté Shine</h4><p style="font-size:0.8rem;color:#888;">Dưỡng Bóng Mềm Mại</p></div></div>
    </aside>
    <aside class="sidebar right" id="rightSidebar">
        <button class="close-sidebar" onclick="closeAll()">&times;</button>
        <h2 class="sidebar-title">Giỏ Hàng Của Bạn</h2>
        <div id="cartItemsContainer"></div>
        <div style="display:flex;justify-content:space-between;font-size:1.2rem;margin:20px 0;padding-top:15px;border-top:1px solid #333;">
            <span>Tổng Cộng</span><span id="cartTotalPrice">990.000đ</span>
        </div>
        <button class="btn-solid" onclick="checkout()">Tiến Hành Thanh Toán</button>
    </aside>
    <section class="hero">
        <img src="logo-ysl.png" alt="YSL Logo" class="hero-img">
        <div class="hero-overlay"></div>
        <div class="hero-content">
```html
    <div class="modal-overlay" id="saleModal">
        <div class="modal-box">
            <button class="close-sidebar" onclick="closeAll()">&times;</button>
            <h2 class="sidebar-title" style="text-align: center;">Ưu Đãi Đặc Quyền</h2>
            <div class="sale-grid">
                <div class="sale-item">
                    <img src="the-bold.png"><h4>Signature The Bold</h4>
                    <p class="product-price">990.000đ <span class="old-price">1.250.000đ</span></p>
                    <button class="btn-outline" onclick="addToCart('Signature The Bold', 990000, 'the-bold.png')">Thêm Vào Giỏ</button>
                </div>
                <div class="sale-item">
                    <img src="candy-glaze.png"><h4>Candy Glaze Set</h4>
                    <p class="product-price">850.000đ <span class="old-price">1.050.000đ</span></p>
                    <button class="btn-outline" onclick="addToCart('Candy Glaze Set', 850000, 'candy-glaze.png')">Thêm Vào Giỏ</button>
                </div>
            </div>
        </div>
    </div>
    <section class="section" id="products">
        <div class="container">
            <div class="section-header"><h2>Tuyệt Tác Son Môi</h2><p style="color:#888;letter-spacing:3px;font-size:0.85rem;">NGHI THỨC LÀM ĐẸP TỐI GIẢN TỪ YSL</p></div>
            <div class="product-grid">
                <div class="product-card">
                    <div><div class="product-img-box"><img src="rouge-pur-couture.png"></div><h3>Rouge Pur Couture</h3><p style="color:#888;font-size:0.85rem;">Khí chất nguyên khối</p><p class="product-price">1.150.000đ</p></div>
                    <button class="btn-outline" onclick="addToCart('Rouge Pur Couture', 1150000, 'rouge-pur-couture.png')">Thêm Vào Giỏ</button>
                </div>
                <div class="product-card">
                    <span class="badge">Sale</span>
                    <div><div class="product-img-box"><img src="the-bold.png"></div><h3>The Bold</h3><p style="color:#888;font-size:0.85rem;">Căng bóng, tỏa sáng</p><p class="product-price">990.000đ <span class="old-price">1.250.000đ</span></p></div>
                    <button class="btn-outline" onclick="addToCart('Signature The Bold', 990000, 'the-bold.png')">Thêm Vào Giỏ</button>
                </div>
                <div class="product-card">
                    <div><div class="product-img-box"><img src="the-slim.png"></div><h3>The Slim</h3><p style="color:#888;font-size:0.85rem;">Thiết kế thon dài thời thượng</p><p class="product-price">1.100.000đ</p></div>
                    <button class="btn-outline" onclick="addToCart('The Slim Matte', 1100000, 'the-slim.png')">Thêm Vào Giỏ</button>
                </div>
                <div class="product-card">
                    <span class="badge">Hot</span>
                    <div><div class="product-img-box"><img src="candy-glaze.png"></div><h3>Candy Glaze</h3><p style="color:#888;font-size:0.85rem;">Chăm sóc đôi môi tuyệt đối</p><p class="product-price">850.000đ <span class="old-price">1.050.000đ</span></p></div>
                    <button class="btn-outline" onclick="addToCart('Candy Glaze Balm', 850000, 'candy-glaze.png')">Thêm Vào Giỏ</button>
                </div>
            </div>
        </div>
    </section>
    <footer id="contact" style="background-color: #000; border-top: 1px solid rgba(255,255,255,0.15); padding: 80px 0 40px;">
        <div class="container">
            <div class="footer-grid">
                <div class="footer-col">
                    <h4>Chuyên Viên YSL</h4>
                    <p>Tư vấn viên: <strong>Ngoc Huong</strong></p>
                    <p>Điện thoại: <a href="tel:0346606376"><strong>0346606376</strong></a></p>
                    <p>Telegram: <a href="https://t.me/ngochuong" target="_blank"><strong>@ngochuong</strong></a></p>
                </div>
                <div class="footer-col">
                    <h4>Cửa Hàng Hiện Tại</h4>
                    <div style="width: 100%; height: 180px; border: 1px solid rgba(255,255,255,0.2); overflow: hidden;">
                        <iframe src="https://maps.google.com/maps?q=Saigon%20Centre,%2065%20L%C3%AA%20L%E1%BB%A3i,%20B%E1%BA%BFn%20Ngh%C3%A9,%20Qu%E1%BA%ADn%201,%20H%E1%BB%93%20Ch%C3%AD%20Minh&t=&z=15&ie=UTF8&iwloc=&output=embed" width="100%" height="100%" style="border:0; filter: grayscale(100%) contrast(1.1);" allowfullscreen="" loading="lazy"></iframe>
                    </div>
                </div>
                <div class="footer-col">
                    <h4>Nhận Tư Vấn Độc Quyền</h4>
                    <form class="consult-form" onsubmit="submitConsult(event)">
                        <input type="text" placeholder="Họ và Tên" required>
                        <input type="tel" placeholder="Số điện thoại" required>
                        <button type="submit" class="btn-outline" style="width: 100%; padding: 14px;">ĐĂNG KÝ TƯ VẤN</button>
                    </form>
                </div>
            </div>
            <div class="copyright">&copy; 2026 Yves Saint Laurent Beauty. All Rights Reserved.</div>
        </div>
    </footer>
    <script>
        let cart = [{ name: 'Signature The Bold', price: 990000, qty: 1, img: 'the-bold.png' }];
        function openSidebar(id) { closeAll(); document.getElementById(id).classList.add('active'); document.getElementById('overlay').classList.add('active'); }
        function openModal() { closeAll(); document.getElementById('saleModal').classList.add('active'); }
        function closeAll() { document.getElementById('leftSidebar').classList.remove('active'); document.getElementById('rightSidebar').classList.remove('active'); document.getElementById('saleModal').classList.remove('active'); document.getElementById('overlay').classList.remove('active'); }
        function renderCart() {
            const c = document.getElementById('cartItemsContainer'); c.innerHTML = ''; let q = 0, p = 0;
            cart.forEach((item, i) => {
                q += item.qty; p += item.price * item.qty;
                c.innerHTML += `<div class="cart-item"><img src="${item.img}"><div style="flex:1"><h4>${item.name}</h4><p style="font-size:0.85rem;color:#888">SL: ${item.qty}</p><p style="font-style:italic">${(item.price*item.qty).toLocaleString('vi-VN')}đ</p><button style="background:none;border:none;color:#888;text-decoration:underline;cursor:pointer;font-size:0.8rem" onclick="removeItem(${i})">Xóa</button></div></div>`;
            });
            document.getElementById('cartCount').innerText = q;
            document.getElementById('cartTotalPrice').innerText = p.toLocaleString('vi-VN') + 'đ';
        }
        function addToCart(name, price, img) { const ex = cart.find(i => i.name === name); if (ex) ex.qty++; else cart.push({ name, price, qty: 1, img }); renderCart(); openSidebar('rightSidebar'); }
        function removeItem(i) { cart.splice(i, 1); renderCart(); }
        function checkout() { if (!cart.length) return alert('Giỏ hàng trống.'); alert('Cảm ơn quý khách! Chuyên viên Ngoc Huong (0346606376) sẽ liên hệ xác nhận đơn hàng ngay.'); closeAll(); }
        function submitConsult(e) { e.preventDefault(); alert('Đăng ký thành công! Tư vấn viên Ngoc Huong sẽ liên hệ với bạn trong ít phút.'); e.target.reset(); }
        let sec = 9930; setInterval(() => { if (sec > 0) { sec--; document.getElementById('countdown').innerText = [Math.floor(sec/3600), Math.floor((sec%3600)/60), sec%60].map(v => String(v).padStart(2,'0')).join(':'); } }, 1000);
        renderCart();
    </script>
</body>
</html>
