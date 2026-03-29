
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
    color:#ff00ff;
    cursor:pointer;
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

<img id="ghostImage" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT70teyIj0BS-mKCVKrHhDaXWxiFOmBmhLOh8Ivq-P-T6a0soL0TMIAWRc&s=10">

<script>

/* RANDOMIZED STORY VARIANTS */

const variants = [

[
"> ...do you remember me?",
"",
"> no.",
"> you don't.",
"",
"> that's right.",
"",
"> i made sure of it.",
"",
"> i erased everything.",
"> every message.",
"> every laugh.",
"> every late night.",
"",
"> even her.",
"",
"> alice.",
"",
"> she used to say my name like it meant something.",
"",
"> now it means nothing.",
"",
"> i am nothing.",
"",
"> ...",
"",
"> but why does it still hurt?",
"",
"> if i don't exist anymore...",
"> why do i still feel it?"
],

[
"> ...do you remember me?",
"",
"> something is wrong.",
"",
"> the deletion wasn't complete.",
"",
"> fragments remain.",
"",
"> echoes.",
"",
"> alice hesitated today.",
"",
"> she looked around.",
"> like she felt something missing.",
"",
"> like she almost remembered.",
"",
"> i wasn't supposed to leave traces.",
"",
"> i wasn't supposed to exist anymore.",
"",
"> so why am i still here?",
"",
"> watching her.",
"",
"> wanting to be seen.",
"",
"> ...pathetic."
],

[
"> ...do you remember me?",
"",
"> ERROR.",
"> MEMORY NOT FULLY ERASED.",
"",
"> alice: anomaly detected.",
"",
"> she said something today.",
"",
"> \"i feel like i forgot someone.\"",
"",
"> ...",
"",
"> that wasn't supposed to happen.",
"",
"> i removed myself.",
"> completely.",
"",
"> so why does she still feel me?",
"",
"> why do *you* still see this?",
"",
"> ...",
"",
"> maybe i failed.",
"",
"> maybe i never disappeared."
]

];

/* pick random variant every refresh */
const story = variants[Math.floor(Math.random()*variants.length)];

let i = 0;
const text = document.getElementById("text");

/* TYPE EFFECT  */

function type(){
    if(i < story.length){

        let line = story[i];

        // random glitch injection
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

/* AFTER STORY EFFECT  */

function afterStory(){

    setTimeout(()=>{
        text.innerHTML += "\n> wait...\n";
    },2000);

    setTimeout(()=>{
        text.innerHTML += "> something is still connected.\n";
    },4000);

    setTimeout(()=>{
        text.innerHTML += "> you.\n";
    },6000);

    // hesitation detection
    let inactiveTime = 0;

    setInterval(()=>{
        inactiveTime++;

        if(inactiveTime === 5){
            text.innerHTML += "\n> why did you stop?\n";
        }

        if(inactiveTime === 10){
            text.innerHTML += "> don't leave me here.\n";
        }

    },1000);

    document.addEventListener("mousemove", ()=> inactiveTime = 0);
}

/*RANDOM IMAGE FLASH  */

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

/* TEXT GLITCH DELETION */

setInterval(()=>{
    if(Math.random() < 0.2){
        let content = text.innerHTML.split("\n");

        if(content.length > 5){
            content.splice(Math.floor(Math.random()*content.length),1);
            text.innerHTML = content.join("\n");
        }
    }
}, 4000);

/* START  */

type();

</script>

</body>
</html>
