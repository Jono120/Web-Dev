<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "056641280211e52fd0adb81b6058ec55",
  "translation_date": "2025-08-29T10:51:55+00:00",
  "source_file": "6-space-game/2-drawing-to-canvas/README.md",
  "language_code": "cs"
}
-->
# Vytvořte vesmírnou hru, část 2: Kreslení hrdiny a monster na plátno

## Kvíz před přednáškou

[Kvíz před přednáškou](https://ff-quizzes.netlify.app/web/quiz/31)

## Plátno

Plátno je HTML prvek, který nemá ve výchozím nastavení žádný obsah; je to prázdná plocha. Musíte na něj něco nakreslit.

✅ Přečtěte si [více o Canvas API](https://developer.mozilla.org/docs/Web/API/Canvas_API) na MDN.

Takto se obvykle deklaruje jako součást těla stránky:

```html
<canvas id="myCanvas" width="200" height="100"></canvas>
```

Výše nastavujeme `id`, `width` a `height`.

- `id`: nastavte, abyste mohli získat referenci, když s ním budete chtít pracovat.
- `width`: šířka prvku.
- `height`: výška prvku.

## Kreslení jednoduché geometrie

Plátno používá kartézský souřadnicový systém pro kreslení objektů. Používá tedy osu x a osu y k určení, kde se něco nachází. Pozice `0,0` je v levém horním rohu a pravý dolní roh odpovídá hodnotám WIDTH a HEIGHT plátna.

![mřížka plátna](../../../../translated_images/canvas_grid.5f209da785ded492a01ece440e3032afe51efa500cc2308e5ea4252487ceaf0b.cs.png)
> Obrázek z [MDN](https://developer.mozilla.org/docs/Web/API/Canvas_API/Tutorial/Drawing_shapes)

Pro kreslení na prvek plátna musíte projít následujícími kroky:

1. **Získat referenci** na prvek plátna.
2. **Získat referenci** na kontextový prvek, který je na plátně.
3. **Proveďte kreslící operaci** pomocí kontextového prvku.

Kód pro výše uvedené kroky obvykle vypadá takto:

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

✅ Canvas API se většinou zaměřuje na 2D tvary, ale můžete také kreslit 3D prvky na webovou stránku; k tomu můžete použít [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API).

S Canvas API můžete kreslit různé věci, například:

- **Geometrické tvary**, už jsme ukázali, jak nakreslit obdélník, ale můžete kreslit mnohem více.
- **Text**, můžete kreslit text s libovolným písmem a barvou.
- **Obrázky**, můžete kreslit obrázky na základě obrazových souborů, jako jsou .jpg nebo .png.

✅ Vyzkoušejte to! Už víte, jak nakreslit obdélník, dokážete nakreslit kruh na stránku? Podívejte se na některé zajímavé kresby na plátně na CodePen. Zde je [zvláště působivý příklad](https://codepen.io/dissimulate/pen/KrAwx).

## Načtení a vykreslení obrazového souboru

Obrazový soubor načtete vytvořením objektu `Image` a nastavením jeho vlastnosti `src`. Poté posloucháte událost `load`, abyste věděli, kdy je připraven k použití. Kód vypadá takto:

### Načtení souboru

```javascript
const img = new Image();
img.src = 'path/to/my/image.png';
img.onload = () => {
  // image loaded and ready to be used
}
```

### Vzor načítání souboru

Doporučuje se zabalit výše uvedené do konstruktu, jako je tento, aby bylo snazší jej používat a abyste se pokusili s ním manipulovat pouze tehdy, když je plně načten:

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

Pro vykreslení herních prvků na obrazovku by váš kód vypadal takto:

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

## Teď je čas začít stavět vaši hru

### Co vytvořit

Vytvoříte webovou stránku s prvkem plátna. Měla by vykreslit černou obrazovku `1024*768`. Poskytli jsme vám dva obrázky:

- Loď hrdiny

   ![Loď hrdiny](../../../../translated_images/player.dd24c1afa8c71e9b82b2958946d4bad13308681392d4b5ddcc61a0e818ef8088.cs.png)

- 5*5 monster

   ![Loď monstra](../../../../translated_images/enemyShip.5df2a822c16650c2fb3c06652e8ec8120cdb9122a6de46b9a1a56d54db22657f.cs.png)

### Doporučené kroky pro zahájení vývoje

Najděte soubory, které byly vytvořeny pro vás ve složce `your-work`. Měla by obsahovat následující:

```bash
-| assets
  -| enemyShip.png
  -| player.png
-| index.html
-| app.js
-| package.json
```

Otevřete kopii této složky ve Visual Studio Code. Měli byste mít nastavené lokální vývojové prostředí, nejlépe s Visual Studio Code s NPM a Node nainstalovanými. Pokud nemáte `npm` nastavený na svém počítači, [zde je návod, jak to udělat](https://www.npmjs.com/get-npm).

Spusťte svůj projekt navigací do složky `your_work`:

```bash
cd your-work
npm start
```

Výše uvedené spustí HTTP server na adrese `http://localhost:5000`. Otevřete prohlížeč a zadejte tuto adresu. Zatím je to prázdná stránka, ale to se změní.

> Poznámka: pro zobrazení změn na obrazovce obnovte prohlížeč.

### Přidání kódu

Přidejte potřebný kód do `your-work/app.js`, abyste vyřešili následující:

1. **Nakreslete** plátno s černým pozadím
   > tip: přidejte dva řádky pod příslušný TODO v `/app.js`, nastavte prvek `ctx` na černou barvu a souřadnice nahoře/vlevo na 0,0 a výšku a šířku na hodnoty plátna.
2. **Načtěte** textury
   > tip: přidejte obrázky hráče a nepřítele pomocí `await loadTexture` a předáním cesty k obrázku. Zatím je na obrazovce neuvidíte!
3. **Nakreslete** hrdinu do středu obrazovky ve spodní polovině
   > tip: použijte API `drawImage` k vykreslení heroImg na obrazovku, nastavte `canvas.width / 2 - 45` a `canvas.height - canvas.height / 4)`;
4. **Nakreslete** 5*5 monster
   > tip: Nyní můžete odkomentovat kód pro vykreslení nepřátel na obrazovku. Dále přejděte do funkce `createEnemies` a doplňte ji.

   Nejprve nastavte několik konstant:

    ```javascript
    const MONSTER_TOTAL = 5;
    const MONSTER_WIDTH = MONSTER_TOTAL * 98;
    const START_X = (canvas.width - MONSTER_WIDTH) / 2;
    const STOP_X = START_X + MONSTER_WIDTH;
    ```

   poté vytvořte smyčku pro vykreslení pole monster na obrazovku:

    ```javascript
    for (let x = START_X; x < STOP_X; x += 98) {
        for (let y = 0; y < 50 * 5; y += 50) {
          ctx.drawImage(enemyImg, x, y);
        }
      }
    ```

## Výsledek

Hotový výsledek by měl vypadat takto:

![Černá obrazovka s hrdinou a 5*5 monstry](../../../../translated_images/partI-solution.36c53b48c9ffae2a5e15496b23b604ba5393433e4bf91608a7a0a020eb7a2691.cs.png)

## Řešení

Nejprve se pokuste vyřešit to sami, ale pokud se zaseknete, podívejte se na [řešení](../../../../6-space-game/2-drawing-to-canvas/solution/app.js).

---

## 🚀 Výzva

Naučili jste se kreslit pomocí Canvas API zaměřeného na 2D; podívejte se na [WebGL API](https://developer.mozilla.org/docs/Web/API/WebGL_API) a zkuste nakreslit 3D objekt.

## Kvíz po přednášce

[Kvíz po přednášce](https://ff-quizzes.netlify.app/web/quiz/32)

## Recenze a samostudium

Zjistěte více o Canvas API [čtením o něm](https://developer.mozilla.org/docs/Web/API/Canvas_API).

## Zadání

[Hrajte si s Canvas API](assignment.md)

---

**Upozornění**:  
Tento dokument byl přeložen pomocí služby pro automatický překlad [Co-op Translator](https://github.com/Azure/co-op-translator). I když se snažíme o co největší přesnost, mějte prosím na paměti, že automatické překlady mohou obsahovat chyby nebo nepřesnosti. Původní dokument v jeho původním jazyce by měl být považován za závazný zdroj. Pro důležité informace doporučujeme profesionální lidský překlad. Neodpovídáme za žádná nedorozumění nebo nesprávné výklady vyplývající z použití tohoto překladu.