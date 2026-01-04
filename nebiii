<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kalp Animasyonu</title>
<style>
html, body {
    margin: 0;
    padding: 0;
    background: black;
    overflow: hidden;
}
canvas {
    display: block;
}
.text {
    position: absolute;
    top: 8%;
    width: 100%;
    text-align: center;
    color: white;
    font-size: 22px;
    font-family: Arial, sans-serif;
    opacity: 0.9;
    z-index: 2;
}
</style>
</head>
<body>

<div class="text">seniii çooookkk<br>seviyoruuuuuummmm</div>
<canvas id="canvas"></canvas>

<script>
const canvas = document.getElementById("canvas");
const ctx = canvas.getContext("2d");

let w, h;
function resize() {
    w = canvas.width = innerWidth;
    h = canvas.height = innerHeight;
}
resize();
addEventListener("resize", resize);

const particles = [];
const particleCount = 2600;
const centerX = () => w / 2;
const centerY = () => h / 2;

const mouse = { x: w / 2, y: h / 2 };
addEventListener("mousemove", e => {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
});

// KLASİK ve NET kalp formülü
function heartPoint(t) {
    return {
        x: 16 * Math.pow(Math.sin(t), 3),
        y: -(13 * Math.cos(t)
            - 5 * Math.cos(2 * t)
            - 2 * Math.cos(3 * t)
            - Math.cos(4 * t))
    };
}

// DOLU KALP: katman katman içe doğru
const heartTargets = [];
const scale = 14;

for (let r = 1; r > 0; r -= 0.015) {
    for (let t = 0; t < Math.PI * 2; t += 0.02) {
        const p = heartPoint(t);
        heartTargets.push({
            x: centerX() + p.x * scale * r,
            y: centerY() + p.y * scale * r
        });
    }
}

// Parçacıkları oluştur
for (let i = 0; i < particleCount; i++) {
    const target = heartTargets[i % heartTargets.length];
    particles.push({
        x: Math.random() * w,
        y: Math.random() * h,
        tx: target.x,
        ty: target.y,
        vx: 0,
        vy: 0
    });
}

function animate() {
    ctx.clearRect(0, 0, w, h);

    for (const p of particles) {
        const dx = mouse.x - p.x;
        const dy = mouse.y - p.y;
        const dist = Math.hypot(dx, dy);

        if (dist < 120) {
            p.vx -= dx / dist;
            p.vy -= dy / dist;
        }

        p.vx += (p.tx - p.x) * 0.02;
        p.vy += (p.ty - p.y) * 0.02;

        p.vx *= 0.85;
        p.vy *= 0.85;

        p.x += p.vx;
        p.y += p.vy;

        ctx.beginPath();
        ctx.arc(p.x, p.y, 1.6, 0, Math.PI * 2);
        ctx.fillStyle = "#e0003a";
        ctx.fill();
    }

    requestAnimationFrame(animate);
}

animate();
</script>
</body>
</html>
