---
layout: page
title: Generador de Fichas Hotspot MikroTik
permalink: "/voucher-gen/"
comments: false
---

Bienvenido al generador de usuarios para MikroTik Hotspot, una herramienta gratuita para crear códigos de acceso en tu Mikrotik.


✅ Generación masiva de usuarios y contraseñas aleatorias.  
✅ Opción de autenticación por PIN o usuario y contraseña.  
✅ Descarga de archivos .rsc para importar en MikroTik.  
✅ Exportación en PDF para impresión.  

<style>
    /* Estilos personalizados para el campo de texto tipo consola */
  #scripts-textarea.console-style {
    background-color: #2d2d2d !important; /* Fondo oscuro */
    color: #d4d4d4 !important;           /* Texto claro */
    font-family: "Courier New", Courier, monospace !important; /* Fuente de consola */
    border: 1px solid #444 !important;   /* Borde oscuro */
    padding: 10px !important;            /* Espaciado interno */
    border-radius: 4px !important;       /* Bordes redondeados */
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.3) !important; /* Sombra */
    white-space: pre !important;         /* Espacios y saltos de línea */
    overflow-x: auto !important;         /* Scroll horizontal */
    overflow-y: auto !important;         /* Scroll vertical */
    max-height: 300px !important;        /* Altura máxima */
    width: 100%; 
    height: 300px;
  }
  .console-style::selection {
    background-color: #3a7fc4; /* Color de selección */
    color: #ffffff; /* Texto seleccionado */
  }
</style>
## Generador Gratuito 🚀
<div class="container mt-5">
    <form id="config-form" class="card p-4 shadow border border-primary bg-light">
        <div class="mb-3">
            <label for="cantidad" class="form-label">Cantidad de fichas (máximo 500):</label>
            <input type="number" id="cantidad" class="form-control" min="1" max="500" required>
        </div>

        <div class="mb-3">
            <label for="prefijo" class="form-label">Prefijo/Lote(Opcional):</label>
            <input type="text" id="prefijo" class="form-control" required>
        </div>

        <div class="mb-3">
            <label for="tiempo" class="form-label">Tiempo límite:</label>
            <div class="row gx-2">
                <div class="col">
                    <input type="number" id="dias" class="form-control" min="0" placeholder="Días">
                </div>
                <div class="col">
                    <input type="number" id="horas" class="form-control" min="0" max="23" placeholder="Horas">
                </div>
                <div class="col">
                    <input type="number" id="minutos" class="form-control" min="0" max="59" placeholder="Minutos">
                </div>
            </div>
        </div>

        <div class="mb-3">
            <label for="logueo-pin" class="form-label">Método de autenticación:</label>
            <select id="logueo-pin" class="form-select">
                <option value="si">Logueo por PIN</option>
                <option value="no">User & Password</option>
            </select>
        </div>

        <div class="mb-3">
            <label for="longitud-pin" class="form-label">Longitud de la contraseña:</label>
            <select id="longitud-pin" class="form-select">
                <option value="4" selected>4</option>
                <option value="5">5</option>
                <option value="6">6</option>
            </select>
        </div>

        <div class="mb-3">
            <label for="profile" class="form-label">User Profile:</label>
            <input type="text" id="profile" class="form-control" value="default" required>
        </div>

        <div class="mb-3">
            <label for="servidor" class="form-label">Server Hotspot:</label>
            <input type="text" id="servidor" class="form-control" value="all" required>
        </div>

        <button type="button" class="btn btn-primary w-100 mb-2" onclick="if (validarFormulario()) generar()">Generar Script y PDF</button>
    </form>

    <div class="card mt-4 p-4 shadow">
        <div class="d-flex justify-content-between">
            <button class="btn btn-success" onclick="copiarTexto()">Copiar al Portapapeles</button>
            <button class="btn btn-warning" onclick="descargarRSC()">Descargar Script (.rsc)</button>
            <button class="btn btn-info" onclick="generarPDF()">Descargar PDF</button>
        </div>
        <textarea id="scripts-textarea" class="form-control mb-3 console-style" readonly></textarea>
    </div>
</div>


<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.4.0/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.25/jspdf.plugin.autotable.min.js"></script>

<script>
function convertirTiempoASegundos(dias, horas, minutos) {
    if (
        isNaN(dias) || isNaN(horas) || isNaN(minutos) ||
        dias < 0 || horas < 0 || horas > 23 || minutos < 0 || minutos > 59
    ) {
        alert("Por favor, ingresa valores válidos para días, horas (máx. 23) y minutos (máx. 59).");
        return null;
    }
    return (dias * 86400) + (horas * 3600) + (minutos * 60);
}

function convertirSegundosAFormato(segundos) {
    const hh = String(Math.floor(segundos / 3600)).padStart(2, "0");
    const mm = String(Math.floor((segundos % 3600) / 60)).padStart(2, "0");
    const ss = String(segundos % 60).padStart(2, "0");
    return `${hh}:${mm}:${ss}`;
}

// Validación de formulario
function validarFormulario() {
    const cantidad = document.getElementById("cantidad").value;
    const dias = document.getElementById("dias").value;
    const horas = document.getElementById("horas").value;
    const minutos = document.getElementById("minutos").value;

    // Validar cantidad de fichas
    if (!cantidad || cantidad < 1 || cantidad > 500) {
        alert("Por favor, ingresa una cantidad válida de fichas (entre 1 y 500).");
        return false;
    }

    // Validar tiempo límite
    if (!dias && !horas && !minutos) {
        alert("Por favor, establece al menos un valor en Días, Horas o Minutos.");
        return false;
    }

    return true; // Todo está correcto
}

function generar() {
    const cantidad = parseInt(document.getElementById("cantidad").value);
    const prefijo = document.getElementById("prefijo").value;
    const dias = parseInt(document.getElementById("dias").value) || 0;
    const horas = parseInt(document.getElementById("horas").value) || 0;
    const minutos = parseInt(document.getElementById("minutos").value) || 0;
    const tiempoEnSegundos = convertirTiempoASegundos(dias, horas, minutos);
    if (tiempoEnSegundos === null) return; // Detener si el tiempo no es válido

    const tiempoFormato = convertirSegundosAFormato(tiempoEnSegundos);
    const logueoPorPIN = document.getElementById("logueo-pin").value;
    const longitudPin = parseInt(document.getElementById("longitud-pin").value);
    const profile = document.getElementById("profile").value.trim(); // Quitar espacios en blanco
    const servidor = document.getElementById("servidor").value.trim(); // Quitar espacios en blanco

    let scripts = [`/ip hotspot user`];
    let usuarios = [];

    for (let i = 0; i < cantidad; i++) {
        let usuario, password;
        let script = `add name=${prefijo}${generarContraseñaAleatoria(longitudPin)}`;

        if (logueoPorPIN === "no") {
            password = generarContraseñaAleatoria(longitudPin);
            script += ` password=${password}`;
        }

        script += ` limit-uptime=${tiempoFormato} disabled=no`;

        // Agregar profile si tiene valor
        if (profile) {
            script += ` profile="${profile}"`;
        }

        // Agregar server_hotspot si tiene valor
        if (servidor) {
            script += ` server_hotspot="${servidor}"`;
        }

        scripts.push(script);

        usuarios.push({
            name: `${prefijo}${generarContraseñaAleatoria(longitudPin)}`,
            password: logueoPorPIN === "si" ? "(PIN)" : password,
        });
    }

    // Mostrar el script generado en el cuadro de texto
    document.getElementById("scripts-textarea").value = scripts.join("\n");
    window.generados = usuarios;
    window.scriptContent = scripts.join("\n");
}

function generarContraseñaAleatoria(longitud) {
    const caracteres = "abcdefghijklmnopqrstuvwxyz0123456789";
    let resultado = "";
    for (let i = 0; i < longitud; i++) {
        resultado += caracteres.charAt(Math.floor(Math.random() * caracteres.length));
    }
    return resultado;
}

function copiarTexto() {
    const textarea = document.getElementById("scripts-textarea");
    textarea.select();
    document.execCommand("copy");
    alert("¡Texto copiado al portapapeles!");
}

function descargarRSC() {
    const blob = new Blob([window.scriptContent || ""], { type: "text/plain" });
    const enlace = document.createElement("a");
    enlace.href = URL.createObjectURL(blob);
    enlace.download = "script-hotspot.rsc";
    enlace.click();
    URL.revokeObjectURL(enlace.href);
}
function generarPDF() {
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    const generados = window.generados || [];
    const logueoPorPIN = document.getElementById("logueo-pin").value;

    // Configuración de la hoja y tabla
    const columnasPorHoja = 4;
    const filasPorHoja = 10;
    const anchoColumna = (doc.internal.pageSize.width - 20) / columnasPorHoja;
    const altoFila = 20;
    const margenSuperior = 20;
    const margenIzquierdo = 10;
    const startY = margenSuperior;

    // Encabezado estilizado
    doc.setFont("Helvetica", "bold");
    doc.setFontSize(18);
    doc.setTextColor(0, 0, 0);
    doc.text("Mikrotik Voucher Generator", doc.internal.pageSize.width / 2, 15, { align: "center" });

    let x = margenIzquierdo;
    let y = startY;
    let currentPage = 1;

    for (let i = 0; i < generados.length; i++) {
        const user = generados[i];

        doc.setDrawColor(0, 0, 0);
        doc.rect(x, y, anchoColumna, altoFila);

        if (logueoPorPIN === "si") {
            doc.setFont("Helvetica", "bold");
            doc.setFontSize(10);
            doc.setTextColor(255, 0, 0); // Rojo para "PIN:"
            doc.text("PIN:", x + 2, y + 6);

            doc.setFont("Helvetica", "normal");
            doc.setTextColor(0, 0, 255); // Azul para el código de usuario
            doc.text(user.name, x + 14, y + 6);
        } else {
            doc.setFont("Helvetica", "bold");
            doc.setFontSize(10);
            doc.setTextColor(255, 0, 0); // Rojo para "User:"
            doc.text("User:", x + 2, y + 6);

            doc.setFont("Helvetica", "normal");
            doc.setTextColor(0, 0, 255); // Azul para el nombre de usuario
            doc.text(user.name, x + 16, y + 6);

            doc.setFont("Helvetica", "bold");
            doc.setTextColor(255, 0, 0); // Rojo para "Password:"
            doc.text("Password:", x + 2, y + 12);

            doc.setFont("Helvetica", "normal");
            doc.setTextColor(0, 0, 255); // Azul para la contraseña
            doc.text(user.password, x + 26, y + 12);
        }

        x += anchoColumna;

        if ((i + 1) % columnasPorHoja === 0) {
            x = margenIzquierdo;
            y += altoFila;
        }

        if ((i + 1) % (columnasPorHoja * filasPorHoja) === 0) {
            doc.addPage();
            currentPage++;
            x = margenIzquierdo;
            y = startY;

            doc.setFont("Helvetica", "bold");
            doc.setFontSize(18);
            doc.setTextColor(0, 0, 0);
            doc.text("Mikrotik Voucher Generator", doc.internal.pageSize.width / 2, 15, { align: "center" });
        }
    }

    // Pie de página
    for (let page = 1; page <= currentPage; page++) {
        doc.setPage(page);
        doc.setFont("Helvetica", "normal");
        doc.setFontSize(10);
        doc.setTextColor(0, 0, 0);
        doc.text(
            `Arturo Vargas https://kuatroestrellas.github.io/blog/voucher-gen/`,
            doc.internal.pageSize.width / 2,
            doc.internal.pageSize.height - 10,
            { align: "center" }
        );
    }

    doc.save("Mikrotik_Vouchers.pdf");
}

</script>