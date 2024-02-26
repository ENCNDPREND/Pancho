<script>
    let distancia = 0;
    let velocidad = 0;
    let tiempo = 0;
    let error = false;  
    let bot = true;    
    let magnitud="010";
  
    function calcular() {
      bot = false; 
        error = false;
        if (distancia === null) {
          distancia=0;
        }
        if (velocidad === null) {
          velocidad=0;
        }
        if (tiempo === null) {
          tiempo=0;
        }


      if (distancia != 0 && velocidad !== 0 && tiempo !== 0) {
        error = true;
        return;
      }

    
      // la magnitud a calcular

      if (distancia !== 0 && velocidad !== 0) {
        magnitud = "tiempo";
        tiempo = distancia / velocidad;
      } else if (distancia !== 0 && tiempo !== 0) {
        magnitud = "velocidad";
        velocidad = distancia / tiempo;
      } else if (velocidad !== 0 && tiempo !== 0) {
        magnitud = "distancia";
        distancia = velocidad * tiempo;
      } // pa redondearlo
      tiempo = tiempo.toFixed(4);
      velocidad = velocidad.toFixed(4);
      distancia = distancia.toFixed(4);
      if (tiempo < 0) {
    tiempo *= -1;
  }
  
    }
  </script>
  
  <div>
    <h1>Calculadora de distancia, velocidad y tiempo</h1>  {magnitud}
    <p>Ingrese dos valores y la calculadora calculará el tercero.</p>

    <label for="distancia"><span>Distancia:</span>
    <input type="number" id="distancia" bind:value={distancia} placeholder="0" step="0.0001"/> </label>
    <label for="velocidad"><span>Velocidad:</span>
    <input type="number" id="velocidad" bind:value={velocidad} placeholder="0" step="0.0001"/> </label>
    <label for="tiempo"><span>Tiempo:</span>
    <input type="number" id="tiempo" bind:value={tiempo} placeholder="0" step="0.0001"/> </label>
  
    <button id="calcularButton" disabled={!bot} on:click={calcular}>Calcular</button>
<button on:click={() => {
    // Reiniciar las variables
    distancia = 0;
    velocidad = 0;
    tiempo = 0;
    bot = true;
    magnitud = "Ingresa nuevos datos";
    // Habilitar el botón de cálculo
    document.getElementById('calcularButton').removeAttribute('disabled');
}}>Reiniciar</button>
  
    {#if error}
      <p class="error">Ingrese al menos dos valores diferentes a 0 y uno en 0.</p>
    {:else}
      {#if magnitud === "tiempo"}
        <p>Tiempo: {tiempo} segundos</p>
      {:else if magnitud === "velocidad"}
        <p>Velocidad: {velocidad} metros por segundo</p>
      {:else if magnitud === "distancia"}
        <p>Distancia: {distancia} metros</p>
      {:else}
        <p>Reset.</p>
      {/if}
    {/if}
  </div>

<style>/* Estilo base para todos los inputs */
    /* Estilos generales */
body {
  font-family: sans-serif;
  margin: 20px;
}

/* Estilos para los inputs */
input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  width: 200px;
  margin-bottom: 10px;
}

/* Estilos para los botones */
button {
  padding: 10px 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: #000;
  color: #fff;
  cursor: pointer;
  margin-right: 10px;
}

/* Estilos específicos para el botón "Calcular" */
button[type="submit"] {
  background-color: #0073b7;
}

/* Estilos específicos para el botón "Reiniciar" */
button[type="reset"] {
  background-color: #ccc;
}

/* Estilos para los mensajes de error */
.error {
  color: red;
  font-weight: bold;
  margin-bottom: 10px;
}

span{
    margin-right: 1rem;
}

label {
    display: block;
}

</style>
