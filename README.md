<html lang="th">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>ร้านค้าของคุณ</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #304674;
      margin: 0;
      padding: 16px;
      color: #fff;
    }

    .container {
      max-width: 1000px;
      margin: auto;
    }

    h1 {
      font-size: 1.5rem;
      text-align: center;
      margin-bottom: 24px;
      color: #ffffff;
    }

    .products-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
    }

    .product-card {
      background: rgba(255, 255, 255, 0.05);
      border-radius: 12px;
      padding: 12px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }

    .product-card img {
      width: 100%;
      height: auto;
      max-height: 180px;
      object-fit: contain;
      border-radius: 6px;
      margin-bottom: 10px;
      background-color: white;
      padding: 6px;
    }

    .product-name {
      font-size: 1.1rem;
      font-weight: 600;
      margin-bottom: 6px;
      color: #ffffff;
    }

    .product-price {
      color: #00ff99;
      font-weight: bold;
      font-size: 1rem;
      margin-bottom: 12px;
    }

    .btn-order {
      background-color: #0070f3;
      color: white;
      border: none;
      border-radius: 8px;
      padding: 10px;
      font-size: 1rem;
      cursor: pointer;
      text-decoration: none;
      width: 100%;
      transition: background-color 0.2s ease;
    }

    .btn-order:hover {
      background-color: #005bb5;
    }

    @media (min-width: 480px) {
      .products-grid {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    @media (min-width: 768px) {
      .products-grid {
        grid-template-columns: repeat(3, 1fr);
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>ร้านค้าของคุณ</h1>
    <div id="products" class="products-grid">
      <!-- สินค้าจะโหลดที่นี่ -->
    </div>
  </div>

  <script>
    const API_URL = "https://script.google.com/macros/s/AKfycbx_6wR2lwS-lGfm91QMEqYQIB9L3wmJtRTInDBj_jOuVek4_h1RRd1Ovpd7sCbrj-54/exec"; // 🔁 เปลี่ยนลิงก์ตรงนี้ด้วยของคุณเอง

    async function fetchProducts() {
      try {
        const res = await fetch(API_URL);
        if (!res.ok) throw new Error("โหลดข้อมูลไม่สำเร็จ");
        const products = await res.json();
        renderProducts(products);
      } catch (err) {
        document.getElementById("products").innerHTML = <p style="color:#ffaaaa;">${err.message}</p>;
        console.error(err);
      }
    }

    function renderProducts(products) {
      const container = document.getElementById("products");
      container.innerHTML = "";

      products.forEach(p => {
        const card = document.createElement("div");
        card.className = "product-card";

        const imageUrl = p.ImageURL || "";
        const name = p.Name || "ไม่มีชื่อสินค้า";
        const price = p.Price || "0";
        const orderLink = p.OrderLink || "#";

        card.innerHTML = `
          <img src="${imageUrl}" alt="${name}" />
          <div class="product-name">${name}</div>
          <div class="product-price">฿${price}</div>
          <a href="${orderLink}" target="_blank" class="btn-order">สั่งซื้อ</a>
        `;

        container.appendChild(card);
      });
    }

    fetchProducts();
  </script>
</body>
</html>
