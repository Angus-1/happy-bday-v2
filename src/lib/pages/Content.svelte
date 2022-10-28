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
            <br>
            <a href={signature.link} class="link-text" target="_blank" rel="noopener noreferrer">
              <p> { signature.link }</p> </a>
              <br>  <br>
              <div class = "image "> <img src={signature.image} alt="image here" width=900 > </div>   
                <br>  <br>
          </div>
      
        </CollapsibleCard>
      </li>
    { /each }
  
  </ul>
<!-----------------collapsible card below---------------------------->
</div>



<!--------------------------------------------css--------------------------------------------------->
<style>
  #bg
  {
    background: linear-gradient(-45deg, #973831,#882b25,#5C2420, #4d1d1a);
	background-size: 400% 400%;
	animation: gradient 10s ease-in-out infinite alternate;
	height: 100vh;
  }
  @keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
  }
  *,
*::before,
*::after {
  box-sizing: border-box;
}

:root {
  --color-primary: #FFEADB;
  --color-secondary: #c46f64;
  --color-tertiary: #b86d63;
  --color-quaternary: #7c3930;
  --color-quinary: #813f36;
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
    background-color:#6e1515;
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
  .header:hover{
    background-color: #d33a3a75;
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
    padding: 0 0 3em 3em;
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
		color: #d3d386;
	}

  .body {
    padding: 0 0 0 0em;
    text-align: center;
    display: block;
    padding-top: 20px;
	}
  .image
  {
    display: flex;
      justify-content: center;
  }
</style>

