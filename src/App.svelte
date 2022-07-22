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

  function addBoxes(){
    boxes = [...boxes, inputBox.value]
  }
</script>

<main>
  <div class="pb-3">
    <div class="pb-3 radial-progress" style="--value:{$progress*100}; --size:12rem; --thickness: 2rem;">
      80%
    </div>
  </div>
  
  <div class="pb-3">
    <progress value={$progress}>

    </progress>  
  </div>

  <div class="w-full pb-3">
    <div class="form-control">
      <div class="input-group ">
        <input  type="text"
                bind:this={inputBox} 
                placeholder="Type here" 
                class="input input-bordered input-primary w-full max-w-xs" />
        <button class="btn" on:click={addBoxes}>Go</button>
      </div>
    </div>
  </div>


  <div class="flex">
    {#each boxes as box}
      <div class="p-3" transition:scale ={
        {
          delay:0,
          duration:200,
          easing:cubicIn,
        }
      }>
        <div class="card w-96 bg-neutral text-neutral-content">
          <div class="card-body items-center text-center">
            <h2 class="card-title">{box}!</h2>
          </div>
        </div>
      </div>
    {/each}
  </div>
  
</main>

<style>
  
</style>
