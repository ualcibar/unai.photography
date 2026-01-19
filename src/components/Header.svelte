<script>
  export let title = "Unai Alcibar-Arechuluaga";
  
  import { onMount } from "svelte";
  
  let open = false;
  let hidden = false;
  let lastScroll = 0;

/*
$: if (typeof document !== "undefined") {
  if (open) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "";
}
}
*/
function toggleMenu() {
  open = !open;
}

function closeMenu() {
  open = false;
  }

/* This makes that the menu hides when goes up and shows when goes down */
onMount(() => {
    const onScroll = () => {
      const current = window.scrollY;
      hidden = current > lastScroll && current > 80;
      lastScroll = current;
    };
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  });
</script>

<header class:hidden>
  <button class="menu-btn" on:click={toggleMenu}>☰</button>
  <h1>{title}</h1>
</header>

<!-- Curtain overlay -->
<div class="curtain" class:open>
  <button class="menu-btn" on:click={toggleMenu}>✕</button>
  <nav>
    <a href="/" on:click={closeMenu}>Home</a>
    <a href="/gallery" on:click={closeMenu}>Gallery</a>
    <a href="/about" on:click={closeMenu}>About</a>
    <a href="/contact" on:click={closeMenu}>Contact</a>
  </nav>
</div>


<style>
header {
  position: fixed;
  top: 0;
  width: 100%;
  max-height: 75px;
  display: flex;
  align-items: center;
  background: linear-gradient(180deg, rgba(20, 20, 20, 0.493) 60% , rgba(0, 0, 0, 0));
  color: white;
  transition: transform 0.3s ease;
  z-index: 1000;
}

h1 {
  margin-left: 78%; /* moves H1 a bit away from menu button */
}

header.hidden {
  transform: translateY(-100%);
}
/* Curtain overlay */
.curtain {
  position: fixed;
  inset: 0;
  background: linear-gradient(90deg, #111, #000);
  transform: translateX(-100%);
  transition: transform 0.6s ease;
  z-index: 1000;
  display: grid;
  place-items: center;
}

/* When menu is open */
.curtain.open {
  transform: translateX(0);
}

/* Menu links */
nav {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  text-align: center;
}

nav a {
  color: white;
  font-size: 3rem;
  text-decoration: none;
  letter-spacing: 0.2rem;
  transition: opacity 0.3s;
}

nav a:hover {
  opacity: 0.7;
}

.menu-btn {
  font-size: 1.5rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  margin-left: 3%; /* moves H1 a bit away from menu button */

}
</style>