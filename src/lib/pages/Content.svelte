<script lang="ts">
  import Anchor from "$lib/components/Anchor.svelte";
  import Text from "$lib/components/Text.svelte";
  import Confetti from "$lib/components/Confetti.svelte";
  import CollapsibleCard from 'svelte-collapsible-card'
  export let link:string;
  import { signatures } from "./signatures";
  /**------------------------------ below script for tap confetti----------------------------- */
  const duration = 1500
  
  /**
* @type {any[]}
*/
  let things = []
  /**
* @type {string | number | NodeJS.Timeout | undefined}
*/
  let timeout

  async function moveConfetti(event) {
    const { target, clientX, clientY } = event

    const elementY = target.getBoundingClientRect().top
    const elementX = target.getBoundingClientRect().left

    const x = clientX - elementX
    const y = clientY - elementY

    things = [...things, { x, y }]

    clearTimeout(timeout)

    timeout = setTimeout(() => things = [], duration)
  }
  
</script>



<!-----------------confetti click should encapsulate page---------------------------->
<div class="box" on:click={moveConfetti}>
  {#each things as thing}
    <div class="mover" style="left: {thing.x}px; top: {thing.y}px">
      <Confetti y={[-0.5, 0.5]} fallDistance=20px amount=10 {duration} />
    </div>
  {/each}



<Anchor id="content"/>
 

  <div
  class="flex flex-col items-center justify-center bg-center bg-no-repeat bg-cover page lg:bg-fixed bg-neutral-600 bg-blend-soft-light dark:bg-blend-soft-light dark:bg-neutral-700"
  id="bg"
>

 <!-----------------collapsible card below---------------------------->
  <ul>
	
    { #each signatures as signature }
      <li>
        <CollapsibleCard>
          <div slot='header' class='header'>
            <div class='names'>
              <h2>{ signature.name }</h2>
            </div>
          </div>
          <div slot='body' class='body'>
            { signature.message } <br><br>
            <p>{ signature.message2 }</p>
            <a href={signature.link} class="link-text" target="_blank" rel="noopener noreferrer">
              { signature.link }
          </div>
        
        </CollapsibleCard>
      </li>
    { /each }
  
  </ul>
<!-----------------collapsible card below---------------------------->
</div>

</div>

<!--------------------------------------------css--------------------------------------------------->
<style>
  #bg
  {
    background-image: radial-gradient(circle,#df2e2e,#d67836,#e71506);
  }

  .box {
      display: flex;
      align-items: center;
      justify-content: center;
      position: relative;
      height: 100%;
      width: 100%;
      background: none;
      overflow: hidden;
    }
  
    .mover {
      position: absolute;
    }
  
    

    /*--------------------------------------------collpasible css --------------------------------------------*/
    ul {
		list-style: none;
		padding: 0;
		margin: 0 auto;
		width:80%;
		color:  #FFEADB;
		font-size: 1.5rem;
    font-weight:bold;
    background-color:#7F1D1D;
    border-radius: 10px;
   
	}
	
	li {
		margin-bottom: 0em;
		border-bottom: 1px solid #FFEADB;
    border-radius: 10px;
	}
	
	.header {
		padding: 0.3em;
		display: flex;
    background-color: #7F1D1D;
    border-radius: 10px;
	}
	

	.names {
		padding: 0 0 0 1em;
		display: flex;
		flex-direction: column;
		justify-content: center;

	}
	
	h2 {
		margin: 0;
		width: 100%;
    
	}
	
	p {
		margin: 0;
	}
	
	.body {
    padding: 0 0 0 0em;
	}
  .link {
		background-color: var(--text);
		display: flex;
		align-items: center;
		justify-content: center;
		color: var(--left);
		font-size: 1.5rem;
		margin: 0;
		padding: 0.5em;
	}

	.link-text {
		color: #f1f5db;
		border: 2px solid var(--left);
		border-radius: 0.25rem;
		padding: 0.25rem;
	}

	.link-text:hover {
		background-color: var(--left);
		color: #dbdbc2;
	}
</style>

