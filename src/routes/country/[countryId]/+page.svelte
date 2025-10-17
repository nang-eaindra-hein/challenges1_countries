<script lang="ts">
  import { page } from "$app/stores";
  import Back from "../../../components/Back.svelte";
  import { goto } from "$app/navigation";

  //border state
  let borderCountries: any[] = $state([]);

  //main country
  let country: any | null = $state(null);

  //border func
  function openBorder(name: string) {
    goto(`/country/${encodeURIComponent(name)}`);
  }

  $effect(() => {
    const countryId = $page.params.countryId; //useparam dynamic route

    if (!countryId) return; //if nth ,stop run

    const fetchFields = async () => {
      //clear out old data for fetch new
      borderCountries = [];
      country = null;

      const res =
        await fetch(`https://restcountries.com/v3.1/name/${encodeURIComponent(countryId)}?fullText=true&
      fields=name,population,capital,region,subregion,flags,currencies,languages,tld,borders`);

      //if res not ok ,stop run
      if (!res.ok) return;

      //country holds full data for one country
      const list = await res.json();
      country = Array.isArray(list) ? list[0] : null;

      //country yw border yw shi m shi check
      if (country?.borders?.length) {
        //shi yin border fetch
        const codes = country.borders.join(",");
        const resBorders = await fetch(
          `https://restcountries.com/v3.1/alpha?codes=${codes}&fields=name,cca3`
        );
        //set border data to json
        borderCountries = resBorders.ok ? await resBorders.json() : [];
      } else {
        borderCountries = [];
      }
    };
    fetchFields();
  });

  /*$effect(() => {
    const fetchFields = async () => {
      const res = await fetch(
        "https://restcountries.com/v3.1/name?fields=name,population,capital,region,subregion,flag,currency,lang,tld,borders"
      );
      fields = await res.json();
    };
   
    for(const c of fields){
      if (c.name.common.toLowerCase() === countryId.toLowerCase()) {
          country = c;
    }}
     fetchFields();
  });*/
</script>

<div class=" text-text bg-background flex-col h-screen w-full">
  <!--main screen-->

  <div class=" text-text bg-background pt-15 w-full'">
    <!--div 2-->
    <Back />
  </div>

  <!--------------------section3----------------------------------------------------->
  <div class="text-text bg-background w-full pt-20 ms-15 flex">
    <!--main layout -->
    {#if country}
      <div class=" border shadow-xl rounded-lg w-200">
        <!--left div-->

        <div>
          <img
            src={country.flags.png}
            alt="flags"
            class="display-block w-full"
          />
        </div>
      </div>
      <!--------------------section4----------------------------------------------------->

      <div class="w-1/2 ms-30">
        <!--right div-->
        <div class="text-text font-bold m-10 text-xl">
          <!--div1 title-->
          <h1>{country.name.common}</h1>
        </div>
        <!--------------------section5----------------------------------------------------->

        <div class="text-text bg-background flex justify-evenly h-80">
          <!--div2 description body-->

          <div class="flex-[1] text-lg">
            <!--div3 body1-->

            <div class="font-semibold">
              Native Name:{country.name.official}
            </div>
            <div class="font-semibold">Population : {country.population}</div>
            <div class="font-semibold">Region :{country.region}</div>
            <div class="font-semibold">Sub Region :{country.subregion}</div>
            <div class="font-semibold">Capital :{country.capital}</div>
          </div>
          <div class="flex-[1]">
            <!--div4 body2-->

            <div class="font-semibold">
              Top Level Domain :{Object.values(country.tld).join(" , ")}
            </div>
            <div class="font-semibold">
              Currencies :{country.currencies
                ? Object.values(country.currencies)
                    .map((c: any) => c.name)
                    .join(", ")
                : "—"}
            </div>
            <div class="font-semibold">
              Languages :{Object.values(country.languages).join(" , ")}
            </div>
          </div>
        </div>
        <!--------------------section6----------------------------------------------------->

        <div class="w-full pt-10 flex justify-start">
          <!--div5 border-->

          <div class="font-bold w-40">
            <!--div6 border title-->
            <p>Border Countries :</p>
          </div>

          <div class="flex flex-wrap gap-2">
            <!--div7 border-country name-->
            {#if borderCountries?.length}
              {#each borderCountries as code}
                <button
                  onclick={() => openBorder(code.name.common)}
                  class=" items-center rounded-md border px-3 py-1 text-sm border-secondary
                 bg-secondary hover:bg-primary hover:text-background
                  shadow-sm"
                >
                  {code.name.common}
                </button>
              {/each}
            {:else}
              <h2>No border</h2>
            {/if}
          </div>
        </div>
      </div>
    {:else}
      <p class="p-8">Loading country data…</p>
    {/if}
  </div>
</div>
