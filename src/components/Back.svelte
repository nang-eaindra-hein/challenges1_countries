<script lang="ts">
  import { MoveLeft } from "lucide-svelte";
  import { goto } from "$app/navigation";

  function goBack() {
    if (window.history.length > 1) {
      window.history.back();
    } else {
      goto("/");
    }
  }
</script>

<button
  onclick={goBack}
  class="ms-15 text-text bg-secondary border-secondary border flex justify-center items-center shadow-lgrounded-lg w-40 h-10 text-sm"
>
  <!--back btn-->

  <MoveLeft />
  Back
</button>
