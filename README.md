<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>ZynxLab Portfolio</title>
<style>
  :root{ --bg:#f5f5f7; --text:#222; --accent:#6C63FF; --card:#fff; }
  body{ margin:0; font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,'Poppins',sans-serif; background:var(--bg); color:var(--text); transition:background .35s,color .35s; }
  /* Loading Screen */
  #loader{ position:fixed; inset:0; background:linear-gradient(135deg,#0b0b12 0%, #111827 100%); display:flex; align-items:center; justify-content:center; z-index:9999; flex-direction:column; color:#fff; }
  .loader-logo{ font-size:28px; letter-spacing:1px; margin-bottom:18px; transform-origin:center; animation:logoPop .9s ease both; }
  @keyframes logoPop{ from{ opacity:0; transform:scale(.6) rotate(-6deg)} to{opacity:1; transform:scale(1) rotate(0)} }
  .loader-bar{ width:160px; height:6px; background:rgba(255,255,255,0.12); border-radius:999px; overflow:hidden; }
  .loader-bar > i{ display:block; height:100%; width:0%; background:linear-gradient(90deg,var(--accent),#34F5CC); animation:loadProgress 2.2s linear forwards; }
  @keyframes loadProgress{ to{ width:100%; }}

  /* Navbar */
  .navbar{ position:sticky; top:0; z-index:50; display:flex; align-items:center; justify-content:space-between; padding:14px 20px; background:rgba(255,255,255,0.6); backdrop-filter:blur(8px); }
  .brand{ font-weight:700; color:var(--accent);} 
  .nav-links{ display:flex; gap:14px; }
  .nav-links a{ color:inherit; text-decoration:none; font-size:15px; opacity:.85 }

  /* Hero */
  .hero{ padding:80px 18px; text-align:center; background:linear-gradient(180deg,#0f1724 0%, #0b1220 40%); color:#fff; }
  .hero h1{ font-size:36px; margin:0 0 8px }
  .hero .tag{ font-size:16px; opacity:.9 }
  .typewriter{ margin-top:12px; height:30px; font-weight:600 }

  /* Layout */
  .container{ max-width:1100px; margin:0 auto; padding:36px 18px }

  /* Projects grid with 3D tilt and gallery */
  .projects-grid{ display:grid; grid-template-columns:repeat(1,1fr); gap:18px }
  .card{ perspective:1200px }
  .card-inner{ background:var(--card); border-radius:14px; padding:18px; box-shadow:0 8px 30px rgba(2,6,23,.08); transform-style:preserve-3d; transition:transform .25s ease, box-shadow .25s; will-change:transform; }
  .card:hover{ box-shadow:0 18px 50px rgba(2,6,23,.12) }
  .card-media{ height:160px; border-radius:10px; overflow:hidden; margin-bottom:12px; background:linear-gradient(135deg,#ddd,#ccc); display:flex; align-items:center; justify-content:center; color:#666 }
  .card h3{ margin:0 0 8px }
  .card p{ margin:0; opacity:.8 }

  /* Gallery grid */
  .gallery{ display:grid; grid-template-columns:repeat(3,1fr); gap:12px; margin-top:22px }
  .gallery-item{ height:120px; border-radius:10px; overflow:hidden; background:#eee; transform:scale(.98); transition:transform .45s cubic-bezier(.2,.8,.2,1), filter .35s; }
  .gallery-item:hover{ transform:scale(1.02) }

  /* Testimonial slider */
  .slider{ position:relative; overflow:hidden; border-radius:12px; background:linear-gradient(180deg,#ffffff,#f8f9fb); padding:18px; box-shadow:0 8px 30px rgba(2,6,23,.06); }
  .slides{ display:flex; gap:12px; transition:transform .5s cubic-bezier(.2,.8,.2,1); }
  .slide{ min-width:100%; padding:8px 12px }
  .slide p{ margin:0; font-size:15px; }
  .slider-controls{ display:flex; gap:8px; justify-content:center; margin-top:10px }
  .dot{ width:8px; height:8px; border-radius:999px; background:#ddd; cursor:pointer }
  .dot.active{ background:var(--accent) }

  /* Footer */
  footer{ padding:26px 18px; color:#666; text-align:center }

  /* Responsive / Desktop */
  @media(min-width:700px){
    .hero h1{ font-size:48px }
    .projects-grid{ grid-template-columns:repeat(2,1fr) }
    .gallery{ grid-template-columns:repeat(4,1fr) }
  }
  @media(min-width:1100px){
    .projects-grid{ grid-template-columns:repeat(3,1fr) }
    .gallery{ grid-template-columns:repeat(6,1fr) }
  }

  /* Dark mode support */
  body.dark{ --bg:#07070a; --text:#eee; --card:#0f1115 }

</style>
</head>
<body>

<!-- Loading Screen -->
<div id="loader" aria-hidden="false">
  <div class="loader-logo">ZynxLab</div>
  <div class="loader-bar"><i></i></div>
</div>

<!-- Navbar -->
<div class="navbar">
  <div class="brand">ZynxLab</div>
  <nav class="nav-links">
    <a href="#projects">Projects</a>
    <a href="#gallery">Gallery</a>
    <a href="#testimonials">Testimonials</a>
    <a href="#contact">Contact</a>
  </nav>
</div>

<!-- Hero -->
<section class="hero">
  <div class="container">
    <h1>Hi, I'm <span style="color:var(--accent)">Zynx</span></h1>
    <div class="tag">Creative editor & preset maker</div>
    <div class="typewriter" id="typeText"></div>
  </div>
</section>

<!-- Projects -->
<section id="projects" class="container">
  <h2>Projects</h2>
  <div class="projects-grid" id="projectsGrid">
    <!-- cards inserted by JS -->
  </div>
</section>

<!-- Gallery -->
<section id="gallery" class="container">
  <h2>Gallery</h2>
  <div class="gallery" id="galleryGrid">
    <!-- gallery items by JS -->
  </div>
</section>

<!-- Testimonials -->
<section id="testimonials" class="container">
  <h2>Testimonials</h2>
  <div class="slider" id="testimonialSlider">
    <div class="slides" id="slidesWrap">
      <!-- slides injected -->
    </div>
    <div class="slider-controls" id="sliderDots"></div>
  </div>
</section>

<!-- Contact -->
<section id="contact" class="container">
  <h2>Contact</h2>
  <p>DM Instagram atau WA aja bro 🔥</p>
</section>

<footer>© 2025 ZynxLab — Crafted with clean aesthetic vibes.</footer>

<script>
// Helper: create element from HTML
function html(str){ const tpl = document.createElement('template'); tpl.innerHTML = str.trim(); return tpl.content.firstChild; }

// Simulated data (replace with real content later)
const PROJECTS = Array.from({length:6}).map((_,i)=>({title:`Preset ${i+1}`,desc:`Clean & aesthetic preset ${i+1}`}));
const GALLERY = Array.from({length:12}).map((_,i)=>({id:i,caption:`Photo ${i+1}`}));
const TESTIMONIALS = [
  {name:'Alya', text:'Hasilnya rapih & cepat — recommended!'},
  {name:'Rafi', text:'Presetnya pas banget, feedku jadi konsisten.'},
  {name:'Maya', text:'Bantuan laporan rapi, bahasa enak dibaca.'}
];

// Populate projects with 3D tilt effect
const projectsGrid = document.getElementById('projectsGrid');
PROJECTS.forEach((p, idx)=>{
  const node = html(`
    <div class="card">
      <div class="card-inner glass">
        <div class="card-media">IMG ${idx+1}</div>
        <h3>${p.title}</h3>
        <p>${p.desc}</p>
      </div>
    </div>
  `);
  projectsGrid.appendChild(node);
});

// Tilt effect
document.querySelectorAll('.card').forEach(card=>{
  const inner = card.querySelector('.card-inner');
  card.addEventListener('mousemove', e=>{
    const rect = card.getBoundingClientRect();
    const x = (e.clientX - rect.left) / rect.width - .5; // -0.5 .. 0.5
    const y = (e.clientY - rect.top) / rect.height - .5;
    const rotX = (y * 10) * -1; // invert
    const rotY = x * 12;
    inner.style.transform = `rotateX(${rotX}deg) rotateY(${rotY}deg) translateZ(8px)`;
  });
  card.addEventListener('mouseleave', ()=>{ inner.style.transform = 'rotateX(0) rotateY(0) translateZ(0)'; });
});

// Populate gallery
const galleryGrid = document.getElementById('galleryGrid');
GALLERY.forEach(g=>{
  const item = document.createElement('div'); item.className='gallery-item'; item.textContent = g.caption; galleryGrid.appendChild(item);
});

// Auto-animate gallery (staggered reveal)
const galleryItems = document.querySelectorAll('.gallery-item');
galleryItems.forEach((it, i)=>{ it.style.transitionDelay = (i * 60) + 'ms'; });

// Testimonials slider
const slidesWrap = document.getElementById('slidesWrap');
const dotsWrap = document.getElementById('sliderDots');
TESTIMONIALS.forEach((t,i)=>{
  const s = html(`<div class="slide"><p>“${t.text}”</p><small class="small">— ${t.name}</small></div>`);
  slidesWrap.appendChild(s);
  const d = document.createElement('div'); d.className='dot'; d.dataset.index = i; dotsWrap.appendChild(d);
});
let slideIndex = 0;
const dots = dotsWrap.querySelectorAll('.dot');
function showSlide(n){ slideIndex = (n + TESTIMONIALS.length) % TESTIMONIALS.length; slidesWrap.style.transform = `translateX(-${slideIndex * 100}%)`; dots.forEach((d,idx)=> d.classList.toggle('active', idx===slideIndex)); }
showSlide(0);
let sliderTimer = setInterval(()=> showSlide(slideIndex+1), 4200);
dots.forEach(d=> d.addEventListener('click', ()=>{ clearInterval(sliderTimer); showSlide(parseInt(d.dataset.index)); sliderTimer = setInterval(()=> showSlide(slideIndex+1), 4200); }));

// Typewriter (hero)
(function(){ const words = ['Editor','Designer','Creator','Preset Maker']; let wi=0, ci=0, del=false, out=document.getElementById('typeText'); function tick(){ const cur=words[wi]; if(!del){ out.textContent = cur.substring(0, ++ci); if(ci===cur.length){ del=true; setTimeout(tick,1200); return; } } else { out.textContent = cur.substring(0, --ci); if(ci===0){ del=false; wi=(wi+1)%words.length; } } setTimeout(tick, del?60:90); } tick(); })();

// Smooth scroll with safety checks
document.querySelectorAll('a[href^="#"]').forEach(link=>{
  link.addEventListener('click', e=>{
    const href = link.getAttribute('href'); if(!href || href==='#') { e.preventDefault(); return; }
    if(!href.startsWith('#') || href.length<2){ e.preventDefault(); return; }
    const target = document.querySelector(href); if(!target){ e.preventDefault(); return; }
    e.preventDefault(); target.scrollIntoView({behavior:'smooth', block:'start'});
  });
});

// Intersection reveal for cards and gallery
const revealEls = document.querySelectorAll('.glass, .card, .gallery-item, .slide');
if('IntersectionObserver' in window){
  const io = new IntersectionObserver((entries, obs)=>{
    entries.forEach(en=>{
      if(en.isIntersecting){ en.target.style.opacity=1; en.target.style.transform='translateY(0)'; en.target.style.transition='transform .6s ease, opacity .6s'; obs.unobserve(en.target); }
    });
  }, {threshold:0.12});
  revealEls.forEach(el=> io.observe(el));
} else { revealEls.forEach(el=>{ el.style.opacity=1; el.style.transform='translateY(0)'; }); }

// Loading hide after content ready
window.addEventListener('load', ()=>{
  const loader = document.getElementById('loader'); loader.style.transition='opacity .45s ease'; loader.style.opacity=0; setTimeout(()=> loader.remove(),500);
  // small entrance for gallery items
  galleryItems.forEach((it,i)=> setTimeout(()=> it.style.transform='translateY(0) scale(1)', 100 + i*60));
});

// Dark mode toggle (persisted)
(function(){ const btn = document.createElement('button'); btn.innerHTML='🌙'; Object.assign(btn.style,{position:'fixed', right:'18px', bottom:'18px', padding:'10px', borderRadius:'50%', border:'none', background:'#111', color:'#fff', zIndex:9999, cursor:'pointer'}); document.body.appendChild(btn); let darkMode=false; try{ if(localStorage.getItem('zynx_dark')==='1'){ darkMode=true; document.body.classList.add('dark'); btn.innerHTML='☀️'; } }catch(e){} function apply(f){ document.body.classList.toggle('dark', f); btn.innerHTML = f? '☀️' : '🌙'; } btn.addEventListener('click', ()=>{ darkMode=!darkMode; apply(darkMode); try{ localStorage.setItem('zynx_dark', darkMode? '1':'0'); }catch(e){} }); })();

</script>
</body>
</html>
