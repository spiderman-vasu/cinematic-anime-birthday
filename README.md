<!DOCTYPE html>
<html lang="en">

<head>

<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Cinematic Anime Birthday Film</title>

<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;500&display=swap" rel="stylesheet">

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body{

    background:black;

    overflow:hidden;

    display:flex;

    justify-content:center;

    align-items:center;

    height:100vh;

    font-family:'Cormorant Garamond', serif;
}

 

.video-container{

    position:relative;

    width:56.25vh;
    height:100vh;

    max-width:100vw;
    max-height:177.77vw;

    overflow:hidden;

    background:black;

    box-shadow:
    0 0 100px rgba(0,0,0,0.9);

    border-left:
    1px solid rgba(255,255,255,0.06);

    border-right:
    1px solid rgba(255,255,255,0.06);
}

 

.scene{

    position:absolute;

    inset:0;

    opacity:0;

    transition:
    opacity 3s ease;
}

.scene.active{
    opacity:1;
}
 

.scene img{

    position:absolute;

    width:100%;
    height:100%;

    object-fit:cover;

    top:0;
    left:0;

    z-index:1;

    animation:
    cinematicZoom 12s ease-in-out forwards,
    cinematicFloat 8s ease-in-out infinite;

    filter:
    brightness(1.02)
    contrast(1.08)
    saturate(1.06);
}

 

.overlay{

    position:absolute;

    inset:0;

    z-index:2;

    background:
    radial-gradient(circle at center,
    rgba(255,220,180,0.08),
    rgba(0,0,0,0.35));

    mix-blend-mode:screen;
}

.lightLeak{

    position:absolute;

    inset:0;

    z-index:2;

    background:
    linear-gradient(
        120deg,
        transparent,
        rgba(255,240,220,0.08),
        transparent
    );

    animation:
    lightMove 8s linear infinite;
}

.grain{

    position:absolute;

    inset:0;

    z-index:2;

    opacity:0.05;

    background-image:
    url("https://grainy-gradients.vercel.app/noise.svg");

    pointer-events:none;
}

 
.text{

    position:absolute;

    bottom:10%;

    width:100%;

    z-index:999;

    text-align:center;

    color:white;

    font-size:2rem;

    font-weight:300;

    letter-spacing:6px;

    opacity:0;

    padding:0 30px;

    text-shadow:
    0 0 20px rgba(255,255,255,0.15);

    animation:
    textReveal 5s ease forwards;
}

 

.sakura{

    position:absolute;

    width:12px;
    height:12px;

    background:pink;

    opacity:0.7;

    border-radius:50% 0 50% 50%;

    z-index:3;

    animation:
    sakuraFall linear infinite;
}

      
@keyframes cinematicZoom{

    from{
        transform:scale(1);
    }

    to{
        transform:scale(1.08);
    }
}

@keyframes cinematicFloat{

    0%{
        transform:translateY(0px);
    }

    50%{
        transform:translateY(-10px);
    }

    100%{
        transform:translateY(0px);
    }
}

@keyframes lightMove{

    from{
        transform:translateX(-100%);
    }

    to{
        transform:translateX(100%);
    }
}

@keyframes textReveal{

    0%{
        opacity:0;
        transform:translateY(20px);
    }

    20%{
        opacity:1;
        transform:translateY(0px);
    }

    80%{
        opacity:1;
    }

    100%{
        opacity:0;
    }
}

@keyframes sakuraFall{

    0%{

        transform:
        translateY(-10vh)
        translateX(0px)
        rotate(0deg);
    }

    100%{

        transform:
        translateY(110vh)
        translateX(120px)
        rotate(360deg);
    }
}

</style>

</head>

<body>

<div class="video-container" id="container"></div>

<audio id="music" loop>

    <source src="music.mp3" type="audio/mpeg">

</audio>

<script>
 

const scenes = [

{
    image:"img1.jpeg",
    text:"Happy Birthday"
},

{
    image:"img2.jpeg",
    text:""
},

{
    image:"img3.jpeg",
    text:"Some souls become unforgettable memories."
},

{
    image:"img4.jpeg",
    text:""
},

{
    image:"img5.jpeg",
    text:"Every frame carries a feeling."
},

{
    image:"img6.jpeg",
    text:""
},

{
    image:"img7.jpeg",
    text:"Thank you for being part of this story."
},

{
    image:"img8.jpeg",
    text:""
},

{
    image:"img9.jpeg",
    text:"Stay happy. Stay bright."
},

{
    image:"img10.jpeg",
    text:"A story worth remembering."
}

];

 

const container =
document.getElementById("container");

let currentIndex = 0;
 

function createScene(data,index){

    const scene =
    document.createElement("div");

    scene.className = "scene";

    scene.innerHTML = `

        <img src="${data.image}">

        <div class="overlay"></div>

        <div class="lightLeak"></div>

        <div class="grain"></div>

        <div class="text">${data.text}</div>

    `;

   

    if(index === 4){

        for(let i=0;i<35;i++){

            const sakura =
            document.createElement("div");

            sakura.className = "sakura";

            sakura.style.left =
            Math.random()*100 + "vw";

            sakura.style.animationDuration =
            5 + Math.random()*8 + "s";

            sakura.style.opacity =
            Math.random();

            sakura.style.transform =
            `scale(${Math.random()})`;

            scene.appendChild(sakura);
        }
    }

    return scene;
}



function nextScene(){

    if(currentIndex >= scenes.length){

        return;
    }

    const scene =
    createScene(
        scenes[currentIndex],
        currentIndex
    );

    container.appendChild(scene);

    setTimeout(()=>{

        scene.classList.add("active");

    },100);

    setTimeout(()=>{

        scene.classList.remove("active");

    },9000);

    setTimeout(()=>{

        scene.remove();

        currentIndex++;

        nextScene();

    },12000);
}

 
nextScene();

 
const music =
document.getElementById("music");

document.body.addEventListener("click",()=>{

    music.play();

},{
    once:true
});

</script>

</body>
</html> 
