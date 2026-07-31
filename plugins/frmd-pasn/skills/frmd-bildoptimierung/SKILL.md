---
name: "frmd-bildoptimierung"
description: "Optimiert Produktfotos gerahmter Trikots, Trading Cards oder signierter Bilder für die FRMD-PASN-Website (frmdpasn.art): freistellen, edler Galerie-Look (Spotlight/Beton/Clean), 4:5-Web-Export. Nutzen, wenn ein FRMD-PASN-Foto für Homepage/Galerie/Hero aufbereitet, ein Trikot-/Card-Foto „optimiert\", „freigestellt\" oder mit Beton-/Galerie-Hintergrund versehen werden soll."
---

# FRMD PASN – Bildoptimierung

Bereitet rohe Produktfotos gerahmter Trikots / Trading Cards / signierter Bilder für die Website **frmdpasn.art** auf: sauber freigestellt, edler Galerie-Hintergrund, web-optimiertes 4:5-Zielformat.

## Wichtige Fakten (zuerst lesen)
- **Marke:** FRMD PASN, One-of-One Custom Framing aus Köln. Look: premium, minimalistisch. Rahmen schwarz.
- **Keine API-Connectoren** für Firefly/Photoroom/Canva. Freistellen läuft über **Photoroom im Browser** (Claude-in-Chrome, Nutzer muss eingeloggt sein). Der finale Aufbau passiert **in Python** (zuverlässiger).
- **Firefly meist überflüssig:** Rahmen sind i. d. R. gerade fotografiert, kaum echte Glasreflexionen. Nur bei sichtbarer Schieflage entzerren.
- **Datei-Zugriff:** In den Chat geladene Bilder liegen nicht automatisch als Datei vor. Basis-Ordner ist `OneDrive - Optima Gruppe AG\FRMD PASN\`. Browser-Downloads landen in `Downloads\` (Ordner ggf. verbinden, um Exporte abzuholen).
- **Echtheitsmerkmale NIE entfernen:** FRMD-PASN-Hologramm, Beckett-„B"-Sticker mit QR, Name-Plate, Trading Card. Beweisen „One of One".

## Ablauf
1. **Analyse:** Auflösung, Schiefe, Reflexionen prüfen. Firefly nur bei Bedarf.
2. **Freistellen (Photoroom, Browser):** Foto laden → Hintergrund automatisch entfernt → KI-Hintergrund-Layer **ausblenden** → als **transparentes PNG** exportieren (PNG-Format, Standard-Auflösung reicht).
3. **Look erzeugen (Python):** Mit dem unten eingebetteten Skript `frmd_composite.py` das PNG auf den Hintergrund setzen. **Standard: immer beide Vorlagen erzeugen** – `kreativ_spotlight` und `beton_struktur`.
4. **Prüfen:** Ergebnis visuell ansehen (Bild lesen), dann dem Nutzer zeigen. Bei Feedback Parameter anpassen.
5. **Freigabe/Export:** Beste Version als `hero-<name>.jpg` (1200×1500).

## Zielformat & Web
- Homepage/Galerie = **4:5**. Hero-Datei **1200×1500** (= aktuelles `hero-wagner.jpg`); Slot nutzt `object-fit: cover` ~0,84 → großzügige Ränder lassen. Zusätzlich 1600×2000 als hochauflösende Reserve.
- JPEG Qualität ~88, `optimize=True` (~200–280 KB).
- Für 1:1 / 16:9 die Wand **seitlich erweitern** (Rahmen nie anschneiden), nicht croppen.

## Verfügbare Looks (Skript-Styles)
- ⭐ `kreativ_spotlight` – warmes Museums-Spotlight, heller Halo (Standard-Vorlage)
- ⭐ `beton_struktur` – strukturierte Betonwand mit Relief (Standard-Vorlage)
- `beton_glatt` – matte Sichtbetonwand (kühl), `beton_brett` – wärmerer Beton, Brettschalung
- `kreativ_dark` – dunkle Wand + Orlando-Magic-Blau-Akzent
- `clean` – helle Studiowand

Feinjustierung Spotlight-Grauton: in `kreativ_spotlight` die Werte `c` (center, hell) und `e` (edge, dunkler) anpassen.

## Ablage & Benennung (in `FRMD PASN\Bildproduktion\`)
```
0_Admin\{Anleitungen, Skripte, Marke}
1_Freigestellt\   (transparente PNGs)
2_Looks\{Spotlight, Beton, Clean}
3_Web-fertig\{Hero, Galerie, Social}
```
- Präfix nach Typ: `trikot_`, `card_`, `foto_`. Schema `<typ>_<name>_<look>_<größe>.jpg` (z. B. `trikot_wagner_22_spotlight_1200.jpg`).
- Rohfotos bleiben in `Frames\`, `Jerseys\`, `Memorabilia\`.

## Skript
Skript nach `frmd_composite.py` schreiben, Abhängigkeiten installieren, dann aufrufen:
```
pip install pillow numpy --break-system-packages
python frmd_composite.py <cutout.png> <style> <out_basename>
# erzeugt <out_basename>_1600.jpg und <out_basename>_1200.jpg
```

```python
import sys
from PIL import Image, ImageFilter, ImageChops, ImageDraw
import numpy as np

def noise(W,H,sh,sw,seed):
    r=np.random.default_rng(seed); s=r.normal(0,1,(sh,sw))
    return np.array(Image.fromarray(((s-s.min())/np.ptp(s)*255).astype('uint8')).resize((W,H),Image.BICUBIC),dtype=float)/255.
def lf(W,H,sh,sw,amp,seed):
    return (noise(W,H,sh,sw,seed)-0.5)*amp*2
def grid(W,H):
    return np.linspace(0,1,W)[None,:], np.linspace(0,1,H)[:,None]

def beton_glatt(W,H):
    xg,yg=grid(W,H)
    top=np.array([201,200,196]); bot=np.array([179,178,173])
    b=np.repeat(top[None,None,:]*(1-yg[:,:,None])+bot[None,None,:]*yg[:,:,None],W,axis=1)
    b=b+(lf(W,H,10,8,6.5,11)+lf(W,H,26,20,3.5,12)+np.random.default_rng(7).normal(0,1,(H,W))*2.6)[:,:,None]
    img=Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'); d=ImageDraw.Draw(img,'RGBA')
    for c in (1,):
        x=int(W*c/2); d.line([(x,0),(x,H)],fill=(150,149,145,55),width=2)
    for r in (1,2):
        y=int(H*r/3); d.line([(0,y),(W,y)],fill=(150,149,145,55),width=2)
    rad=max(6,int(W*0.007))
    for xi in (0,W//2,W):
        for yi in (0,H//3,2*H//3,H):
            x=min(max(xi,rad*4),W-rad*4); y=min(max(yi,rad*4),H-rad*4)
            d.ellipse([x-rad,y-rad,x+rad,y+rad],fill=(120,119,115,70))
            d.ellipse([x-rad+1,y+1,x+rad-1,y+rad+1],fill=(232,231,226,30))
    a=np.array(img.filter(ImageFilter.GaussianBlur(0.6)),dtype=float)
    a=a+((0.5-np.sqrt((xg-0.42)**2*1.1+(yg-0.28)**2))*20)[:,:,None]
    a=a-((np.sqrt((xg-0.5)**2+(yg-0.5)**2)-0.3).clip(0)*28)[:,:,None]
    return Image.fromarray(np.clip(a,0,255).astype('uint8'),'RGB'),'wall'

def beton_brett(W,H):
    xg,yg=grid(W,H)
    top=np.array([190,186,178]); bot=np.array([168,164,156])
    b=np.repeat(top[None,None,:]*(1-yg[:,:,None])+bot[None,None,:]*yg[:,:,None],W,axis=1)
    b=b+(lf(W,H,12,9,5.5,5)+lf(W,H,30,22,3,6)+np.random.default_rng(7).normal(0,1,(H,W))*2.4)[:,:,None]
    img=Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'); d=ImageDraw.Draw(img,'RGBA')
    pl=int(H/9)
    for i in range(1,9):
        y=i*pl; d.line([(0,y),(W,y)],fill=(150,146,138,60),width=2); d.line([(0,y+2),(W,y+2)],fill=(214,210,202,35),width=1)
    rad=max(5,int(W*0.006))
    for i in range(1,9,2):
        y=i*pl
        for fx in (0.2,0.5,0.8):
            x=int(W*fx); d.ellipse([x-rad,y-rad,x+rad,y+rad],fill=(120,116,108,70)); d.ellipse([x-rad+1,y+1,x+rad-1,y+rad+1],fill=(226,222,214,28))
    a=np.array(img.filter(ImageFilter.GaussianBlur(0.5)),dtype=float)
    a=a+((0.5-np.sqrt((xg-0.4)**2*1.1+(yg-0.3)**2))*18)[:,:,None]-((np.sqrt((xg-0.5)**2+(yg-0.5)**2)-0.3).clip(0)*26)[:,:,None]
    return Image.fromarray(np.clip(a,0,255).astype('uint8'),'RGB'),'wall'

def beton_struktur(W,H):
    xg,yg=grid(W,H)
    top=np.array([196,196,193]); bot=np.array([171,171,167])
    b=np.repeat(top[None,None,:]*(1-yg[:,:,None])+bot[None,None,:]*yg[:,:,None],W,axis=1)
    hf=noise(W,H,16,12,3)*0.5+noise(W,H,40,30,4)*0.3+noise(W,H,120,90,5)*0.2
    gy,gx=np.gradient(hf); shade=-(gx*-0.7+gy*-0.7); shade=shade/(np.abs(shade).max()+1e-6)
    b=b+(shade*46)[:,:,None]
    sp=np.random.default_rng(8).random((H,W)); b=b+(np.where(sp>0.994,-30,0)+np.where(sp<0.004,22,0))[:,:,None]
    img=Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'); d=ImageDraw.Draw(img,'RGBA')
    pl=int(H/8)
    for i in range(1,8):
        y=i*pl; d.line([(0,y),(W,y)],fill=(120,119,114,90),width=3); d.line([(0,y+3),(W,y+3)],fill=(225,224,219,35),width=1)
    d.line([(W//2,0),(W//2,H)],fill=(120,119,114,70),width=2)
    a=np.array(img.filter(ImageFilter.GaussianBlur(0.5)),dtype=float)
    a=a+((0.5-np.sqrt((xg-0.4)**2*1.1+(yg-0.3)**2))*16)[:,:,None]-((np.sqrt((xg-0.5)**2+(yg-0.5)**2)-0.32).clip(0)*24)[:,:,None]
    return Image.fromarray(np.clip(a,0,255).astype('uint8'),'RGB'),'wall'

def kreativ_dark(W,H):
    xg,yg=grid(W,H)
    top=np.array([26,28,34]); bot=np.array([12,13,17])
    b=np.repeat(top[None,None,:]*(1-yg[:,:,None])+bot[None,None,:]*yg[:,:,None],W,axis=1)
    b=b+(lf(W,H,40,30,3,3))[:,:,None]
    b=b+((0.42-np.sqrt((xg-0.5)**2*1.15+(yg-0.42)**2)).clip(0)*140)[:,:,None]*np.array([1.0,0.98,0.92])[None,None,:]
    blue=(0.5-np.sqrt((xg-0.5)**2*1.4+(yg-0.92)**2)).clip(0)
    b[:,:,2]+=blue*120; b[:,:,1]+=blue*40; b[:,:,0]+=blue*10
    rim=np.exp(-((yg-0.16)**2)/0.0009)*np.exp(-((xg-0.5)**2)/0.06); b[:,:,2]+=rim*70; b[:,:,1]+=rim*25
    b=b-((np.sqrt((xg-0.5)**2+(yg-0.5)**2)-0.28).clip(0)*70)[:,:,None]
    return Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'),'dark'

def kreativ_spotlight(W,H):
    xg,yg=grid(W,H)
    t=np.clip(np.sqrt((xg-0.5)**2*1.05+(yg-0.40)**2)/0.92,0,1)
    c=np.array([222,217,210]); e=np.array([120,115,109])
    b=c[None,None,:]*(1-t[:,:,None])+e[None,None,:]*t[:,:,None]
    b=b+((noise(W,H,40,30,21)-0.5)*7)[:,:,None]
    fp=np.exp(-((yg-0.9)**2)/0.006)*np.exp(-((xg-0.5)**2)/0.12); b=b+(fp*18)[:,:,None]*np.array([1.0,0.96,0.88])[None,None,:]
    return Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'),'dark'

def clean(W,H):
    xg,yg=grid(W,H)
    top=np.array([238,237,234]); bot=np.array([224,223,220])
    b=np.repeat(top[None,None,:]*(1-yg[:,:,None])+bot[None,None,:]*yg[:,:,None],W,axis=1)
    b=b+(lf(W,H,50,40,1.1,9))[:,:,None]
    b=b+((0.5-np.sqrt((xg-0.45)**2*1.1+(yg-0.32)**2))*14)[:,:,None]-((np.sqrt((xg-0.5)**2+(yg-0.5)**2)-0.34).clip(0)*22)[:,:,None]
    return Image.fromarray(np.clip(b,0,255).astype('uint8'),'RGB'),'wall'

STYLES={'beton_glatt':beton_glatt,'beton_brett':beton_brett,'beton_struktur':beton_struktur,
        'kreativ_dark':kreativ_dark,'kreativ_spotlight':kreativ_spotlight,'clean':clean}

def compose(cutout_path, style, out_base, frac=0.80):
    cut=Image.open(cutout_path).convert('RGBA')
    al=np.array(cut)[:,:,3]; ys,xs=np.where(al>20)
    frame=cut.crop((xs.min(),ys.min(),xs.max()+1,ys.max()+1)); FW,FH=frame.size
    for W,H,suf,q in [(1600,2000,'_1600',90),(1200,1500,'_1200',88)]:
        bg,mode=STYLES[style](W,H); bg=bg.convert('RGBA')
        th=int(H*frac); tw=int(th*FW/FH)
        if tw>int(W*0.86): tw=int(W*0.86); th=int(tw*FH/FW)
        fr=frame.resize((tw,th),Image.LANCZOS); px=(W-tw)//2; py=(H-th)//2
        sh=Image.new('L',(W,H),0); sh.paste(fr.split()[3],(px,py))
        if mode=='dark': sh=sh.filter(ImageFilter.GaussianBlur(30)); sh=ImageChops.offset(sh,0,20); op=0.55
        else: sh=sh.filter(ImageFilter.GaussianBlur(13)); sh=ImageChops.offset(sh,5,9); op=0.45
        shl=Image.new('RGBA',(W,H),(0,0,0,0)); shl.putalpha(Image.fromarray((np.array(sh,dtype=float)*op).astype('uint8'),'L'))
        comp=Image.alpha_composite(bg,shl); comp.alpha_composite(fr,(px,py))
        comp.convert('RGB').save(f"{out_base}{suf}.jpg",quality=q,optimize=True)
        print("saved",f"{out_base}{suf}.jpg")

if __name__=='__main__':
    if len(sys.argv)!=4 or sys.argv[2] not in STYLES:
        print("Nutzung: python frmd_composite.py <cutout.png> <style> <out_basename>")
        print("Styles:", ", ".join(STYLES)); sys.exit(1)
    compose(sys.argv[1], sys.argv[2], sys.argv[3])
```

