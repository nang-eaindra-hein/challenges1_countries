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
  class="ms-20 hover:opacity-50 transition-opacity duration-150 text-text bg-secondary flex
   justify-center items-center shadow-md p-4 py-2 text-sm rounded-lg"
>
  <!--back btn-->

  <MoveLeft class="me-2" />
  Back
</button>
