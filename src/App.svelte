<script>
  import {writable} from 'svelte/store'
  import {tweened} from 'svelte/motion'
  import {cubicIn, elasticIn, elasticOut, expoInOut, quadOut, quintIn} from 'svelte/easing'
  import Spring from './Spring.svelte';
  import {fade, fly, slide, scale} from 'svelte/transition'

  // for different easing function visit this url
  // https://svelte.dev/repl/6904f0306d6f4985b55f5f9673f762ef?version=3.4.1
  const progress = tweened(0,{
    delay:0,
    duration: 700,
    easing: cubicIn
  })


  setTimeout(()=>{
    progress.set(.75)
  },1500)

 
  let inputBox
  let boxes = []
  let showParagraph = true
  $:pulseAnimClass = ""


  function addBoxes(){
    boxes = [...boxes, inputBox.value]
  }

  function discard(value){
    boxes=boxes.filter(el=> el !== value)
  }

  function puleAnim(){
    pulseAnimClass = "animate-bounce"
    setTimeout(()=>{
      pulseAnimClass = ""
    },3000)
  }
</script>

<main class="w-screen text-center overflow-hidden	">

  <div class="pb-3">
    <div class="pb-3 radial-progress" style="--value:{$progress*100}; --size:12rem; --thickness: 2rem;">
      80%
    </div>
  </div>
  
  <div class="pb-3">
    <progress value={$progress}>

    </progress>  
  </div>



  <div class="pb-3">
    <div class="form-control items-center flex justify-center">
      <div class="input-group w-1/2 flex justify-center">
        <input  type="text"
        bind:this={inputBox} 
        placeholder="Type here" 
        class="input input-bordered input-primary w-full max-w-xs items-center" />
        
        <button class="btn" on:click={addBoxes}>Go</button>
      </div>
    </div>
  </div>

  <div>
    <button on:click={()=>{
      showParagraph = !showParagraph
    }}
    class="mb-3 btn btn-primary animate-pulse">
      Toggle
    </button>

    {#if showParagraph}
      <p transition:fly|local ={
        {
          delay:0,
          duration:200,
          easing:cubicIn,
          x: 200,
          y: 0,
        }
      }>
        Now You See Me
      </p>  
    <div class="flex">
      {#each boxes as box}
        <div class="p-3" 
          transition:fly|local =
          {
            {
              delay:0,
              duration:200,
              easing:cubicIn,
              x: 0,
              y:200,
            }
          }
          on:click={discard.bind(this,box)}
          on:introstart={puleAnim}
        >
          <div class="card w-96 bg-neutral text-neutral-content {pulseAnimClass}">
            <div class="card-body items-center text-center">
              <h2 class="card-title">{box}!</h2>
            </div>
          </div>
        </div>
      {/each}
    </div>
    {:else}
      <p transition:fly ={
        {
          delay:1,
          duration:200,
          easing:cubicIn,
          x: -200,
          y: 0,
        }
      }>Now You Not</p>
    {/if}

  </div>
</main>

<style>
  
</style>
