<!--
  KLOTHE - Single-file website ready for GitHub Pages
  - Save as index.html at your repository root (e.g., kr/klothe/index.html)
  - Commit & push to GitHub, then enable GitHub Pages from the repo settings (use main branch / root)
  - Customize product data, images and social links below

  Features:
  - Responsive layout (mobile-first)
  - Hero with CTA, product grid, product modal, about section, contact form (mailto), footer with social links
  - Simple shopping-cart demo (no payments) stored in localStorage
  - Easy to customize: look for the `PRODUCTS` array in the <script> tag
-->

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Klothe — Streetwear x Formal</title>
  <meta name="description" content="Klothe — Premium streetwear and perfumes. Shop clothes and signature scents.">

  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --muted:#9aa4b2; --accent:#ffd166; --text:#e6eef6;
      --glass: rgba(255,255,255,0.03);
      font-family: 'Poppins', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;background:linear-gradient(180deg,#081025 0%, #071226 60%);color:var(--text);}
    a{color:inherit;text-decoration:none}
    .container{max-width:1100px;margin:0 auto;padding:28px}

    header{display:flex;align-items:center;justify-content:space-between;padding:12px 0}
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:44px;height:44px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#ff8a65);display:flex;align-items:center;justify-content:center;font-weight:700;color:#0b1220}
    nav{display:flex;gap:14px;align-items:center}
    nav a{font-weight:600;color:var(--muted);}
    .btn{background:var(--accent);color:#081225;padding:10px 14px;border-radius:10px;font-weight:700}

    .hero{display:grid;grid-template-columns:1fr;gap:20px;align-items:center;padding:28px 0}
    .hero .left h1{font-size:clamp(28px,6vw,44px);margin:0 0 8px}
    .hero .left p{color:var(--muted);margin:0 0 16px}
    .cta-row{display:flex;gap:12px}

    .card{background:var(--card);padding:16px;border-radius:14px;box-shadow:0 6px 24px rgba(0,0,0,0.45)}

    .products{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:16px;margin-top:20px}
    .product{border-radius:12px;padding:12px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);display:flex;flex-direction:column;gap:8px}
    .product img{width:100%;height:200px;object-fit:cover;border-radius:8px}
    .product .name{font-weight:700}
    .price{font-weight:700}
    .muted{color:var(--muted);font-size:14px}

    footer{padding:28px 0;color:var(--muted)}

    /* Modal */
    .modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,0.6);display:none;align-items:center;justify-content:center;padding:24px}
    .modal{width:100%;max-width:760px;background:var(--card);border-radius:12px;padding:18px;display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .modal img{width:100%;height:320px;object-fit:cover;border-radius:8px}
    .close{background:transparent;border:0;color:var(--muted);font-weight:700}

    /* Cart */
    .cart-toggle{position:fixed;right:20px;bottom:20px;background:var(--card);padding:10px;border-radius:12px;box-shadow:0 6px 18px rgba(0,0,0,0.5)}
    .cart-count{background:var(--accent);color:#081225;padding:6px 8px;border-radius:999px;margin-left:6px;font-weight:700}

    @media(min-width:900px){
      .hero{grid-template-columns:1fr 420px}
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <div class="brand">
        <div class="logo">K</div>
        <div>
          <div style="font-weight:700">Klothe</div>
          <div style="font-size:12px;color:var(--muted)">Streetwear • Formal • Perfumes</div>
        </div>
      </div>
      <nav>
        <a href="#products">Shop</a>
        <a href="#about">About</a>
        <a href="#contact">Contact</a>
        <a class="btn" href="#products">Shop Now</a>
      </nav>
    </header>

    <section class="hero">
      <div class="left">
        <h1>Street style that works with your day.<br><span style="color:var(--accent)">Klothe</span> — made for the move.</h1>
        <p class="muted">Curated clothes and signature perfumes. Free delivery on orders above KES 3,500 (customize in script).</p>
        <div class="cta-row">
          <a class="btn" href="#products">Browse Collection</a>
          <a style="padding:10px 14px;border-radius:10px;background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)" href="#contact">Say hi</a>
        </div>
      </div>

      <aside class="card">
        <div style="font-weight:700;margin-bottom:6px">Featured</div>
        <div style="display:flex;gap:12px;align-items:center">
          <img src="https://images.unsplash.com/photo-1520975915933-8b78eca5d3a1?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder" alt="featured" style="width:110px;height:110px;object-fit:cover;border-radius:10px">
          <div>
            <div style="font-weight:700">Nairobi Jacket</div>
            <div class="muted">Lightweight, sharp silhouette</div>
            <div style="margin-top:8px;font-weight:700">KES 2,400</div>
          </div>
        </div>
      </aside>
    </section>

    <section id="products">
      <h2 style="margin:14px 0 6px">Latest</h2>
      <div class="products" id="productGrid"></div>
    </section>

    <section id="about" style="margin-top:26px">
      <div class="card">
        <h3>About Klothe</h3>
        <p class="muted">Klothe blends streetwear energy with refined tailoring and signature fragrances. Built in Nairobi. We ship across Kenya and selected East African markets.</p>
        <div style="margin-top:10px;display:flex;gap:12px;flex-wrap:wrap">
          <div class="muted">Handmade details</div>
          <div class="muted">Eco-conscious packaging</div>
          <div class="muted">Local manufacturing</div>
        </div>
      </div>
    </section>

    <section id="contact" style="margin-top:20px">
      <div class="card">
        <h3>Contact</h3>
        <p class="muted">Questions? Collaborations? Drop us a message.</p>
        <form onsubmit="contactSubmit(event)">
          <div style="display:flex;gap:10px;flex-wrap:wrap">
            <input id="name" placeholder="Your name" required style="flex:1;padding:10px;border-radius:8px;border:0;background:var(--glass);color:var(--text)">
            <input id="email" placeholder="Email" type="email" required style="flex:1;padding:10px;border-radius:8px;border:0;background:var(--glass);color:var(--text)">
          </div>
          <textarea id="message" placeholder="Message" required style="width:100%;margin-top:10px;padding:10px;border-radius:8px;border:0;background:var(--glass);color:var(--text);height:120px"></textarea>
          <div style="margin-top:10px;display:flex;gap:8px;align-items:center">
            <button class="btn" type="submit">Send</button>
            <div class="muted">Or email us at <a href="mailto:bm1053397@gmail.com" style="color:var(--accent)">bm1053397@gmail.com</a></div>
          </div>
        </form>
      </div>
    </section>

    <footer style="margin-top:26px;display:flex;justify-content:space-between;align-items:center">
      <div class="muted">© <span id="year"></span> Klothe — All rights reserved</div>
      <div style="display:flex;gap:10px;align-items:center">
        <a href="#" title="Instagram">Instagram</a>
        <a href="#" title="Facebook">Facebook</a>
        <a href="#" title="Twitter">X</a>
      </div>
    </footer>
  </div>

  <!-- Cart toggle -->
  <div class="cart-toggle card" id="cartToggle">
    <div style="display:flex;align-items:center;gap:8px">Cart <span class="cart-count" id="cartCount">0</span></div>
  </div>

  <!-- Product modal -->
  <div class="modal-backdrop" id="modalBackdrop">
    <div class="modal card" role="dialog" aria-modal="true">
      <div>
        <img id="modalImg" src="" alt="">
      </div>
      <div>
        <div style="display:flex;justify-content:space-between;align-items:start">
          <div>
            <h3 id="modalName"></h3>
            <div class="muted" id="modalCategory"></div>
          </div>
          <button class="close" onclick="closeModal()">✕</button>
        </div>
        <p id="modalDesc" class="muted" style="margin-top:10px"></p>
        <div style="margin-top:12px;font-weight:700" id="modalPrice"></div>
        <div style="margin-top:14px;display:flex;gap:8px">
          <button class="btn" onclick="addToCartModal()">Add to cart</button>
          <button style="padding:10px 14px;border-radius:10px;background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)" onclick="closeModal()">Close</button>
        </div>
      </div>
    </div>
  </div>

  <script>
    // ====== CUSTOMIZE PRODUCTS HERE ======
    const PRODUCTS = [
      {id:1,name:'Nairobi Jacket',category:'Clothes',price:2400,desc:'Lightweight jacket with clean tailoring.',img:'https://images.unsplash.com/photo-1593032465177-07c7f5f3d6a6?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder'},
      {id:2,name:'Street Tee - Black',category:'Clothes',price:950,desc:'100% cotton, relaxed fit.',img:'https://images.unsplash.com/photo-1512436991641-6745cdb1723f?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder'},
      {id:3,name:'Signature Eau de Parfum',category:'Perfumes',price:4500,desc:'Warm amber with citrus top notes.',img:'https://images.unsplash.com/photo-1543340713-3baf5b2d0e1d?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder'},
      {id:4,name:'Tailored Chinos',category:'Clothes',price:1800,desc:'Tapered, comfortable stretch fabric.',img:'https://images.unsplash.com/photo-1514996937319-344454492b37?q=80&w=800&auto=format&fit=crop&ixlib=rb-4.0.3&s=placeholder'}
    ];

    // Render products
    const grid = document.getElementById('productGrid');
    function renderProducts(){
      grid.innerHTML = '';
      PRODUCTS.forEach(p=>{
        const el = document.createElement('div'); el.className='product card';
        el.innerHTML = `
          <img src="${p.img}" alt="${p.name}">
          <div class="name">${p.name}</div>
          <div class="muted">${p.category}</div>
          <div style="display:flex;justify-content:space-between;align-items:center"> <div class="price">KES ${p.price.toLocaleString()}</div> <div><button onclick="openModal(${p.id})" style="padding:8px 10px;border-radius:8px;border:0;background:var(--accent);font-weight:700;color:#081225">View</button></div></div>
        `;
        grid.appendChild(el);
      });
    }
    renderProducts();

    // Modal behavior
    let activeProduct = null;
    function openModal(id){
      const p = PRODUCTS.find(x=>x.id===id); if(!p) return;
      activeProduct = p;
      document.getElementById('modalImg').src = p.img;
      document.getElementById('modalName').textContent = p.name;
      document.getElementById('modalCategory').textContent = p.category;
      document.getElementById('modalDesc').textContent = p.desc;
      document.getElementById('modalPrice').textContent = 'KES ' + p.price.toLocaleString();
      document.getElementById('modalBackdrop').style.display = 'flex';
    }
    function closeModal(){document.getElementById('modalBackdrop').style.display='none'; activeProduct=null}

    // ====== Simple cart (localStorage) ======
    const CART_KEY = 'klothe_cart_v1';
    function getCart(){try{return JSON.parse(localStorage.getItem(CART_KEY))||[]}catch(e){return []}}
    function saveCart(c){localStorage.setItem(CART_KEY,JSON.stringify(c));updateCartCount()}
    function addToCart(id,qty=1){
      const p = PRODUCTS.find(x=>x.id===id); if(!p) return;
      const cart = getCart();
      const found = cart.find(x=>x.id===id);
      if(found) found.qty += qty; else cart.push({id:p.id,name:p.name,price:p.price,qty});
      saveCart(cart);
      alert(p.name + ' added to cart');
    }
    function addToCartModal(){ if(activeProduct) addToCart(activeProduct.id); closeModal(); }
    function updateCartCount(){ const c = getCart().reduce((s,i)=>s+i.qty,0); document.getElementById('cartCount').textContent = c }
    updateCartCount();

    // Cart toggle opens a simple cart quickview
    document.getElementById('cartToggle').addEventListener('click', ()=>{
      const cart = getCart();
      if(cart.length===0){ alert('Your cart is empty'); return }
      let text = 'Cart items:\n\n'; let total=0;
      cart.forEach(it=>{ text += `${it.name} x${it.qty} — KES ${ (it.price*it.qty).toLocaleString() }\n`; total += it.price*it.qty });
      text += '\nTotal: KES ' + total.toLocaleString();
      text += '\n\nTo checkout, contact us at bm1053397@gmail.com or proceed with your preferred mobile payment method.';
      alert(text);
    });

    // Contact form behavior (simple mailto)
    function contactSubmit(e){ e.preventDefault();
      const name = document.getElementById('name').value.trim();
      const email = document.getElementById('email').value.trim();
      const message = document.getElementById('message').value.trim();
      const subject = encodeURIComponent('Klothe website inquiry from ' + name);
      const body = encodeURIComponent(`Name: ${name}\nEmail: ${email}\n\n${message}`);
      window.location.href = `mailto:bm1053397@gmail.com?subject=${subject}&body=${body}`;
    }

    // Small helpers
    document.getElementById('year').textContent = new Date().getFullYear();

    // Close modal on backdrop click
    document.getElementById('modalBackdrop').addEventListener('click', (e)=>{ if(e.target.id==='modalBackdrop') closeModal() });

  </script>
</body>
</html>
