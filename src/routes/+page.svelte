<script lang="ts">
  import { Search } from "lucide-svelte";

  //search+debounced
  let search = $state("");
  let debouncedSearch = $state("");

  //dropdown
  let dropdown = $state("");
  let fields: any[] = $state([]);

  //debounce yk effect
  $effect(() => {
    search;
    const timeout = setTimeout(() => {
      debouncedSearch = search;
    }, 300);

    return () => {
      clearTimeout(timeout);
    };
  });

  //debounce yk console
  $effect(() => {
    console.log(debouncedSearch);
  });

  //debounce+ filter yk efffect
  $effect(() => {
    const term = debouncedSearch.trim();
    const region = dropdown.trim();
    (async () => {
      let url: string;

      // search first, then filter by region locally
      if (term && region) {
        url = `https://restcountries.com/v3.1/name/${encodeURIComponent(term)}?fields=name,population,capital,region,subregion,flags`;
      } else if (!term && region) {
        // only region
        url = `https://restcountries.com/v3.1/region/${encodeURIComponent(region)}?fields=name,population,capital,region,subregion,flags`;
      } else if (term && !region) {
        // only search
        url = `https://restcountries.com/v3.1/name/${encodeURIComponent(term)}?fields=name,population,capital,region,subregion,flags`;
      } else {
        // neither
        url = `https://restcountries.com/v3.1/all?fields=name,population,capital,region,subregion,flags`;
      }

      //fetch for url
      const res = await fetch(url);
      let data = res.ok ? await res.json() : [];

      // when BOTH search and region are set, filter by region here
      if (term && region) {
        const result = region.toLowerCase();
        data = data.filter((c: any) => c.region?.toLowerCase() === result);
      }
      fields = Array.isArray(data) ? data : [];
    })();
  });
</script>

<div class="h-screen ease-in-out w-full text-text">
  <!--main screen-->

  <div class="flex text-text justify-between w-full pt-8 px-16">
    <!--div2-->
    <!--search bar-->

    <div class="relative">
      <Search
        class=" text-text absolute w-5 h-5 left-4 top-1/2 -translate-y-1/2"
      />

      <input
        type="text"
        placeholder="Search for a Country.."
        bind:value={search}
        class="flex pl-12 rounded border-primary w-120 shadow-md p-3 text-sm transition-colors duration-150"
      />
    </div>

    <!--dropdown-->
    <select
      bind:value={dropdown}
      class="text-text rounded shadow-md border-primary font-light texts-sm px-4 cursor-pointer transition-colors duration-150"
    >
      <option value="" selected disabled>Filter by Region</option>

      <option value="Americas">Americas</option>
      <option value="Asia">Asia</option>
      <option value="Europe">Europe</option>
      <option value="Oceania">Oceania</option>
    </select>
  </div>

  <!-------------------------section 3----------------------------------------------------------->

  <div class=" pt-10 grid grid-cols-4 gap-8 px-16">
    <!--div3-->

    <!--box1-->

    <!--inside box1-->

    {#each fields as c}
      <div
        class=" hover:opacity-80 bg-secondary rounded-md shadow-md duration-150 transition-opacity"
      >
        <a href={`/country/${c.name.common}`}>
          <div>
            <!--image-->
            <img src={c.flags.png} alt="flag" class="w-full display-block" />
          </div>

          <div class="p-4">
            <div class="font-bold text-md mb-2">
              <!--title-->
              {c.name.common}
            </div>

            <div class="text-sm">
              <div>
                <span class="font-semibold">Population: </span>
                {c.population.toLocaleString()}
              </div>
              <div>
                <span class="font-semibold">Region:</span>
                {c.region}
              </div>
              <div>
                <span class="font-semibold">Capital: </span>
                {c.capital}
              </div>
            </div>
          </div>
        </a>
      </div>
    {/each}
  </div>
</div>
