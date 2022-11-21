<script>

  let behaviour = "selection";
  let selection ="";
  let message  =""
  let status =""
  let machineSelection =""

  const machineTurn = async () =>{
    await fetch('https://err83c2bs1.execute-api.us-east-1.amazonaws.com/Prod/hello?played='+selection)
    .then(r => r.json())
    .then(data => {
      message = data.message
      status = data.status
      machineSelection = data.machineSelection
    })
    behaviour = "result"
  }

  $: if(selection) machineTurn()

  const playAgain = () =>{
    let selection ="";
    let message =""
    let status =""
    let machineSelection  =""
    behaviour = "selection"
  }

</script>


{#if behaviour === "selection"}
  <div>
    <div class="title">
      <h2>Bienvenido a <br> ¡PIEDRA PAPEL O TIJERA!</h2>
    </div>
    
    <div class="objective">
      <span>Has tu selección y derrota la computadora >:D</span>
    </div>
    
    <div>
      <div>
        <button class="selectionButton" on:click={()=>{selection ="piedra"}} ><img src="src/assets/piedra.png" alt="piedra" class="selectionImage"> Piedra</button>
        <button class="selectionButton" on:click={()=>{selection ="papel"}}><img src="src/assets/papel.png" alt="papel" class="selectionImage"> Papel</button>
        <button class="selectionButton" on:click={()=>{selection ="tijera"}}><img src="src/assets/tijera.png" alt="tijera" class="selectionImage"> Tijera</button>
      </div>
    </div>
  </div>

{:else if behaviour === "result"}
  <div>
    {#if status === "win"}
      <img src="src/assets/humano.png" alt="machine" class="horizontalImage">
    {:else if status === "draw"}
      <img src="src/assets/draw.jpg" alt="draw" class="horizontalImage">
    {:else if status === "lose"}
      <img src="src/assets/machine.jpg" alt="draw" class="verticalImage">
    {/if}
  </div>
  
  <div>
    <span>La maquina eligió</span>
    <h2>{machineSelection}</h2>
    <span>{message}</span>
  </div>

  <div>
    <button on:click={playAgain}>Volver a jugar</button>
  </div>
  
{/if}

<style>
  .verticalImage{
    height: 15%;
    width: 30%;
  }

  .horizontalImage{
    height: 40%;
    width: 25%;
  }

  .objective{
    margin-bottom: 2%;
  }

  .title{
    margin-bottom: 10%;
  }
  .selectionButton{
    height: 100px;
    width: 100px;
    padding: 0px;
    border-radius: 10px;
    color: #242424;
    transition: 0.2s;
    margin-right: 2%;
  }

  .selectionButton:hover{
    color:aliceblue;
  }

  .selectionImage{
    width: 100%;
    height: 100%;
    border-radius: 10px;
  }

</style>