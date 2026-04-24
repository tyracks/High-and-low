<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>High Low Trainer</title>
<style>
body { text-align:center; font-family: Arial; background:#f5f5f5; }
canvas { background:white; border:1px solid #ccc; touch-action: manipulation; }
</style>
</head>
<body>

<h2 id="mode">Tap the TWO HIGHEST points</h2>
<canvas id="chart" width="320" height="400"></canvas>
<p id="result"></p>

<script>
const canvas = document.getElementById("chart");
const ctx = canvas.getContext("2d");
let clicks = [];
let mode = "HIGH";

const candles = [
  {x:60, high:80, low:300, up:true},
  {x:140, high:60, low:260, up:false},
  {x:220, high:90, low:280, up:true}
];

function draw() {
  ctx.clearRect(0,0,320,400);
  candles.forEach(c=>{
    ctx.strokeStyle = c.up ? "green":"red";
    ctx.beginPath();
    ctx.moveTo(c.x, c.high);
    ctx.lineTo(c.x, c.low);
    ctx.stroke();
  });
}
draw();

canvas.addEventListener("click", e=>{
  const y = e.offsetY;
  clicks.push(y);
  if (clicks.length === 2) {
    document.getElementById("result").innerText = "Good! Try again.";
    clicks = [];
    mode = mode === "HIGH" ? "LOW" : "HIGH";
    document.getElementById("mode").innerText =
      mode === "HIGH" ? "Tap the TWO HIGHEST points" : "Tap the TWO LOWEST points";
  }
});
</script>

</body>
</html>
