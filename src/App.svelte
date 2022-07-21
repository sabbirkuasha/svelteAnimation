<script>
  import {writable} from 'svelte/store'
  import {tweened} from 'svelte/motion'
  import {cubicIn, elasticIn, elasticOut, expoInOut, quadOut, quintIn} from 'svelte/easing'

  // for different easing function visit this url
  // https://svelte.dev/repl/6904f0306d6f4985b55f5f9673f762ef?version=3.4.1
  const progress = tweened(0,{
    delay:0,
    duration: 700,
    easing: elasticOut
  })


  setTimeout(()=>{
    progress.set(.75)
  },1500)
</script>

<main>
  <progress value={$progress}>

  </progress>
</main>

<style>
  
</style>
