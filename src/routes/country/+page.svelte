<script lang="ts">
  import Back from "../../components/Back.svelte";
  import { MoveLeft } from "lucide-svelte";

  let fields: any[""] = $state("");

  const fetchFields = async () => {
    const res = await fetch(
      "https://restcountries.com/v3.1/all?fields=flags,name,borders,region,subregion,population,currencies,capital,languages,tld"
    );
    fields = await res.json();
  };
  fetchFields();
</script>

<div class=" text-text bg-background flex-col h-screen w-full">
  <!--main screen-->
  <div class=" text-text bg-background pt-15 w-full'">
    <!--div 2-->

    <div
      class="ms-15 text-text bg-secondary border-secondary border flex justify-center items-center shadow-lgrounded-lg w-40 h-10 text-sm"
    >
      <!--back btn-->
      <button class="text-text bg-secondary flex">
        <MoveLeft />
        <Back />
      </button>
    </div>
  </div>
  <!--------------------section3----------------------------------------------------->
  <div class="text-text bg-background w-full pt-20 ms-15 flex">
    <!--main layout -->

    <div class=" border shadow-xl rounded-lg w-200">
      <!--left div-->
      {#each fields as field}
        <div>
          <img src={field.flags.png} alt="flags" class="display-block w-full" />
        </div>
      {/each}
    </div>
    <!--------------------section4----------------------------------------------------->

    <div class="w-1/2 ms-30">
      <!--right div-->
      <div class="text-text font-bold m-10 text-xl">
        <!--div1 title-->
        <h1>Country Name</h1>
      </div>
      <!--------------------section5----------------------------------------------------->

      <div class="text-text bg-background flex justify-evenly h-80">
        <!--div2 description body-->

        <div class="flex-[1] text-lg">
          <!--div3 body1-->
          {#each fields as field}
            <div class="font-semibold">
              Native Name:{field.name.nativenames}
            </div>
            <div class="font-semibold">Population :{field.population}</div>
            <div class="font-semibold">Region :{field.region}</div>
            <div class="font-semibold">Sub Region :{field.subregion}</div>
            <div class="font-semibold">Capital :{field.capital}</div>
          {/each}
        </div>
        <div class="flex-[1]">
          <!--div4 body2-->
          {#each fields as field}
            <div class="font-semibold">Top Level Domain :{field.tld}</div>
            <div class="font-semibold">Currencies :{field.currencies}</div>
            <div class="font-semibold">Languages :{field.languages}</div>
          {/each}
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
          {#each fields as field}
            <div>
              <button>{field.borders}</button>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </div>
</div>
