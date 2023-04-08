<script lang="ts">
  import Map from "./Map.svelte";
  import Music from "./Music.svelte";

  let money = 350;
  let final_money: string = "";
  format_money(money);

  let written_text:string = ""

  function format_money(money) {
    if (money > 999999999) final_money = "999999999";
    else {
      final_money = String(money);
      while (final_money.length < 9) final_money = "0" + final_money;
    }
  }

  document.addEventListener("keydown", (event) => {
    written_text+=event.key

    if (written_text.endsWith("hesoyam")) {
      cheat_hesoyam();
    }
  });

  function cheat_hesoyam(){
    money+=250_000
    document.getElementById("hud-stats-img").src="images/hud_stats_full.webp"
    console.log("HESOYAM - Cheat Activated")
    format_money(money)
    cheat_activated()
  }

  function cheat_activated(){
    cheat_activated_sound_effect()
    cheat_activated_label();
  }

  function cheat_activated_sound_effect(){
    const cheat_activated_audio = new Audio("music/cheat_activated.mp3")
    cheat_activated_audio.play();
  }

  function cheat_activated_label(){
    const cheat_activated_label =  document.getElementById("cheat-activated")
    cheat_activated_label.style.opacity="1"

    setTimeout(() => {
        cheat_activated_label.style.opacity="0"
    }, 5000);

  }
</script>

<div class="hud">
    <div id="cheat-activated">
        Cheat Activated
    </div>
  <Music />
  <div class="right">
    <div id="stats">
      <img
        id="hud-stats-img"
        src="images/hud_stats.webp"
        alt="Grand Theft Auto: San Andreas - weapon, health and money"
      />
      <div id="money">${final_money}</div>
    </div>
    <Map />
  </div>
</div>

<style>
  .hud {
    pointer-events: none;
    position: fixed;
    z-index: 99;
    width: 100%;
    height: 100%;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
  }

  .hud .right {
    position: absolute;
    height: 100%;
    right: 0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 5% 1%;
  }

  .hud #stats {
    width: 300px;
  }

  .hud #stats #money {
    font-family: "Pricedown";
    color: #366d28;
    font-size: 64px;
    margin-top:-12px;
    -webkit-text-stroke: 2px #000;
  }

  .hud #cheat-activated{
    transition: .5s;
    opacity: 0;
    position: absolute;
    font-family: "Futura LT Bold";
    inset:5%;
    color:#fff;
    background: #0000008e;
    width: 250px;
    height: fit-content;
    padding:8px;

  }
</style>
