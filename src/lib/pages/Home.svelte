<script lang="ts">
  import Anchor from "$lib/components/Anchor.svelte";
  let color = "text-grey-200";
  let hover = "sm:hover:text-primary-500";
  import Confetti from "$lib/components/Confetti.svelte";
  import ToggleConfetti from "$lib/components/ToggleConfetti.svelte"
  import { tick } from 'svelte'
    /**------------------------------ below script for falling confetti----------------------------- */
    export let toggleOnce = false
    export let relative = true
  
    let active = false
  
    async function click() {
      if (toggleOnce) {
        active = !active
        return
      }
  
      active = false
      await tick();
      active = true
    }
   
 /**------------------------------ below script for tap confetti----------------------------- */
    const duration = 2000
  
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
  
<!---------------------------------  confetti falling from home page------------------------------- -->
  <ToggleConfetti toggleOnce relative={true}>
    <div style="position: fixed; top: -50px; left: 0; height: 100vh; width: 100vw; display: flex; justify-content: center; overflow: hidden;">
      <Confetti x={[-5, 5]} y={[0, 0.1]} delay={[500, 2000]}  infinite duration=5000 amount=200 fallDistance="100vh" />
    </div>
  </ToggleConfetti>

 <!-- -------------------------------confetti on click ----------------------------------- -->
  <div class="box" on:click={moveConfetti}>
      {#each things as thing}
      <div class="mover" style="left: {thing.x}px; top: {thing.y}px">
        <Confetti y={[-0.5, 0.5]} fallDistance=20px amount=10 {duration} />
      </div>
    {/each}


 <!-- -------------------------------homepage stuff ----------------------------------- -->

<Anchor id="home" />
<div
  class="flex flex-col items-center justify-center bg-center bg-no-repeat bg-cover page lg:bg-fixed bg-neutral-600 bg-blend-soft-light dark:bg-blend-soft-light dark:bg-neutral-700"
  id="bg"
>
  <div class="text-center">
    <div class="content">
      <h2 class="text_shadows">Happy Spooktacular Bday Charles!🎃🐒</h2> 
    </div>
  </div>
</div>
</div>

 <!-- -------------------------------------css ------------------------------------------------------- -->
<style>
  /*-----------------------confetti on click css -----------------------------*/

  
    .mover {
      position: absolute;
    }
  
  
/*---------------------------------body css -----------------------------------------*/
  #bg {
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



.content {
  display: flex;
  align-content: center;
  justify-content: center;
}
/* ---------------------------- letter animation css-----------------------------  */
.text_shadows {
  text-shadow: 3px 3px 0 var(--color-secondary), 6px 6px 0 var(--color-tertiary),
    9px 9px var(--color-quaternary), 12px 12px 0 var(--color-quinary);
  font-family: bungee, sans-serif;
  font-weight: 200;
  text-transform: uppercase;
  font-size: calc(1.2rem + 2.2vw);
  text-align: center;
  margin: 0;
  color: var(--color-primary);
   padding:20px;
  animation: shadows 2.00s ease-in infinite, move 3.2s ease-in infinite;

  letter-spacing: 0.4rem;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
 
@keyframes shadows {
  0% {
    text-shadow: none;
  }
  10% {
    text-shadow: 3px 3px 0 var(--color-secondary);
  }
  20% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary);
  }
  30% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary), 9px 9px var(--color-quaternary);
  }
  40% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary), 9px 9px var(--color-quaternary),
      12px 12px 0 var(--color-quinary);
  }
  50% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary), 9px 9px var(--color-quaternary),
      12px 12px 0 var(--color-quinary);
  }
  60% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary), 9px 9px var(--color-quaternary),
      12px 12px 0 var(--color-quinary);
  }
  70% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary), 9px 9px var(--color-quaternary);
  }
  80% {
    text-shadow: 3px 3px 0 var(--color-secondary),
      6px 6px 0 var(--color-tertiary);
  }
  90% {
    text-shadow: 3px 3px 0 var(--color-secondary);
  }
  100% {
    text-shadow: none;
  }
}

@keyframes move {
  0% {
    transform: translate(0px, 0px);
  }
  40% {
    transform: translate(-12px, -12px);
  }
  50% {
    transform: translate(-12px, -12px);
  }
  60% {
    transform: translate(-12px, -12px);
  }
  100% {
    transform: translate(0px, 0px);
  }
}

</style>