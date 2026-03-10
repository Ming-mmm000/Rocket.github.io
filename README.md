index.html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Rocket Orbit Simulator</title>
<style>
body{
text-align:center;
font-family:Arial;
background:black;
color:white;
}

#startScreen{
margin-top:150px;
}

button{
padding:10px 20px;
font-size:18px;
}

#panel{
position:fixed;
bottom:10px;
left:50%;
transform:translateX(-50%);
background:#222;
padding:10px;
border-radius:10px;
}

canvas{
background:black;
}
</style>
</head>

<body>

<div id="startScreen">
<h1>Rocket Orbit Simulator</h1>
<button onclick="start()">Start</button>
</div>

<canvas id="space" width="800" height="500" style="display:none;"></canvas>

<div id="panel" style="display:none;">
Speed <input id="speed" value="2">
Planet Mass <input id="mass" value="1000">
Radius <input id="radius" value="150">
<button onclick="launch()">Launch</button>
</div>

<script>

let canvas=document.getElementById("space")
let ctx=canvas.getContext("2d")

let rocket
let earth={x:400,y:250}
let r
let angle=0
let speed

function start(){

document.getElementById("startScreen").style.display="none"
canvas.style.display="block"
document.getElementById("panel").style.display="block"

drawEarth()

}

function launch(){

speed=parseFloat(document.getElementById("speed").value)
r=parseFloat(document.getElementById("radius").value)

rocket={
x:earth.x+r,
y:earth.y
}

animate()

}

function drawEarth(){

ctx.fillStyle="blue"
ctx.beginPath()
ctx.arc(earth.x,earth.y,20,0,Math.PI*2)
ctx.fill()

}

function animate(){

ctx.clearRect(0,0,800,500)

drawEarth()

angle+=speed*0.01

rocket.x=earth.x+r*Math.cos(angle)
rocket.y=earth.y+r*Math.sin(angle)

ctx.fillStyle="red"
ctx.beginPath()
ctx.arc(rocket.x,rocket.y,6,0,Math.PI*2)
ctx.fill()

requestAnimationFrame(animate)

}

</script>

</body>
</html>
