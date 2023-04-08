<script>
  // Define an array with the audio file URLs
  let audioFiles = [
    "music/cult_of_personality.mp3",
    "music/it_was_a_good_day.mp3",
    "music/personal_jesus.mp3",
  ];

  audioFiles = shuffle(audioFiles);

  let audio;

  // Initialize an index variable to keep track of the current audio file
  let currentIndex = 0;

  // Function to play the next audio file in the sequence
  function playNextAudio() {
    // Create a new Audio object with the next audio file URL
    audio = new Audio(audioFiles[currentIndex]);
    audio.volume = 0.25;
    // Listen for the 'ended' event to detect when the audio has finished playing
    audio.addEventListener("ended", () => {
      // Increment the index to move to the next audio file in the sequence
      currentIndex++;

      // If there are more audio files to play, call the playNextAudio() function again
      if (currentIndex < audioFiles.length) {
        playNextAudio();
      }
    });

    // Play the audio file
    audio.play();
  }

  function shuffle(array) {
    let currentIndex = array.length,
      randomIndex;

    // While there remain elements to shuffle.
    while (currentIndex != 0) {
      // Pick a remaining element.
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;

      // And swap it with the current element.
      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex],
        array[currentIndex],
      ];
    }

    return array;
  }

  let music_playing = false;
  let music_started = false;

  document.addEventListener("keydown", (event) => {
    if (event.key === "r") {
      // The 'r' key was pressed
      if (!music_playing && !music_started) {
        // Call the playNextAudio() function to start playing the sequence
        music_playing = true;
        music_started = true;
        playNextAudio();
        show_radio();
      } else if (music_playing) {
        // pause audio
        hide_radio();
        music_playing = false;
        audio.pause();
      } else if (!music_playing && music_started) {
        // resume audio
        show_radio();
        audio.play();
        music_playing = true;
      }
    }
  });

  function show_radio() {
    const radio = document.getElementById("radio");
    radio.style.visibility = "visible";
  }

  function hide_radio() {
    const radio = document.getElementById("radio");
    radio.style.visibility = "hidden";
  }
</script>

<div id="radio">Radio Los Santos</div>

<style>
  #radio {
    font-family: "Bank Gothic Regular";
    letter-spacing: 3px;
    word-spacing: 10px;
    font-size: 24px;
    margin-top: 16px;
    visibility: hidden;
    position: absolute;
    color: #c6a659;
  }
</style>
