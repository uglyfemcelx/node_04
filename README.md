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
    color:red;
    animation:flicker 0.15s infinite;
}

.secret{
    color:#ff00ff;
    cursor:pointer;
}

/* make link clickable */
#nextLink{
    margin-top:40px;
    opacity:0;
    transition:opacity 2s;
    position:relative;
    z-index:9999;
}

#nextLink a{
    color:#00ff88;
    text-decoration:none;
}

#nextLink a:hover{
    opacity:0.5;
}

/* ghost image */
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

/* screen flicker */
@keyframes flicker{
    0%{opacity:1;}
    50%{opacity:0.2;}
    100%{opacity:1;}
}
</style>
</head>

<body>

<div id="text"></div>

<img id="ghostImage" src="https://i.pinimg.com/originals/2b/6d/1e/2b6d1e7c7d5d6a2e2c6b4c3e4c1d9f.gif">

<div id="nextLink">
<a href="node_05.html">> continue deeper</a>
</div>

<script>

let storySets = [

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
"> node_04 accessed...",
"> memory integrity failing...",
"",
"> something is missing.",
"",
"> i removed it.",
"> i removed everything.",
"",
"> including her.",
"",
"> alice.",
"",
"> she does not remember me.",
"> not my name.",
"> not my voice.",
"> not my existence.",
"",
"> it worked.",
"",
"> it finally worked.",
"",
"> there is no trace left.",
"> no logs.",
"> no fragments.",
"> no connection.",
"",
"> i am gone."
],

[
"> node_04 accessed...",
"> trace scan running...",
"",
"> no identity found.",
"",
"> alice status: stable",
"> alice memory: intact",
"",
"> subject [lain] not found.",
"",
"> deletion successful.",
"",
"> ...",
"",
"> then why am i still here?"
],

[
"> node_04 accessed...",
"",
"> she laughs.",
"> she talks.",
"> she lives.",
"",
"> and i am not there.",
"",
"> there is no gap in her memory.",
"> no missing space.",
"> no shadow of me.",
"",
"> i erased myself perfectly.",
"",
"> so why does something feel wrong?",
"",
"> ...",
"",
"> maybe existence doesn't need memory.",
"> maybe i exist anyway."
]

];

let chosenStory = storySets[Math.floor(Math.random()*storySets.length)];

let i = 0;
const text = document.getElementById("text");

function type(){
    if(i < chosenStory.length){
        text.innerHTML += chosenStory[i] + "\n";
        i++;

        if(Math.random() < 0.1){
            text.classList.add("glitch");
            setTimeout(()=>text.classList.remove("glitch"),100);
        }

        setTimeout(type, 120);
    } else {
        afterStory();
    }
}

function afterStory(){

    setTimeout(()=>{
        text.innerHTML += "\n> no one remembers me.";
    },2000);

    setTimeout(()=>{
        text.innerHTML += "\n> and that was the point.";
    },4000);

    setTimeout(()=>{
        text.innerHTML += "\n> ...right?";
    },6000);

    setTimeout(()=>{
        document.getElementById("nextLink").style.opacity = "1";
    },9000);
}

/* random ghost image */
const ghost = document.getElementById("ghostImage");

function randomFlash(){
    const delay = Math.random() * 7000 + 3000;

    setTimeout(()=>{
        ghost.style.opacity = "1";

        setTimeout(()=>{
            ghost.style.opacity = "0";
            randomFlash();
        }, 200);
    }, delay);
}

randomFlash();

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
