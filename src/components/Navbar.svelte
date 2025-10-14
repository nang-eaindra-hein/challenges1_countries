<script>
  import { Moon } from "lucide-svelte";
</script>

<div
  class="border border-stone-300 text-primary flex p-8 justify-between shadow-md"
>
  <div class="font-bold text-xl text-stone-700">
    <h1>Where is the world?</h1>
  </div>

  <button>
    <div class="flex text-stone-700">
      <Moon />
      <div class="ms-1">Darkmode</div>
    </div>
  </button>
</div>
