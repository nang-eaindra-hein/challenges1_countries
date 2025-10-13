<script>
  import { Search } from "lucide-svelte";
  let search = $state("");
  let dropdown = $state("");
</script>

<div class="flex-col h-screen w-full">
  <!--main screen-->

  <div class="flex justify-between pt-7 w-full h-27 relative">
    <!--div2-->

    <!--<div class="w-96 h-96 bg-blue-500 relative">
            <div class="w-24 h-24 bg-red-500 absolute right-[calc(50%-48px)] bottom-[calc(50%-48px)]>"></div>
            <div class="w-24 h-24 bg-red-500 absolute right-1/2 bottom-1/2 translate-x-1/2 translate-y-1/2"></div>
        </div>-->

    <!--search bar-->

    <div>
      <Search class="absolute w-5 h-5 left-31 top-15 " />

      <input
        type="text"
        placeholder="Search for a Country.."
        bind:value={search}
        class=" flex pl-10 border rounded border-stone-200 m-4 p-4 w-120 shadow-lg ms-28 text-sm"
      />
    </div>

    <div
      class="flex border rounded shadow-md border-stone-200 m-4 p-2 w-40 me-28"
    >
      <!--dropdown-->
      <select bind:value={dropdown} class="w-full">
        <option value="" selected disabled>Filter by Region</option>

        <option value="Africa">Africa</option>
        <option value="America">America</option>
        <option value="Asia">Asia</option>
        <option value="Europe">Europe</option>
        <option value="Oceania">Oceania</option>
      </select>
    </div>
  </div>

  <!-------------------------section 3----------------------------------------------------------->

  <div class="justify-evenly w-full flex pt-10">
    <!--div3-->
    <div class="border rounded-md border-stone-200 shadow-lg px-25 py-25">
      <!--box1-->
      <div>
        <!--inside box1-->
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border border-stone-200 shadow-lg px-25 py-25 rounded-md">
      <!--box2-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border rounded-lg border-stone-200 shadow-lg px-25 py-25">
      <!--box3-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border border-stone-200 rounded shadow-lg px-25 py-25">
      <!--box4-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>
  </div>
  <!-------------------------section 4----------------------------------------------------------->
  <div class=" w-ful flex justify-evenly pt-15">
    <!--div 4-->
    <div class="border rounded border-stone-200 px-25 py-25 shadow-lg">
      <!--box1-->
      <div>
        <!--inside box1-->
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border rounded border-stone-200 shadow-lg px-25 py-25">
      <!--box2-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border border-stone-200 shadow-lg px-25 py-25">
      <!--box3-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>

    <div class="border border-stone-200 shadow-lg px-25 py-25">
      <!--box4-->
      <div>
        <p>img</p>
        <p>text</p>
      </div>
    </div>
  </div>
</div>
