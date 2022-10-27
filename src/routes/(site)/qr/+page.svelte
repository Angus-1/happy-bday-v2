<script lang="ts">
    import Page from "$lib/components/Page.svelte";
    import { QRCodeImage } from "svelte-qrcode-image";
    let site_url ="http://monkeyy.net/"
    import Text from "$lib/components/Text.svelte";


  </script>
  
<Text>
    <div
  class="flex flex-col items-center justify-center bg-center bg-no-repeat bg-cover page lg:bg-fixed bg-red-900"
  id="bg"
>

<div class = "size"> 
  <QRCodeImage text = {site_url} width=600 height=600/>
</div>

  <div>
</Text>

