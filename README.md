<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
    <title>Hutan Masak - Game Memasak Hewan untuk HP</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
        }

        body {
            background: linear-gradient(145deg, #1a4d2a 0%, #0d331c 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Quicksand', 'Comic Neue', system-ui, -apple-system, sans-serif;
            padding: 12px;
        }

        /* Container utama - layar HP friendly */
        .game-wrapper {
            max-width: 550px;
            width: 100%;
            margin: 0 auto;
            background: #fef0cf;
            border-radius: 56px 56px 48px 48px;
            box-shadow: 0 20px 35px rgba(0,0,0,0.4), inset 0 1px 4px rgba(255,250,210,0.8);
            padding: 16px 18px 24px 18px;
        }

        /* Panel utama */
        .game-panel {
            background: #ffefc0;
            border-radius: 44px;
            padding: 16px;
            box-shadow: inset 0 0 0 3px #fff8e7, inset 0 0 0 8px #e8cf94, 0 8px 18px rgba(0,0,0,0.2);
        }

        /* Header skor dan progress */
        .stats-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 12px;
            background: #6b4423;
            border-radius: 60px;
            padding: 8px 16px;
            margin-bottom: 18px;
            box-shadow: inset 0 1px 3px #c9944a, 0 5px 0 #3e2a14;
        }

        .stat-card {
            background: #2c1f0f;
            padding: 6px 14px;
            border-radius: 40px;
            display: flex;
            align-items: center;
            gap: 8px;
            font-weight: bold;
            color: #ffefb9;
            font-size: 1.1rem;
            flex: 1;
            justify-content: center;
        }

        .stat-card span:first-child {
            font-size: 1rem;
            background: #d4963a;
            padding: 3px 10px;
            border-radius: 30px;
        }

        /* Karakter Hewan - area sentuh */
        .character-area {
            background: #f9e2a4;
            border-radius: 55px;
            padding: 12px;
            margin-bottom: 18px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
            flex-wrap: wrap;
            box-shadow: inset 0 0 0 2px #fff0c8, 0 6px 0 #c2a162;
        }

        .animal-box {
            display: flex;
            align-items: center;
            gap: 12px;
            background: #ffefcf;
            padding: 6px 20px 6px 16px;
            border-radius: 60px;
            flex: 2;
            min-width: 140px;
        }

        .animal-emoji {
            font-size: 3.4rem;
            filter: drop-shadow(3px 5px 0 rgba(0,0,0,0.2));
            transition: transform 0.1s ease;
        }

        .animal-name {
            font-weight: bold;
            font-size: 1rem;
            background: #b4752e;
            padding: 5px 12px;
            border-radius: 30px;
            color: white;
        }

        .level-badge {
            background: #ffb347;
            padding: 6px 14px;
            border-radius: 40px;
            font-size: 0.8rem;
            font-weight: bold;
            color: #3d2b14;
        }

        /* Area Pesanan / Resep */
        .order-card {
            background: #f3e2b5;
            border-radius: 40px;
            padding: 14px;
            margin-bottom: 18px;
            text-align: center;
            border: 2px dashed #dba549;
        }

        .order-label {
            font-weight: bold;
            font-size: 0.8rem;
            background: #c58333;
            display: inline-block;
            padding: 4px 16px;
            border-radius: 30px;
            color: white;
            margin-bottom: 8px;
        }

        .recipe-target {
            background: white;
            border-radius: 60px;
            padding: 10px 8px;
            margin: 8px 0;
            font-size: 1.6rem;
            font-weight: bold;
            letter-spacing: 2px;
            box-shadow: inset 0 1px 4px #e6d5aa, 0 4px 8px rgba(0,0,0,0.1);
            word-break: break-word;
        }

        .recipe-detail {
            font-size: 0.8rem;
            background: #ecc47c;
            display: inline-block;
            padding: 4px 12px;
            border-radius: 30px;
            color: #2f2416;
            font-weight: bold;
        }

        /* Bahan-bahan - grid sentuh */
        .ingredients-area {
            background: #e7cf97;
            border-radius: 45px;
            padding: 12px;
            margin-bottom: 18px;
        }

        .ingredients-area h3 {
            font-size: 0.95rem;
            text-align: center;
            margin-bottom: 12px;
            color: #3b2a18;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
        }

        .ingredients-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(85px, 1fr));
            gap: 10px;
        }

        .ingredient-btn {
            background: #fff6e0;
            border-radius: 50px;
            padding: 10px 4px;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.05s linear;
            box-shadow: 0 4px 0 #b88a48;
            text-align: center;
            touch-action: manipulation;
        }

        .ingredient-btn:active {
            transform: translateY(2px);
            box-shadow: 0 1px 0 #b88a48;
        }

        .ingredient-emoji {
            font-size: 2rem;
        }

        .ingredient-name {
            font-size: 0.7rem;
            font-weight: bold;
            color: #5a3c18;
        }

        /* Panci / Wajan sentuh */
        .pot-area {
            background: #6f502b;
            border-radius: 55px;
            padding: 12px;
            margin-bottom: 18px;
            box-shadow: inset 0 0 0 3px #ebce8a, 0 7px 0 #3a2a12;
        }

        .pot-container {
            background: #4d3a1e;
            border-radius: 50px;
            padding: 12px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .pot-content {
            background: #2f2412;
            min-height: 80px;
            border-radius: 50px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            flex-wrap: wrap;
            padding: 12px;
            font-size: 1.8rem;
            color: #ffefb0;
            text-align: center;
            cursor: pointer;
            transition: 0.1s;
            touch-action: manipulation;
        }

        .pot-content:active {
            background: #4a3a1f;
        }

        .cook-button {
            background: #f59f2a;
            border: none;
            font-size: 1.5rem;
            font-weight: bold;
            padding: 14px;
            border-radius: 50px;
            color: white;
            cursor: pointer;
            transition: 0.07s linear;
            box-shadow: 0 6px 0 #b45317;
            text-align: center;
            touch-action: manipulation;
            letter-spacing: 2px;
        }

        .cook-button:active {
            transform: translateY(3px);
            box-shadow: 0 2px 0 #b45317;
        }

        /* Pesan notifikasi */
        .message-area {
            background: #efdfb0;
            border-radius: 40px;
            padding: 12px;
            text-align: center;
            font-weight: bold;
            font-size: 0.8rem;
            color: #5a3f1c;
            margin-bottom: 12px;
            transition: 0.1s;
        }

        .reset-btn {
            background: #cb873b;
            width: 100%;
            border: none;
            padding: 12px;
            border-radius: 50px;
            font-weight: bold;
            font-size: 1rem;
            color: white;
            cursor: pointer;
            box-shadow: 0 4px 0 #7a481f;
            transition: 0.05s linear;
            touch-action: manipulation;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .reset-btn:active {
            transform: translateY(2px);
            box-shadow: 0 1px 0 #7a481f;
        }

        @media (max-width: 480px) {
            .game-wrapper {
                padding: 10px 12px 18px 12px;
            }
            .ingredients-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 8px;
            }
            .recipe-target {
                font-size: 1.3rem;
            }
            .animal-emoji {
                font-size: 2.7rem;
            }
            .stat-card {
                font-size: 0.9rem;
                padding: 4px 8px;
            }
        }
    </style>
</head>
<body>
<div class="game-wrapper">
    <div class="game-panel">
        <!-- Skor & Resep -->
        <div class="stats-bar">
            <div class="stat-card">
                <span>🍲 SKOR</span>
                <span id="scoreValue">0</span>
            </div>
            <div class="stat-card">
                <span>📜 MENU</span>
                <span id="recipeCounter">0</span>
            </div>
        </div>

        <!-- Karakter Hewan -->
        <div class="character-area">
            <div class="animal-box">
                <div class="animal-emoji" id="animalEmoji">🦝</div>
                <div class="animal-name" id="animalName">Chef Raccoon</div>
            </div>
            <div class="level-badge" id="levelBadge">⭐ Level 1</div>
        </div>

        <!-- Pesanan Aktif -->
        <div class="order-card">
            <div class="order-label">🍽️ RESEP HARI INI 🍽️</div>
            <div class="recipe-target" id="targetRecipe">🍲 ???</div>
            <div class="recipe-detail" id="recipeHint">Kumpulkan bahan yang tepat!</div>
        </div>

        <!-- Bahan Dapur (Grid sentuh) -->
        <div class="ingredients-area">
            <h3>🥕 BAHAN DAPUR (ketuk untuk masukkan ke wajan)</h3>
            <div class="ingredients-grid" id="ingredientsGrid"></div>
        </div>

        <!-- Area Panci + Tombol Masak -->
        <div class="pot-area">
            <div class="pot-container">
                <div class="pot-content" id="potContent">
                    🍳 Kosong
                </div>
                <button class="cook-button" id="cookBtn">🔥 MASAK! 🔥</button>
            </div>
        </div>

        <!-- Notifikasi & Reset -->
        <div class="message-area" id="messageBox">
            ✨ Halo! Masukkan bahan, lalu tekan MASAK ✨
        </div>
        <button class="reset-btn" id="resetGameBtn">🔄 Mulai Ulang Petualangan 🔄</button>
    </div>
</div>

<script>
    // ======================= DATA GAME =========================
    // Karakter Hewan (berubah setiap 3 resep berhasil)
    const ANIMALS = [
        { name: "Chef Raccoon", emoji: "🦝", level: "Pemakan Segala" },
        { name: "Chef Bear", emoji: "🐻‍❄️", level: "Master Madu" },
        { name: "Chef Bunny", emoji: "🐇", level: "Pelompat Wortel" },
        { name: "Chef Fox", emoji: "🦊", level: "Koki Licin" },
        { name: "Chef Panda", emoji: "🐼", level: "Bamboo Chef" }
    ];
    
    // Resep-resep masakan
    const RECIPES = [
        { id: 0, name: "Sup Wortel Segar", emoji: "🥕", ingredients: ["wortel", "air"], display: "🥕 Sup Wortel 🥣", reward: 20 },
        { id: 1, name: "Telur Dadar Hutan", emoji: "🍳", ingredients: ["telur", "minyak"], display: "🍳 Telur Dadar 🍳", reward: 20 },
        { id: 2, name: "Spaghetti Lezat", emoji: "🍝", ingredients: ["pasta", "saus"], display: "🍝 Spaghetti Merah 🍅", reward: 20 },
        { id: 3, name: "Salad Buah Segar", emoji: "🥗", ingredients: ["apel", "pisang"], display: "🥗 Salad Buah 🍎🍌", reward: 20 },
        { id: 4, name: "Ikan Bakar Jeruk", emoji: "🐟", ingredients: ["ikan", "jeruk"], display: "🐟 Ikan Bakar Jeruk 🍊", reward: 20 },
        { id: 5, name: "Nasi Goreng Spesial", emoji: "🍚", ingredients: ["nasi", "telur"], display: "🍚 Nasi Goreng 🍳", reward: 25 },
        { id: 6, name: "Pancake Madu", emoji: "🥞", ingredients: ["tepung", "madu"], display: "🥞 Pancake Madu 🍯", reward: 25 }
    ];
    
    // Daftar Bahan yang tersedia
    const INGREDIENTS = [
        { id: "wortel", name: "Wortel", emoji: "🥕" },
        { id: "air", name: "Air", emoji: "💧" },
        { id: "telur", name: "Telur", emoji: "🥚" },
        { id: "minyak", name: "Minyak", emoji: "🫒" },
        { id: "pasta", name: "Pasta", emoji: "🍝" },
        { id: "saus", name: "Saus", emoji: "🥫" },
        { id: "apel", name: "Apel", emoji: "🍎" },
        { id: "pisang", name: "Pisang", emoji: "🍌" },
        { id: "ikan", name: "Ikan", emoji: "🐟" },
        { id: "jeruk", name: "Jeruk", emoji: "🍊" },
        { id: "nasi", name: "Nasi", emoji: "🍚" },
        { id: "tepung", name: "Tepung", emoji: "🌾" },
        { id: "madu", name: "Madu", emoji: "🍯" }
    ];
    
    // Game State
    let currentScore = 0;
    let completedMenus = 0;       // total resep berhasil dimasak
    let currentAnimalIdx = 0;
    let currentRecipe = null;
    let potItems = [];            // daftar id bahan di panci
    
    // DOM elements
    const scoreSpan = document.getElementById("scoreValue");
    const recipeCounterSpan = document.getElementById("recipeCounter");
    const animalEmojiSpan = document.getElementById("animalEmoji");
    const animalNameSpan = document.getElementById("animalName");
    const levelBadge = document.getElementById("levelBadge");
    const targetRecipeDiv = document.getElementById("targetRecipe");
    const recipeHintSpan = document.getElementById("recipeHint");
    const potContentDiv = document.getElementById("potContent");
    const cookBtn = document.getElementById("cookBtn");
    const messageBox = document.getElementById("messageBox");
    const ingredientsGrid = document.getElementById("ingredientsGrid");
    const resetBtn = document.getElementById("resetGameBtn");
    
    // Helper: tampilkan pesan
    function showMessage(msg, isError = false) {
        messageBox.innerHTML = isError ? `⚠️ ${msg} ⚠️` : `✨ ${msg} ✨`;
        messageBox.style.background = isError ? "#fad6aa" : "#fff2d2";
        setTimeout(() => {
            if (messageBox.innerHTML === `⚠️ ${msg} ⚠️` || messageBox.innerHTML === `✨ ${msg} ✨`) {
                messageBox.innerHTML = "🍳 Ketuk bahan, masak sesuai resep! 🍳";
                messageBox.style.background = "#efdfb0";
            }
        }, 1800);
    }
    
    // Update tampilan hewan berdasarkan jumlah completedMenus
    function updateAnimalByProgress() {
        let newIndex = Math.floor(completedMenus / 3) % ANIMALS.length;
        if (newIndex !== currentAnimalIdx) {
            currentAnimalIdx = newIndex;
            animalEmojiSpan.innerText = ANIMALS[currentAnimalIdx].emoji;
            animalNameSpan.innerText = ANIMALS[currentAnimalIdx].name;
            levelBadge.innerHTML = `⭐ ${ANIMALS[currentAnimalIdx].level} ⭐`;
            showMessage(`${ANIMALS[currentAnimalIdx].name} datang membantu dapur! 🎉`, false);
        } else {
            animalEmojiSpan.innerText = ANIMALS[currentAnimalIdx].emoji;
            animalNameSpan.innerText = ANIMALS[currentAnimalIdx].name;
            levelBadge.innerHTML = `⭐ ${ANIMALS[currentAnimalIdx].level} ⭐`;
        }
    }
    
    // Update UI statistik (skor, jumlah menu selesai, hewan)
    function updateStatsUI() {
        scoreSpan.innerText = currentScore;
        recipeCounterSpan.innerText = `${completedMenus}`;
        updateAnimalByProgress();
    }
    
    // Pilih resep baru secara acak (bisa sama, tetapi lebih seru)
    function pickNewRecipe() {
        const randomIndex = Math.floor(Math.random() * RECIPES.length);
        currentRecipe = { ...RECIPES[randomIndex] };
        targetRecipeDiv.innerHTML = currentRecipe.display;
        const bahanList = currentRecipe.ingredients.map(b => {
            const found = INGREDIENTS.find(i => i.id === b);
            return found ? found.emoji : b;
        }).join(' + ');
        recipeHintSpan.innerHTML = `📜 butuh: ${bahanList}`;
        showMessage(`Pesanan baru: ${currentRecipe.name}!`, false);
    }
    
    // Update tampilan panci
    function updatePotDisplay() {
        if (potItems.length === 0) {
            potContentDiv.innerHTML = "🍳 (kosong, ketuk untuk ambil bahan)";
            return;
        }
        const itemEmojis = potItems.map(id => {
            const ing = INGREDIENTS.find(i => i.id === id);
            return ing ? ing.emoji : id;
        });
        potContentDiv.innerHTML = itemEmojis.join(" + ");
    }
    
    // Tambah bahan ke panci (dari klik bahan)
    function addToPot(ingredientId) {
        if (!currentRecipe) {
            showMessage("Resep belum siap, coba lagi!", true);
            return;
        }
        if (potItems.length >= 5) {
            showMessage("Panci terlalu penuh! Klik panci untuk mengambil bahan.", true);
            return;
        }
        potItems.push(ingredientId);
        updatePotDisplay();
        const ingName = INGREDIENTS.find(i => i.id === ingredientId)?.name || ingredientId;
        showMessage(`✔️ ${ingName} masuk wajan!`, false);
    }
    
    // Hapus bahan dari panci (klik panci)
    function removeLastFromPot() {
        if (potItems.length === 0) {
            showMessage("Panci kosong, tidak ada yang bisa diambil", false);
            return;
        }
        const removed = potItems.pop();
        const ingName = INGREDIENTS.find(i => i.id === removed)?.name || removed;
        updatePotDisplay();
        showMessage(`🔪 Mengambil ${ingName} dari panci`, false);
    }
    
    // Cek apakah bahan di panci cocok dengan resep saat ini (urutan tak penting)
    function isRecipeMatch() {
        if (!currentRecipe) return false;
        const required = [...currentRecipe.ingredients];
        if (potItems.length !== required.length) return false;
        const potCopy = [...potItems];
        for (let req of required) {
            const idx = potCopy.indexOf(req);
            if (idx === -1) return false;
            potCopy.splice(idx, 1);
        }
        return true;
    }
    
    // Proses memasak
    function cookMeal() {
        if (!currentRecipe) {
            showMessage("Tidak ada pesanan aktif!", true);
            return;
        }
        if (potItems.length === 0) {
            showMessage("Panci kosong! Masukkan bahan dulu.", true);
            return;
        }
        
        if (isRecipeMatch()) {
            // Sukses!
            const reward = currentRecipe.reward || 20;
            currentScore += reward;
            completedMenus++;
            updateStatsUI();
            showMessage(`🎉 Hore! ${currentRecipe.name} berhasil! +${reward} poin! 🎉`, false);
            
            // Kosongkan panci
            potItems = [];
            updatePotDisplay();
            
            // Resep baru
            pickNewRecipe();
            
            // Bonus tiap 5 resep
            if (completedMenus % 5 === 0 && completedMenus > 0) {
                const bonus = 30;
                currentScore += bonus;
                updateStatsUI();
                showMessage(`🏆 Bonus resek ke-${completedMenus}! +${bonus} poin! Karakter sem
