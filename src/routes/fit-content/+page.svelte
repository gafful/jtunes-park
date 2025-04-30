<script lang="ts">
import { onMount } from "svelte"
  

let mainContent: HTMLElement

onMount(() => {
  if (!mainContent) return

  // Variables to track scroll state
  let isScrolling = false
  let scrollTimeout: string | number | NodeJS.Timeout | undefined
  let lastScrollTop = 0
  let scrollDirection = null

  // Function to handle scroll events
  const handleScroll = () => {
    if (!isScrolling) {
      isScrolling = true
    }

    // Clear the timeout
    clearTimeout(scrollTimeout)

    // Determine scroll direction
    const currentScrollTop = mainContent.scrollTop
    scrollDirection = currentScrollTop > lastScrollTop ? "down" : "up"
    lastScrollTop = currentScrollTop

    // Check if we're near boundaries
    const isNearTop = currentScrollTop < 10
    const isNearBottom =
      mainContent.scrollHeight - currentScrollTop - mainContent.clientHeight <
      10

    // If scrolling up and near top, ensure we can see the very top
    if (scrollDirection === "up" && isNearTop) {
      requestAnimationFrame(() => {
        mainContent.style.scrollSnapType = "y mandatory"
      })
    }
    // If scrolling down and near bottom, ensure we can see the very bottom
    else if (scrollDirection === "down" && isNearBottom) {
      requestAnimationFrame(() => {
        mainContent.style.scrollSnapType = "y mandatory"
      })
    }
    // Otherwise, disable snap scrolling to allow normal scrolling
    else {
      mainContent.style.scrollSnapType = "none"
    }

    // Set a timeout to detect when scrolling stops
    scrollTimeout = setTimeout(() => {
      isScrolling = false
      mainContent.style.scrollSnapType = "none"
    }, 150)
  }

  // Add scroll listener
  mainContent.addEventListener("scroll", handleScroll, { passive: true })

  // Cleanup function
  return () => {
    if (mainContent) {
      mainContent.removeEventListener("scroll", handleScroll)
      clearTimeout(scrollTimeout)
    }
  }
})

// Function to update `adminSection` based on the current route
function setSection(section: string) {
  adminSectionStore.set(section)
}
</script>

<div
  class="bg-gradient-to-b from-white from-0% via-white via-40% to-[#BAB9FF] to-100%"
>
  <div class="flex h-screen">
    <nav class="hidden lg:flex flex-col w-72 border-r bg-gray-50">Nav</nav>

    <div class="flex-1 flex flex-col">
      <header
        class="lg:hidden fixed top-0 left-0 right-0 border-b bg-gray-50 z-50"
      >
        Headers 1
      </header>

      <main
      bind:this={mainContent}
        class="flex-1 overflow-y-auto p-6 overscroll-contain"
        style="-webkit-overflow-scrolling: touch;"
      >
        <!-- Top anchor for scroll snapping -->
        <div id="scroll-top" class="scroll-snap-align-start h-px w-full"></div>

        <div class="pt-10 pb-36">
          <div class="min-h-full flex flex-col w-full">Main Area1</div>
        </div>

        <!-- Bottom anchor for scroll snapping -->
        <div id="scroll-bottom" class="scroll-snap-align-end h-px w-full"></div>
      </main>
    </div>
  </div>
</div>

<style>

  /* Scroll snap alignment elements */
  :global(.scroll-snap-align-start) {
    scroll-snap-align: start;
  }

  :global(.scroll-snap-align-end) {
    scroll-snap-align: end;
  }

  /* Styling for WebKit browsers */
  :global(.overscroll-contain) {
    overscroll-behavior: contain;
    -webkit-overflow-scrolling: touch;
  }
</style>