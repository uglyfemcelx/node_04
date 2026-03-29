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
    pointer-events: auto;
}

.glitch{
    color:red;
    animation:flicker 0.2s infinite;
}

.secret{
    color:#ff00ff;
    cursor:pointer;
    pointer-events:auto;
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
    50%{opacity:0.2;}
    100%{opacity:1;}
}
</style>
</head>

<body>

<div id="text"></div>

<img id="ghostImage" src="https://i.pinimg.com/originals/95/13/49/95134990bb9cf476b5209154bdc3e4d5.gif">

<script>

/* randomized story variants */

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

/* afterstory effect */

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

    // clickably node5 link
    setTimeout(()=>{
        const link = document.createElement("div");
        link.classList.add("secret");
        link.textContent = "> ...something is still connected.";

        link.addEventListener("click", ()=>{
            window.location.href = "node5.html";
        });

        document.body.appendChild(link);
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

/* random image flashyflashflash */

const ghost = document.getElementById("ghostImage");

function randomFlash(){
    const delay = Math.random() * 8000 + 4000;

    setTimeout(()=>{
        ghost.style.opacity = "1";

        setTimeout(()=>{
            ghost.style.opacity = "0";
            randomFlash();
        }, 200);
    }, delay);
}

randomFlash();

/* rando text deletion */

setInterval(()=>{
    if(Math.random() < 0.3){
        const content = text.innerHTML.split("\n");
        if(content.length > 5){
            content.splice(Math.floor(Math.random()*content.length), 1);
            text.innerHTML = content.join("\n");
        }
    }
}, 4000);


/* rando text corruption */
setInterval(()=>{
    if(Math.random() < 0.15){
        text.innerHTML = text.innerHTML.replace(
            /alice|memory|existence|me/gi,
            "████"
        );
    }
},3000);

type();


</script>

</body>
</html>
