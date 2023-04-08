<script lang="ts" defer>
  let main_element;

  let old_scroll: number = 0;

  window.onload = () => {
    main_element = document.querySelector(".sections");

    //render_map();
    main_element.addEventListener("scroll", render_map);
  };

  function render_map() {
    // Position of top of the map
    const min_y = 20;
    set_map_cursor_y(min_y);

    // Position of bottom of the map
    const max_y = 90;

    // Difference between top and bottom to add it to cursor position
    const difference = Math.abs(max_y) - Math.abs(min_y);

    const scroll = main_element.scrollTop;
    const number_of_section = document.querySelectorAll(".section").length - 1;
    const height = main_element.clientHeight * number_of_section;

    const percentage = get_percentage_of_scroll(height, scroll);

    const total_difference = min_y + difference * percentage;
    // Cursor will be up if the scroll was up
    const up = old_scroll > scroll;
    old_scroll = scroll;

    set_map_cursor_y(total_difference);
    set_map_cursor_rotation(up);
  }

  function get_percentage_of_scroll(height, scroll) {
    return 100 / 100 / (height / scroll);
  }

  function set_map_cursor_y(total_difference) {
    // Set Y position of map background
    document.getElementById("map").style.backgroundPosition =
      "center " + total_difference + "%";
  }

  function set_map_cursor_rotation(up) {
    // Set cursor up or down
    const cursor = document.getElementById("map-cursor");
    if (up) cursor.style.rotate = "180deg";
    else cursor.style.rotate = "0deg";
  }
</script>

<div id="map">
  <img src="images/player_cursor.webp" alt="Player Cursor" id="map-cursor" />
</div>

<style>
  #map {
    width: 200px;
    aspect-ratio: 1/1;
    background-image: url("public/images/gta_san_andreas_map.webp");
    background-size: cover;
    background-position: center 20%;
    transition: 0.1s ease-out;

    border-radius: 100%;
    border: 8px solid #000;

    display: grid;
    place-items: center;
  }

  #map #map-cursor {
    width: 40px;
    transition: 0.2s;
  }
</style>
