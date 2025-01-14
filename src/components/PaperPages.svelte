<script lang="ts">
  let HTMLPaperPages: HTMLElement

  const scrollEffect = () => {
    const items = HTMLPaperPages.children[0].nodeName === 'ASTRO-SLOT' ? HTMLPaperPages.children[0].children : HTMLPaperPages.children

    for (let item of items) {
      const page = item as HTMLElement

      if (page.getBoundingClientRect().top <= 300) {
        page.classList.add('dropped')
      } else {
        page.classList.remove('dropped')
      }
    }
  }
</script>

<style lang="scss">
  @use 'src/sass/mixins.scss' as *;

  :global(body.dark-mode .paper-pages .page-wrapper) {
    filter: invert(0.9);
  }
  .paper-pages {
    display: flex;
    flex-direction: column;
    gap: 300px;
    height: fit-content;
    margin-top: 150vh;

    :global(.page-wrapper) {
      transition: 0.5s ease;
      position: sticky;
      top: calc(15vh * var(--y));
      margin-left: calc(50px * var(--x));
      transform: rotateZ(var(--z)) translateY(20px) scale(1);
      border: 1px solid rgb(216, 216, 216);
      background-color: white;
      z-index: 2;

      background-image: url('/assets/papertexture.webp');
      background-size: cover;
      box-shadow: 10px 10px 40px 0 rgba(0, 0, 0, 0.3);
      padding: 70px;
      width: 100%;
      height: 90vh;
      max-height: 750px;
      left: 0;
      overflow: hidden;
    }

    :global(.polaroid) {
      transition: 0.5s ease;
      position: sticky;
      top: calc(5vh + var(--menuHeight) * var(--y));
      margin-left: calc(50px * var(--x));
      margin-bottom: 50px;
      transform: rotateZ(var(--z)) translateY(20px) scale(1);
      box-shadow: 5px 5px 20px 0 rgba(0, 0, 0, 0.3);
      z-index: 2;

      object-fit: cover;
      max-width: 50%;

      @include notDesktop {
        margin: 0;
        max-width: 400px;
      }
    }

    @include notDesktop {
      margin-bottom: 10px;
      padding: 10px;
      :global(.page-wrapper) {
        padding: 5vw;
        margin-left: 0px;
        height: 100vh;
        top: 0;
        max-height: unset;
      }
    }

    :global(.page-wrapper.dropped),
    :global(.polaroid.dropped) {
      transform: rotateZ(var(--z)) translateY(-10px) scale(0.9);
      box-shadow: 2px 2px 5px 2px rgba(19, 19, 19, 0.2);
    }
  }
</style>

<div class="paper-pages g-wrapper" bind:this={HTMLPaperPages}>
  <slot />
</div>

<svelte:window on:scroll={scrollEffect} />
