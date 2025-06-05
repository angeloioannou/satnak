<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Satoshi Samurai 3D</title>
  <style>
    body { margin: 0; overflow: hidden; font-family: sans-serif; background: #000; color: #fff; }
    #hud {
      position: absolute;
      top: 10px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(0, 0, 0, 0.5);
      padding: 8px 16px;
      border: 2px solid #f2a900;
      border-radius: 8px;
    }
    canvas { display: block; }
  </style>
</head>
<body>
  <div id="hud">🪙 BTC: 0 | 📍 Tokyo Market | 🧩 Clues: 0/3</div>
  <script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>
  <script>
    let score = 0, clues = 0, level = 1;

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Samurai (player)
    const samuraiGeometry = new THREE.BoxGeometry(1, 1, 1);
    const samuraiMaterial = new THREE.MeshBasicMaterial({ color: 0xf2a900 });
    const samurai = new THREE.Mesh(samuraiGeometry, samuraiMaterial);
    samurai.position.y = -4;
    scene.add(samurai);

    // Coin array
    const coins = [];

    // Camera position
    camera.position.z = 10;

    // Spawn coin
    function spawnCoin() {
      const geometry = new THREE.SphereGeometry(0.3, 16, 16);
      const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
      const coin = new THREE.Mesh(geometry, material);
      coin.position.x = (Math.random() - 0.5) * 8;
      coin.position.y = 5;
      coin.speed = 0.05 + Math.random() * 0.03;
      scene.add(coin);
      coins.push(coin);
    }

    // Update HUD
    function updateHUD() {
      document.getElementById("hud").innerText =
        `🪙 BTC: ${score} | 📍 ${["Tokyo", "Wall Street", "Valley", "Forest", "Cave"][level - 1]} | 🧩 Clues: ${clues}/3`;
    }

    // Boss fight
    function bossFight() {
      alert("⚔️ Fight Satoshi! Use arrows to dodge!");
      // Future: Add 3D enemy model and fight mechanics
    }

    // Coin logic
    function updateCoins() {
      for (let i = coins.length - 1; i >= 0; i--) {
        coins[i].po
