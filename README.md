# Happy-Birthday-didi
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday Hanu Didi 🎂</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    text-align: center;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
    overflow: hidden;
    color: white;
}

/* Floating Hearts */
.heart {
    position: absolute;
    font-size: 20px;
    animation: float 6s linear infinite;
}
@keyframes float {
    from { transform: translateY(100vh); }
    to { transform: translateY(-10vh); }
}

h1 { margin-top: 10px; }

#gameArea {
    position: relative;
    height: 70vh;
}

.gift {
    position: absolute;
    font-size: 30px;
    cursor: pointer;
}

#score {
    font-size: 20px;
}

/* Final Screen */
#finalScreen {
    display: none;
    font-size: 26px;
    padding: 20px;
}

.cake {
    font-size: 90px;
}

/* Fireworks */
.firework {
    position: absolute;
    width: 5px;
    height: 5px;
    background: white;
    animation: explode 1s ease-out forwards;
}
@keyframes explode {
    to {
        transform: translate(var(--x), var(--y));
        opacity: 0;
    }
}
</style>

</head>

<body>

<h1>🎉 Happy Birthday Hanu Didi 🎉</h1>
<p>Catch 10 gifts to unlock your special surprise 🎁</p>

<div id="score">Score: 0</div>
<div id="gameArea"></div>

<div id="finalScreen">
    <div class="cake">🎂</div>
    <p id="typedMessage"></p>
</div>

<script>
let score = 0;
let gameArea = document.getElementById("gameArea");

/* Hearts animation */
setInterval(()=>{
    let heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "💖";
    heart.style.left = Math.random()*100 + "vw";
    document.body.appendChild(heart);
    setTimeout(()=>heart.remove(),6000);
},300);

/* Game */
function createGift(){
    let gift = document.createElement("div");
    gift.className = "gift";
    gift.innerHTML = "🎁";

    gift.style.left = Math.random()*window.innerWidth + "px";
    gift.style.top = "0px";

    gameArea.appendChild(gift);

    let fall = setInterval(()=>{
        gift.style.top = (parseInt(gift.style.top)+5)+"px";
        if(parseInt(gift.style.top) > window.innerHeight){
            gift.remove();
            clearInterval(fall);
        }
    },30);

    gift.onclick = ()=>{
        score++;
        document.getElementById("score").innerText="Score: "+score;
        gift.remove();
        clearInterval(fall);

        if(score >= 10){
            showFinal();
        }
    }
}

setInterval(createGift,800);

/* Final Screen */
function showFinal(){
    gameArea.style.display="none";
    document.getElementById("finalScreen").style.display="block";
    typeMessage();
    fireworks();
}

/* Typing Message */
let msg = "Happy Birthday Hanu Didi 💖 You are not just my sister, you are my strength, my happiness and my best friend. I wish you endless success, love and smiles always 🎂✨";
let i=0;

function typeMessage(){
    if(i < msg.length){
        document.getElementById("typedMessage").innerHTML += msg.charAt(i);
        i++;
        setTimeout(typeMessage,50);
    }
}

/* Fireworks */
function fireworks(){
    for(let i=0;i<120;i++){
        let fw = document.createElement("div");
        fw.className="firework";
        fw.style.left="50%";
        fw.style.top="50%";
        fw.style.setProperty('--x',(Math.random()*200-100)+'px');
        fw.style.setProperty('--y',(Math.random()*200-100)+'px');
        document.body.appendChild(fw);
        setTimeout(()=>fw.remove(),1000);
    }
}
</script>

</body>
</html>
