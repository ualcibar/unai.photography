<script>
  // You can replace these with your real links
  const socials = [
    { name: "Instagram", url: "https://instagram.com", icon: "/icons/instagram.svg" },
    { name: "Youtube", url: "https://Youtube.com", icon: "/icons/Youtube.svg" },
    { name: "Linkedin", url: "https://Linkedin.net", icon: "/icons/Linkedin.svg" },
  ];
</script>

<div class="socials">
  {#each socials as social, i}
    <a 
      href={social.url}
      target="_blank"
      rel="noopener"
      style="--i:{i}"
      aria-label={social.name}
    >
      <img src={social.icon} alt={social.name} />
    </a>
  {/each}
</div>

<style>
.socials {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}

/* Icon links */
.socials a {
  display: inline-flex;
  width: 2.5rem;
  height: 2.5rem;
  transition: transform 0.3s ease, filter 0.3s ease;
  animation: iconIn 0.5s ease forwards;
  animation-delay: calc(var(--i) * 0.1s);
  opacity: 0;
}

/* Icon image */
.socials img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

/* Hover animation */
.socials a:hover {
  transform: scale(1.2) rotate(8deg);
  filter: drop-shadow(0 0 8px rgba(255,255,255,0.8));
}

/* Entrance animation */
@keyframes iconIn {
  from {
    opacity: 0;
    transform: translateY(10px) scale(0.8);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}
</style>