<script>
  let carrera = 0;
  let materias = 0;
  let aprobadas = 0;
  let reprobadas = 0;
  let restantes = 0;
  let semestresCursados = 0;
  let semestresRestantes = 0;

  let log = "";
  let msg1 = "";
  let msg2 = "";
  let msg3 = "";
  let msg4 = "";
  let cierre1 = false; 
  let cierre2 = false;
  let cierre3 = false;
  let cierre4 = false;
  let mostrarLabel2 = false;
  let mostrarLabel3 = false;
  let mostrarLabel4 = false;
  let mostrarLabel5 = false;
  let porcentaje = 0;

  function disableSelect(num) {
    switch (num) {
      case 1:
      num=0;
        if (carrera !== 0) {
          cantidadMaterias(carrera);
          cierre1 = true;
          mostrarLabel2 = true;
          msg1 = "";
        }else{
          msg1="Ingresa una carrera";
        }
        break;
      case 2:
      num=0;
        if (aprobadas >= 0 && aprobadas <= materias && aprobadas !== null) {
          cierre2 = true;
          mostrarLabel3 = true;
          restantes= materias - aprobadas;
          msg2="";
        }else{
          msg2="Ingresa un numero coherente XD";
        }
        //Se guardan aprobadas
        break;

      case 3:
      num=0;
        if (reprobadas >= 0 && reprobadas <= (materias - aprobadas) && reprobadas !== null) {
          cierre3 = true;
          mostrarLabel4 = true;
          msg3="";
        }else{
          msg3="Ingresa un numero coherente XD";
        }
        break;
      case 4:
      num=0;
        if (semestresCursados >= 0 && semestresCursados <= 12 && semestresCursados !== null) {
          cierre4 = true;
          mostrarLabel5 = true;
          msg4="";
          reconemdacion();
        }else{
          msg4="Ingresa un numero coherente XD";
        }
        break;
    
      default:
        break;
    }
  }

  function reconemdacion() {
    porcentaje = ((aprobadas * 100) / materias).toFixed(2);
    semestresRestantes = 12 - semestresCursados;



  }

  function cantidadMaterias(carrera) {
if (carrera === "Licenciatura en Administración Industrial" ){ materias = 61;}
if (carrera = "Ingeniería en Informática") {materias = 65;}
if (carrera = "Ingeniería en Transporte") {materias = 66; }
if (carrera = "Ingeniería Ferroviaria") {materias = 57; }
if (carrera = "Ingeniería Industrial") {materias = 73;}
if (carrera = "Licenciatura en Ciencias de la Informática"){ materias = 59;}
  }

</script>

<div><button style="float: right; background-color: black; color: white;" onclick="location.reload()">Reset</button>
  <h2>Semestrador                  </h2> 


  <label for="carrera"><span>¿Cuál es tu carrera? {carrera} {materias}</span>
  <select name="carrera" id="carrera" bind:value={carrera} disabled={cierre1}>
    <option>Licenciatura en Administración Industrial.</option>
    <option>Ingeniería en Informática.</option>
    <option>Ingeniería en Transporte.</option>
    <option>Ingeniería Ferroviaria.</option>
    <option>Ingeniería Industrial.</option>
    <option>Licenciatura en Ciencias de la Informática.</option>
  </select>
  <button on:click={() => disableSelect(1)}>OK</button> <sub>{msg1}</sub>
  </label>
  {#if mostrarLabel2}
  <label for="aprobadas" ><span>¿Cuantas materias has aprobado? {aprobadas} </span>
    <input type="number" id="aprobadas" bind:value={aprobadas} disabled={cierre2} min="0" max={materias} step="1"/>
    <button on:click={() => disableSelect(2)}>OK</button> <sub>{msg2}</sub>
  </label>
  {/if}
  
  {#if mostrarLabel3}
  <label for="reprobadas" ><span>¿Cuantas materias debes? {reprobadas}</span>
    <input type="number" id="reprobadas" bind:value={reprobadas} disabled={cierre3} min="0" max={materias - aprobadas} step="1"/>
    <button on:click={() => disableSelect(3)}>OK</button> <sub>{msg3}</sub>
  </label>
  {/if}

  {#if mostrarLabel4}
  <label for="semestres" ><span>¿Cuantos semestres has cursado? {semestresCursados}</span>
    <input type="number" id="semestres" bind:value={semestresCursados} disabled={cierre4} min="0" max=12 step="1"/>
    <button on:click={() => disableSelect(4)}>OK</button> <sub>{msg4}</sub>
  </label>
  {/if}
 
  {#if mostrarLabel5}
  <label for="parrafo" ><span>Recomendaciones{semestresCursados}</span> </label>
  {#if porcentaje >= 100}
  <em>Felicidades, terminaste la carrera de {carrera}</em>
  {:else}
  <em>Hasta el momento llevas un {porcentaje}% de tu carrera </em> 
  
  {#if reprobadas === 0}
  <em>No tienes ninguna materia reprobada, ¡algo de qué sentirse orgulloso!</em>
{:else if reprobadas >= 1 && reprobadas <= 3}
<em>Tienes {reprobadas} materia(s) reprobada(s). ¡No te desanimes, puedes mejorar! Recuerda que el desfase viene cuando tienes una materia reprobada de hace mas de 3 periodos.</em>
{:else}
<em>Tienes {reprobadas} materias reprobadas. Es importante que te enfoques en mejorar tu rendimiento académico ya que no te puedes inscribir con este numero de materias reprobadas. Recuerda que el desfase viene cuando tienes una materia reprobada de hace mas de 3 periodos.</em>
{/if} <!-- repro -->

{#if semestresRestantes === 0}
<em>Pero requieres hacer un dictamen para poder cursar los semestres necesarios para cursar tus {restantes} materias restantes, ya que has agotado los permitidos.</em>
{:else}
<em>Te restan {semestresRestantes} semestres para cursar tus {restantes} materias restantes, </em>
  
{/if}
<em>vamos a hacer un pequeño plan.</em>
{#if reprobadas >= 4}
<em>Deberás inscribirte a los ETS de las materias que debes para poder continuar 
  con tu carrera.</em>
{:else if reprobadas >= 1 && reprobadas <= 3}
<em>Deberás inscribirte con carga media o menor el siguiente semestre.</em>
{:else if reprobadas >= 1 && reprobadas <= 3}
<em>Podrás inscribirte con la carga que necesites.</em>
{/if}
  {/if}<!-- 100 -->
  {/if}
</div>


<style>
  ins{

  }
  body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  sub{
    color: #ff0000;
  }

  .container {
    background-color: #fff;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    width: 400px;
  }

  h1 {
    font-size: 24px;
    margin-bottom: 20px;
  }

  label {
    display: block;
    margin-bottom: 10px;
  }

  select,
  input[type="number"] {
    width: 100%;
    padding: 8px;
    font-size: 16px;
    border-radius: 4px;
    border: 1px solid #ccc;
    box-sizing: border-box;
    margin-top: 5px;
  }

  button {
    margin: 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    padding: 10px 20px;
    cursor: pointer;
    font-size: 16px;
  }

  button:hover {
    background-color: #0056b3;
  }

  span {
    font-weight: bold;
  }
</style>