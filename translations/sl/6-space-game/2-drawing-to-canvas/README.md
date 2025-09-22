<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-29T12:51:07+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "sl"
}
-->
# Zgradite vesoljsko igro, 2. del: Risanje junaka in pošasti na platno

## Predhodni kviz

[Predhodni kviz](https://ff-quizzes.netlify.app/web/quiz/31)

## Platno

Platno (Canvas) je HTML element, ki privzeto nima vsebine; je prazno platno. Dodati mu morate vsebino z risanjem nanj.

✅ Preberite [več o Canvas API](https://developer.mozilla.org/docs/Web/API/Canvas_API) na MDN.

Tukaj je primer, kako ga običajno deklariramo kot del telesa strani:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

Zgoraj nastavimo `id`, `width` in `height`.

- `id`: nastavite to, da lahko pridobite referenco, ko morate z njim interagirati.
- `width`: to je širina elementa.
- `height`: to je višina elementa.

## Risanje preproste geometrije

Platno uporablja kartezični koordinatni sistem za risanje. Zato uporablja x-os in y-os za izražanje lokacije nečesa. Lokacija `0,0` je zgornji levi kot, spodnji desni kot pa je določena z nastavljeno ŠIRINO in VIŠINO platna.

![mreža platna](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.sl.png)  
> Slika iz [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

Za risanje na element platna morate slediti naslednjim korakom:

1. **Pridobite referenco** na element platna.
2. **Pridobite referenco** na element Context, ki se nahaja na platnu.
3. **Izvedite risalno operacijo** z uporabo elementa Context.

Koda za zgornje korake običajno izgleda takole:

```javascript
// draws a red rectangle
//1. get the canvas reference
canvas = document.getElementById("myCanvas");

//2. set the context to 2D to draw basic shapes
ctx = canvas.getContext("2d");

//3. fill it with the color red
ctx.fillStyle = 'red';

//4. and draw a rectangle with these parameters, setting location and size
ctx.fillRect(0,0, 200, 200) // x,y,width, height
```

✅ Canvas API se večinoma osredotoča na 2D oblike, vendar lahko na spletno stran narišete tudi 3D elemente; za to lahko uporabite [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API).

S Canvas API lahko narišete vse vrste stvari, kot so:

- **Geometrijske oblike**, že smo pokazali, kako narisati pravokotnik, vendar lahko narišete še veliko več.
- **Besedilo**, lahko narišete besedilo s katero koli pisavo in barvo.
- **Slike**, lahko narišete sliko na podlagi slikovne datoteke, kot je .jpg ali .png.

✅ Poskusite! Zdaj, ko veste, kako narisati pravokotnik, lahko poskusite narisati krog na stran? Oglejte si nekaj zanimivih risb na platnu na CodePen. Tukaj je [posebej impresiven primer](https://codepen.io/dissimulate/pen/KrAwx).

## Nalaganje in risanje slikovnega vira

Slikovni vir naložite tako, da ustvarite objekt `Image` in nastavite njegovo lastnost `src`. Nato poslušate dogodek `load`, da veste, kdaj je pripravljen za uporabo. Koda izgleda takole:

### Nalaganje vira

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### Vzorec nalaganja vira

Priporočljivo je, da zgornje zavijete v strukturo, kot je ta, da je lažje za uporabo in da poskrbite, da ga poskušate manipulirati šele, ko je popolnoma naložen:

```javascript
function loadAsset(path) {
  return new Promise((resolve) => {
    const img = new Image();
    img.src = path;
    img.onload = () => {
      // image loaded and ready to be used
      resolve(img);
    }
  })
}

// use like so

async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')
}

```

Za risanje igralnih virov na zaslon bi vaša koda izgledala takole:

```javascript
async function run() {
  const heroImg = await loadAsset('hero.png')
  const monsterImg = await loadAsset('monster.png')

  canvas = document.getElementById("myCanvas");
  ctx = canvas.getContext("2d");
  ctx.drawImage(heroImg, canvas.width/2,canvas.height/2);
  ctx.drawImage(monsterImg, 0,0);
}
```

## Zdaj je čas, da začnete graditi svojo igro

### Kaj zgraditi

Zgradili boste spletno stran z elementom platna. Prikazati mora črn zaslon velikosti `1024*768`. Na voljo imate dve sliki:

- Junakovo plovilo

   ![Junakovo plovilo](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.sl.png)

- 5*5 pošasti

   ![Pošastno plovilo](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.sl.png)

### Priporočeni koraki za začetek razvoja

Poiščite datoteke, ki so bile ustvarjene za vas v podmapi `your-work`. Vsebujejo naj naslednje:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Odprite kopijo te mape v Visual Studio Code. Potrebujete lokalno razvojno okolje, po možnosti z Visual Studio Code, NPM in Node nameščenimi. Če `npm` ni nastavljen na vašem računalniku, [tukaj je, kako to storiti](https://www.npmjs.com/get-npm).

Začnite svoj projekt tako, da se premaknete v mapo `your_work`:

```bash
cd your-work
npm start
```

Zgornji ukaz bo zagnal HTTP strežnik na naslovu `http://localhost:5000`. Odprite brskalnik in vnesite ta naslov. Trenutno je stran prazna, vendar se bo to spremenilo.

> Opomba: za ogled sprememb na zaslonu osvežite brskalnik.

### Dodajte kodo

Dodajte potrebno kodo v `your-work/app.js`, da rešite spodnje:

1. **Narišite** platno s črnim ozadjem  
   > namig: dodajte dve vrstici pod ustrezen TODO v `/app.js`, nastavite element `ctx` na črno in zgornje/leve koordinate na 0,0, višino in širino pa na velikost platna.
2. **Naložite** teksture  
   > namig: dodajte slike igralca in sovražnika z uporabo `await loadTexture` in podajte pot do slike. Na zaslonu jih še ne boste videli!
3. **Narišite** junaka na sredino zaslona v spodnji polovici  
   > namig: uporabite API `drawImage`, da narišete heroImg na zaslon, nastavite `canvas.width / 2 - 45` in `canvas.height - canvas.height / 4)`.
4. **Narišite** 5*5 pošasti  
   > namig: zdaj lahko odstranite komentarje iz kode za risanje sovražnikov na zaslon. Nato pojdite v funkcijo `createEnemies` in jo dokončajte.

   Najprej nastavite nekaj konstant:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

    nato ustvarite zanko za risanje matrike pošasti na zaslon:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## Rezultat

Končni rezultat naj bi izgledal takole:

![Črn zaslon z junakom in 5*5 pošasti](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.sl.png)

## Rešitev

Najprej poskusite rešiti sami, če pa se zataknete, si oglejte [rešitev](../../../../6-space-game/2-drawing-to-canvas/solution/app.js).

---

## 🚀 Izziv

Naučili ste se risanja z 2D Canvas API; poglejte si [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) in poskusite narisati 3D objekt.

## Zaključni kviz

[Zaključni kviz](https://ff-quizzes.netlify.app/web/quiz/32)

## Pregled in samostojno učenje

Več o Canvas API se naučite z [branjem o njem](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## Naloga

[Preizkusite Canvas API](assignment.md)

---

**Omejitev odgovornosti**:  
Ta dokument je bil preveden z uporabo storitve za prevajanje z umetno inteligenco [Co-op Translator](https://github.com/Azure/co-op-translator). Čeprav si prizadevamo za natančnost, vas prosimo, da upoštevate, da lahko avtomatizirani prevodi vsebujejo napake ali netočnosti. Izvirni dokument v njegovem izvirnem jeziku je treba obravnavati kot avtoritativni vir. Za ključne informacije priporočamo profesionalni človeški prevod. Ne prevzemamo odgovornosti za morebitna nesporazumevanja ali napačne razlage, ki bi nastale zaradi uporabe tega prevoda.