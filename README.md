# PROJECT-ARTIFICIAL-INTELLIGENCE
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FurnAI — AI Furniture Matching Assistant</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root{--cream:#f5efe6;--warm-white:#faf7f2;--walnut:#3d2b1f;--oak:#8b6344;--sand:#c9aa87;--sage:#7a9e7e;--terracotta:#c0714a;--charcoal:#2a2420;--light-sand:#e8d9c5;}
*{margin:0;padding:0;box-sizing:border-box;}
body{background-color:var(--warm-white);color:var(--walnut);font-family:'DM Sans',sans-serif;overflow-x:hidden;}
nav{position:fixed;top:0;width:100%;z-index:100;display:flex;justify-content:space-between;align-items:center;padding:1.2rem 3rem;background:rgba(250,247,242,0.92);backdrop-filter:blur(12px);border-bottom:1px solid var(--light-sand);}
.nav-logo{font-family:'Playfair Display',serif;font-size:1.5rem;font-weight:900;color:var(--walnut);}
.nav-logo span{color:var(--terracotta);}
.nav-links{display:flex;gap:2rem;list-style:none;}
.nav-links a{text-decoration:none;color:var(--oak);font-size:0.85rem;font-weight:500;letter-spacing:0.5px;text-transform:uppercase;transition:color 0.2s;}
.nav-links a:hover{color:var(--terracotta);}
.nav-cta{background:var(--walnut)!important;color:var(--cream)!important;padding:0.5rem 1.3rem;border-radius:100px;}
.nav-cta:hover{background:var(--terracotta)!important;}
.hero{min-height:100vh;display:grid;grid-template-columns:1fr 1fr;align-items:center;padding:7rem 3rem 3rem;gap:4rem;background:linear-gradient(135deg,var(--warm-white) 0%,var(--cream) 100%);position:relative;overflow:hidden;}
.hero::before{content:'';position:absolute;top:-100px;right:-100px;width:500px;height:500px;border-radius:50%;background:radial-gradient(circle,rgba(192,113,74,0.1) 0%,transparent 70%);pointer-events:none;}
.hero-text{animation:fadeUp 0.8s ease both;}
.hero-badge{display:inline-flex;align-items:center;gap:0.5rem;background:var(--light-sand);border-radius:100px;padding:0.4rem 1rem;font-size:0.78rem;font-weight:600;color:var(--oak);margin-bottom:1.8rem;}
.hero-badge::before{content:'✦';color:var(--terracotta);}
h1{font-family:'Playfair Display',serif;font-size:clamp(2.6rem,5vw,4.2rem);line-height:1.1;font-weight:900;color:var(--charcoal);margin-bottom:1.4rem;}
h1 em{color:var(--terracotta);font-style:italic;}
.hero-sub{font-size:1rem;color:var(--oak);line-height:1.75;max-width:440px;margin-bottom:2.5rem;font-weight:300;}
.hero-btns{display:flex;gap:1rem;flex-wrap:wrap;}
.btn-primary{background:var(--walnut);color:var(--cream);padding:0.9rem 2.2rem;border-radius:100px;font-size:0.95rem;font-weight:600;text-decoration:none;border:none;cursor:pointer;transition:all 0.25s;display:inline-block;box-shadow:0 8px 24px rgba(61,43,31,0.25);}
.btn-primary:hover{background:var(--terracotta);transform:translateY(-2px);}
.btn-secondary{background:transparent;color:var(--walnut);padding:0.9rem 2.2rem;border-radius:100px;font-size:0.95rem;font-weight:500;text-decoration:none;border:2px solid var(--sand);cursor:pointer;transition:all 0.25s;display:inline-block;}
.btn-secondary:hover{border-color:var(--walnut);background:var(--light-sand);}
.hero-visual{animation:fadeUp 0.8s 0.2s ease both;}
.room-card{background:var(--cream);border-radius:24px;padding:2rem;box-shadow:0 30px 80px rgba(61,43,31,0.15);}
.room-illustration{width:100%;height:260px;background:linear-gradient(160deg,#d4c4b0 0%,#b8a48c 40%,#8b7355 100%);border-radius:16px;margin-bottom:1.5rem;position:relative;overflow:hidden;}
.ai-tag{position:absolute;top:1rem;right:1rem;background:var(--sage);color:white;font-size:0.72rem;font-weight:600;padding:0.3rem 0.75rem;border-radius:100px;}
.room-svg{width:100%;height:100%;}
.match-result{display:flex;flex-direction:column;gap:0.75rem;}
.match-label{font-size:0.75rem;text-transform:uppercase;letter-spacing:1px;color:var(--oak);font-weight:600;}
.furniture-chips{display:flex;flex-wrap:wrap;gap:0.5rem;}
.chip{background:var(--light-sand);color:var(--walnut);padding:0.35rem 0.9rem;border-radius:100px;font-size:0.8rem;font-weight:500;}
.chip.active{background:var(--walnut);color:var(--cream);}
.match-score{display:flex;align-items:center;gap:0.75rem;margin-top:0.4rem;}
.score-bar{flex:1;height:6px;background:var(--light-sand);border-radius:100px;overflow:hidden;}
.score-fill{height:100%;background:linear-gradient(90deg,var(--sage),var(--terracotta));border-radius:100px;width:87%;animation:growBar 1.5s 1s ease both;}
.score-text{font-size:0.85rem;font-weight:700;color:var(--terracotta);}
.stats-bar{background:var(--walnut);padding:2.5rem 3rem;display:grid;grid-template-columns:repeat(4,1fr);gap:2rem;text-align:center;}
.stat-num{font-family:'Playfair Display',serif;font-size:2.4rem;font-weight:900;color:var(--sand);line-height:1;}
.stat-label{font-size:0.78rem;color:rgba(245,239,230,0.6);margin-top:0.4rem;}
section{padding:5.5rem 3rem;}
.section-tag{display:inline-block;font-size:0.72rem;font-weight:700;text-transform:uppercase;letter-spacing:1.5px;color:var(--terracotta);margin-bottom:1rem;}
h2{font-family:'Playfair Display',serif;font-size:clamp(1.8rem,3.5vw,2.8rem);font-weight:900;color:var(--charcoal);line-height:1.2;margin-bottom:1rem;}
h2 em{color:var(--terracotta);font-style:italic;}
.steps-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:2rem;margin-top:3rem;}
.step-card{background:var(--cream);border-radius:20px;padding:2.2rem;border:1px solid var(--light-sand);transition:transform 0.3s,box-shadow 0.3s;}
.step-card:hover{transform:translateY(-6px);box-shadow:0 20px 50px rgba(61,43,31,0.1);}
.step-num{font-family:'Playfair Display',serif;font-size:3rem;font-weight:900;color:var(--light-sand);line-height:1;margin-bottom:1rem;}
.step-icon{width:50px;height:50px;border-radius:14px;background:var(--walnut);display:flex;align-items:center;justify-content:center;font-size:1.3rem;margin-bottom:1rem;}
.step-card h3{font-family:'Playfair Display',serif;font-size:1.2rem;font-weight:700;color:var(--charcoal);margin-bottom:0.6rem;}
.step-card p{font-size:0.88rem;color:var(--oak);line-height:1.7;font-weight:300;}
.ai-section{background:linear-gradient(135deg,var(--cream) 0%,var(--light-sand) 100%);}
.ai-inner{max-width:860px;margin:0 auto;}
