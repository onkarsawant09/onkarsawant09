<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>Tiger | Full Stack Developer & MCA Student</title>
  <!-- Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/locomotive-scroll@4.1.4/dist/locomotive-scroll.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background: #05050A;
      font-family: 'Inter', sans-serif;
      color: #EBECF0;
      overflow-x: hidden;
    }

    /* Custom Cursor */
    .cursor-dot, .cursor-ring {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 9999;
      border-radius: 50%;
      opacity: 0;
      transition: opacity 0.2s ease;
    }
    .cursor-dot {
      width: 6px;
      height: 6px;
      background: #E63946;
      transform: translate(-50%, -50%);
    }
    .cursor-ring {
      width: 32px;
      height: 32px;
      border: 1.5px solid rgba(230, 57, 70, 0.5);
      transform: translate(-50%, -50%);
      transition: width 0.3s, height 0.3s, border-color 0.3s;
    }
    body:hover .cursor-dot,
    body:hover .cursor-ring {
      opacity: 1;
    }

    /* Loader */
    .loader {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #05050A;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 10000;
      transition: opacity 0.8s cubic-bezier(0.77, 0, 0.18, 1);
    }
    .loader-content {
      text-align: center;
    }
    .loader-logo {
      font-size: 3rem;
      font-weight: 700;
      letter-spacing: -0.02em;
      background: linear-gradient(135deg, #E63946, #ff8c00);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 1rem;
    }
    .loader-bar {
      width: 200px;
      height: 2px;
      background: #1A1A24;
      border-radius: 4px;
      overflow: hidden;
      margin: 0 auto;
    }
    .loader-progress {
      width: 0%;
      height: 100%;
      background: #E63946;
      transition: width 0.3s ease;
    }
    .loader-percent {
      font-size: 0.9rem;
      margin-top: 0.5rem;
      color: #A0A0B0;
    }

    /* Navbar */
    .navbar {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      width: 85%;
      max-width: 1200px;
      padding: 0.8rem 2rem;
      background: rgba(10, 10, 18, 0.6);
      backdrop-filter: blur(12px);
      border-radius: 60px;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border: 1px solid rgba(255,255,255,0.08);
      transition: all 0.3s;
    }
    .logo {
      font-weight: 700;
      font-size: 1.5rem;
      letter-spacing: -0.02em;
      background: linear-gradient(120deg, #fff, #E63946);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .nav-links {
      display: flex;
      gap: 2rem;
    }
    .nav-links a {
      color: #EBECF0;
      text-decoration: none;
      font-weight: 500;
      font-size: 0.9rem;
      transition: color 0.2s;
      position: relative;
    }
    .nav-links a:hover {
      color: #E63946;
    }
    .mobile-menu {
      display: none;
      font-size: 1.8rem;
      cursor: pointer;
    }
    @media (max-width: 768px) {
      .nav-links {
        position: fixed;
        top: 80px;
        left: 0;
        width: 100%;
        flex-direction: column;
        background: rgba(5,5,10,0.95);
        backdrop-filter: blur(20px);
        padding: 2rem;
        gap: 1.5rem;
        transform: translateY(-150%);
        transition: transform 0.4s;
        border-radius: 0 0 20px 20px;
        text-align: center;
      }
      .nav-links.active {
        transform: translateY(0);
      }
      .mobile-menu {
        display: block;
      }
      .navbar {
        width: 90%;
        padding: 0.5rem 1.5rem;
      }
    }

    /* Sections */
    section {
      padding: 6rem 5%;
      position: relative;
      z-index: 2;
    }
    .container {
      max-width: 1300px;
      margin: 0 auto;
    }
    h2 {
      font-size: 2.8rem;
      font-weight: 600;
      letter-spacing: -0.02em;
      margin-bottom: 2rem;
      background: linear-gradient(135deg, #fff, #E63946);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      display: inline-block;
    }

    /* Hero */
    #hero {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .hero-content {
      z-index: 10;
    }
    .hero-title {
      font-size: 5rem;
      font-weight: 700;
      line-height: 1.1;
      letter-spacing: -0.03em;
      margin-bottom: 1rem;
    }
    .hero-title span {
      display: inline-block;
      opacity: 0;
      transform: translateY(50px);
      animation: staggerReveal 0.6s forwards cubic-bezier(0.2, 0.9, 0.4, 1.1);
    }
    @keyframes staggerReveal {
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    .hero-tagline {
      font-size: 1.2rem;
      color: #A0A0B0;
      margin-top: 1rem;
      backdrop-filter: blur(8px);
    }
    .hero-cta {
      margin-top: 2rem;
      display: flex;
      gap: 1rem;
      justify-content: center;
    }
    .btn {
      padding: 0.8rem 1.8rem;
      border-radius: 40px;
      font-weight: 500;
      text-decoration: none;
      transition: all 0.3s;
      border: 1px solid rgba(230,57,70,0.5);
      background: rgba(230,57,70,0.1);
      color: #fff;
    }
    .btn-primary {
      background: #E63946;
      border: none;
      box-shadow: 0 4px 14px rgba(230,57,70,0.3);
    }
    .btn-primary:hover {
      transform: translateY(-3px);
      background: #ff4d5a;
      box-shadow: 0 10px 25px rgba(230,57,70,0.4);
    }
    .btn-outline:hover {
      border-color: #E63946;
      background: rgba(230,57,70,0.2);
      transform: translateY(-3px);
    }

    /* Timeline */
    .timeline {
      position: relative;
      max-width: 800px;
      margin: 0 auto;
    }
    .timeline-item {
      display: flex;
      gap: 2rem;
      margin-bottom: 2rem;
      opacity: 0;
      transform: translateX(-30px);
      transition: all 0.6s;
    }
    .timeline-item.reveal {
      opacity: 1;
      transform: translateX(0);
    }
    .timeline-year {
      font-weight: 700;
      font-size: 1.4rem;
      color: #E63946;
      min-width: 100px;
    }
    .timeline-desc {
      background: rgba(20,20,30,0.5);
      backdrop-filter: blur(8px);
      padding: 1rem 1.5rem;
      border-radius: 16px;
      border-left: 3px solid #E63946;
    }

    /* Skills Galaxy (CSS only, interactive orbit) */
    .skills-galaxy {
      perspective: 1000px;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
      gap: 1.5rem;
      margin-top: 3rem;
    }
    .skill-orbit {
      animation: float 5s infinite alternate;
      transition: all 0.3s;
      background: rgba(30,30,45,0.5);
      backdrop-filter: blur(8px);
      padding: 0.8rem 1.5rem;
      border-radius: 50px;
      font-weight: 500;
      border: 1px solid rgba(255,255,255,0.05);
      cursor: default;
    }
    .skill-orbit:hover {
      transform: scale(1.1) translateY(-5px);
      background: rgba(230,57,70,0.2);
      border-color: #E63946;
      box-shadow: 0 0 15px rgba(230,57,70,0.3);
    }
    @keyframes float {
      0% { transform: translateY(0px); }
      100% { transform: translateY(-10px); }
    }

    /* Project Cards */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
      gap: 2rem;
    }
    .project-card {
      background: rgba(15,15,25,0.6);
      backdrop-filter: blur(10px);
      border-radius: 24px;
      padding: 1.5rem;
      transition: all 0.4s cubic-bezier(0.2,0.9,0.4,1.1);
      border: 1px solid rgba(255,255,255,0.05);
      transform-style: preserve-3d;
    }
    .project-card:hover {
      transform: translateY(-8px) rotateX(3deg);
      border-color: rgba(230,57,70,0.4);
      box-shadow: 0 20px 40px rgba(0,0,0,0.4);
    }
    .project-title {
      font-size: 1.5rem;
      font-weight: 600;
      margin-bottom: 0.5rem;
    }
    .project-desc {
      color: #A0A0B0;
      margin-bottom: 1rem;
    }
    .project-links {
      display: flex;
      gap: 1rem;
    }
    .project-links a {
      color: #E63946;
      text-decoration: none;
      font-weight: 500;
    }

    /* Social + Contact */
    .social-grid {
      display: flex;
      justify-content: center;
      gap: 2rem;
      flex-wrap: wrap;
      margin: 3rem 0;
    }
    .social-card {
      background: rgba(20,20,30,0.5);
      backdrop-filter: blur(8px);
      padding: 1rem 2rem;
      border-radius: 60px;
      transition: transform 0.3s, background 0.3s;
      text-decoration: none;
      color: #fff;
      display: flex;
      align-items: center;
      gap: 0.8rem;
    }
    .social-card:hover {
      transform: translateY(-5px);
      background: #E63946;
    }
    .contact-form {
      max-width: 600px;
      margin: 0 auto;
      background: rgba(10,10,18,0.6);
      backdrop-filter: blur(12px);
      padding: 2rem;
      border-radius: 32px;
    }
    .form-group {
      margin-bottom: 1rem;
    }
    input, textarea {
      width: 100%;
      padding: 1rem;
      background: #0F0F18;
      border: 1px solid #2A2A3A;
      border-radius: 16px;
      color: #fff;
      font-family: inherit;
    }
    button {
      background: #E63946;
      border: none;
      padding: 1rem;
      border-radius: 40px;
      font-weight: 600;
      color: white;
      width: 100%;
      cursor: pointer;
      transition: 0.2s;
    }
    button:hover {
      background: #ff4d5a;
    }

    footer {
      padding: 2rem;
      text-align: center;
      border-top: 1px solid rgba(255,255,255,0.05);
    }

    /* 3D Canvas */
    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 0;
      pointer-events: none;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <div class="loader" id="loader">
    <div class="loader-content">
      <div class="loader-logo">TIGER</div>
      <div class="loader-bar"><div class="loader-progress" id="progress-bar"></div></div>
      <div class="loader-percent" id="progress-percent">0%</div>
    </div>
  </div>

  <div class="cursor-dot"></div>
  <div class="cursor-ring"></div>

  <nav class="navbar">
    <div class="logo">TIGER</div>
    <div class="nav-links" id="navLinks">
      <a href="#hero">Home</a>
      <a href="#about">About</a>
      <a href="#education">Education</a>
      <a href="#skills">Skills</a>
      <a href="#projects">Projects</a>
      <a href="#contact">Contact</a>
    </div>
    <div class="mobile-menu" id="mobileMenu">☰</div>
  </nav>

  <div id="canvas-container"></div>

  <main data-scroll-container>
    <section id="hero">
      <div class="hero-content container">
        <div class="hero-title">
          <span>Hi,</span> <span>I'm</span> <span style="color:#E63946;">Tiger</span><br>
          <span>Full</span> <span>Stack</span> <span>Developer</span>
        </div>
        <div class="hero-tagline">Student • MCA • Problem Solver • UI/UX Enthusiast</div>
        <div class="hero-cta">
          <a href="#projects" class="btn btn-primary">View Work</a>
          <a href="#contact" class="btn btn-outline">Contact Me</a>
        </div>
      </div>
    </section>

    <section id="about">
      <div class="container">
        <h2>About Me</h2>
        <div style="max-width: 800px; background: rgba(20,20,30,0.4); backdrop-filter: blur(8px); padding: 2rem; border-radius: 32px;">
          <p>I'm a Computer Application student and Full Stack Developer passionate about building modern web experiences. Currently pursuing MCA, I blend creativity with technical precision to craft interfaces that are both beautiful and functional.</p>
          <p style="margin-top: 1rem;">Always learning, always building. My goal: become a software engineer who delivers impact.</p>
        </div>
      </div>
    </section>

    <section id="education">
      <div class="container">
        <h2>Education & Journey</h2>
        <div class="timeline">
          <div class="timeline-item"><div class="timeline-year">2018</div><div class="timeline-desc"><strong>SSC</strong> – First Class with Distinction</div></div>
          <div class="timeline-item"><div class="timeline-year">2020</div><div class="timeline-desc"><strong>HSC</strong> – Science Stream</div></div>
          <div class="timeline-item"><div class="timeline-year">2023</div><div class="timeline-desc"><strong>BBA(CA)</strong> – Bachelor of Business Administration in Computer Applications</div></div>
          <div class="timeline-item"><div class="timeline-year">2025</div><div class="timeline-desc"><strong>MCA</strong> – Master of Computer Applications (Pursuing)</div></div>
          <div class="timeline-item"><div class="timeline-year">Future</div><div class="timeline-desc"><strong>Software Engineer</strong> – Building impactful solutions</div></div>
        </div>
      </div>
    </section>

    <section id="skills">
      <div class="container">
        <h2>Tech Galaxy</h2>
        <div class="skills-galaxy">
          <span class="skill-orbit">HTML5</span> <span class="skill-orbit">CSS3</span> <span class="skill-orbit">JavaScript</span>
          <span class="skill-orbit">React</span> <span class="skill-orbit">Node.js</span> <span class="skill-orbit">PHP</span>
          <span class="skill-orbit">MySQL</span> <span class="skill-orbit">Python</span> <span class="skill-orbit">Git</span>
          <span class="skill-orbit">GitHub</span> <span class="skill-orbit">AI Tools</span> <span class="skill-orbit">Three.js</span>
        </div>
      </div>
    </section>

    <section id="projects">
      <div class="container">
        <h2>Featured Projects</h2>
        <div class="projects-grid">
          <div class="project-card"><div class="project-title">Portfolio 3D</div><div class="project-desc">Interactive 3D portfolio with Three.js and GSAP.</div><div class="project-links"><a href="#">Live Demo</a><a href="#">GitHub</a></div></div>
          <div class="project-card"><div class="project-title">Full Stack App</div><div class="project-desc">MERN stack e‑commerce platform with admin panel.</div><div class="project-links"><a href="#">Live Demo</a><a href="#">GitHub</a></div></div>
          <div class="project-card"><div class="project-title">AI Dashboard</div><div class="project-desc">Analytics dashboard using Python & React.</div><div class="project-links"><a href="#">Live Demo</a><a href="#">GitHub</a></div></div>
        </div>
      </div>
    </section>

    <section id="social">
      <div class="container">
        <h2>Connect with me</h2>
        <div class="social-grid">
          <a href="https://github.com/onkarsawant09" class="social-card">🐙 GitHub</a>
          <a href="https://linkedin.com/in/onkar-sawant-20264a396" class="social-card">🔗 LinkedIn</a>
          <a href="https://instagram.com/tigranomkar_.09" class="social-card">📸 Instagram</a>
          <a href="mailto:tigranomkar09@gmail.com" class="social-card">✉️ Email</a>
        </div>
      </div>
    </section>

    <section id="contact">
      <div class="container">
        <h2>Send a message</h2>
        <form class="contact-form" id="contactForm">
          <div class="form-group"><input type="text" placeholder="Your name" required></div>
          <div class="form-group"><input type="email" placeholder="Email" required></div>
          <div class="form-group"><textarea rows="4" placeholder="Message..."></textarea></div>
          <button type="submit">Send Message →</button>
        </form>
      </div>
    </section>

    <footer>
      <p>© 2026 Tiger • Full Stack Developer • MCA Student</p>
      <p style="margin-top: 0.5rem; font-size: 0.8rem;">Based in India</p>
    </footer>
  </main>

  <script src="https://cdn.jsdelivr.net/npm/locomotive-scroll@4.1.4/dist/locomotive-scroll.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
  <script>
    // Loader simulation
    let progress = 0;
    const interval = setInterval(() => {
      progress += Math.random() * 15;
      if (progress >= 100) {
        progress = 100;
        clearInterval(interval);
        document.getElementById('loader').style.opacity = '0';
        setTimeout(() => {
          document.getElementById('loader').style.display = 'none';
        }, 800);
      }
      document.getElementById('progress-bar').style.width = progress + '%';
      document.getElementById('progress-percent').innerText = Math.floor(progress) + '%';
    }, 120);

    // Locomotive Scroll
    const scroll = new LocomotiveScroll({
      el: document.querySelector('[data-scroll-container]'),
      smooth: true,
      multiplier: 0.8,
      smartphone: { smooth: true }
    });

    // GSAP ScrollTrigger
    gsap.registerPlugin(ScrollTrigger);
    ScrollTrigger.scrollerProxy('[data-scroll-container]', {
      scrollTop(value) { if(arguments.length) return scroll.scrollTo(value, 0, 0); return scroll.scroll.instance.scroll.y; },
      getBoundingClientRect() { return { top:0, left:0, width: window.innerWidth, height: window.innerHeight }; }
    });
    ScrollTrigger.addEventListener('refresh', () => scroll.update());
    ScrollTrigger.refresh();

    // reveal timeline items
    const timelineItems = document.querySelectorAll('.timeline-item');
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if(entry.isIntersecting) entry.target.classList.add('reveal');
      });
    }, { threshold: 0.3 });
    timelineItems.forEach(i => observer.observe(i));

    // Custom cursor + magnetic effect
    const cursorDot = document.querySelector('.cursor-dot');
    const cursorRing = document.querySelector('.cursor-ring');
    document.addEventListener('mousemove', (e) => {
      gsap.to(cursorDot, { x: e.clientX, y: e.clientY, duration: 0.1 });
      gsap.to(cursorRing, { x: e.clientX, y: e.clientY, duration: 0.2 });
    });
    document.querySelectorAll('.btn, .social-card, .project-card, .nav-links a').forEach(el => {
      el.addEventListener('mouseenter', () => {
        cursorRing.style.width = '48px';
        cursorRing.style.height = '48px';
        cursorRing.style.borderColor = '#E63946';
      });
      el.addEventListener('mouseleave', () => {
        cursorRing.style.width = '32px';
        cursorRing.style.height = '32px';
        cursorRing.style.borderColor = 'rgba(230,57,70,0.5)';
      });
    });

    // Three.js scene (particles + floating rings)
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    scene.background = null;
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 15;
    const renderer = new THREE.WebGLRenderer({ alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(window.devicePixelRatio);
    container.appendChild(renderer.domElement);

    // Particles
    const particleCount = 1200;
    const geometry = new THREE.BufferGeometry();
    const positions = new Float32Array(particleCount * 3);
    for(let i=0; i<particleCount; i++) {
      positions[i*3] = (Math.random() - 0.5) * 80;
      positions[i*3+1] = (Math.random() - 0.5) * 50;
      positions[i*3+2] = (Math.random() - 0.5) * 40 - 20;
    }
    geometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
    const material = new THREE.PointsMaterial({ color: 0xE63946, size: 0.1, transparent: true, opacity: 0.5 });
    const particles = new THREE.Points(geometry, material);
    scene.add(particles);

    // floating rings
    const ringGeo = new THREE.TorusGeometry(1.5, 0.05, 64, 200);
    const ringMat = new THREE.MeshStandardMaterial({ color: 0xE63946, emissive: 0x330000, roughness: 0.3, metalness: 0.7 });
    const ring = new THREE.Mesh(ringGeo, ringMat);
    ring.position.x = 2;
    ring.position.y = 1;
    scene.add(ring);

    const ring2 = new THREE.Mesh(ringGeo, ringMat);
    ring2.scale.set(0.7,0.7,0.7);
    ring2.position.x = -2;
    ring2.position.y = -1.5;
    scene.add(ring2);

    const ambientLight = new THREE.AmbientLight(0x222222);
    scene.add(ambientLight);
    const light = new THREE.DirectionalLight(0xffffff, 1);
    light.position.set(2,3,4);
    scene.add(light);

    let mouseX = 0, mouseY = 0;
    document.addEventListener('mousemove', (e) => {
      mouseX = (e.clientX / window.innerWidth) * 2 - 1;
      mouseY = (e.clientY / window.innerHeight) * 2 - 1;
    });

    function animate() {
      requestAnimationFrame(animate);
      particles.rotation.y += 0.0005;
      particles.rotation.x += 0.0003;
      ring.rotation.x += 0.01;
      ring.rotation.z += 0.01;
      ring2.rotation.y += 0.015;
      ring2.rotation.x += 0.005;
      // parallax camera
      camera.position.x += (mouseX * 0.5 - camera.position.x) * 0.05;
      camera.position.y += (-mouseY * 0.3 - camera.position.y) * 0.05;
      camera.lookAt(0,0,0);
      renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // mobile menu
    const mobileBtn = document.getElementById('mobileMenu');
    const navLinks = document.getElementById('navLinks');
    mobileBtn.addEventListener('click', () => navLinks.classList.toggle('active'));

    // form submission
    document.getElementById('contactForm').addEventListener('submit', (e) => {
      e.preventDefault();
      alert('✨ Message sent! (demo)');
    });

    // stagger hero reveal
    const spans = document.querySelectorAll('.hero-title span');
    spans.forEach((span, idx) => { span.style.animationDelay = `${idx * 0.05}s`; });
  </script>
</body>
</html>
