<script>
  let numeroPregunta = 0;
  let preguntas = [
    "¿Tiene fiebre?",
    "¿Tiene dolor de cabeza?",
    "¿Tiene dolor de oído?",
    "¿Tiene dolor de garganta?",
    "¿Tiene tos?",
    "¿Tiene náuseas?",
    "¿Tiene dificultad para respirar?",
    "¿Tiene dolor en el pecho?",
    "¿Tiene vómitos?",
    "¿Tiene diarrea?",
    "¿Ha estado en contacto con algún enfermo?",
    "¿Tiene picazón en los ojos o estornudos?",
    "¿Ha viajado recientemente?",
    "¿Se siente constantemente cansado?"
  ];

  let respuestas = new Array(preguntas.length).fill(false);

  const enfermedades = {
    "Resfriado común": [0, 1, 2, 3, 4],
    "Gripe": [0, 1, 2, 3, 4, 6, 7, 12],
    "Infección de oído": [1, 2, 5, 6],
    "Dolor de garganta": [1, 2, 4, 6],
    "Bronquitis": [0, 3, 6, 7],
    "Neumonía": [0, 3, 6, 7, 12],
    "Gastroenteritis": [8, 9, 10],
    "Alergia": [1, 2, 4, 11],
    "Fatiga crónica": [12, 13]
  };

  let diagnostico = '';

  function responder(index, respuesta) {
    respuestas[index] = respuesta;
    numeroPregunta++;
    diagnosticar();
  }

  function diagnosticar() {
    let mejorCoincidencia = { enfermedad: '', coincidencias: 0 };
  
    for (const [enfermedad, criterio] of Object.entries(enfermedades)) {
        let coincidencias = 0;
        for (const criterioIndex of criterio) {
            if (respuestas[criterioIndex]) {
                coincidencias++;
            }
        }
      
        if (coincidencias > mejorCoincidencia.coincidencias) {
            mejorCoincidencia.enfermedad = enfermedad;
            mejorCoincidencia.coincidencias = coincidencias;
        }
    }

    if (mejorCoincidencia.coincidencias > 2) {
        diagnostico = mejorCoincidencia.enfermedad;
    } else {
        diagnostico = "No se pudo determinar la enfermedad";
    }
}
</script>



{#if numeroPregunta < preguntas.length}
  <div class="question-container">
    <p>{preguntas[numeroPregunta]}</p>
    <button on:click={() => responder(numeroPregunta, true)}>Sí</button>
    <button on:click={() => responder(numeroPregunta, false)}>No</button>
  </div>
{:else}
  <div>
    <h2>Diagnóstico</h2>
    <p>Basado en sus respuestas:</p>
    <p>{diagnostico}</p>
  </div>
{/if}

<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f7f7f7;
    color: #333;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .container {
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 400px;
  }

  .question-container {
    margin-bottom: 20px;
    text-align: center;
  }

  .question-container p {
    font-size: 40px;
    margin-bottom: 10px;
  }

  button {
    background-color: #4CAF50; /* Green */
    border: none;
    color: white;
    padding: 10px 24px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 30px;
    margin-right: 10px;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s;
  }

  button:hover {
    background-color: #6ffb73; /* Green */
  }

  button:focus {
    outline: none;
  }

  h2 {
    font-size: 30px;
    margin-bottom: 20px;
  }

  p {
    font-size: 20px;
    line-height: 1.5;
    margin: 0;
  }
</style>