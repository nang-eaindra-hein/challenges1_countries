<script>
  import Back from "../../components/Back.svelte";
  import { MoveLeft } from "lucide-svelte";
</script>

<div class=" flex-col h-screen w-full">
  <!--main screen-->
  <div class=" pt-15 w-full'">
    <!--div 2-->

    <div
      class="ms-15 border flex justify-center items-center shadow-lg border-stone-200 rounded-lg w-40 h-10 text-sm"
    >
      <!--back btn-->
      <button class="flex">
        <MoveLeft />
        <Back />
      </button>
    </div>
  </div>
  <!--------------------section3----------------------------------------------------->
  <div class="bg-red--900 w-full pt-20 ms-15 flex">
    <!--main layout -->

    <div
      class="w-1/2 bg-blue-200 border border-stone-200 shadow-xl rounded-lg px-1 py-50"
    >
      <!--left div-->
      <p>img</p>
    </div>
    <!--------------------section4----------------------------------------------------->

    <div class="w-1/2 ms-15">
      <!--right div-->
      <div class="font-bold text-xl text-stone-800 m-2">
        <!--div1 title-->
        <h1>Country Name</h1>
      </div>
      <!--------------------section5----------------------------------------------------->

      <div class="flex justify-evenly h-80">
        <!--div2 description body-->

        <div class="flex-[1] bg-red-100">
          <!--div3 body1-->

          <p>description1 of body</p>
        </div>
        <div class="flex-[1] bg-yellow-200">
          <!--div4 body2-->
          <p>description2 of body</p>
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
          class="border w-40 h-10 text-center rounded-lg p-1 border-stone-200 shadow-lg"
        >
          <!--div7 border-country name-->
          country name
        </div>
      </div>
    </div>
  </div>
</div>
