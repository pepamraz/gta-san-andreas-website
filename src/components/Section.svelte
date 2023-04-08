<script lang="ts">
  export let imageUrl: string = "";
  export let title: string = "";
  export let content: string = "";
</script>

<section
  class="section"
  style="background-image: url(images/{imageUrl});"
>
  <div class="overlay" />
  <div class="content">
    {#if title}
      <h2>{title}</h2>
    {/if}

    {#if content}
      <p>{content}</p>
    {/if}
  </div>
</section>
