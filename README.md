<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CyberVue Sécurité — Installation & Maintenance de Vidéosurveillance</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&family=Roboto:wght@300;400;500;700&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
:root{
--navy:#0D1B3E;--navy-light:#162D5E;--blue:#1E88E5;--cyan:#00BCD4;
--orange:#E8722A;--orange-light:#FF8A50;--white:#FFFFFF;--gray:#B0BEC5;
--dark-gray:#37474F;--light-bg:#F0F4F8;--success:#4CAF50;--danger:#f44336;
}
html{scroll-behavior:smooth}
body{font-family:'Roboto',sans-serif;color:#333;overflow-x:hidden;background:var(--white)}
h1,h2,h3,h4,h5,h6{font-family:'Poppins',sans-serif}
a{text-decoration:none;color:inherit}

/* NAVBAR */
.navbar{position:fixed;top:0;left:0;right:0;z-index:1000;padding:1rem 2rem;display:flex;align-items:center;justify-content:space-between;transition:all .4s;background:transparent}
.navbar.scrolled{background:rgba(13,27,62,.95);backdrop-filter:blur(20px);padding:.7rem 2rem;box-shadow:0 4px 30px rgba(0,0,0,.3)}
.nav-logo{display:flex;align-items:center;gap:.6rem}
.nav-logo-icon{width:45px;height:45px;background:linear-gradient(135deg,var(--navy),var(--blue));border-radius:50%;display:flex;align-items:center;justify-content:center;border:2px solid var(--cyan);overflow:hidden;flex-shrink:0}
.nav-logo-icon svg{width:26px;height:26px}
.nav-logo-text{font-family:'Poppins',sans-serif;font-size:1.15rem;font-weight:700;color:var(--white);line-height:1.1;white-space:nowrap}
.nav-logo-text span{color:var(--orange)}
.nav-links{display:flex;align-items:center;gap:1.8rem;list-style:none}
.nav-links a{color:rgba(255,255,255,.85);font-size:.8rem;font-weight:500;letter-spacing:.5px;text-transform:uppercase;transition:color .3s;position:relative;font-family:'Poppins',sans-serif}
.nav-links a::after{content:'';position:absolute;bottom:-4px;left:0;width:0;height:2px;background:var(--orange);transition:width .3s}
.nav-links a:hover::after{width:100%}
.nav-links a:hover{color:var(--white)}
.nav-right{display:flex;align-items:center;gap:1rem}
.admin-link{padding:.5rem 1.2rem;background:transparent;color:rgba(255,255,255,.7);border:1px solid rgba(255,255,255,.2);border-radius:30px;font-size:.7rem;font-weight:600;letter-spacing:1px;text-transform:uppercase;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.admin-link:hover{border-color:var(--cyan);color:var(--cyan)}
.admin-link.logged-in{background:var(--cyan);color:var(--white);border-color:var(--cyan)}
.nav-cta{padding:.55rem 1.3rem;background:var(--orange);color:var(--white);border:none;border-radius:30px;font-size:.75rem;font-weight:600;letter-spacing:1px;text-transform:uppercase;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.nav-cta:hover{background:var(--orange-light);transform:translateY(-2px);box-shadow:0 8px 25px rgba(232,114,42,.4)}
.hamburger{display:none;flex-direction:column;cursor:pointer;gap:5px;background:none;border:none;padding:.5rem}
.hamburger span{width:25px;height:2.5px;background:var(--white);transition:all .3s;border-radius:2px}

/* HERO */
.hero{position:relative;min-height:100vh;display:flex;align-items:center;overflow:hidden;background:linear-gradient(135deg,var(--navy) 0%,var(--navy-light) 50%,#0A2540 100%)}
.hero-particles{position:absolute;inset:0;overflow:hidden}
.particle{position:absolute;width:3px;height:3px;background:var(--cyan);border-radius:50%;opacity:.3;animation:float linear infinite}
@keyframes float{0%{transform:translateY(100vh) rotate(0deg);opacity:0}10%{opacity:.3}90%{opacity:.3}100%{transform:translateY(-10vh) rotate(720deg);opacity:0}}
.hero-grid{position:absolute;inset:0;background-image:radial-gradient(circle,var(--cyan) 1px,transparent 1px);background-size:40px 40px;opacity:.1}
.hero-content{position:relative;z-index:2;max-width:1200px;margin:0 auto;padding:8rem 2rem 4rem;display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center}
.hero-text{color:var(--white)}
.hero-badge{display:inline-flex;align-items:center;gap:.5rem;padding:.4rem 1rem;background:rgba(0,188,212,.15);border:1px solid rgba(0,188,212,.3);border-radius:30px;margin-bottom:1.5rem}
.hero-badge-dot{width:8px;height:8px;background:var(--cyan);border-radius:50%;animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(1.5)}}
.hero-badge span{color:var(--cyan);font-size:.75rem;font-weight:600;text-transform:uppercase;letter-spacing:2px}
.hero h1{font-size:clamp(2rem,4.5vw,3.5rem);line-height:1.15;margin-bottom:1.5rem;font-weight:800}
.hero h1 .highlight{color:var(--orange)}
.hero h1 .cyan{color:var(--cyan)}
.hero p{color:rgba(255,255,255,.7);font-size:1.05rem;line-height:1.8;margin-bottom:2.5rem;max-width:500px}
.hero-buttons{display:flex;gap:1rem;flex-wrap:wrap}
.btn-primary{padding:1rem 2.5rem;background:var(--orange);color:var(--white);border:none;border-radius:50px;font-size:.9rem;font-weight:600;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif;letter-spacing:.5px}
.btn-primary:hover{background:var(--orange-light);transform:translateY(-3px);box-shadow:0 15px 35px rgba(232,114,42,.35)}
.btn-secondary{padding:1rem 2.5rem;background:transparent;color:var(--white);border:2px solid rgba(255,255,255,.3);border-radius:50px;font-size:.9rem;font-weight:600;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.btn-secondary:hover{border-color:var(--cyan);color:var(--cyan);transform:translateY(-3px)}
.hero-visual{position:relative;display:flex;align-items:center;justify-content:center}
.hero-camera{position:relative;z-index:2;animation:cameraFloat 4s ease-in-out infinite}
@keyframes cameraFloat{0%,100%{transform:translateY(0) rotate(-5deg)}50%{transform:translateY(-15px) rotate(0deg)}}
.hero-glow{position:absolute;width:300px;height:300px;background:radial-gradient(circle,rgba(0,188,212,.2),transparent 70%);border-radius:50%;top:50%;left:50%;transform:translate(-50%,-50%);animation:glowPulse 3s ease-in-out infinite}
@keyframes glowPulse{0%,100%{transform:translate(-50%,-50%) scale(1);opacity:.5}50%{transform:translate(-50%,-50%) scale(1.2);opacity:.8}}
.hero-ring{position:absolute;width:400px;height:400px;border:1px solid rgba(0,188,212,.15);border-radius:50%;top:50%;left:50%;transform:translate(-50%,-50%);animation:ringRotate 20s linear infinite}
.hero-ring:nth-child(2){width:350px;height:350px;animation-direction:reverse;animation-duration:15s;border-color:rgba(232,114,42,.1)}
@keyframes ringRotate{from{transform:translate(-50%,-50%) rotate(0deg)}to{transform:translate(-50%,-50%) rotate(360deg)}}
.hero-stats{display:flex;gap:2rem;margin-top:3rem}
.hero-stat{text-align:center}
.hero-stat-num{font-family:'Poppins',sans-serif;font-size:2rem;font-weight:800;color:var(--cyan)}
.hero-stat-label{font-size:.75rem;color:rgba(255,255,255,.5);text-transform:uppercase;letter-spacing:1px}

/* SECTIONS */
.services{padding:6rem 2rem;background:var(--light-bg);position:relative}
.services::before{content:'';position:absolute;top:0;left:0;right:0;height:4px;background:linear-gradient(90deg,var(--orange),var(--cyan),var(--blue))}
.section-header{text-align:center;margin-bottom:4rem}
.section-overline{display:inline-flex;align-items:center;gap:.5rem;color:var(--orange);font-size:.75rem;font-weight:700;text-transform:uppercase;letter-spacing:3px;margin-bottom:1rem}
.section-overline::before,.section-overline::after{content:'';width:30px;height:2px;background:var(--orange)}
.section-header h2{font-size:clamp(1.8rem,3.5vw,2.8rem);color:var(--navy);margin-bottom:1rem;font-weight:700}
.section-header p{color:var(--dark-gray);max-width:600px;margin:0 auto;line-height:1.8;font-size:1rem}
.services-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:2rem}
.service-card{background:var(--white);border-radius:16px;padding:2.5rem;transition:all .4s;position:relative;overflow:hidden;border:1px solid #e8edf2}
.service-card:hover{transform:translateY(-10px);box-shadow:0 25px 60px rgba(13,27,62,.12);border-color:var(--cyan)}
.service-card::before{content:'';position:absolute;top:0;left:0;right:0;height:4px;background:linear-gradient(90deg,var(--orange),var(--cyan));transform:scaleX(0);transition:transform .4s;transform-origin:left}
.service-card:hover::before{transform:scaleX(1)}
.service-icon{width:65px;height:65px;border-radius:16px;display:flex;align-items:center;justify-content:center;margin-bottom:1.5rem}
.service-icon svg{width:32px;height:32px}
.service-card h3{font-size:1.2rem;color:var(--navy);margin-bottom:.8rem;font-weight:700}
.service-card p{color:var(--dark-gray);font-size:.9rem;line-height:1.7}
.service-tag{display:inline-block;padding:.3rem .8rem;background:var(--light-bg);border-radius:20px;font-size:.7rem;font-weight:600;color:var(--blue);margin-top:1rem;text-transform:uppercase;letter-spacing:1px}

/* ABOUT */
.about{padding:6rem 2rem;background:var(--white)}
.about-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:4rem;align-items:center}
.about-image{position:relative;border-radius:20px;overflow:hidden;box-shadow:0 30px 60px rgba(13,27,62,.15)}
.about-image svg{width:100%;height:100%;display:block}
.about-image-badge{position:absolute;bottom:1.5rem;left:1.5rem;background:var(--orange);color:var(--white);padding:.8rem 1.5rem;border-radius:12px;font-family:'Poppins',sans-serif;font-weight:700;font-size:.85rem}
.about-content h2{font-size:2.2rem;color:var(--navy);margin-bottom:1.5rem;font-weight:700}
.about-content p{color:var(--dark-gray);line-height:1.9;margin-bottom:1.5rem;font-size:.95rem}
.about-features{display:grid;grid-template-columns:1fr 1fr;gap:1rem;margin-top:2rem}
.about-feature{display:flex;align-items:center;gap:.8rem;padding:.8rem;background:var(--light-bg);border-radius:10px}
.about-feature-icon{width:36px;height:36px;background:linear-gradient(135deg,var(--blue),var(--cyan));border-radius:8px;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.about-feature-icon svg{width:18px;height:18px;stroke:white}
.about-feature span{font-size:.85rem;font-weight:600;color:var(--navy)}

/* OFFERS */
.offers{padding:6rem 2rem;background:linear-gradient(135deg,var(--navy) 0%,var(--navy-light) 100%);position:relative;overflow:hidden}
.offers::before{content:'';position:absolute;top:-50%;right:-20%;width:600px;height:600px;background:radial-gradient(circle,rgba(0,188,212,.08),transparent 70%);border-radius:50%}
.offers .section-header h2{color:var(--white)}
.offers .section-header p{color:rgba(255,255,255,.6)}
.offers .section-overline{color:var(--orange)}
.offers .section-overline::before,.offers .section-overline::after{background:var(--orange)}
.offers-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:2rem;position:relative;z-index:2}
.offer-card{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.1);border-radius:16px;padding:2.5rem;transition:all .4s;backdrop-filter:blur(10px)}
.offer-card:hover{background:rgba(255,255,255,.1);border-color:var(--cyan);transform:translateY(-5px)}
.offer-card.featured{background:linear-gradient(135deg,rgba(232,114,42,.2),rgba(232,114,42,.05));border-color:var(--orange)}
.offer-card.featured:hover{border-color:var(--orange)}
.offer-badge{display:inline-block;padding:.3rem .8rem;background:var(--orange);color:var(--white);border-radius:20px;font-size:.65rem;font-weight:700;text-transform:uppercase;letter-spacing:1px;margin-bottom:1rem}
.offer-card h3{color:var(--white);font-size:1.1rem;margin-bottom:.8rem;font-weight:700}
.offer-card>p{color:rgba(255,255,255,.6);font-size:.85rem;line-height:1.7;margin-bottom:1.5rem}
.offer-card ul{list-style:none}
.offer-card ul li{color:rgba(255,255,255,.7);font-size:.85rem;padding:.4rem 0;display:flex;align-items:center;gap:.5rem}
.offer-card ul li::before{content:'✓';color:var(--cyan);font-weight:700;font-size:.8rem}
.offer-card.featured ul li::before{color:var(--orange)}
.offer-btn{display:inline-block;padding:.8rem 1.8rem;border-radius:30px;font-size:.8rem;font-weight:600;cursor:pointer;transition:all .3s;border:none;font-family:'Poppins',sans-serif;margin-top:1rem}
.btn-outline-light{background:transparent;border:1.5px solid rgba(255,255,255,.3);color:var(--white)}
.btn-outline-light:hover{border-color:var(--cyan);color:var(--cyan)}
.btn-orange{background:var(--orange);color:var(--white)}
.btn-orange:hover{background:var(--orange-light);transform:translateY(-2px)}

/* WHY US */
.why-us{padding:6rem 2rem;background:var(--light-bg)}
.why-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:repeat(4,1fr);gap:2rem}
.why-card{text-align:center;padding:2rem 1.5rem}
.why-number{font-family:'Poppins',sans-serif;font-size:3rem;font-weight:800;background:linear-gradient(135deg,var(--orange),var(--cyan));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;line-height:1;margin-bottom:.5rem}
.why-card h4{font-size:1rem;color:var(--navy);margin-bottom:.5rem;font-weight:700}
.why-card p{font-size:.85rem;color:var(--dark-gray);line-height:1.6}

/* TESTIMONIALS */
.testimonials{padding:6rem 2rem;background:var(--white)}
.testimonials-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:2rem}
.testimonial-card{background:var(--light-bg);border-radius:16px;padding:2rem;position:relative}
.testimonial-card::before{content:'"';position:absolute;top:1rem;right:1.5rem;font-size:4rem;color:var(--orange);opacity:.2;font-family:serif;line-height:1}
.testimonial-stars{color:var(--orange);font-size:.9rem;margin-bottom:1rem}
.testimonial-card p{color:var(--dark-gray);font-size:.9rem;line-height:1.8;margin-bottom:1.5rem;font-style:italic}
.testimonial-author{display:flex;align-items:center;gap:1rem}
.testimonial-avatar{width:45px;height:45px;border-radius:50%;background:linear-gradient(135deg,var(--blue),var(--cyan));display:flex;align-items:center;justify-content:center;color:var(--white);font-weight:700;font-size:1rem;font-family:'Poppins',sans-serif}
.testimonial-name{font-weight:700;color:var(--navy);font-size:.9rem}
.testimonial-role{font-size:.75rem;color:var(--gray)}

/* CONTACT */
.contact{padding:6rem 2rem;background:linear-gradient(135deg,var(--navy) 0%,var(--navy-light) 100%);position:relative}
.contact::before{content:'';position:absolute;bottom:0;left:0;right:0;height:200px;background:linear-gradient(180deg,transparent,rgba(0,188,212,.05))}
.contact-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:4rem;position:relative;z-index:2}
.contact-info h2{color:var(--white);font-size:2.2rem;margin-bottom:1rem;font-weight:700}
.contact-info>p{color:rgba(255,255,255,.6);line-height:1.8;margin-bottom:2rem}
.contact-items{display:flex;flex-direction:column;gap:1.5rem}
.contact-item{display:flex;align-items:flex-start;gap:1rem}
.contact-item-icon{width:50px;height:50px;background:rgba(0,188,212,.1);border:1px solid rgba(0,188,212,.2);border-radius:12px;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.contact-item-icon svg{width:22px;height:22px;stroke:var(--cyan)}
.contact-item-text h4{color:var(--white);font-size:.9rem;font-weight:600;margin-bottom:.3rem}
.contact-item-text p{color:rgba(255,255,255,.6);font-size:.85rem;line-height:1.5}
.contact-item-text a{color:var(--cyan);transition:color .3s}
.contact-item-text a:hover{color:var(--orange)}
.contact-form{background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.1);border-radius:20px;padding:2.5rem;backdrop-filter:blur(10px)}
.contact-form h3{color:var(--white);font-size:1.3rem;margin-bottom:1.5rem;font-weight:700}
.form-group{margin-bottom:1.2rem}
.form-group label{display:block;color:rgba(255,255,255,.7);font-size:.8rem;font-weight:500;margin-bottom:.4rem;text-transform:uppercase;letter-spacing:1px}
.form-group input,.form-group textarea,.form-group select{width:100%;padding:.9rem 1.2rem;background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.15);border-radius:10px;color:var(--white);font-size:.9rem;font-family:'Roboto',sans-serif;transition:border-color .3s;outline:none}
.form-group input::placeholder,.form-group textarea::placeholder{color:rgba(255,255,255,.3)}
.form-group input:focus,.form-group textarea:focus,.form-group select:focus{border-color:var(--cyan)}
.form-group select{cursor:pointer}
.form-group select option{background:var(--navy);color:var(--white)}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:1rem}
.form-submit{width:100%;padding:1rem;background:linear-gradient(135deg,var(--orange),var(--orange-light));color:var(--white);border:none;border-radius:12px;font-size:.9rem;font-weight:700;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif;letter-spacing:1px;text-transform:uppercase;margin-top:.5rem}
.form-submit:hover{transform:translateY(-2px);box-shadow:0 15px 35px rgba(232,114,42,.3)}

/* FOOTER */
.footer{background:var(--navy);padding:4rem 2rem 1.5rem;border-top:1px solid rgba(255,255,255,.05)}
.footer-grid{max-width:1200px;margin:0 auto;display:grid;grid-template-columns:2fr 1fr 1fr 1.5fr;gap:3rem;margin-bottom:3rem}
.footer-brand p{color:rgba(255,255,255,.5);font-size:.85rem;line-height:1.8;margin-top:1rem;max-width:300px}
.footer h4{color:var(--white);font-size:.8rem;font-weight:700;text-transform:uppercase;letter-spacing:2px;margin-bottom:1.2rem}
.footer ul{list-style:none}
.footer ul li{margin-bottom:.7rem}
.footer ul a{color:rgba(255,255,255,.5);font-size:.85rem;transition:color .3s}
.footer ul a:hover{color:var(--cyan)}
.footer-bottom{max-width:1200px;margin:0 auto;padding-top:1.5rem;border-top:1px solid rgba(255,255,255,.08);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:1rem}
.footer-bottom p{color:rgba(255,255,255,.4);font-size:.8rem}

/* SCROLL TOP */
.scroll-top{position:fixed;bottom:2rem;right:2rem;width:50px;height:50px;background:linear-gradient(135deg,var(--orange),var(--orange-light));color:var(--white);border:none;border-radius:50%;cursor:pointer;display:flex;align-items:center;justify-content:center;z-index:100;opacity:0;visibility:hidden;transition:all .3s;box-shadow:0 8px 25px rgba(232,114,42,.3)}
.scroll-top.visible{opacity:1;visibility:visible}
.scroll-top:hover{transform:translateY(-3px)}

/* TOAST */
.toast{position:fixed;bottom:2rem;right:2rem;background:var(--navy);color:var(--white);padding:1rem 1.5rem;border-radius:12px;font-size:.85rem;z-index:5000;transform:translateY(100px);opacity:0;transition:all .4s;display:flex;align-items:center;gap:.8rem;box-shadow:0 10px 30px rgba(0,0,0,.3);border-left:4px solid var(--cyan)}
.toast.show{transform:translateY(0);opacity:1}

/* REVEAL */
.reveal{opacity:0;transform:translateY(40px);transition:all .8s ease}
.reveal.visible{opacity:1;transform:translateY(0)}

/* ============ ADMIN PANEL ============ */
.admin-overlay{position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:9000;opacity:0;visibility:hidden;transition:all .4s}
.admin-overlay.open{opacity:1;visibility:visible}

/* LOGIN MODAL */
.login-modal{position:fixed;top:0;left:0;right:0;bottom:0;z-index:9500;display:flex;align-items:center;justify-content:center;background:rgba(13,27,62,.9);opacity:0;visibility:hidden;transition:all .4s}
.login-modal.open{opacity:1;visibility:visible}
.login-box{background:var(--white);border-radius:20px;padding:3rem;max-width:420px;width:90%;position:relative;animation:fadeInScale .4s ease}
@keyframes fadeInScale{from{opacity:0;transform:scale(.85)}to{opacity:1;transform:scale(1)}}
.login-close{position:absolute;top:1rem;right:1rem;background:none;border:none;font-size:1.5rem;cursor:pointer;color:#999;transition:color .3s;width:35px;height:35px;display:flex;align-items:center;justify-content:center;border-radius:50%}
.login-close:hover{color:var(--navy);background:#f0f0f0}
.login-logo{text-align:center;margin-bottom:2rem}
.login-logo h2{font-size:1.6rem;color:var(--navy);font-weight:700}
.login-logo h2 span{color:var(--orange)}
.login-logo p{color:#999;font-size:.85rem;margin-top:.3rem}
.login-form .form-group{margin-bottom:1rem}
.login-form label{display:block;color:var(--navy);font-size:.8rem;font-weight:600;margin-bottom:.4rem;text-transform:uppercase;letter-spacing:1px}
.login-form input{width:100%;padding:.9rem 1.2rem;background:#f5f7fa;border:2px solid #e8edf2;border-radius:10px;color:var(--navy);font-size:.9rem;font-family:'Roboto',sans-serif;transition:border-color .3s;outline:none}
.login-form input:focus{border-color:var(--cyan)}
.login-error{color:var(--danger);font-size:.8rem;text-align:center;margin-top:.5rem;display:none}
.login-error.show{display:block}
.login-submit{width:100%;padding:1rem;background:linear-gradient(135deg,var(--navy),var(--navy-light));color:var(--white);border:none;border-radius:12px;font-size:.9rem;font-weight:700;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif;letter-spacing:1px;text-transform:uppercase;margin-top:.5rem}
.login-submit:hover{transform:translateY(-2px);box-shadow:0 10px 30px rgba(13,27,62,.3)}
.login-hint{text-align:center;margin-top:1.5rem;padding-top:1.5rem;border-top:1px solid #eee}
.login-hint p{color:#999;font-size:.75rem}
.login-hint code{background:#f0f0f0;padding:.2rem .5rem;border-radius:4px;font-size:.7rem;color:var(--navy)}

/* ADMIN DASHBOARD */
.admin-panel{position:fixed;top:0;left:0;right:0;bottom:0;z-index:9000;display:flex;opacity:0;visibility:hidden;transition:all .4s}
.admin-panel.open{opacity:1;visibility:visible}
.admin-sidebar{width:260px;background:var(--navy);display:flex;flex-direction:column;padding:1.5rem 0;flex-shrink:0;overflow-y:auto}
.admin-sidebar-header{padding:0 1.5rem 2rem;border-bottom:1px solid rgba(255,255,255,.1);margin-bottom:1rem}
.admin-sidebar-header h3{color:var(--white);font-size:1rem}
.admin-sidebar-header h3 span{color:var(--orange)}
.admin-sidebar-header p{color:rgba(255,255,255,.4);font-size:.7rem;margin-top:.3rem}
.admin-nav{list-style:none;flex:1}
.admin-nav li{margin-bottom:.2rem}
.admin-nav a{display:flex;align-items:center;gap:.8rem;padding:.8rem 1.5rem;color:rgba(255,255,255,.6);font-size:.85rem;font-weight:500;transition:all .3s;cursor:pointer;border:none;background:none;width:100%;text-align:left;font-family:'Roboto',sans-serif}
.admin-nav a:hover,.admin-nav a.active{color:var(--white);background:rgba(255,255,255,.08)}
.admin-nav a.active{border-right:3px solid var(--cyan)}
.admin-nav a svg{width:18px;height:18px;flex-shrink:0}
.admin-sidebar-footer{padding:1rem 1.5rem;border-top:1px solid rgba(255,255,255,.1)}
.admin-logout{display:flex;align-items:center;gap:.5rem;color:rgba(255,255,255,.5);font-size:.8rem;cursor:pointer;padding:.5rem 0;transition:color .3s;background:none;border:none;font-family:'Roboto',sans-serif}
.admin-logout:hover{color:var(--danger)}
.admin-logout svg{width:16px;height:16px}
.admin-main{flex:1;background:var(--light-bg);overflow-y:auto;display:flex;flex-direction:column}
.admin-topbar{background:var(--white);padding:1rem 2rem;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #e8edf2;flex-shrink:0}
.admin-topbar h2{font-size:1.3rem;color:var(--navy)}
.admin-topbar-actions{display:flex;gap:.5rem}
.admin-topbar-btn{padding:.5rem 1rem;background:var(--light-bg);border:1px solid #e8edf2;border-radius:8px;font-size:.8rem;cursor:pointer;transition:all .3s;font-family:'Roboto',sans-serif;color:var(--navy)}
.admin-topbar-btn:hover{border-color:var(--cyan);color:var(--cyan)}
.admin-content{flex:1;padding:2rem;overflow-y:auto}
.admin-page{display:none}
.admin-page.active{display:block}

/* ADMIN STATS */
.admin-stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:1.5rem;margin-bottom:2rem}
.admin-stat-card{background:var(--white);border-radius:12px;padding:1.5rem;border:1px solid #e8edf2}
.admin-stat-card .stat-icon{width:45px;height:45px;border-radius:10px;display:flex;align-items:center;justify-content:center;margin-bottom:1rem}
.admin-stat-card .stat-icon svg{width:22px;height:22px}
.admin-stat-card h4{font-size:.75rem;color:#999;text-transform:uppercase;letter-spacing:1px;margin-bottom:.3rem}
.admin-stat-card .stat-value{font-family:'Poppins',sans-serif;font-size:1.8rem;font-weight:700;color:var(--navy)}

/* ADMIN TABLE */
.admin-table-wrap{background:var(--white);border-radius:12px;border:1px solid #e8edf2;overflow:hidden}
.admin-table-header{padding:1.2rem 1.5rem;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #e8edf2}
.admin-table-header h3{font-size:1rem;color:var(--navy)}
.admin-add-btn{padding:.5rem 1.2rem;background:var(--orange);color:var(--white);border:none;border-radius:8px;font-size:.8rem;font-weight:600;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.admin-add-btn:hover{background:var(--orange-light)}
.admin-table{width:100%;border-collapse:collapse}
.admin-table th{padding:.8rem 1.5rem;text-align:left;font-size:.75rem;font-weight:600;text-transform:uppercase;letter-spacing:1px;color:#999;background:#f8f9fa;border-bottom:1px solid #e8edf2}
.admin-table td{padding:.8rem 1.5rem;font-size:.85rem;color:var(--navy);border-bottom:1px solid #f0f0f0}
.admin-table tr:hover td{background:#f8f9fa}
.admin-table-actions{display:flex;gap:.5rem}
.admin-table-actions button{padding:.3rem .8rem;border:1px solid #e8edf2;background:var(--white);border-radius:6px;font-size:.75rem;cursor:pointer;transition:all .3s;font-family:'Roboto',sans-serif}
.admin-table-actions .edit-btn:hover{border-color:var(--blue);color:var(--blue)}
.admin-table-actions .del-btn:hover{border-color:var(--danger);color:var(--danger)}
.featured-tag{background:var(--orange);color:var(--white);padding:.2rem .5rem;border-radius:4px;font-size:.65rem;font-weight:600}

/* ADMIN FORM MODAL */
.form-modal{position:fixed;inset:0;z-index:10000;display:flex;align-items:center;justify-content:center;background:rgba(0,0,0,.6);opacity:0;visibility:hidden;transition:all .3s}
.form-modal.open{opacity:1;visibility:visible}
.form-modal-box{background:var(--white);border-radius:16px;padding:2rem;max-width:600px;width:90%;max-height:85vh;overflow-y:auto;animation:fadeInScale .3s ease}
.form-modal-box h3{font-size:1.3rem;color:var(--navy);margin-bottom:1.5rem}
.admin-form .form-group{margin-bottom:1rem}
.admin-form label{display:block;color:var(--navy);font-size:.8rem;font-weight:600;margin-bottom:.4rem}
.admin-form input,.admin-form textarea,.admin-form select{width:100%;padding:.8rem 1rem;background:#f5f7fa;border:2px solid #e8edf2;border-radius:8px;color:var(--navy);font-size:.9rem;font-family:'Roboto',sans-serif;transition:border-color .3s;outline:none}
.admin-form input:focus,.admin-form textarea:focus,.admin-form select:focus{border-color:var(--cyan)}
.admin-form textarea{resize:vertical;min-height:80px}
.admin-form .form-actions{display:flex;gap:1rem;margin-top:1.5rem}
.admin-form .btn-save{padding:.8rem 2rem;background:var(--orange);color:var(--white);border:none;border-radius:8px;font-weight:600;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.admin-form .btn-save:hover{background:var(--orange-light)}
.admin-form .btn-cancel{padding:.8rem 2rem;background:#f0f0f0;color:#666;border:none;border-radius:8px;font-weight:600;cursor:pointer;transition:all .3s;font-family:'Poppins',sans-serif}
.admin-form .btn-cancel:hover{background:#e0e0e0}
.admin-form .checkbox-group{display:flex;align-items:center;gap:.5rem}
.admin-form .checkbox-group input[type="checkbox"]{width:auto;padding:0}
.admin-form .form-row{display:grid;grid-template-columns:1fr 1fr;gap:1rem}
.admin-form .feature-item{display:flex;align-items:center;gap:.5rem;margin-bottom:.5rem}
.admin-form .feature-item input{flex:1}
.admin-form .feature-item .remove-feature{background:none;border:none;color:var(--danger);cursor:pointer;font-size:1.1rem;padding:.3rem}
.add-feature-btn{background:none;border:1px dashed #ccc;color:#999;padding:.5rem;border-radius:6px;cursor:pointer;font-size:.8rem;width:100%;margin-top:.3rem;transition:all .3s}
.add-feature-btn:hover{border-color:var(--cyan);color:var(--cyan)}

/* EDIT CONTACT SECTION */
.edit-section{background:var(--white);border-radius:12px;border:1px solid #e8edf2;padding:1.5rem;margin-bottom:1.5rem}
.edit-section h4{font-size:1rem;color:var(--navy);margin-bottom:1rem;padding-bottom:.8rem;border-bottom:1px solid #e8edf2}
.edit-section .form-group{margin-bottom:1rem}

/* RESPONSIVE */
@media(max-width:1024px){
.hero-content{grid-template-columns:1fr;text-align:center}
.hero p{margin:0 auto 2.5rem}
.hero-buttons{justify-content:center}
.hero-visual{display:none}
.hero-stats{justify-content:center}
.about-grid{grid-template-columns:1fr}
.contact-grid{grid-template-columns:1fr}
.why-grid{grid-template-columns:repeat(2,1fr)}
.footer-grid{grid-template-columns:1fr 1fr}
.admin-sidebar{width:200px}
}
@media(max-width:768px){
.nav-links{display:none}
.nav-links.mobile-open{display:flex;flex-direction:column;position:absolute;top:100%;left:0;right:0;background:rgba(13,27,62,.98);padding:2rem;gap:1.5rem;backdrop-filter:blur(20px)}
.hamburger{display:flex}
.why-grid{grid-template-columns:1fr 1fr}
.form-row{grid-template-columns:1fr}
.footer-grid{grid-template-columns:1fr}
.about-features{grid-template-columns:1fr}
.hero h1{font-size:2rem}
.admin-panel{flex-direction:column}
.admin-sidebar{width:100%;max-height:60px;overflow:hidden;flex-direction:row;padding:0;align-items:center}
.admin-sidebar.open{max-height:400px;flex-direction:column;padding:1rem 0;align-items:stretch}
.admin-sidebar-header{display:none}
.admin-nav{display:none}
.admin-sidebar.open .admin-nav{display:block}
.admin-sidebar-footer{display:none}
}
@media(max-width:480px){
.why-grid{grid-template-columns:1fr}
.hero-stats{flex-direction:column;gap:1rem}
.admin-form .form-row{grid-template-columns:1fr}
.nav-logo-text{font-size:1rem}
}
</style>
</head>
<body>

<!-- NAVBAR -->
<nav class="navbar" id="navbar">
  <a href="#" class="nav-logo">
    <div class="nav-logo-icon">
      <svg viewBox="0 0 24 24" fill="none" stroke="#00BCD4" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
        <path d="M9.5 2h5l1.5 3h3v4a5 5 0 0 1-10 0V5h3l1.5-3z"/>
        <circle cx="12" cy="12" r="3" fill="#00BCD4" opacity=".3"/>
        <circle cx="12" cy="12" r="1.5" fill="#00BCD4"/>
        <circle cx="10" cy="18" r="1" fill="#E8722A"/>
      </svg>
    </div>
    <div class="nav-logo-text">CyberVue <span>Sécurité</span></div>
  </a>
  <ul class="nav-links" id="navLinks">
    <li><a href="#accueil">Accueil</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#apropos">À Propos</a></li>
    <li><a href="#offres">Offres</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-right">
    <button class="admin-link" id="adminLink" onclick="openLogin()">🔐 Admin</button>
    <a href="#contact" class="nav-cta">Devis Gratuit</a>
    <button class="hamburger" id="hamburger" onclick="toggleMobile()">
      <span></span><span></span><span></span>
    </button>
  </div>
</nav>

<!-- HERO -->
<section class="hero" id="accueil">
  <div class="hero-particles" id="particles"></div>
  <div class="hero-grid"></div>
  <div class="hero-content">
    <div class="hero-text">
      <div class="hero-badge"><div class="hero-badge-dot"></div><span>Sécurité 24/7</span></div>
      <h1 id="heroTitle">Installation & Maintenance de <span class="highlight">Vidéosurveillance</span> <span class="cyan">Professionnelle</span></h1>
      <p id="heroText">Protégez ce qui compte le plus grâce à notre service d'installation de systèmes de vidéosurveillance professionnelle pour maisons, boutiques et entreprises.</p>
      <div class="hero-buttons">
        <a href="#contact" class="btn-primary">Demander un Devis</a>
        <a href="#services" class="btn-secondary">Nos Services</a>
      </div>
      <div class="hero-stats" id="heroStats">
        <div class="hero-stat"><div class="hero-stat-num">500+</div><div class="hero-stat-label">Installations</div></div>
        <div class="hero-stat"><div class="hero-stat-num">24/7</div><div class="hero-stat-label">Assistance</div></div>
        <div class="hero-stat"><div class="hero-stat-num">100%</div><div class="hero-stat-label">Satisfaction</div></div>
      </div>
    </div>
    <div class="hero-visual">
      <div class="hero-glow"></div>
      <div class="hero-ring"></div>
      <div class="hero-ring"></div>
      <div class="hero-camera">
        <svg width="280" height="280" viewBox="0 0 200 200" fill="none">
          <defs>
            <linearGradient id="camGrad" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#162D5E"/><stop offset="100%" style="stop-color:#0D1B3E"/></linearGradient>
            <linearGradient id="lensGrad" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" style="stop-color:#00BCD4"/><stop offset="100%" style="stop-color:#1E88E5"/></linearGradient>
            <filter id="glow"><feGaussianBlur stdDeviation="3" result="coloredBlur"/><feMerge><feMergeNode in="coloredBlur"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
          </defs>
          <ellipse cx="160" cy="80" rx="25" ry="35" fill="#2C3E50" stroke="#455A64" stroke-width="2"/>
          <circle cx="160" cy="75" r="4" fill="#455A64"/><circle cx="155" cy="85" r="4" fill="#455A64"/><circle cx="165" cy="85" r="4" fill="#455A64"/>
          <rect x="40" y="55" width="130" height="90" rx="15" fill="url(#camGrad)" stroke="#37474F" stroke-width="2"/>
          <path d="M40 70 Q40 55 70 55 L130 55 Q155 55 155 70" fill="#1E3A5F" stroke="#455A64" stroke-width="1.5"/>
          <circle cx="115" cy="100" r="35" fill="#0D1B3E" stroke="#37474F" stroke-width="2"/>
          <circle cx="115" cy="100" r="28" fill="#0A1628" stroke="#1E88E5" stroke-width="1.5"/>
          <circle cx="115" cy="100" r="20" fill="url(#lensGrad)" opacity=".3" filter="url(#glow)"/>
          <circle cx="115" cy="100" r="14" fill="#00BCD4" opacity=".5" filter="url(#glow)"/>
          <circle cx="115" cy="100" r="8" fill="#E0F7FA"/><circle cx="115" cy="100" r="3" fill="#FFFFFF"/>
          <circle cx="115" cy="100" r="32" fill="none" stroke="#E8722A" stroke-width="1.5" stroke-dasharray="4 6" opacity=".6"/>
          <circle cx="88" cy="85" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="95" cy="78" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="105" cy="75" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="125" cy="75" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="135" cy="78" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="142" cy="85" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="88" cy="115" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="95" cy="122" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="105" cy="125" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="125" cy="125" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="135" cy="122" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="142" cy="115" r="3" fill="#455A64" stroke="#00BCD4" stroke-width="1" opacity=".5"/>
          <circle cx="60" cy="130" r="4" fill="#E8722A" filter="url(#glow)"/>
          <path d="M160 115 L175 130 L175 160" stroke="#455A64" stroke-width="3" fill="none" stroke-linecap="round"/>
        </svg>
      </div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section class="services" id="services">
  <div class="section-header reveal">
    <div class="section-overline">Ce que nous faisons</div>
    <h2 id="servicesTitle">Nos Services</h2>
    <p id="servicesDesc">Des solutions complètes de vidéosurveillance pour protéger votre domicile, votre boutique ou votre entreprise.</p>
  </div>
  <div class="services-grid" id="servicesGrid"></div>
</section>

<!-- ABOUT -->
<section class="about" id="apropos">
  <div class="about-grid">
    <div class="about-image reveal">
      <svg viewBox="0 0 500 400" fill="none" xmlns="http://www.w3.org/2000/svg" style="width:100%;height:100%;background:linear-gradient(135deg,#0D1B3E,#162D5E)">
        <g opacity=".15" stroke="#00BCD4" stroke-width="1" fill="none">
          <path d="M50 50h80l20 20v40"/><path d="M150 80h60"/><path d="M250 80v60l-30 30"/><path d="M250 170h80l20-20v-40"/>
          <path d="M350 150v80"/><path d="M350 230h60l20 20v40"/><path d="M400 270v80"/>
          <path d="M50 200h100l30 30v60"/><path d="M150 260h80"/><path d="M250 260v80"/>
          <circle cx="130" cy="70" r="5" fill="#00BCD4" opacity=".5"/>
          <circle cx="250" cy="170" r="5" fill="#00BCD4" opacity=".5"/>
          <circle cx="430" cy="270" r="5" fill="#00BCD4" opacity=".5"/>
          <circle cx="150" cy="290" r="5" fill="#00BCD4" opacity=".5"/>
          <circle cx="250" cy="340" r="5" fill="#00BCD4" opacity=".5"/>
          <circle cx="350" cy="230" r="5" fill="#00BCD4" opacity=".5"/>
        </g>
        <g opacity=".3">
          <rect x="80" y="120" width="60" height="200" rx="2" fill="#1E88E5"/>
          <rect x="100" y="140" width="10" height="15" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="115" y="140" width="10" height="15" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="100" y="165" width="10" height="15" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="115" y="165" width="10" height="15" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="160" y="80" width="80" height="240" rx="2" fill="#1E88E5"/>
          <rect x="180" y="100" width="15" height="20" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="200" y="100" width="15" height="20" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="180" y="130" width="15" height="20" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="200" y="130" width="15" height="20" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="260" y="150" width="70" height="170" rx="2" fill="#1E88E5"/>
          <rect x="275" y="170" width="12" height="18" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="295" y="170" width="12" height="18" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="275" y="200" width="12" height="18" rx="1" fill="#00BCD4" opacity=".5"/>
          <rect x="295" y="200" width="12" height="18" rx="1" fill="#00BCD4" opacity=".5"/>
        </g>
        <g transform="translate(180,160)">
          <rect x="0" y="10" width="100" height="60" rx="8" fill="#0D1B3E" stroke="#00BCD4" stroke-width="2"/>
          <circle cx="75" cy="40" r="20" fill="#0D1B3E" stroke="#00BCD4" stroke-width="2"/>
          <circle cx="75" cy="40" r="12" fill="#00BCD4" opacity=".3"/>
          <circle cx="75" cy="40" r="6" fill="#00BCD4"/>
          <circle cx="15" cy="55" r="3" fill="#E8722A"/>
        </g>
        <g transform="translate(300,140)" opacity=".4">
          <path d="M0 30c10-10 20-10 30 0" stroke="#00BCD4" stroke-width="2" fill="none"/>
          <path d="M-5 20c15-15 35-15 50 0" stroke="#00BCD4" stroke-width="2" fill="none"/>
          <path d="M-10 10c20-20 50-20 70 0" stroke="#00BCD4" stroke-width="2" fill="none"/>
          <circle cx="15" cy="35" r="3" fill="#00BCD4"/>
        </g>
        <g transform="translate(100,250)" opacity=".2">
          <path d="M40 0L80 15v35c0 20-20 40-40 50C20 90 0 70 0 50V15L40 0z" fill="none" stroke="#E8722A" stroke-width="2"/>
          <path d="M30 40l10 10 20-20" stroke="#E8722A" stroke-width="3" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
        </g>
      </svg>
      <div class="about-image-badge" id="aboutBadge"> Sécurité Certifiée</div>
    </div>
    <div class="about-content reveal">
      <div class="section-overline" style="justify-content:flex-start">À Propos</div>
      <h2 id="aboutTitle">CyberVue Sécurité</h2>
      <p id="aboutText1">Nous sommes spécialisés dans l'<strong>installation et la maintenance de systèmes de vidéosurveillance</strong> professionnels. Notre mission est de protéger ce qui compte le plus pour vous — votre maison, votre boutique ou votre entreprise.</p>
      <p id="aboutText2">Grâce à notre expertise technique et à des équipements de dernière génération, nous offrons des solutions de sécurité sur mesure, adaptées à chaque client et chaque environnement.</p>
      <div class="about-features" id="aboutFeatures"></div>
    </div>
  </div>
</section>

<!-- OFFERS -->
<section class="offers" id="offres">
  <div class="section-header reveal">
    <div class="section-overline">Vos Offres</div>
    <h2 id="offersTitle">Nos Formules de Sécurité</h2>
    <p id="offersDesc">Des solutions adaptées à chaque besoin, du particulier au professionnel.</p>
  </div>
  <div class="offers-grid" id="offersGrid"></div>
</section>

<!-- WHY US -->
<section class="why-us">
  <div class="section-header reveal">
    <div class="section-overline">Pourquoi Nous</div>
    <h2 id="whyTitle">Nos Chiffres Clés</h2>
    <p id="whyDesc">La confiance de nos clients est notre plus grande récompense.</p>
  </div>
  <div class="why-grid" id="whyGrid"></div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials">
  <div class="section-header reveal">
    <div class="section-overline">Témoignages</div>
    <h2 id="testimonialsTitle">Ce que disent nos clients</h2>
    <p id="testimonialsDesc">La satisfaction de nos clients est notre priorité absolue.</p>
  </div>
  <div class="testimonials-grid" id="testimonialsGrid"></div>
</section>

<!-- CONTACT -->
<section class="contact" id="contact">
  <div class="contact-grid">
    <div class="contact-info reveal">
      <div class="section-overline" style="color:var(--orange);justify-content:flex-start">Contact</div>
      <h2 id="contactTitle">Contactez-Nous</h2>
      <p id="contactDesc">Besoin d'une installation de vidéosurveillance ? Contactez-nous pour un devis gratuit et personnalisé.</p>
      <div class="contact-items" id="contactItems"></div>
    </div>
    <div class="contact-form reveal">
      <h3>Demande de Devis Gratuit</h3>
      <form onsubmit="submitForm(event)">
        <div class="form-row">
          <div class="form-group"><label>Nom complet</label><input type="text" placeholder="Votre nom" required></div>
          <div class="form-group"><label>Téléphone</label><input type="tel" placeholder="+224 ..." required></div>
        </div>
        <div class="form-group"><label>Email</label><input type="email" placeholder="votre@email.com"></div>
        <div class="form-group">
          <label>Type de service</label>
          <select required>
            <option value="">Sélectionnez un service</option>
            <option>Installation maison</option>
            <option>Installation entreprise/boutique</option>
            <option>Maintenance & assistance</option>
            <option>Configuration à distance</option>
            <option>Autre</option>
          </select>
        </div>
        <div class="form-group"><label>Message</label><textarea rows="4" placeholder="Décrivez votre besoin..."></textarea></div>
        <button type="submit" class="form-submit">Envoyer la demande</button>
      </form>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer">
  <div class="footer-grid">
    <div class="footer-brand">
      <a href="#" class="nav-logo">
        <div class="nav-logo-icon" style="width:40px;height:40px">
          <svg viewBox="0 0 24 24" fill="none" stroke="#00BCD4" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M9.5 2h5l1.5 3h3v4a5 5 0 0 1-10 0V5h3l1.5-3z"/><circle cx="12" cy="12" r="1.5" fill="#00BCD4"/>
          </svg>
        </div>
        <div class="nav-logo-text" style="font-size:1.1rem">CyberVue <span>Sécurité</span></div>
      </a>
      <p>Installation et maintenance de systèmes de vidéosurveillance professionnelle. Protégez ce qui compte le plus.</p>
    </div>
    <div><h4>Navigation</h4><ul><li><a href="#accueil">Accueil</a></li><li><a href="#services">Services</a></li><li><a href="#apropos">À Propos</a></li><li><a href="#offres">Offres</a></li><li><a href="#contact">Contact</a></li></ul></div>
    <div><h4>Services</h4><ul><li><a href="#services">Installation CCTV</a></li><li><a href="#services">Surveillance à distance</a></li><li><a href="#services">Maintenance 24/7</a></li><li><a href="#services">Systèmes de sécurité</a></li></ul></div>
    <div><h4>Contact</h4><ul><li><a href="tel:+224629121864">📞 +224 629 12 18 64</a></li><li><a href="#">📍 Derrière la maternité, chez CAPIB Prestation</a></li><li><a href="#">🕐 Assistance 24h/24, 7j/7</a></li></ul></div>
  </div>
  <div class="footer-bottom">
    <p>© 2026 CyberVue Sécurité. Tous droits réservés.</p>
    <p>Installation & Maintenance de Vidéosurveillance</p>
  </div>
</footer>

<!-- SCROLL TOP -->
<button class="scroll-top" id="scrollTop" onclick="window.scrollTo({top:0,behavior:'smooth'})">
  <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><polyline points="18 15 12 9 6 15"/></svg>
</button>

<!-- TOAST -->
<div class="toast" id="toast">
  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="#00BCD4" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>
  <span id="toastMessage">Message envoyé !</span>
</div>

<!-- LOGIN MODAL -->
<div class="login-modal" id="loginModal">
  <div class="login-box">
    <button class="login-close" onclick="closeLogin()">✕</button>
    <div class="login-logo">
      <h2>CyberVue <span>Sécurité</span></h2>
      <p>Panneau d'administration</p>
    </div>
    <form class="login-form" onsubmit="handleLogin(event)">
      <div class="form-group">
        <label>Identifiant</label>
        <input type="text" id="loginUser" placeholder="admin" required>
      </div>
      <div class="form-group">
        <label>Mot de passe</label>
        <input type="password" id="loginPass" placeholder="••••••••" required>
      </div>
      <div class="login-error" id="loginError">Identifiant ou mot de passe incorrect</div>
      <button type="submit" class="login-submit">Se connecter</button>
    </form>
    <div class="login-hint">
      <p>Identifiant : <code>admin</code> | Mot de passe : <code>cybervue2026</code></p>
    </div>
  </div>
</div>

<!-- ADMIN PANEL -->
<div class="admin-panel" id="adminPanel">
  <aside class="admin-sidebar" id="adminSidebar">
    <div class="admin-sidebar-header">
      <h3>CyberVue <span>Sécurité</span></h3>
      <p>Panneau de gestion</p>
    </div>
    <ul class="admin-nav">
      <li><a class="active" onclick="switchAdminPage('dashboard',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>
        Dashboard
      </a></li>
      <li><a onclick="switchAdminPage('offers',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
        Offres
      </a></li>
      <li><a onclick="switchAdminPage('services',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.7 6.3a1 1 0 000 1.4l1.6 1.6a1 1 0 001.4 0l3.77-3.77a6 6 0 01-7.94 7.94l-6.91 6.91a2.12 2.12 0 01-3-3l6.91-6.91a6 6 0 017.94-7.94l-3.76 3.76z"/></svg>
        Services
      </a></li>
      <li><a onclick="switchAdminPage('testimonials',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg>
        Témoignages
      </a></li>
      <li><a onclick="switchAdminPage('contact',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Contact
      </a></li>
      <li><a onclick="switchAdminPage('content',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M11 4H4a2 2 0 00-2 2v14a2 2 0 002 2h14a2 2 0 002-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 013 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
        Contenu
      </a></li>
    </ul>
    <div class="admin-sidebar-footer">
      <button class="admin-logout" onclick="logout()">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
        Déconnexion
      </button>
    </div>
  </aside>
  <main class="admin-main">
    <div class="admin-topbar">
      <h2 id="adminPageTitle">Dashboard</h2>
      <div class="admin-topbar-actions">
        <button class="admin-topbar-btn" onclick="closeAdmin()">← Retour au site</button>
      </div>
    </div>
    <div class="admin-content">

      <!-- DASHBOARD PAGE -->
      <div class="admin-page active" id="page-dashboard">
        <div class="admin-stats" id="adminStats"></div>
        <div class="admin-table-wrap">
          <div class="admin-table-header">
            <h3>📋 Demandes de Devis Récentes</h3>
          </div>
          <table class="admin-table" id="quoteTable">
            <thead><tr><th>Nom</th><th>Téléphone</th><th>Service</th><th>Date</th><th>Statut</th></tr></thead>
            <tbody id="quoteBody"></tbody>
          </table>
        </div>
      </div>

      <!-- OFFERS PAGE -->
      <div class="admin-page" id="page-offers">
        <div class="admin-table-wrap">
          <div class="admin-table-header">
            <h3>🛡️ Gestion des Offres</h3>
            <button class="admin-add-btn" onclick="openOfferForm()">+ Nouvelle Offre</button>
          </div>
          <table class="admin-table">
            <thead><tr><th>Nom</th><th>Description</th><th>Populaire</th><th>Actions</th></tr></thead>
            <tbody id="offersTableBody"></tbody>
          </table>
        </div>
      </div>

      <!-- SERVICES PAGE -->
      <div class="admin-page" id="page-services">
        <div class="admin-table-wrap">
          <div class="admin-table-header">
            <h3>🔧 Gestion des Services</h3>
            <button class="admin-add-btn" onclick="openServiceForm()">+ Nouveau Service</button>
          </div>
          <table class="admin-table">
            <thead><tr><th>Nom</th><th>Description</th><th>Tag</th><th>Actions</th></tr></thead>
            <tbody id="servicesTableBody"></tbody>
          </table>
        </div>
      </div>

      <!-- TESTIMONIALS PAGE -->
      <div class="admin-page" id="page-testimonials">
        <div class="admin-table-wrap">
          <div class="admin-table-header">
            <h3>💬 Gestion des Témoignages</h3>
            <button class="admin-add-btn" onclick="openTestimonialForm()">+ Nouveau Témoignage</button>
          </div>
          <table class="admin-table">
            <thead><tr><th>Client</th><th>Rôle</th><th>Avis</th><th>Actions</th></tr></thead>
            <tbody id="testimonialsTableBody"></tbody>
          </table>
        </div>
      </div>

      <!-- CONTACT PAGE -->
      <div class="admin-page" id="page-contact">
        <div class="edit-section">
          <h4>📞 Informations de Contact</h4>
          <div class="form-group"><label>Téléphone</label><input type="text" id="editPhone" value="+224 629 12 18 64"></div>
          <div class="form-group"><label>Adresse</label><textarea id="editAddress" rows="2">Derrière la maternité
chez CAPIB Prestation</textarea></div>
          <div class="form-group"><label>Horaires</label><textarea id="editHours" rows="2">Assistance 24h/24, 7j/7
Maintenance & Support continu</textarea></div>
          <button class="admin-add-btn" onclick="saveContact()" style="margin-top:1rem">💾 Sauvegarder</button>
        </div>
      </div>

      <!-- CONTENT PAGE -->
      <div class="admin-page" id="page-content">
        <div class="edit-section">
          <h4>🏠 Hero (Bannière principale)</h4>
          <div class="form-group"><label>Titre Hero</label><input type="text" id="editHeroTitle"></div>
          <div class="form-group"><label>Description Hero</label><textarea id="editHeroText" rows="3"></textarea></div>
        </div>
        <div class="edit-section">
          <h4>📊 Statistiques Hero</h4>
          <div class="form-row">
            <div class="form-group"><label>Stat 1 (valeur)</label><input type="text" id="editStat1Val"></div>
            <div class="form-group"><label>Stat 1 (label)</label><input type="text" id="editStat1Label"></div>
          </div>
          <div class="form-row">
            <div class="form-group"><label>Stat 2 (valeur)</label><input type="text" id="editStat2Val"></div>
            <div class="form-group"><label>Stat 2 (label)</label><input type="text" id="editStat2Label"></div>
          </div>
          <div class="form-row">
            <div class="form-group"><label>Stat 3 (valeur)</label><input type="text" id="editStat3Val"></div>
            <div class="form-group"><label>Stat 3 (label)</label><input type="text" id="editStat3Label"></div>
          </div>
        </div>
        <div class="edit-section">
          <h4>ℹ️ À Propos</h4>
          <div class="form-group"><label>Titre</label><input type="text" id="editAboutTitle"></div>
          <div class="form-group"><label>Texte 1</label><textarea id="editAboutText1" rows="3"></textarea></div>
          <div class="form-group"><label>Texte 2</label><textarea id="editAboutText2" rows="3"></textarea></div>
        </div>
        <div class="edit-section">
          <h4>🏷️ Section Offres</h4>
          <div class="form-group"><label>Titre</label><input type="text" id="editOffersTitle"></div>
          <div class="form-group"><label>Description</label><textarea id="editOffersDesc" rows="2"></textarea></div>
        </div>
        <div class="edit-section">
          <h4>📊 Section Chiffres Clés</h4>
          <div class="form-group"><label>Titre</label><input type="text" id="editWhyTitle"></div>
          <div class="form-group"><label>Description</label><textarea id="editWhyDesc" rows="2"></textarea></div>
        </div>
        <div class="edit-section">
          <h4>💬 Section Témoignages</h4>
          <div class="form-group"><label>Titre</label><input type="text" id="editTestimonialsTitle"></div>
          <div class="form-group"><label>Description</label><textarea id="editTestimonialsDesc" rows="2"></textarea></div>
        </div>
        <div class="edit-section">
          <h4>📧 Section Contact</h4>
          <div class="form-group"><label>Titre</label><input type="text" id="editContactTitle"></div>
          <div class="form-group"><label>Description</label><textarea id="editContactDesc" rows="2"></textarea></div>
        </div>
        <button class="admin-add-btn" onclick="saveContent()" style="margin-top:1rem;margin-bottom:2rem">💾 Sauvegarder tout le contenu</button>
      </div>

    </div>
  </main>
</div>

<!-- OFFER FORM MODAL -->
<div class="form-modal" id="offerFormModal">
  <div class="form-modal-box">
    <h3 id="offerFormTitle">Nouvelle Offre</h3>
    <form class="admin-form" id="offerForm" onsubmit="saveOffer(event)">
      <input type="hidden" id="offerId">
      <div class="form-group"><label>Nom de l'offre</label><input type="text" id="offerName" required></div>
      <div class="form-group"><label>Description courte</label><textarea id="offerDesc" rows="2" required></textarea></div>
      <div class="form-group">
        <label>Caractéristiques (une par ligne)</label>
        <div id="offerFeatures">
          <div class="feature-item"><input type="text" placeholder="Ex: 2 à 4 caméras HD"><button type="button" class="remove-feature" onclick="removeFeature(this)">✕</button></div>
        </div>
        <button type="button" class="add-feature-btn" onclick="addFeature()">+ Ajouter une caractéristique</button>
      </div>
      <div class="form-group"><label>Badge (laisser vide si aucun)</label><input type="text" id="offerBadge" placeholder="Ex: ⭐ Populaire"></div>
      <div class="form-group"><label>Featured (mise en avant)</label><div class="checkbox-group"><input type="checkbox" id="offerFeatured"><label for="offerFeatured" style="margin:0;font-weight:400">Mettre en avant</label></div></div>
      <div class="form-actions">
        <button type="submit" class="btn-save">💾 Sauvegarder</button>
        <button type="button" class="btn-cancel" onclick="closeOfferForm()">Annuler</button>
      </div>
    </form>
  </div>
</div>

<!-- SERVICE FORM MODAL -->
<div class="form-modal" id="serviceFormModal">
  <div class="form-modal-box">
    <h3 id="serviceFormTitle">Nouveau Service</h3>
    <form class="admin-form" id="serviceForm" onsubmit="saveService(event)">
      <input type="hidden" id="serviceId">
      <div class="form-group"><label>Nom du service</label><input type="text" id="serviceName" required></div>
      <div class="form-group"><label>Description</label><textarea id="serviceDesc" rows="3" required></textarea></div>
      <div class="form-group"><label>Tag</label><input type="text" id="serviceTag" placeholder="Ex: Maisons & Entreprises"></div>
      <div class="form-actions">
        <button type="submit" class="btn-save">💾 Sauvegarder</button>
        <button type="button" class="btn-cancel" onclick="closeServiceForm()">Annuler</button>
      </div>
    </form>
  </div>
</div>

<!-- TESTIMONIAL FORM MODAL -->
<div class="form-modal" id="testimonialFormModal">
  <div class="form-modal-box">
    <h3 id="testimonialFormTitle">Nouveau Témoignage</h3>
    <form class="admin-form" id="testimonialForm" onsubmit="saveTestimonial(event)">
      <input type="hidden" id="testimonialId">
      <div class="form-row">
        <div class="form-group"><label>Nom</label><input type="text" id="testimonialName" required></div>
        <div class="form-group"><label>Rôle</label><input type="text" id="testimonialRole" placeholder="Ex: Propriétaire de boutique"></div>
      </div>
      <div class="form-group"><label>Avis / Commentaire</label><textarea id="testimonialText" rows="3" required></textarea></div>
      <div class="form-group"><label>Note (1-5)</label><input type="number" id="testimonialStars" min="1" max="5" value="5"></div>
      <div class="form-actions">
        <button type="submit" class="btn-save">💾 Sauvegarder</button>
        <button type="button" class="btn-cancel" onclick="closeTestimonialForm()">Annuler</button>
      </div>
    </form>
  </div>
</div>

<script>
// ============ DEFAULT DATA ============
const DEFAULT_DATA = {
  services: [
    { id:1, name:"Installation Professionnelle", desc:"Installation complète de systèmes de vidéosurveillance avec des équipements de haute qualité, adaptés à vos besoins spécifiques.", tag:"Maisons & Entreprises", icon:"shield" },
    { id:2, name:"Configuration à Distance", desc:"Surveillez vos caméras depuis votre smartphone ou ordinateur, où que vous soyez dans le monde, en temps réel.", tag:"Monitoring 24/7", icon:"settings" },
    { id:3, name:"Maintenance & Assistance", desc:"Service de maintenance et d'assistance technique disponible 24h/24 et 7j/7 pour garantir le fonctionnement optimal de votre système.", tag:"Support 24/7", icon:"tool" },
    { id:4, name:"Surveillance Multi-Écrans", desc:"Solutions de visionnage multi-caméras avec enregistrement DVR/NVR pour une surveillance complète et continue.", tag:"Enregistrement HD", icon:"monitor" }
  ],
  offers: [
    { id:1, name:"Formule Maison", desc:"Système de sécurité idéal pour protéger votre domicile et votre famille.", features:["2 à 4 caméras HD","Enregistreur DVR inclus","Accès mobile à distance","Installation complète","Formation à l'utilisation"], featured:false, badge:"" },
    { id:2, name:"Formule Entreprise", desc:"Solution complète pour boutiques, bureaux et espaces commerciaux.", features:["4 à 16 caméras HD/4K","NVR professionnel","Surveillance multi-écrans","Configuration à distance","Maintenance 24/7 incluse","Stockage cloud disponible"], featured:true, badge:"⭐ Populaire" },
    { id:3, name:"Formule Maintenance", desc:"Service de maintenance et assistance pour vos systèmes existants.", features:["Diagnostic complet","Réparation & remplacement","Mise à jour firmware","Support technique 24/7","Contrats annuels"], featured:false, badge:"" }
  ],
  testimonials: [
    { id:1, name:"Amadou K.", role:"Propriétaire de boutique", text:"Installation rapide et professionnelle. Je peux maintenant surveiller ma boutique depuis mon téléphone. Excellent service !", stars:5 },
    { id:2, name:"Fatoumata D.", role:"Directrice d'entreprise", text:"L'équipe de CyberVue Sécurité a installé 8 caméras dans notre entreprise. La qualité d'image est impressionnante et le support est réactif.", stars:5 },
    { id:3, name:"Moussa S.", role:"Particulier", text:"Depuis l'installation, je me sens en sécurité chez moi. L'accès à distance fonctionne parfaitement. Je recommande vivement !", stars:5 }
  ],
  contact: {
    phone:"+224 629 12 18 64",
    address:"Derrière la maternité\nchez CAPIB Prestation",
    hours:"Assistance 24h/24, 7j/7\nMaintenance & Support continu"
  },
  content: {
    heroTitle:'Installation & Maintenance de <span class="highlight">Vidéosurveillance</span> <span class="cyan">Professionnelle</span>',
    heroText:"Protégez ce qui compte le plus grâce à notre service d'installation de systèmes de vidéosurveillance professionnelle pour maisons, boutiques et entreprises.",
    heroStats:[
      {val:"500+",label:"Installations"},
      {val:"24/7",label:"Assistance"},
      {val:"100%",label:"Satisfaction"}
    ],
    aboutTitle:"CyberVue Sécurité",
    aboutText1:"Nous sommes spécialisés dans l'<strong>installation et la maintenance de systèmes de vidéosurveillance</strong> professionnels. Notre mission est de protéger ce qui compte le plus pour vous — votre maison, votre boutique ou votre entreprise.",
    aboutText2:"Grâce à notre expertise technique et à des équipements de dernière génération, nous offrons des solutions de sécurité sur mesure, adaptées à chaque client et chaque environnement.",
    offersTitle:"Nos Formules de Sécurité",
    offersDesc:"Des solutions adaptées à chaque besoin, du particulier au professionnel.",
    whyTitle:"Nos Chiffres Clés",
    whyDesc:"La confiance de nos clients est notre plus grande récompense.",
    testimonialsTitle:"Ce que disent nos clients",
    testimonialsDesc:"La satisfaction de nos clients est notre priorité absolue.",
    contactTitle:"Contactez-Nous",
    contactDesc:"Besoin d'une installation de vidéosurveillance ? Contactez-nous pour un devis gratuit et personnalisé."
  },
  quotes: []
};

// ============ DATA MANAGEMENT ============
function getData(key) {
  const stored = localStorage.getItem('cybervue_' + key);
  if (stored) return JSON.parse(stored);
  return JSON.parse(JSON.stringify(DEFAULT_DATA[key] || DEFAULT_DATA));
}

function setData(key, data) {
  localStorage.setItem('cybervue_' + key, JSON.stringify(data));
}

// ============ RENDER FUNCTIONS ============
function renderAll() {
  renderServices();
  renderOffers();
  renderTestimonials();
  renderContact();
  renderContent();
  renderAboutFeatures();
}

function renderServices() {
  const services = getData('services');
  const grid = document.getElementById('servicesGrid');
  const icons = {
    shield:'<svg viewBox="0 0 24 24" fill="none" stroke="#1E88E5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>',
    settings:'<svg viewBox="0 0 24 24" fill="none" stroke="#00BCD4" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83 0 2 2 0 010-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>',
    tool:'<svg viewBox="0 0 24 24" fill="none" stroke="#E8722A" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14.7 6.3a1 1 0 000 1.4l1.6 1.6a1 1 0 001.4 0l3.77-3.77a6 6 0 01-7.94 7.94l-6.91 6.91a2.12 2.12 0 01-3-3l6.91-6.91a6 6 0 017.94-7.94l-3.76 3.76z"/></svg>',
    monitor:'<svg viewBox="0 0 24 24" fill="none" stroke="#1E88E5" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="3" width="20" height="14" rx="2" ry="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>'
  };
  const bgColors = {shield:'icon-blue',settings:'icon-cyan',tool:'icon-orange',monitor:'icon-blue'};
  grid.innerHTML = services.map(s => `
    <div class="service-card reveal visible">
      <div class="service-icon ${bgColors[s.icon] || 'icon-blue'}">${icons[s.icon] || icons.shield}</div>
      <h3>${s.name}</h3>
      <p>${s.desc}</p>
      <span class="service-tag">${s.tag}</span>
    </div>
  `).join('');
}

function renderOffers() {
  const offers = getData('offers');
  const grid = document.getElementById('offersGrid');
  grid.innerHTML = offers.map(o => `
    <div class="offer-card ${o.featured ? 'featured reveal visible' : 'reveal visible'}">
      ${o.badge ? `<span class="offer-badge">${o.badge}</span>` : ''}
      <h3>${o.name}</h3>
      <p>${o.desc}</p>
      <ul>${o.features.map(f => `<li>${f}</li>`).join('')}</ul>
      <button class="offer-btn ${o.featured ? 'btn-orange' : 'btn-outline-light'}" onclick="scrollToContact()">Demander un devis</button>
    </div>
  `).join('');
}

function renderTestimonials() {
  const testimonials = getData('testimonials');
  const grid = document.getElementById('testimonialsGrid');
  grid.innerHTML = testimonials.map(t => `
    <div class="testimonial-card reveal visible">
      <div class="testimonial-stars">${'★'.repeat(t.stars)}${'☆'.repeat(5 - t.stars)}</div>
      <p>"${t.text}"</p>
      <div class="testimonial-author">
        <div class="testimonial-avatar">${t.name.split(' ').map(w => w[0]).join('')}</div>
        <div><div class="testimonial-name">${t.name}</div><div class="testimonial-role">${t.role}</div></div>
      </div>
    </div>
  `).join('');
}

function renderContact() {
  const contact = getData('contact');
  const items = document.getElementById('contactItems');
  items.innerHTML = `
    <div class="contact-item">
      <div class="contact-item-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0118 0z"/><circle cx="12" cy="10" r="3"/></svg></div>
      <div class="contact-item-text"><h4>Adresse</h4><p>${contact.address.replace(/\n/g,'<br>')}</p></div>
    </div>
    <div class="contact-item">
      <div class="contact-item-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-6-6 19.79 19.79 0 01-3.07-8.67A2 2 0 014.11 2h3a2 2 0 012 1.72 12.84 12.84 0 00.7 2.81 2 2 0 01-.45 2.11L8.09 9.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45 12.84 12.84 0 002.81.7A2 2 0 0122 16.92z"/></svg></div>
      <div class="contact-item-text"><h4>Téléphone</h4><p><a href="tel:${contact.phone.replace(/\s/g,'')}">${contact.phone}</a></p></div>
    </div>
    <div class="contact-item">
      <div class="contact-item-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg></div>
      <div class="contact-item-text"><h4>Horaires</h4><p>${contact.hours.replace(/\n/g,'<br>')}</p></div>
    </div>
  `;
}

function renderContent() {
  const c = getData('content');
  document.getElementById('heroTitle').innerHTML = c.heroTitle;
  document.getElementById('heroText').textContent = c.heroText;
  document.getElementById('heroStats').innerHTML = c.heroStats.map(s => `<div class="hero-stat"><div class="hero-stat-num">${s.val}</div><div class="hero-stat-label">${s.label}</div></div>`).join('');
  document.getElementById('aboutTitle').textContent = c.aboutTitle;
  document.getElementById('aboutText1').innerHTML = c.aboutText1;
  document.getElementById('aboutText2').textContent = c.aboutText2;
  document.getElementById('offersTitle').textContent = c.offersTitle;
  document.getElementById('offersDesc').textContent = c.offersDesc;
  document.getElementById('whyTitle').textContent = c.whyTitle;
  document.getElementById('whyDesc').textContent = c.whyDesc;
  document.getElementById('testimonialsTitle').textContent = c.testimonialsTitle;
  document.getElementById('testimonialsDesc').textContent = c.testimonialsDesc;
  document.getElementById('contactTitle').textContent = c.contactTitle;
  document.getElementById('contactDesc').textContent = c.contactDesc;
}

function renderAboutFeatures() {
  const features = [
    {icon:'check',text:'Installation certifiée'},
    {icon:'clock',text:'Assistance 24/24'},
    {icon:'shield',text:'Protection maximale'},
    {icon:'users',text:'Équipe expérimentée'}
  ];
  const icons = {
    check:'<svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>',
    clock:'<svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>',
    shield:'<svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>',
    users:'<svg viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>'
  };
  document.getElementById('aboutFeatures').innerHTML = features.map(f => `
    <div class="about-feature"><div class="about-feature-icon">${icons[f.icon]}</div><span>${f.text}</span></div>
  `).join('');
}

// ============ ADMIN PANEL ============
let isLoggedIn = false;

function openLogin() {
  if (isLoggedIn) {
    openAdmin();
    return;
  }
  document.getElementById('loginModal').classList.add('open');
  document.getElementById('loginError').classList.remove('show');
  document.getElementById('loginUser').value = '';
  document.getElementById('loginPass').value = '';
}

function closeLogin() {
  document.getElementById('loginModal').classList.remove('open');
}

function handleLogin(e) {
  e.preventDefault();
  const user = document.getElementById('loginUser').value;
  const pass = document.getElementById('loginPass').value;
  if (user === 'admin' && pass === 'cybervue2026') {
    isLoggedIn = true;
    closeLogin();
    openAdmin();
    document.getElementById('adminLink').textContent = '⚙️ Admin';
    document.getElementById('adminLink').classList.add('logged-in');
    showToast('Connexion réussie ! Bienvenue dans l\'admin.');
  } else {
    document.getElementById('loginError').classList.add('show');
  }
}

function openAdmin() {
  document.getElementById('adminPanel').classList.add('open');
  document.body.style.overflow = 'hidden';
  loadAdminData();
}

function closeAdmin() {
  document.getElementById('adminPanel').classList.remove('open');
  document.body.style.overflow = '';
  renderAll();
}

function logout() {
  isLoggedIn = false;
  closeAdmin();
  document.getElementById('adminLink').textContent = '🔐 Admin';
  document.getElementById('adminLink').classList.remove('logged-in');
  showToast('Déconnexion réussie.');
}

function switchAdminPage(page, el) {
  document.querySelectorAll('.admin-page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + page).classList.add('active');
  document.querySelectorAll('.admin-nav a').forEach(a => a.classList.remove('active'));
  el.classList.add('active');
  const titles = {dashboard:'Dashboard',offers:'Gestion des Offres',services:'Gestion des Services',testimonials:'Gestion des Témoignages',contact:'Informations de Contact',content:'Contenu du Site'};
  document.getElementById('adminPageTitle').textContent = titles[page] || 'Admin';
  if (page === 'offers') loadOffersAdmin();
  if (page === 'services') loadServicesAdmin();
  if (page === 'testimonials') loadTestimonialsAdmin();
  if (page === 'contact') loadContactAdmin();
  if (page === 'content') loadContentAdmin();
  if (page === 'dashboard') loadDashboard();
}

// DASHBOARD
function loadDashboard() {
  const services = getData('services');
  const offers = getData('offers');
  const testimonials = getData('testimonials');
  const quotes = getData('quotes');
  document.getElementById('adminStats').innerHTML = `
    <div class="admin-stat-card"><div class="stat-icon" style="background:rgba(30,136,229,.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#1E88E5" stroke-width="2"><path d="M14.7 6.3a1 1 0 000 1.4l1.6 1.6a1 1 0 001.4 0l3.77-3.77a6 6 0 01-7.94 7.94l-6.91 6.91a2.12 2.12 0 01-3-3l6.91-6.91a6 6 0 017.94-7.94l-3.76 3.76z"/></svg></div><h4>Services</h4><div class="stat-value">${services.length}</div></div>
    <div class="admin-stat-card"><div class="stat-icon" style="background:rgba(232,114,42,.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#E8722A" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg></div><h4>Offres</h4><div class="stat-value">${offers.length}</div></div>
    <div class="admin-stat-card"><div class="stat-icon" style="background:rgba(0,188,212,.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#00BCD4" stroke-width="2"><path d="M21 15a2 2 0 01-2 2H7l-4 4V5a2 2 0 012-2h14a2 2 0 012 2z"/></svg></div><h4>Témoignages</h4><div class="stat-value">${testimonials.length}</div></div>
    <div class="admin-stat-card"><div class="stat-icon" style="background:rgba(76,175,80,.1)"><svg viewBox="0 0 24 24" fill="none" stroke="#4CAF50" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg></div><h4>Devis</h4><div class="stat-value">${quotes.length}</div></div>
  `;
  const tbody = document.getElementById('quoteBody');
  if (quotes.length === 0) {
    tbody.innerHTML = '<tr><td colspan="5" style="text-align:center;color:#999;padding:2rem">Aucune demande de devis pour le moment</td></tr>';
  } else {
    tbody.innerHTML = quotes.map(q => `
      <tr>
        <td>${q.name}</td>
        <td>${q.phone}</td>
        <td>${q.service}</td>
        <td>${q.date}</td>
        <td><span style="background:#e8f5e9;color:#4CAF50;padding:.2rem .6rem;border-radius:4px;font-size:.75rem">Nouveau</span></td>
      </tr>
    `).join('');
  }
}

// OFFERS ADMIN
function loadOffersAdmin() {
  const offers = getData('offers');
  document.getElementById('offersTableBody').innerHTML = offers.map(o => `
    <tr>
      <td><strong>${o.name}</strong></td>
      <td>${o.desc.substring(0,60)}...</td>
      <td>${o.featured ? '<span class="featured-tag">⭐ Oui</span>' : 'Non'}</td>
      <td class="admin-table-actions">
        <button class="edit-btn" onclick="editOffer(${o.id})">✏️ Modifier</button>
        <button class="del-btn" onclick="deleteOffer(${o.id})">🗑️ Supprimer</button>
      </td>
    </tr>
  `).join('');
}

function openOfferForm(id) {
  document.getElementById('offerForm').reset();
  document.getElementById('offerId').value = '';
  document.getElementById('offerFormTitle').textContent = 'Nouvelle Offre';
  document.getElementById('offerFeatures').innerHTML = '<div class="feature-item"><input type="text" placeholder="Ex: 2 à 4 caméras HD"><button type="button" class="remove-feature" onclick="removeFeature(this)">✕</button></div>';
  if (id) {
    const offers = getData('offers');
    const o = offers.find(x => x.id === id);
    if (o) {
      document.getElementById('offerFormTitle').textContent = 'Modifier Offre';
      document.getElementById('offerId').value = o.id;
      document.getElementById('offerName').value = o.name;
      document.getElementById('offerDesc').value = o.desc;
      document.getElementById('offerFeatured').checked = o.featured;
      document.getElementById('offerBadge').value = o.badge || '';
      document.getElementById('offerFeatures').innerHTML = o.features.map(f => `<div class="feature-item"><input type="text" value="${f}"><button type="button" class="remove-feature" onclick="removeFeature(this)">✕</button></div>`).join('');
    }
  }
  document.getElementById('offerFormModal').classList.add('open');
}

function closeOfferForm() { document.getElementById('offerFormModal').classList.remove('open'); }

function saveOffer(e) {
  e.preventDefault();
  const offers = getData('offers');
  const id = document.getElementById('offerId').value;
  const name = document.getElementById('offerName').value;
  const desc = document.getElementById('offerDesc').value;
  const featured = document.getElementById('offerFeatured').checked;
  const badge = document.getElementById('offerBadge').value;
  const features = Array.from(document.querySelectorAll('#offerFeatures .feature-item input')).map(i => i.value).filter(v => v);

  if (id) {
    const idx = offers.findIndex(o => o.id == id);
    if (idx > -1) offers[idx] = { ...offers[idx], name, desc, featured, badge, features };
  } else {
    const newId = offers.length > 0 ? Math.max(...offers.map(o => o.id)) + 1 : 1;
    offers.push({ id: newId, name, desc, featured, badge, features });
  }
  setData('offers', offers);
  closeOfferForm();
  loadOffersAdmin();
  showToast('Offre sauvegardée avec succès !');
}

function editOffer(id) { openOfferForm(id); }
function deleteOffer(id) {
  if (!confirm('Supprimer cette offre ?')) return;
  let offers = getData('offers');
  offers = offers.filter(o => o.id !== id);
  setData('offers', offers);
  loadOffersAdmin();
  showToast('Offre supprimée.');
}

function addFeature() {
  const div = document.createElement('div');
  div.className = 'feature-item';
  div.innerHTML = '<input type="text" placeholder="Nouvelle caractéristique"><button type="button" class="remove-feature" onclick="removeFeature(this)">✕</button>';
  document.getElementById('offerFeatures').appendChild(div);
  div.querySelector('input').focus();
}

function removeFeature(btn) {
  const items = document.querySelectorAll('#offerFeatures .feature-item');
  if (items.length > 1) btn.parentElement.remove();
}

// SERVICES ADMIN
function loadServicesAdmin() {
  const services = getData('services');
  document.getElementById('servicesTableBody').innerHTML = services.map(s => `
    <tr>
      <td><strong>${s.name}</strong></td>
      <td>${s.desc.substring(0,60)}...</td>
      <td>${s.tag}</td>
      <td class="admin-table-actions">
        <button class="edit-btn" onclick="editService(${s.id})">✏️ Modifier</button>
        <button class="del-btn" onclick="deleteService(${s.id})">🗑️ Supprimer</button>
      </td>
    </tr>
  `).join('');
}

function openServiceForm(id) {
  document.getElementById('serviceForm').reset();
  document.getElementById('serviceId').value = '';
  document.getElementById('serviceFormTitle').textContent = 'Nouveau Service';
  if (id) {
    const services = getData('services');
    const s = services.find(x => x.id === id);
    if (s) {
      document.getElementById('serviceFormTitle').textContent = 'Modifier Service';
      document.getElementById('serviceId').value = s.id;
      document.getElementById('serviceName').value = s.name;
      document.getElementById('serviceDesc').value = s.desc;
      document.getElementById('serviceTag').value = s.tag;
    }
  }
  document.getElementById('serviceFormModal').classList.add('open');
}

function closeServiceForm() { document.getElementById('serviceFormModal').classList.remove('open'); }

function saveService(e) {
  e.preventDefault();
  const services = getData('services');
  const id = document.getElementById('serviceId').value;
  const name = document.getElementById('serviceName').value;
  const desc = document.getElementById('serviceDesc').value;
  const tag = document.getElementById('serviceTag').value;
  const icons = ['shield','settings','tool','monitor'];
  const icon = icons[services.length % 4];

  if (id) {
    const idx = services.findIndex(s => s.id == id);
    if (idx > -1) services[idx] = { ...services[idx], name, desc, tag };
  } else {
    const newId = services.length > 0 ? Math.max(...services.map(s => s.id)) + 1 : 1;
    services.push({ id: newId, name, desc, tag, icon });
  }
  setData('services', services);
  closeServiceForm();
  loadServicesAdmin();
  showToast('Service sauvegardé avec succès !');
}

function editService(id) { openServiceForm(id); }
function deleteService(id) {
  if (!confirm('Supprimer ce service ?')) return;
  let services = getData('services');
  services = services.filter(s => s.id !== id);
  setData('services', services);
  loadServicesAdmin();
  showToast('Service supprimé.');
}

// TESTIMONIALS ADMIN
function loadTestimonialsAdmin() {
  const testimonials = getData('testimonials');
  document.getElementById('testimonialsTableBody').innerHTML = testimonials.map(t => `
    <tr>
      <td><strong>${t.name}</strong></td>
      <td>${t.role}</td>
      <td>${t.text.substring(0,50)}...</td>
      <td class="admin-table-actions">
        <button class="edit-btn" onclick="editTestimonial(${t.id})">✏️ Modifier</button>
        <button class="del-btn" onclick="deleteTestimonial(${t.id})">🗑️ Supprimer</button>
      </td>
    </tr>
  `).join('');
}

function openTestimonialForm(id) {
  document.getElementById('testimonialForm').reset();
  document.getElementById('testimonialId').value = '';
  document.getElementById('testimonialFormTitle').textContent = 'Nouveau Témoignage';
  if (id) {
    const testimonials = getData('testimonials');
    const t = testimonials.find(x => x.id === id);
    if (t) {
      document.getElementById('testimonialFormTitle').textContent = 'Modifier Témoignage';
      document.getElementById('testimonialId').value = t.id;
      document.getElementById('testimonialName').value = t.name;
      document.getElementById('testimonialRole').value = t.role;
      document.getElementById('testimonialText').value = t.text;
      document.getElementById('testimonialStars').value = t.stars;
    }
  }
  document.getElementById('testimonialFormModal').classList.add('open');
}

function closeTestimonialForm() { document.getElementById('testimonialFormModal').classList.remove('open'); }

function saveTestimonial(e) {
  e.preventDefault();
  const testimonials = getData('testimonials');
  const id = document.getElementById('testimonialId').value;
  const name = document.getElementById('testimonialName').value;
  const role = document.getElementById('testimonialRole').value;
  const text = document.getElementById('testimonialText').value;
  const stars = parseInt(document.getElementById('testimonialStars').value) || 5;

  if (id) {
    const idx = testimonials.findIndex(t => t.id == id);
    if (idx > -1) testimonials[idx] = { ...testimonials[idx], name, role, text, stars };
  } else {
    const newId = testimonials.length > 0 ? Math.max(...testimonials.map(t => t.id)) + 1 : 1;
    testimonials.push({ id: newId, name, role, text, stars });
  }
  setData('testimonials', testimonials);
  closeTestimonialForm();
  loadTestimonialsAdmin();
  showToast('Témoignage sauvegardé avec succès !');
}

function editTestimonial(id) { openTestimonialForm(id); }
function deleteTestimonial(id) {
  if (!confirm('Supprimer ce témoignage ?')) return;
  let testimonials = getData('testimonials');
  testimonials = testimonials.filter(t => t.id !== id);
  setData('testimonials', testimonials);
  loadTestimonialsAdmin();
  showToast('Témoignage supprimé.');
}

// CONTACT ADMIN
function loadContactAdmin() {
  const contact = getData('contact');
  document.getElementById('editPhone').value = contact.phone;
  document.getElementById('editAddress').value = contact.address;
  document.getElementById('editHours').value = contact.hours;
}

function saveContact() {
  const contact = {
    phone: document.getElementById('editPhone').value,
    address: document.getElementById('editAddress').value,
    hours: document.getElementById('editHours').value
  };
  setData('contact', contact);
  showToast('Informations de contact sauvegardées !');
}

// CONTENT ADMIN
function loadContentAdmin() {
  const c = getData('content');
  document.getElementById('editHeroTitle').value = c.heroTitle.replace(/<[^>]*>/g, '');
  document.getElementById('editHeroText').value = c.heroText;
  document.getElementById('editStat1Val').value = c.heroStats[0].val;
  document.getElementById('editStat1Label').value = c.heroStats[0].label;
  document.getElementById('editStat2Val').value = c.heroStats[1].val;
  document.getElementById('editStat2Label').value = c.heroStats[1].label;
  document.getElementById('editStat3Val').value = c.heroStats[2].val;
  document.getElementById('editStat3Label').value = c.heroStats[2].label;
  document.getElementById('editAboutTitle').value = c.aboutTitle;
  document.getElementById('editAboutText1').value = c.aboutText1.replace(/<[^>]*>/g, '');
  document.getElementById('editAboutText2').value = c.aboutText2;
  document.getElementById('editOffersTitle').value = c.offersTitle;
  document.getElementById('editOffersDesc').value = c.offersDesc;
  document.getElementById('editWhyTitle').value = c.whyTitle;
  document.getElementById('editWhyDesc').value = c.whyDesc;
  document.getElementById('editTestimonialsTitle').value = c.testimonialsTitle;
  document.getElementById('editTestimonialsDesc').value = c.testimonialsDesc;
  document.getElementById('editContactTitle').value = c.contactTitle;
  document.getElementById('editContactDesc').value = c.contactDesc;
}

function saveContent() {
  const c = getData('content');
  c.heroTitle = document.getElementById('editHeroTitle').value;
  c.heroText = document.getElementById('editHeroText').value;
  c.heroStats = [
    {val:document.getElementById('editStat1Val').value,label:document.getElementById('editStat1Label').value},
    {val:document.getElementById('editStat2Val').value,label:document.getElementById('editStat2Label').value},
    {val:document.getElementById('editStat3Val').value,label:document.getElementById('editStat3Label').value}
  ];
  c.aboutTitle = document.getElementById('editAboutTitle').value;
  c.aboutText1 = document.getElementById('editAboutText1').value;
  c.aboutText2 = document.getElementById('editAboutText2').value;
  c.offersTitle = document.getElementById('editOffersTitle').value;
  c.offersDesc = document.getElementById('editOffersDesc').value;
  c.whyTitle = document.getElementById('editWhyTitle').value;
  c.whyDesc = document.getElementById('editWhyDesc').value;
  c.testimonialsTitle = document.getElementById('editTestimonialsTitle').value;
  c.testimonialsDesc = document.getElementById('editTestimonialsDesc').value;
  c.contactTitle = document.getElementById('editContactTitle').value;
  c.contactDesc = document.getElementById('editContactDesc').value;
  setData('content', c);
  showToast('Contenu sauvegardé avec succès !');
}

// ============ GENERAL ============
function showToast(message) {
  const toast = document.getElementById('toast');
  document.getElementById('toastMessage').textContent = message;
  toast.classList.add('show');
  setTimeout(() => toast.classList.remove('show'), 4000);
}

function scrollToContact() {
  document.getElementById('contact').scrollIntoView({behavior:'smooth'});
}

function submitForm(e) {
  e.preventDefault();
  const inputs = e.target.querySelectorAll('input, textarea, select');
  const quote = {
    name: inputs[0].value,
    phone: inputs[1].value,
    email: inputs[2].value,
    service: inputs[3].value,
    message: inputs[4].value,
    date: new Date().toLocaleDateString('fr-FR')
  };
  const quotes = getData('quotes');
  quotes.unshift(quote);
  setData('quotes', quotes);
  showToast('Demande envoyée avec succès ! Nous vous contacterons bientôt.');
  e.target.reset();
}

function toggleMobile() {
  document.getElementById('navLinks').classList.toggle('mobile-open');
}

document.querySelectorAll('.nav-links a').forEach(link => {
  link.addEventListener('click', () => document.getElementById('navLinks').classList.remove('mobile-open'));
});

window.addEventListener('scroll', function() {
  const navbar = document.getElementById('navbar');
  const scrollTop = document.getElementById('scrollTop');
  navbar.classList.toggle('scrolled', window.scrollY > 100);
  scrollTop.classList.toggle('visible', window.scrollY > 600);
});

// PARTICLES
(function() {
  const container = document.getElementById('particles');
  for (let i = 0; i < 30; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.left = Math.random() * 100 + '%';
    p.style.animationDuration = (8 + Math.random() * 12) + 's';
    p.style.animationDelay = Math.random() * 10 + 's';
    p.style.width = p.style.height = (1 + Math.random() * 3) + 'px';
    container.appendChild(p);
  }
})();

// SCROLL REVEAL
const observer = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) entry.target.classList.add('visible');
  });
}, {threshold: 0.1, rootMargin: '0px 0px -50px 0px'});
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// SMOOTH SCROLL
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    if (target) target.scrollIntoView({behavior:'smooth',block:'start'});
  });
});

// KEYBOARD
document.addEventListener('keydown', e => {
  if (e.key === 'Escape') {
    closeLogin();
    closeOfferForm();
    closeServiceForm();
    closeTestimonialForm();
  }
});

// INIT
renderAll();
</script>
</body>
</html>

