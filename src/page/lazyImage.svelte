// LazyImage.svelte

<script>
  export let src = "";
  export let alt = "";
  export let width = 0;
  export let height = 0;
  let currentSrc = "";

  function lazyLoad(node) {
    const observer = new IntersectionObserver(onIntersect, {
      // If the image gets within 50px in the Y axis, start the download.
      rootMargin: "50px 0px",
      threshold: 0.01
    });

    function onIntersect(entries) {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          node.setAttribute("src", src);
        }
      });
    }

    observer.observe(node);
    return {
      destroy() {
        observer && observer.unobserve(node);
      }
    };
  }
</script>

<img use:lazyLoad {alt} data-width={width} data-height={height} />