<script lang="ts">
  import { Moon } from "lucide-svelte";
  import { onMount } from "svelte";

  let isDark: boolean = $state(false);

  onMount(() => {
    const saved = localStorage.getItem("isDark");
    const systemDark = window.matchMedia(
      "(prefers-color-scheme: dark)"
    ).matches;
    isDark = saved === null ? systemDark : saved === "true";
    document.documentElement.classList.toggle("dark", isDark);
  });

  function toggleDark() {
    isDark = !isDark;
    document.documentElement.classList.toggle("dark", isDark);
    localStorage.setItem("isDark", String(isDark));
  }
</script>

<div
  class="border border-primary bg-secondary flex p-8 justify-between shadow-md transition-colors duration-500 ease-in-out"
>
  <div class="font-bold text-xl text-text">
    <a href="/"> <h1>Where is the world?</h1></a>
  </div>

  <button onclick={toggleDark}>
    {#if isDark}
      <Moon class="text-text" />
      <div class="ms-1 text-text">LightMode</div>
    {:else}
      <Moon class="text-text" />
      <div class="ms-1 text-text">DarkMode</div>
    {/if}
  </button>
</div>
<!--{ const saved = localStorage.getItem("theme"); 
const systemDark = window.matchMedia("(prefers-color-scheme: dark)").matches; 
isDark = saved ? saved === "dark" : systemDark; 
document.documentElement.classList.toggle("dark", isDark); } 
function toggleDark() 
{ isDark = !isDark; 
document.documentElement.classList.toggle("dark", isDark); 
localStorage.setItem("theme", isDark ? "dark" : "light"); }-->
