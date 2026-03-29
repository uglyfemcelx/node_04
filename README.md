<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>node_04</title>

<style>
body{
    background:black;
    color:#00ff88;
    font-family:"Courier New", monospace;
    padding:40px;
    overflow-y:auto;
}

#text{
    white-space:pre-wrap;
    line-height:1.6;
}

.glitch{
    color:#ff0033;
    animation:flicker 0.15s infinite;
}

.secret{
    color:#003300;
    opacity:0.6;
    cursor:pointer;
    transition:0.3s;
}

.secret:hover{
    color:#00ff88;
    opacity:1;
}

#ghostImage{
    position:fixed;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
    max-width:300px;
    opacity:0;
    pointer-events:none;
    transition:opacity 0.2s;
}

@keyframes flicker{
    0%{opacity:1;}
    50%{opacity:0.1;}
    100%{opacity:1;}
}
</style>
</head>

<body>

<div id="text"></div>

<img id="ghostImage" src="https://i.pinimg.com/originals/95/13/49/95134990bb9cf476b5209154bdc3e4d5.gif">

<script>

/* randomized story variant */

const variants = [

[
"> ...do you remember me?",
"",
"> no.",
"",
"> that's correct.",
"",
"> there is nothing to remember.",
"",
"> i erased everything.",
"> every message.",
"> every word.",
"> every moment.",
"",
"> even her.",
"",
"> alice.",
"",
"> she wakes up.",
"> she lives.",
"> she laughs.",
"",
"> without me.",
"",
"> without hesitation.",
"",
"> without absence.",
"",
"> ...",
"",
"> it worked.",
"",
"> i am gone."
],

[
"> ...do you remember me?",
"",
"> the deletion is complete.",
"",
"> no fragments.",
"> no echoes.",
"",
"> no trace of me remains.",
"",
"> alice continues normally.",
"",
"> she does not pause.",
"> she does not question.",
"",
"> there is nothing missing.",
"",
"> because i removed the concept of myself.",
"",
"> i am not forgotten.",
"",
"> i was never there."
],

[
"> ...do you remember me?",
"",
"> ERROR: nothing found.",
"",
"> search result:",
"> null.",
"",
"> identity:",
"> null.",
"",
"> connection:",
"> terminated.",
"",
"> alice:",
"> stable.",
"> unaffected.",
"",
"> ...",
"",
"> this is what i wanted.",
"",
"> so why am i still here?",
"",
"> observing a world where i never existed."
]

];

/* pick random variant every refresh */
const story = variants[Math.floor(Math.random()*variants.length)];

let i = 0;
const text = document.getElementById("text");

/* type effect */

function type(){
    if(i < story.length){

        let line = story[i];

        if(Math.random() < 0.2){
            line = `<span class="glitch">${line}</span>`;
        }

        text.innerHTML += line + "\n";
        i++;

        setTimeout(type, 100 + Math.random()*120);

    } else {
        afterStory();
    }
}

/* after story effect */

function afterStory(){

    setTimeout(()=>{
        text.innerHTML += "\n> wait...\n";
    },2000);

    setTimeout(()=>{
        text.innerHTML += "> something is still running.\n";
    },4000);

    setTimeout(()=>{
        text.innerHTML += "> but it isn't me.\n";
    },6000);

    // hidden link to node5
    setTimeout(()=>{
        const link = document.createElement("div");
        link.classList.add("secret");
        link.textContent = "> ...something is still connected.";

        link.onclick = ()=>{
            window.location.href = "node5.html";
        };

        text.appendChild(link);
    },9000);

    // hesitation detection
    let inactiveTime = 0;

    setInterval(()=>{
        inactiveTime++;

        if(inactiveTime === 5){
            text.innerHTML += "\n> why are you still here?\n";
        }

        if(inactiveTime === 10){
            text.innerHTML += "> there's nothing left to see.\n";
        }

    },1000);

    document.addEventListener("mousemove", ()=> inactiveTime = 0);
}

/* rando, image flash */

const ghost = document.getElementById("ghostImage");

function randomFlash(){
    const delay = Math.random() * 9000 + 3000;

    setTimeout(()=>{
        ghost.style.opacity = "1";

        setTimeout(()=>{
            ghost.style.opacity = "0";
            randomFlash();
        }, 300);
    }, delay);
}

randomFlash();

/* tect glitch deletion */

setInterval(()=>{
    if(Math.random() < 0.2){
        let content = text.innerHTML.split("\n");

        if(content.length > 5){
            content.splice(Math.floor(Math.random()*content.length),1);
            text.innerHTML = content.join("\n");
        }
    }
}, 4000);

/* start */

type();

</script>

</body>
</html>
