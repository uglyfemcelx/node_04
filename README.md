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
}

#text{
    white-space:pre-wrap;
    line-height:1.6;
}

.glitch{
    color:#ff00ff;
    animation:flicker 0.2s infinite;
}

@keyframes flicker{
    0%{opacity:1;}
    50%{opacity:0.3;}
    100%{opacity:1;}
}

.choice{
    margin-top:20px;
}

button{
    background:black;
    color:#00ff88;
    border:1px solid #00ff88;
    padding:10px;
    margin-right:10px;
    cursor:pointer;
    font-family:inherit;
}

button:hover{
    opacity:0.6;
}
</style>
</head>

<body>

<div id="text"></div>

<script>

const text = document.getElementById("text");

let userName = localStorage.getItem("username");

const storyBase = [
"> node_04 detected...",
"> connection restored...",
"",
"> you came back.",
"",
"> node_03 ended with a question.",
"> now there is another.",
"",
"> will you stay?"
];

let i = 0;

function type(){
    if(i < storyBase.length){
        text.innerHTML += storyBase[i] + "\n";
        i++;
        setTimeout(type, 120);
    } else {
        showChoices();
    }
}

function showChoices(){

    const div = document.createElement("div");
    div.className = "choice";

    div.innerHTML = `
        <p>> choose:</p>
        <button onclick="yes()">stay</button>
        <button onclick="no()">leave</button>
    `;

    text.appendChild(div);
}

// branching paths
function yes(){

    localStorage.setItem("node4_choice","stay");

    text.innerHTML += "\n> you chose to stay.\n";

    if(userName){
        text.innerHTML += `> i remember you, ${userName}\n`;
    } else {
        text.innerHTML += "> i don't know your name...\n";
    }

    text.innerHTML += `
> then stay a little longer.
> the wired doesn’t forget easily.
`;

    text.classList.add("glitch");

}

function no(){

    localStorage.setItem("node4_choice","leave");

    text.innerHTML += "\n> you chose to leave.\n";

    text.innerHTML += `
> that’s fine.
> people always leave.
> even i did once.
`;

    if(userName){
        text.innerHTML += `\n> goodbye, ${userName}.\n`;
    }

}

// remember previous visit
window.onload = ()=>{
    const prev = localStorage.getItem("node4_choice");

    if(prev){
        text.innerHTML += `\n> you were here before.\n> last time you chose: ${prev}\n`;
    }
};

type();

</script>

</body>
</html>
