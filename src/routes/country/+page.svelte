<script lang="ts">
  import Back from "../../components/Back.svelte";
  let country: any | null = $state(null);
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
            <div class="font-semibold">Population :{country.population}</div>
            <div class="font-semibold">Region :{country.region}</div>
            <div class="font-semibold">Sub Region :{country.subregion}</div>
            <div class="font-semibold">Capital :{country.capital}</div>
          </div>
          <div class="flex-[1]">
            <!--div4 body2-->

            <div class="font-semibold">Top Level Domain :{country.tld}</div>
            <div class="font-semibold">Currencies :{country.currency}</div>
            <div class="font-semibold">Languages :{country.lang}</div>
          </div>
        </div>
        <!--------------------section6----------------------------------------------------->

        <div class="w-full pt-10 flex justify-start">
          <!--div5 border-->

          <div class="font-bold w-40">
            <!--div6 border title-->
            <p>Border Countries :</p>
          </div>

          <div
            class="border border-secondary bg-secondary w-40 h-10 text-center rounded-lg p-1 shadow-lg"
          >
            <!--div7 border-country name-->

            <div>
              <button>{country.borders}</button>
            </div>
          </div>
        </div>
      </div>
    {/if}
  </div>
</div>
