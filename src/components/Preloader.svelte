<script lang="ts" defer>
  import { onMount } from "svelte";

  onMount(() => {
    document.getElementById("preloader-new-game").onmouseenter = () => {
      const audio = new Audio("music/main-menu-sound-effect.mp3");
      audio.volume=.5
      audio.play();
    };

    document.getElementById("preloader-new-game").onclick = () => {
        const preloader = document.getElementById("preloader") 
        preloader.style.opacity="0"
        setTimeout(() => {
            preloader.style.display="none";
        }, 1000);
    };
  });
</script>

<div id="preloader">
  <div id="preloader-main-menu">Main Menu</div>
  <div id="preloader-new-game">Start new game</div>
  <div id="preloader-image">
  <img src="images/vinewood.jpg" alt="">
</div>
</div>

<style>
  #preloader {
    position: fixed;
    width: 100%;
    height: 100%;
    inset: 0;
    background-color: #000;
    z-index: 999;
    opacity:1;
    transition:1s;
  }

  #preloader-new-game {
    color: #b7cee4b7;
    font-family: "Bank Gothic Regular";
    letter-spacing: 3px;
    cursor: pointer;
    text-align: center;
    position:absolute;
    left:50%;
    top:50%;
    transform: translate(-50%,-50%);
    width:100vw;
  }

  #preloader-new-game:hover {
    color: #b7cee4;
  }

  #preloader-main-menu {
    font-family: "Diploma";
    color: #fff;
    place-self: start;
    font-size: 48px;
    padding: 3rem;
    z-index: 10000;
    position:absolute;
  }

  #preloader-image{
    position:absolute;
    top:0;
    right: 0;
    -webkit-mask-image: url("images/vinewood-mask.png");
  mask-image: url("images/vinewood-mask.png");
  -webkit-mask-repeat: no-repeat;
  mask-repeat: no-repeat;  
  filter:brightness(.5) contrast(1.3);
}
</style>
