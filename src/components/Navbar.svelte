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
  class="border-primary bg-secondary flex p-5 justify-between items-center shadow-xl ease-in-out transition-colors duration-150"
>
  <div class="font-semibold ms-15 text-lg text-text hover:opacity-50">
    <a href="/"> <h1>Where is the world?</h1></a>
  </div>

  <button
    onclick={toggleDark}
    class="flex text-sm me-15 font-light hover:opacity-50"
  >
    {#if isDark}
      <Moon class="text-white w-5 h-5 " />
      <div class="ms-1 text-text">Light Mode</div>
    {:else}
      <Moon class="text-text w-5 h-5" />
      <div class="ms-1 text-text">Dark Mode</div>
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
