<script>
  export let title = "Unai Alcibar-Arechuluaga";
  
  import { onMount } from "svelte";

  import { courtainImage } from "../images/background/DSCF6843.jpg";
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
  <button class="menu-btn" on:click={toggleMenu}>{open ? "✕" : "☰"}</button>
  <h1>{title}</h1>
  <button class="menu-language">EUS</button> |
  <button class="menu-language">ES</button> |
  <button class="menu-language">ENG</button>
</header>

<!-- Curtain overlay -->
<div class="curtain" class:open>
  <nav>
    <a href="/" on:click={closeMenu}>Home</a>
    <a href="/gallery" on:click={closeMenu}>Proyects</a>
    <a href="/gallery" on:click={closeMenu}>Photo Diary</a>
    <a href="/about" on:click={closeMenu}>About Me</a>
    <a href="/about" on:click={closeMenu}>Store</a>
    <a href="/contact" on:click={closeMenu}>Contact</a>
  </nav>
  
</div>


<style>
header {
  position: fixed;
  top: 0;
  width: 100%;
  height: 75px;
  display: flex;
  align-items: center;
  justify-content: start; /* pushes h1 left & button right */
  color: white;
  transition: transform 0.3s ease;
  z-index: 1000;
}

/* Title */
header h1 {
  font-size: clamp(1.5rem, 4vw, 2.5rem);
  /* margin-left: 3rem; */
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
}

/* Hide header on scroll */
header.hidden {
  transform: translateY(-100%);
}

/* Menu button */
.menu-btn {
  padding: 0 1.5rem; /* responsive horizontal spacing */
  font-size: clamp(1.5rem, 5vw, 2.5rem);
  background: none;
  border: none;
  color: white;
  cursor: pointer;
}
.menu-language {
  padding: 0 1rem; /* responsive horizontal spacing */
  font-size: clamp(1rem, 3vw, 1.7rem);
  background: none;
  border: none;
  color: white;
  cursor: pointer;
}
/* Curtain overlay */
.curtain {
  position: fixed;
  inset: 0;
  background: linear-gradient(90deg, #111, #000);
  transform: translateX(-100%);
  transition: transform 0.7s ease;
  z-index: 999;
}

/* When open */
.curtain.open {
  transform: translateX(0);
}

/* Menu container */
nav {
  position: absolute;
  left: 2rem;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

button:hover {
  transform: scale(1.1);
  transition: transform 0.3s;
}

/* Menu links */
nav a {
  color: white;
  font-size: clamp(2rem, 6vw, 3.5rem);
  text-decoration: none;
  letter-spacing: 0.15rem;
  transition: opacity 0.3s, transform 0.3s;
}

nav a:hover::after {
  width: 100%;
}


nav a:hover {
  opacity: 0.7;
  transform: translateX(60px) scale(1.1);

}

nav:has(a:hover) ~ .curtain,
.curtain:has(nav a:hover) {
  /* background: linear-gradient(90deg, #400, #900); */
}

</style>