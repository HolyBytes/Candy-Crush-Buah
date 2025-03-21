**🍭 Deskripsi Lengkap Source Code (SC) Candy Crush Buah**  
SC ini adalah **game berbasis web** yang terinspirasi dari **Candy Crush**, menggunakan **HTML, CSS, dan JavaScript**. Tujuan permainan adalah **mencocokkan minimal 3 buah/permen yang sama dalam satu garis** untuk mendapatkan skor.  

🔗 **Mau langsung main? Yuk coba sekarang!**  
👉 **[Mainkan Candy Crush Buah](https://holybytes.github.io/Candy-Crush-Buah/)**  

---

## **📌 1. Struktur Source Code**  
SC ini terdiri dari **satu file utama**, yaitu **`index.html`**, yang mencakup:  
- **HTML** → Struktur tampilan game.  
- **CSS (internal)** → Desain dan animasi papan permainan.  
- **JavaScript** → Logika permainan, termasuk pencocokan, efek spesial, dan perhitungan skor.  

---

## **🎨 2. Desain dan Tampilan**  

### **a. Warna dan Tema**  
✔ **Latar belakang** → Gradien pink dan peach dengan animasi.  
✔ **Tombol interaktif** → Warna merah dengan efek hover membesar.  
✔ **Papan permainan** → **Grid 8x8** dengan kotak putih dan bayangan lembut.  
✔ **Efek spesial**:  
   - **💣 Bom** → Menghapus area **3x3**.  
   - **🍭 Permen Garis** → Menghapus **satu baris atau kolom** penuh.  

### **b. Animasi dan Efek**  
✔ **Tombol hover** → Sedikit membesar saat disentuh.  
✔ **Animasi kotak** → Transisi halus saat berpindah.  
✔ **Efek visual** → Kotak khusus berwarna merah (bom) dan hijau (permen garis).  

---

## **🛠 3. Elemen HTML (Struktur Game)**  
### **a. Menu Utama**  
```html
<div id="main-menu">
    <h1>🍭 Candy Crush Buah 🍬</h1>
    <button onclick="startGame()">Mulai Permainan</button>
    <button onclick="showInstructions()">Cara Bermain</button>
</div>
```
✔ Berisi **judul game dan dua tombol** untuk memilih mode permainan.  

### **b. Papan Permainan (Grid 8x8)**  
```html
<div id="game-container">
    <div id="score">⭐ Skor: 0</div>
    <div id="game-board"></div>
    <button onclick="restartGame()">Restart</button>
</div>
```
✔ Menampilkan **papan permainan (grid 8x8), skor, dan tombol restart**.  

---

## **🎮 4. Logika Permainan (JavaScript dari `index4.html`)**  
Kode ini menangani **logika permainan**, termasuk **pembuatan papan permainan, pertukaran item, pencocokan buah/permen, dan skor**.  

### **a. Struktur Data**  
```js
const items = ['🍎', '🍌', '🍇', '🍉', '🍰', '🍭'];
const boardSize = 8;
let board = [];
let score = 0;
```
✔ **Menyimpan daftar buah/permen, ukuran papan (8x8), dan skor pemain**.  

---

### **b. Fungsi Memulai Game**  
```js
function startGame() {
    document.getElementById('main-menu').style.display = 'none';
    document.getElementById('game-container').style.display = 'flex';
    score = 0;
    initBoard();
}
```
✔ **Menampilkan papan permainan**, menyembunyikan menu utama, dan menginisialisasi papan.  

---

### **c. Pengecekan Kombinasi Buah yang Cocok**  
```js
function checkMatches() {
    const matches = [];
    for (let i = 0; i < boardSize; i++) {
        for (let j = 0; j < boardSize; j++) {
            if (j < boardSize - 2 && board[i][j] === board[i][j + 1] && board[i][j] === board[i][j + 2]) {
                matches.push({ row: i, col: j });
            }
            if (i < boardSize - 2 && board[i][j] === board[i + 1][j] && board[i][j] === board[i + 2][j]) {
                matches.push({ row: i, col: j });
            }
        }
    }
    if (matches.length > 0) {
        removeMatches(matches);
    }
}
```
✔ **Mengecek apakah ada 3 buah/permen yang berjejer horizontal atau vertikal**.  

---

### **d. Efek Bom dan Permen Garis**  
```js
function removeMatches(matches) {
    matches.forEach(({ row, col }) => {
        board[row][col] = randomItem();
    });
    score += matches.length;
    scoreDisplay.textContent = `⭐ Skor: ${score}`;
    renderBoard();
    setTimeout(checkMatches, 300);
}
```
✔ Jika ada **buah/permen yang cocok**, maka **dihilangkan dan skor bertambah**.  

---

### **e. Fungsi Menampilkan Instruksi**  
```js
function showInstructions() {
    alert('🍬 Geser buah/permen untuk mencocokkan minimal 3 item:\n\n💣 Bom: Dapatkan dengan mencocokkan 4 item (meledak area 3x3)\n🍭 Permen Garis: Dapatkan dengan mencocokkan 5 item (menghapus baris/kolom).');
}
```
✔ Menampilkan **cara bermain dalam pop-up alert**.  

---

### **f. Fungsi Mengacak Buah & Render Papan**  
```js
function randomItem() {
    return items[Math.floor(Math.random() * items.length)];
}

function initBoard() {
    board = [];
    for (let i = 0; i < boardSize; i++) {
        const row = [];
        for (let j = 0; j < boardSize; j++) {
            row.push(randomItem());
        }
        board.push(row);
    }
    renderBoard();
}
```
✔ **Menghasilkan buah acak di setiap kotak** dan menampilkan **papan permainan pertama kali**.  

---

### **g. Fungsi Swap (Menukar Buah yang Diklik)**  
```js
let firstTile = null;

function handleTileClick(e) {
    const row = parseInt(e.target.dataset.row);
    const col = parseInt(e.target.dataset.col);

    if (firstTile) {
        swapTiles(firstTile.row, firstTile.col, row, col);
        firstTile = null;
    } else {
        firstTile = { row, col };
    }
}
```
✔ **Pemain memilih 2 kotak, lalu buahnya ditukar**.  

---

## **🔥 5. Fitur Unggulan**  
✔ **Gameplay sederhana tapi menantang**.  
✔ **Papan permainan 8x8** dengan efek spesial.  
✔ **Bom & Permen Garis** menambah strategi.  
✔ **Tampilan modern & animasi interaktif**.  
✔ **Efek hover dan transisi halus**.  

---

## **🚀 6. Kesimpulan**  
SC ini adalah **game Candy Crush Buah berbasis web** yang ringan dan menyenangkan! Menggunakan **HTML, CSS, dan JavaScript** dengan **logika pencocokan** dan **efek spesial** untuk pengalaman bermain yang seru.  

🔗 **Mau langsung main? Yuk coba sekarang!**  
👉 **[Mainkan Candy Crush Buah](https://holybytes.github.io/Candy-Crush-Buah/)**  
