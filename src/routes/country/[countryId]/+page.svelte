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
</script>

<div class=" text-text transition:colors duration:150 flex-col h-screen w-full">
  <!--main screen-->

  <div class="pt-10">
    <!--div 2-->
    <Back />
  </div>

  <!--------------------section3----------------------------------------------------->
  <div class="text-text w-full pt-20 ms-15 flex">
    <!--main layout -->
    {#if country}
      <div class="ms-8 shadow-4xl rounded-lg">
        <!--left div-->

        <div>
          <img
            src={country.flags.svg}
            alt="flags"
            class="display-block w-full"
          />
        </div>
      </div>
      <!--------------------section4----------------------------------------------------->

      <div class="ms-20 w-full">
        <!--right div-->
        <div class="text-text font-semibold m-4 text-2xl">
          <!--div1 title-->
          <h1>{country.name.common}</h1>
        </div>
        <!--------------------section5----------------------------------------------------->

        <div class="text-text flex justify-evenly w-200 h-50">
          <!--div2 description body-->

          <div class="m-2 p-1 w-full">
            <!--div3 body1-->

            <div class="flex w-full pb-1">
              <div class="font-semibold text-md">Native Name</div>
              <div class="font-light text-sm">: {country.name.official}</div>
            </div>

            <div class="flex w-full pb-1">
              <div class="font-semibold text-md">Population</div>
              <div class="font-light text-sm">
                : {country.population.toLocaleString()}
              </div>
            </div>

            <div class="flex w-full pb-1">
              <div class="font-semibold text-md">Region</div>
              <div class="font-light text-sm">: {country.region}</div>
            </div>

            <div class="flex w-full pb-1">
              <div class="font-semibold text-md">Sub Region</div>
              <div class="font-light text-sm">: {country.subregion}</div>
            </div>

            <div class="flex w-full">
              <div class="font-semibold text-md">Capital</div>
              <div class="font-light text-sm">: {country.capital}</div>
            </div>
          </div>

          <div class="m-5 w-full">
            <!--div4 body2-->
            <div class="flex w-full pb-2">
              <div class="font-semibold text-md">Top Level Domain</div>
              <div class="font-light text-sm">
                : {Object.values(country.tld).join(" , ")}
              </div>
            </div>

            <div class="flex w-full pb-1">
              <div class="font-semibold text-md">Currencies</div>
              <div class="font-light text-sm">
                : {country.currencies
                  ? Object.values(country.currencies)
                      .map((c: any) => c.name)
                      .join(", ")
                  : "—"}
              </div>
            </div>

            <div class="flex w-full">
              <div class="font-semibold text-md">Languages</div>
              <div class="font-light text-sm">
                : {Object.values(country.languages).join(" , ")}
              </div>
            </div>
          </div>
        </div>
        <!--------------------section6----------------------------------------------------->

        <div class="w-full flex justify-start">
          <!--div5 border-->

          <div class="font-semibold text-md w-40">
            <!--div6 border title-->
            <p>Border Countries :</p>
          </div>

          <div class="flex flex-wrap gap-4">
            <!--div7 border-country name-->
            {#if borderCountries?.length}
              {#each borderCountries as code}
                <button
                  onclick={() => openBorder(code.name.common)}
                  class="rounded-md w-25 h-7 text-sm
                 hover:opacity-80
                  shadow"
                >
                  {code.name.common}
                </button>
              {/each}
            {:else}
              <h2>No Border Countries</h2>
            {/if}
          </div>
        </div>
      </div>
    {:else}
      <p class="justify-center items-center">Loading country data…</p>
    {/if}
  </div>
</div>
