<script lang="ts">
  import { Search } from "lucide-svelte";

  let search = $state("");
  let dropdown = $state("");
  let fields: any[] = $state([]);
  let africa = $state("africa");

  $effect(() => {
    if (search) {
      const searchedFields = async () => {
        const res = await fetch(
          `https://restcountries.com/v3.1/name/${search}`
        );
        fields = await res.json();
      };
      searchedFields();
    } else {
      const fetchFields = async () => {
        const res = await fetch(
          "https://restcountries.com/v3.1/all?fields=name,population,capital,region,subregion,flags,flag"
        );
        fields = await res.json();
      };
      fetchFields();
    }
  });

  function getAfrica() {
    const africaFields = async () => {
      const res = await fetch(
        `https://restcountries.com/v3.1/all?fields=name,region/${africa}`
      );
      africa = await res.json();
    };
    africaFields();
  }

  /* $effect(() => {
    fetch(`https://restcountries.com/v3.1/name/${search}`)
      .then((res) => {
        return res.json();
      })
      .then((data) => (fields = data));
  });

  /*  function test(data) {
    return (fields = data);
  }

  (data) => (fields = data);

  data = await res.json(); */

  /*onMount(() => {
    const getFields = async () => {
      const response = await fetch(
        "https://restcountries.com/v3.1/all?fields=name"
      );
      const fields = await response.json();

      console.log(fields[0].name.official);
    };
    getFields();
  });

  /*async function bigData() {
    const fields = ["name"];
  }
  const res = await fetch ("https://restcountries.com/v3.1/all?fields=name"){
    method : 'POST',
    headers : {'Content-Type': "application/json"},
    body : JSON-stringify({name:}),
  }
  const data = await res.json();
  console.log(data);*/
</script>

<div class="flex-col h-screen w-full text-text bg-background">
  <!--main screen-->

  <div
    class="flex text-text bg-background justify-between pt-7 w-full h-27 relative"
  >
    <!--div2-->

    <!--<div class="w-96 h-96 bg-blue-500 relative">
            <div class="w-24 h-24 bg-red-500 absolute right-[calc(50%-48px)] bottom-[calc(50%-48px)]>"></div>
            <div class="w-24 h-24 bg-red-500 absolute right-1/2 bottom-1/2 translate-x-1/2 translate-y-1/2"></div>
        </div>-->

    <!--search bar-->

    <div>
      <Search class="text-text bg-secondary absolute w-7 h-7 left-31 top-15 " />

      <input
        type="text"
        placeholder="Search for a Country.."
        bind:value={search}
        class=" flex pl-12 border bg-secondary rounded border-primary m-3 p-5 w-120 shadow-lg ms-30 text-md"
      />
    </div>

    <div
      class="text-text bg-secondary flex border rounded shadow-md border-primary m-4 p-2 w-40 me-28"
    >
      <!--dropdown-->
      <select bind:value={dropdown} class="w-full">
        <option value="" selected disabled>Filter by Region</option>

        <!--<button onclick={getAfrica}
          ><option value="Africa">Africa</option></button
        >-->
        <option value="America">America</option>
        <option value="Asia">Asia</option>
        <option value="Europe">Europe</option>
        <option value="Oceania">Oceania</option>
      </select>
    </div>
  </div>

  <!-------------------------section 3----------------------------------------------------------->

  <div class=" bg-background w-full justify-evenly pt-10 grid grid-cols-4">
    <!--div3-->

    <!--box1-->

    <!--inside box1-->
    {#each fields as field}
      <div
        class="border border-secondary bg-secondary rounded-md shadow-lg m-25"
      >
        <div>
          <!--image-->
          <img src={field.flags.png} alt="flag" class="w-full display-block" />
        </div>

        <div class="font-bold p-2 text-xl m-3">
          <!--title-->
          {field.name.common}
        </div>

        <div class="p-5">
          <div>
            <span class="font-semibold">Population: </span>{field.population}
          </div>
          <div>
            <span class="font-semibold">Region :</span>
            {field.region}
          </div>
          <div>
            <span class="font-semibold">Capital : </span>{field.capital}
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>
