# Malla--carrera-<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Malla Interactiva</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Malla de Carrera</h1>
  <div id="malla"></div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: sans-serif;
  padding: 20px;
}

.materia {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 5px;
  display: inline-block;
  cursor: pointer;
  border-radius: 6px;
}

.aprobada {
  text-decoration: line-through;
  background-color: #d4edda;
}

.bloqueada {
  background-color: #f8d7da;
}const materias = {
  "Matemática I": [],
  "Álgebra": [],
  "Física I": ["Matemática I"],
  "Programación I": [],
  "Estructuras de Datos": ["Programación I"],
  "Sistemas Operativos": ["Estructuras de Datos", "Física I"],
};

const estado = {}; // materias aprobadas
const mallaDiv = document.getElementById("malla");

function actualizarMalla() {
  mallaDiv.innerHTML = "";

  for (let materia in materias) {
    const bloqueada = materias[materia].some(req => !estado[req]);
    const div = document.createElement("div");
    div.className = "materia";
    if (estado[materia]) div.classList.add("aprobada");
    else if (bloqueada) div.classList.add("bloqueada");
    div.innerText = materia;
    div.onclick = () => {
      if (!bloqueada || estado[materia]) {
        estado[materia] = !estado[materia];
        actualizarMalla();
      }
    };
    mallaDiv.appendChild(div);
  }
}

actualizarMalla();

