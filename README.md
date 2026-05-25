<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Courses">
<title>Mes Courses</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=DM+Sans:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg:#f5f0e8; --surface:#fffdf7; --text:#1a1207; --muted:#8a7d6b;
  --orange:#d4541a; --blue:#1a6b8a; --green:#2a6b3c; --red:#e2001a;
  --border:#e0d8cc; --shadow:0 2px 12px rgba(26,18,7,0.08);
}
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
body{background:var(--bg);font-family:'DM Sans',sans-serif;color:var(--text);min-height:100vh;padding-bottom:86px;}

/* HEADER */
.hdr{background:var(--text);padding:16px 14px 12px;position:sticky;top:0;z-index:100;box-shadow:0 2px 16px rgba(0,0,0,0.3);}
.hdr-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;}
.logo{font-family:'Syne',sans-serif;font-size:22px;font-weight:800;color:#fff;}
.logo span{color:var(--orange);}

/* TABS */
.tabs{display:flex;gap:5px;}
.tab{flex:1;padding:8px 2px;border:none;border-radius:10px;font-family:'Syne',sans-serif;font-size:10px;font-weight:700;cursor:pointer;text-align:center;line-height:1.3;background:rgba(255,255,255,0.1);color:rgba(255,255,255,0.5);transition:all .2s;}
.tab .ic{font-size:14px;display:block;margin-bottom:2px;}
.tab.on{color:#fff;}
.tab[data-m="maison"].on{background:var(--orange);}
.tab[data-m="magasin"].on{background:var(--blue);}
.tab[data-m="panier"].on{background:var(--green);}
.tab[data-m="carte"].on{background:var(--red);}

/* SEARCH */
.srch{margin-top:10px;position:relative;display:none;}
.srch.show{display:block;}
.srch input{width:100%;background:rgba(255,255,255,0.13);border:1.5px solid rgba(255,255,255,0.2);border-radius:10px;padding:10px 36px 10px 14px;font-size:15px;color:#fff;outline:none;font-family:'DM Sans',sans-serif;}
.srch input::placeholder{color:rgba(255,255,255,0.4);}
.srch-x{position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;color:rgba(255,255,255,0.5);font-size:17px;cursor:pointer;display:none;}

/* INFO */
.info{display:flex;align-items:center;justify-content:space-between;padding:9px 14px;background:var(--surface);border-bottom:1px solid var(--border);}
.info-n{font-family:'Syne',sans-serif;font-size:13px;font-weight:700;}
.info-n b{font-size:18px;}
.c-orange b{color:var(--orange);}
.c-blue b{color:var(--blue);}
.c-green b{color:var(--green);}
.rst{font-size:12px;color:var(--muted);background:none;border:1px solid var(--border);border-radius:8px;cursor:pointer;padding:5px 10px;font-family:'DM Sans',sans-serif;}

/* CONFIRM OVERLAY */
.overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,0.5);z-index:999;align-items:flex-end;justify-content:center;}
.overlay.show{display:flex;}
.confirm-box{background:#fff;border-radius:20px 20px 0 0;padding:24px 20px 36px;width:100%;max-width:480px;text-align:center;}
.confirm-box p{font-size:16px;font-weight:500;color:var(--text);margin-bottom:20px;line-height:1.4;}
.confirm-btns{display:flex;gap:10px;}
.confirm-btns button{flex:1;padding:14px;border:none;border-radius:12px;font-size:15px;font-weight:700;cursor:pointer;font-family:'Syne',sans-serif;}
.cb-yes{background:var(--orange);color:#fff;}
.cb-yes.green{background:var(--green);}
.cb-no{background:var(--bg);color:var(--muted);}

/* SECTIONS */
.secs{padding:10px 12px;}
.sec{margin-bottom:8px;border-radius:14px;overflow:hidden;background:var(--surface);box-shadow:var(--shadow);}
.sec-hdr{display:flex;align-items:center;justify-content:space-between;padding:11px 13px;cursor:pointer;border-bottom:1px solid var(--border);}
.sec-name{font-family:'Syne',sans-serif;font-size:12px;font-weight:800;text-transform:uppercase;letter-spacing:.4px;display:flex;align-items:center;gap:6px;}
.sec-meta{display:flex;align-items:center;gap:7px;}
.sec-ct{font-size:11px;color:var(--muted);background:var(--bg);padding:2px 7px;border-radius:10px;}
.chev{color:var(--muted);font-size:10px;transition:transform .2s;}
.sec.fold .chev{transform:rotate(-90deg);}
.sec.fold .sec-body{display:none;}

/* ITEMS */
.itm{display:flex;align-items:center;gap:10px;padding:11px 13px;border-bottom:1px solid var(--border);cursor:pointer;transition:background .12s;}
.itm:last-child{border-bottom:none;}
.itm:active{background:var(--bg);}
.box{width:22px;height:22px;border-radius:6px;border:2px solid var(--border);flex-shrink:0;display:flex;align-items:center;justify-content:center;background:#fff;transition:all .18s;}
.ck{display:none;font-size:12px;font-weight:700;}
.lbl{font-size:15px;flex:1;}

/* maison sélectionné = orange */
.m-maison .itm.sel .box{background:var(--orange);border-color:var(--orange);}
.m-maison .itm.sel .ck{display:block;color:#fff;}
.m-maison .itm.sel .lbl{font-weight:500;}

/* magasin à prendre = cercle bleu, pris = vert barré */
.m-magasin .box{border-radius:50%;border-color:var(--blue);}
.m-magasin .itm.got .box{background:var(--green);border-color:var(--green);}
.m-magasin .itm.got .ck{display:block;color:#fff;}
.m-magasin .itm.got .lbl{color:#aaa;text-decoration:line-through;}

/* panier = tout vert */
.m-panier .box{background:var(--green);border-color:var(--green);}
.m-panier .ck{display:block;color:#fff;}
.m-panier .lbl{color:#555;}

/* EMPTY */
.empty{text-align:center;padding:50px 20px;color:var(--muted);}
.empty .ei{font-size:46px;margin-bottom:10px;}

/* CARTE */
.carte{display:none;padding:24px 14px;flex-direction:column;align-items:center;gap:18px;}
.carte.show{display:flex;}
.carte-card{background:#fff;border-radius:20px;padding:28px 18px 20px;box-shadow:0 4px 24px rgba(0,0,0,0.13);width:100%;max-width:380px;display:flex;flex-direction:column;align-items:center;gap:14px;}
.monop{font-family:'Syne',sans-serif;font-size:30px;font-weight:800;color:var(--red);letter-spacing:-1px;}
.monop span{color:var(--text);}
.carte-sub{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;}
.bc-wrap{width:100%;overflow:hidden;}
.bc-num{font-family:'Syne',sans-serif;font-size:15px;font-weight:700;letter-spacing:2px;color:var(--text);}
.carte-tip{background:var(--bg);border-radius:12px;padding:13px 14px;font-size:13px;color:var(--muted);text-align:center;line-height:1.5;width:100%;max-width:380px;}

/* BOTTOM */
.btm{position:fixed;bottom:0;left:0;right:0;background:var(--text);padding:12px 14px;padding-bottom:calc(12px + env(safe-area-inset-bottom));display:flex;align-items:center;justify-content:space-between;z-index:100;}
.btm-inf{color:rgba(255,255,255,0.6);font-size:13px;}
.btm-inf strong{color:#fff;font-family:'Syne',sans-serif;font-size:15px;}
.btm-btn{background:rgba(255,255,255,0.12);border:1.5px solid rgba(255,255,255,0.2);border-radius:10px;padding:8px 13px;color:#fff;font-size:13px;cursor:pointer;font-family:'DM Sans',sans-serif;}

mark{background:#ffe066;border-radius:2px;}
</style>
</head>
<body>

<div class="hdr">
  <div class="hdr-top">
    <div class="logo">Mes <span>Courses</span></div>
  </div>
  <div class="tabs">
    <button class="tab on" data-m="maison"><span class="ic">🏠</span>MAISON</button>
    <button class="tab" data-m="magasin"><span class="ic">🛍️</span>MAGASIN</button>
    <button class="tab" data-m="panier"><span class="ic">🧺</span>PANIER</button>
    <button class="tab" data-m="carte"><span class="ic">💳</span>CARTE</button>
  </div>
  <div class="srch" id="srch">
    <input id="sinput" type="search" placeholder="Rechercher un article…" autocomplete="off" autocorrect="off" autocapitalize="off">
    <button class="srch-x" id="sx">✕</button>
  </div>
</div>

<div class="info" id="info-bar">
  <div class="info-n c-orange" id="info-n"><b id="info-b">0</b> <span id="info-t">sélectionné(s)</span> <span id="info-total" style="font-size:11px;color:var(--muted);font-family:'DM Sans',sans-serif;font-weight:400;"></span></div>
  <button class="rst" id="rst">↺ Réinitialiser</button>
</div>

<div class="overlay" id="overlay">
  <div class="confirm-box">
    <p id="confirm-msg"></p>
    <div class="confirm-btns">
      <button class="cb-no" id="cb-no">Annuler</button>
      <button class="cb-yes" id="cb-yes">Confirmer</button>
    </div>
  </div>
</div>

<div class="secs m-maison" id="secs"></div>

<div class="carte" id="carte">
  <div class="carte-card">
    <div class="monop">monop<span>'</span></div>
    <div class="carte-sub">Carte de fidélité</div>
    <div class="bc-wrap"><svg id="bc" width="100%" height="90"></svg></div>
    <div class="bc-num">9240036667162</div>
  </div>
  <div class="carte-tip">📱 Présente cet écran en caisse pour scanner ta carte.</div>
</div>

<div class="btm">
  <div class="btm-inf" id="btm-inf"></div>
  <button class="btm-btn" id="btm-btn"></button>
</div>

<script>
// ── DATA ──────────────────────────────────────────────────────────────────
const DATA = [
  {n:"Bazar / Divers",e:"🛒",i:["Agrafeuse","Ampoule Raphou 12V 50hz","Assiettes","Bloc fiches bristol","Carnet","Cartes visite","Colle","Crème pied","Cure dent","Cadeaux Pâques","Deco anniv Toinou","Eau déminéralisée","Feutre rouge et noir","Feutres veleda","Huile barbe","Œufs de mouettes","Papier collant habits","Pique brochettes","Protège slips","Sachet cadeau anniv Tom","Souris tip ex","Stabilo jaune","Stylo 4 couleurs","Tupperware antoine","Tupperware plastique","Verre bodega","Verre Tom"]},
  {n:"Hygiène & Beauté",e:"🧴",i:["Bougies","Brosse à dents","Brosse pour brosse électrique oral B","Cotons tige","Crème cheveux","Demaq'Up","Dentifrice","Deo Antoine Axe Gold","Deo Ced","Eau bombe","Éponges bain","Gel Antoine","Gel douche enfant","Gel vivelle dop","H&S","Kleenex","Lingettes cucu","Mousse à raser","Pansement","Pansement ampoule","Rasoirs","Sanex","Sanex deo raphou","Savon main","Savon Tom","Sèche cheveux"]},
  {n:"Traiteur / Charcuterie fine",e:"🥓",i:["Chiffonnade jambon blanc","Chiffonnade jambon cru","Chorizo","Pancetta très fine","Parmesan","Saucisson truffe le plus sec possible","Tomates séchées","Troffi x2","Truffe"]},
  {n:"Boucherie",e:"🥩",i:["Bœuf aiguillettes de rumsteak","Carré d'agneau","Chipolatas","Côtelettes","Épaule agneau","Épaule agneau découpée","Faux filet bœuf","Jarret de porc","Joue de bœuf","Merguez","Os à moelle","Osso bucco","Pied de porc","Porc Échine tranche","Porc poitrine","Poulet rôti","Rôtisserie","Saucisse toulouse","Sauté de porc","Selle agneau","Steak haché","Veau"]},
  {n:"Fromagerie / Épicerie fine coupe",e:"🧀",i:["Choucroute","Comté coupe","Édam vieux","Fromages coupe","Jambon coupe","Mimolette vieille","Pain pita","Saucisse italienne","Saucisson"]},
  {n:"Frais emballé (charcuterie / plats)",e:"🥗",i:["Bacon","Chorizo","Croque monsieur","Dés de jambon","Gnocchi","Jambon","Jambon cru","Panisses","Patanegra","Pâtes fraîches","Polenta","Ravioles","Raviolis","Saucisses Strasbourg","Viande des grisons"]},
  {n:"Volaille / Viande libre-service",e:"🍗",i:["Aiguillettes de poulet","Ailes de poulet x12","Blanc de poulet x8","Bœuf haché","Coquelets x3","Cuisses de canard","Cuisse de poulet","Escalope de dinde x6","Magret de canard","Œufs de caille écalés","Pilons de poulet x8","Saucisses montbéliard","Veau haché"]},
  {n:"Fruits & Légumes",e:"🥦",i:["Ail","Ananas","Aneth","Artichauts","Asperges","Aubergines x5","Avocats","Basilic","Betterave","Brocolis","Carotte","Cebette","Céleri","Cerises","Cerneaux noix","Champignons","Champignons shitake","Chou fleur","Chou chinois ou chou blanc","Ciboulette","Citron bio","Citrons bio","Citrons verts","Clémentine","Concombre x2","Coriandre","Courge","Échalotes","Endives mini","Épinard","Fenouil","Fèves","Framboises","Fraises","Gaspacho","Gingembre","Haricots frais","Kiwi","Laitue","Mandarine","Mangue","Mâche x2","Melon x2","Menthe","Myrtilles","Navet","Nectarine","Œufs de mouettes","Oignon rouge x2","Oignons blancs","Oignons frais","Oignons paille x2","Olives apéro x2","Orange","Pastèque","Patate douce","Pêches","Pêches plates","Persil","Petites tomates","Pignons","Poireaux","Poivrons rouge x2","Pommes x3","Pommes de terre","Pommes de terre grenailles","Pommes rouges","Pousse de soja","Pruneaux","Radis","Raisin","Riz sushis","Salade romaine","Salade verte","Sushis","Tomates normales x2","Wasabi"]},
  {n:"Rayon frais (œufs, lardons…)",e:"🥚",i:["Bacon","Lardons x3","Œufs de caille","Pâte brisée x2","Pâtes à pizza x3"]},
  {n:"Yaourts & Boissons froides",e:"🥛",i:["Choco Fresh","Crêpes","Danonino","Dessert Cathy","Fromage blanc","Jus d'ananas","Jus de fruits","Kinder puingui","Yaourt","Yaourt grec","Yaourt nature","Yop"]},
  {n:"Fromage libre-service",e:"🫙",i:["Beurre","Burrata","Burrata à la truffe","Bûche de chèvre","Caprice des dieux indiv","Cheddar","Comté","Crème fraîche épaisse","Crème fraiche semi épaisse","Crème fraîche liquide","Crottin","Emmental tranché","Fêta","Fromage raclette","Gervais","Gouda","Mozza bille","Mozza râpée","Morbier","Parmesan","Parmesan râpé","Râpé","Ricotta","Roquefort","Saint Moret grosse barquette","Saint Moret individuel","Tartare"]},
  {n:"Poissonnerie & Conserves poisson",e:"🐟",i:["Anchois","Blinis","Brandade","Cabillaud","Cacolac","Calamar","Crevettes","Croûtons","Écrevisses","Guacamole","Hareng à l'huile","Lait","Lotte","Maquereau au poivre","Moules","Œufs de saumon","Œufs x10","Poisson","Poutargue","Saumon frais","Saumon fumé tranches","Saumon gravlax x2","Saumon mi cuit x2","Saumon sésame x4","Thon","Tzatziki"]},
  {n:"Épicerie salée & Condiments",e:"🧂",i:["Bouillon bœuf","Bouillon volaille","Bouquet garni","Câpres","Concentré de tomates","Cornichons","Curcuma","Fécule de Pdt","Gros sel de guérande","Ketchup","Maïs","Mayo Amora fouettée","Mini pain burger","Moutarde","Moutarde ancienne","Olives noires","Olives noires kerretz","Olives vertes","Pain burger","Pain de mie","Paprika doux","Poivre","Riste aubergine","Royco asperge","Saké","Sardines","Sauce soja sucrée","Sel fin La Baleine","Sel moulin","Thon à l'huile","Thon naturel","Vinaigre blanc","Vinaigre de riz","Vinaigrette","Oignons frits"]},
  {n:"Épicerie féculents & Conserves",e:"🍝",i:["Beurre de cacahuète","Cannelloni","Champignons","Champignons noirs","Concentré de tomates","Coulis de tomates","Couscous","Curry vert","Ebly","Feuille de riz","Gressins","Kit Fajitas","Lasagne","Lentilles","Lait de coco","Nouilles chinoises","Pain burger","Pâtes","Pâtes alphabet","Pâtes blé dur","Pâtes coquillettes","Pâtes orecchiette","Perles de blé","Pois chiche","Purée","Quinoa","Riz","Riz thaï 1kg mini","Risotto","Sauce nems","Tomates en boîte","Tomates pelées","Vermicelles de riz"]},
  {n:"Huiles & Apéritif",e:"🫒",i:["Bretzels","Cacahuètes","Chips","Chips barbecue","Chips de légumes","Chips lentilles","Huile friture Frial Rouge","Huile olive","Isio 4","Pistaches"]},
  {n:"Biscuits & Céréales petit-déj",e:"🍪",i:["Baiochi","Barre M&M'S","Björg Avoine","Céréales Monoprix","Crêpe dentelle","Crêpes wahou","Finger","Galette de riz choco","Gaufres chocolat","Gaufres sucre","Granola","Lulu l'ourson","Mikado","Napolitain","Petits écoliers","Prince"]},
  {n:"Pâtisserie & Confiserie",e:"🍫",i:["Bonbons Haribo","Chapelure","Chocolat","Chocolat Lindt noisettes","Chocolat Lindt noir 70%","Farine","Maïzena","Miel","Nutella","Pâte d'amande","Piment Tabasco vert","Sucre en poudre","Sucre morceaux","Sucre vanillé"]},
  {n:"Compotes & Petit-déjeuner",e:"🥣",i:["Bonjour","Compote monop","Compotes rouges","Compotes vertes","Cookie crisps","Corn flakes","Fitness Monoprix","Galette Maïs","Krisprols"]},
  {n:"Cave / Alcools",e:"🍾",i:["Aperol","Bitter San Pellegrino","Champagne rosé","Prosecco","Ricard","St germain"]},
  {n:"Entretien & Ménage",e:"🧹",i:["Ajax vitres","Antical","Capsuleslave vaisselle","Capsules machine à laver","Décapfour","Désodorisant toilette","Destop","Éponges rouges","Éponges vertes","Feuille papier cuisson","Javel","Javel gel","Javel spray","K2R","Lessive poudre","Lingettes cucul","Lingettes désinfectantes wc","Lingettes WC","Liquide vaisselle petit","M. propre sol","Papier alu","Pastilles javel","PQ","Sac congélation","Sac glaçons","Sac poubelle 50 L","Sac poubelle 100 L","Sanitol cuisine","Sopalin","WC net"]},
  {n:"Surgelés",e:"❄️",i:["Brocolis","Croustines","Épinards congelés x2","Frites allumettes","Gambas","Glaçons","Haricots verts","Mars glaces","Petit pois","Poisson","Poisson pané","Pommes de terre noisettes","Pommes de terre rissolées","Pops","Steak haché"]},
  {n:"Boissons & Pain emballé",e:"🥤",i:["Badoit","Boisson anniversaire","Cidre","Coca","Coca zéro","Corona","Eau","Fruit shoot","Fustea","Jus d'abricot","Jus pomme","Oasis","PaC citron","Pago multifruit","Pain complet","Pain tranché","Pain tranché noir","Petites bouteilles eau"]}
];
// Tri alphabétique sans accent de chaque rayon
const collator = new Intl.Collator('fr', {sensitivity:'base'});
DATA.forEach(sec => sec.i.sort((a,b) => collator.compare(a,b)));
const TOTAL = DATA.reduce((s,sec)=>s+sec.i.length, 0);

// ── STATE ────────────────────────────────────────────────────────────────
const SK = 'courses_v4';
let S = {sel:{}, got:{}};   // sel = sélectionné maison, got = dans le panier
let mode = 'maison';
let q = '';

function load(){ try{ const r=localStorage.getItem(SK); if(r) S=JSON.parse(r); }catch(e){} }
function save(){ try{ localStorage.setItem(SK,JSON.stringify(S)); }catch(e){} }
function kk(sn,it){ return sn+'||'+it; }
function nrm(s){ return s.toLowerCase().normalize('NFD').replace(/[\u0300-\u036f]/g,''); }
function hl(txt){ if(!q) return txt; const n=nrm(txt),nq=nrm(q),i=n.indexOf(nq); if(i<0) return txt; return txt.slice(0,i)+'<mark>'+txt.slice(i,i+q.length)+'</mark>'+txt.slice(i+q.length); }
function cntSel(){ return Object.keys(S.sel).length; }
function cntGot(){ return Object.keys(S.got).length; }
function cntPend(){ return Object.keys(S.sel).filter(k=>!S.got[k]).length; }

// ── TOGGLE ───────────────────────────────────────────────────────────────
function toggle(sn, it){
  const k=kk(sn,it);
  if(mode==='maison'){
    if(S.sel[k]){ delete S.sel[k]; delete S.got[k]; }
    else { S.sel[k]=1; }
  } else if(mode==='magasin'){
    if(S.got[k]){ delete S.got[k]; }
    else { S.got[k]=1; }
  }
  save();
  render();
}

// ── CONFIRM OVERLAY ───────────────────────────────────────────────────────
function showConfirm(msg, onYes){
  document.getElementById('confirm-msg').textContent = msg;
  document.getElementById('overlay').className = 'overlay show';
  document.getElementById('cb-yes').onclick = ()=>{
    document.getElementById('overlay').className = 'overlay';
    onYes();
  };
  document.getElementById('cb-no').onclick = ()=>{
    document.getElementById('overlay').className = 'overlay';
  };
}

// ── RESET ────────────────────────────────────────────────────────────────
function reset(){
  if(mode==='maison'){
    showConfirm('Effacer toute la sélection ?', ()=>{ S={sel:{},got:{}}; save(); render(); });
  } else if(mode==='magasin'){
    showConfirm('Remettre tous les articles en "à prendre" ?', ()=>{ S.got={}; save(); render(); });
  } else if(mode==='panier'){
    showConfirm('Vider le panier ?', ()=>{ S.got={}; save(); render(); });
  }
}

// ── BARCODE EAN-13 (pur SVG, sans lib) ──────────────────────────────────
function drawBarcode(){
  const num = '9240036667162';
  // Encoding table EAN-13
  const L=[
    [0,0,0,1,1,0,1],[0,0,1,1,0,0,1],[0,0,1,0,0,1,1],[0,1,1,1,1,0,1],
    [0,1,0,0,0,1,1],[0,1,1,0,0,0,1],[0,1,0,1,1,1,1],[0,1,1,1,0,1,1],
    [0,1,1,0,1,1,1],[0,0,0,1,0,1,1]
  ];
  const G=[
    [0,1,0,0,1,1,1],[0,1,1,0,0,1,1],[0,0,1,1,0,1,1],[0,1,0,0,0,0,1],
    [0,0,1,1,1,0,1],[0,1,1,1,0,0,1],[0,0,0,0,1,0,1],[0,0,1,0,0,0,1],
    [0,0,0,1,0,0,1],[0,0,1,0,1,1,1]
  ];
  const R=[
    [1,1,1,0,0,1,0],[1,1,0,0,1,1,0],[1,1,0,1,1,0,0],[1,0,0,0,0,1,0],
    [1,0,1,1,1,0,0],[1,0,0,1,1,1,0],[1,0,1,0,0,0,0],[1,0,0,0,1,0,0],
    [1,0,0,1,0,0,0],[1,1,1,0,1,0,0]
  ];
  // First digit parity patterns
  const P=[
    [0,0,0,0,0,0],[0,0,1,0,1,1],[0,0,1,1,0,1],[0,0,1,1,1,0],
    [0,1,0,0,1,1],[0,1,1,0,0,1],[0,1,1,1,0,0],[0,1,0,1,0,1],
    [0,1,0,1,1,0],[0,1,1,0,1,0]
  ];
  const d = num.split('').map(Number);
  const parity = P[d[0]];
  let bars = [1,0,1]; // start guard
  for(let i=0;i<6;i++){
    const enc = parity[i]===0 ? L[d[i+1]] : G[d[i+1]];
    bars = bars.concat(enc);
  }
  bars = bars.concat([0,1,0,1,0]); // middle guard
  for(let i=7;i<13;i++) bars = bars.concat(R[d[i]]);
  bars = bars.concat([1,0,1]); // end guard

  const svgEl = document.getElementById('bc');
  const W = svgEl.parentElement.offsetWidth || 300;
  const bw = W / bars.length;
  const H = 80;
  let rects = '';
  bars.forEach((b,i)=>{
    if(b) rects += `<rect x="${(i*bw).toFixed(2)}" y="0" width="${bw.toFixed(2)}" height="${H}" fill="#1a1207"/>`;
  });
  svgEl.setAttribute('viewBox',`0 0 ${W} ${H}`);
  svgEl.innerHTML = rects;
}

// ── RENDER ───────────────────────────────────────────────────────────────
function render(){
  const secsEl = document.getElementById('secs');
  const carteEl = document.getElementById('carte');
  const infoBar = document.getElementById('info-bar');
  const srch = document.getElementById('srch');

  // Tabs highlight
  document.querySelectorAll('.tab').forEach(t=>t.classList.toggle('on', t.dataset.m===mode));

  if(mode==='carte'){
    secsEl.style.display='none';
    carteEl.className='carte show';
    infoBar.style.display='none';
    srch.className='srch';
    document.getElementById('btm-inf').innerHTML='💳 Monoprix';
    document.getElementById('btm-btn').textContent='🏠 Ma liste';
    document.getElementById('btm-btn').onclick=()=>{mode='maison';render();};
    drawBarcode();
    return;
  }

  secsEl.style.display='';
  carteEl.className='carte';
  infoBar.style.display='';
  srch.className='srch'+(mode==='maison'?' show':'');

  // Info bar
  const ib = document.getElementById('info-n');
  const bb = document.getElementById('info-b');
  const it = document.getElementById('info-t');
  const itotal = document.getElementById('info-total');
  ib.className = 'info-n c-'+mode;
  if(mode==='maison'){ bb.textContent=cntSel(); it.textContent=' sélectionné(s)'; itotal.textContent='/ '+TOTAL+' articles'; }
  else if(mode==='magasin'){ bb.textContent=cntPend(); it.textContent=' à prendre'; itotal.textContent=''; }
  else { bb.textContent=cntGot(); it.textContent=' dans le panier'; itotal.textContent=''; }

  // Bottom
  const bi=document.getElementById('btm-inf'), btn=document.getElementById('btm-btn');
  if(mode==='maison'){
    bi.innerHTML='<strong>'+cntSel()+'</strong> sélectionné(s)';
    btn.textContent='🛍️ Aller en magasin';
    btn.onclick=()=>{mode='magasin';render();};
  } else if(mode==='magasin'){
    bi.innerHTML='🧺 Panier : <strong>'+cntGot()+'</strong>';
    btn.textContent='Voir le panier';
    btn.onclick=()=>{mode='panier';render();};
  } else {
    bi.innerHTML='<strong>'+cntGot()+'</strong> pris';
    btn.textContent='🛍️ Retour magasin';
    btn.onclick=()=>{mode='magasin';render();};
  }

  // Mode class
  secsEl.className='secs m-'+mode;
  secsEl.innerHTML='';

  let any=false;
  DATA.forEach(sec=>{
    let items=sec.i;
    if(mode==='magasin') items=items.filter(it=>S.sel[kk(sec.n,it)]&&!S.got[kk(sec.n,it)]);
    else if(mode==='panier') items=items.filter(it=>S.got[kk(sec.n,it)]);
    if(q) items=items.filter(it=>nrm(it).includes(nrm(q)));
    if(!items.length) return;
    any=true;

    const sd=document.createElement('div'); sd.className='sec';
    const sh=document.createElement('div'); sh.className='sec-hdr';
    sh.innerHTML='<div class="sec-name"><span>'+sec.e+'</span>'+sec.n+'</div><div class="sec-meta"><span class="sec-ct">'+items.length+'</span><span class="chev">▾</span></div>';
    sh.addEventListener('click',()=>sd.classList.toggle('fold'));
    const sb=document.createElement('div'); sb.className='sec-body';
    items.forEach(it=>{
      const k=kk(sec.n,it);
      const div=document.createElement('div');
      let cls='itm';
      if(mode==='maison'&&S.sel[k]) cls+=' sel';
      if(mode==='magasin'&&S.got[k]) cls+=' got';
      if(mode==='panier') cls+=' got';
      div.className=cls;
      div.innerHTML='<div class="box"><span class="ck">✓</span></div><div class="lbl">'+hl(it)+'</div>';
      div.addEventListener('click',()=>toggle(sec.n,it));
      sb.appendChild(div);
    });
    sd.appendChild(sh); sd.appendChild(sb); secsEl.appendChild(sd);
  });

  if(!any){
    const e=document.createElement('div'); e.className='empty';
    if(mode==='maison') e.innerHTML='<div class="ei">📝</div>Aucun article trouvé.';
    else if(mode==='magasin') e.innerHTML='<div class="ei">🎉</div>Tous les articles sont dans le panier !';
    else e.innerHTML='<div class="ei">🧺</div>Le panier est vide.<br>Décoche des articles en mode Magasin.';
    secsEl.appendChild(e);
  }
}

// ── EVENTS ───────────────────────────────────────────────────────────────
document.getElementById('rst').addEventListener('click', reset);

document.getElementById('sinput').addEventListener('input',function(){
  q=this.value.trim();
  document.getElementById('sx').style.display=q?'block':'none';
  render();
});
document.getElementById('sx').addEventListener('click',()=>{
  document.getElementById('sinput').value=''; q='';
  document.getElementById('sx').style.display='none';
  render();
});
document.querySelectorAll('.tab').forEach(t=>{
  t.addEventListener('click',()=>{ mode=t.dataset.m; render(); });
});

load(); render();

</script>
</body>
</html>
