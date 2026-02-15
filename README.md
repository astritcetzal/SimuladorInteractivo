# SimuladorInteractivo
### Astrit Airan Cetzal Cetal
### Tecnológico de software
### 17/02/2026
### Profesor: Jorge Javier Pedrozo Romero

# Introducción 
Este es un simuldor interactivo web diseñado para comparar dos algoritmos de asignacion de memoria, best fit y worst fit. Este simulador ha sido desarrollado para fines educativos, con el objetivo de entnder visualizar el comportamiento de los algoritmos.

# Instrucciones 

1. Al usuario se le presenta primero la "Configuarcion de memoria" donde puede asinar un valor a la memoria, y la cantidad de bloques que quiere que este tenga. 
2. Despues debe hacer click al boton "Generar Bloques Editables" aqui ya se le asigna el tamaño de los bloques pero si el usuario gusta puede modificarlo. 
3. Le da a iniciar simulacion 
4. Debe ponerle un id a cada proceso al igual que un tamaño 5. Darle click a "Asignar Proceso" donde podrá observar que la estructura de la memoria cambia, porque al asignar a un bloque un proceso entrante el simulador divide tal bloqle y una parte es ocupada por el proceso y el otro se convierte en un nuevo bloque disponible. 
6. En el registro del sistema puede observar que tanta memoria se ha utilizado, la fragmentacion, la cantidad de bloques y las fallas 


# Explicación de los algortimos
Best Fit:  este algoritmo se caracteriza por asignarle al proceso entrante el bloque libre mas pequeño lo suficientemente grande para el proceso; este algoritmo debe recorrer toda la memoria hasta encontrar ese bloque. 

Worst Fit: es un algorirmo de asignacion de memoria el cual se encarga de asignar el bloque de memoria mas grande a cada proceso que entre.

# Reflexión

Ha sido una actividad bastante productiva, para ser sincera no soy muy buena con java script asi que opté por usar IA, pero igual para ahorrar tiempo. Me gustó esta actividad porque me ayudo a entender la diferencia entre dos algoritmos de asignación de memoria. 

# Referencias

[1] J. Carretero Pérez, F. García Carballeira, P. de Miguel Anasagasti y F. Pérez Costoya, Sistemas Operativos: Una visión aplicada. Madrid, España: McGraw-Hill Interamericana, 2001.

[2] A. M. McHoes e I. M. Flynn, Understanding Operating Systems, 6.ª ed. Boston, MA, EE. UU.: Course Technology Cengage Learning, 2011.

# Cláusula de uso de IA

Declaro que utilicé herramientas de Inteligencia Artificial de manera asistida. A  

## Acontinuación detallo cada uso: 

## Usuario: Astrit Airan Cetzal Cetzal

## IA: Gemini 3

##Proposito:
Como no se mucho de java script darle las instrucciones a la IA me ha resultado más facil y eficiente. 

## Promt:
Actua como un desarrollador de software profesional experto es java script y sistemas operativos. Necesito que crees un simulador interactivo web (en un solo archivo) para comparar dos algoritmos de gestión de memoria: best fit y worst fit.

se necesita:
1. Debe permitir configurar un tamaño total de memoria y dividirlo en bloques iniciales. El usuario debe poder agregar procesos con ID y tamaño especifico.
2. Implementa bien la logica de BEST FIT (el bloque más peque{o que quepa}) y WORST FIT (El bloque más grnade disponible).
3. Usa una esteica moderna los bloques de memoria deben representarse con rectangulos y cambiar de color cuando esten "libres" o "ocupados"
4. Muestra para ambos algoritmos el porcentaje de utilización, la frgamentacion externa, el bloque libre mas grande y el numero de fallas.
5. incluye una consola de logs interna, animaciones al asignar procesos y una sección final de "comparativa de ganadores" que desmuestre cual algoritmo fué más eficiente 

Que el usuario pueda asignarle un tamaño especifico a la memoria y la cantidad de bloques que deben tener, recuerda que cada bloque debe tener un tamaño diferente, no todos pueden tener la misma cantidad de memoria para todos los bloques antes de inicializar la asignacion

porfa para que sea mas fácil utiliza style dentro del head para que me sea más facil cambiarle los colores  

quiero ver los resultados, quien tuvo mas fragmentación 

Claro que sí. Como experto en desarrollo y sistemas operativos, he preparado una solución completa en un solo archivo HTML.

## Archivos adjentos: N/A

## Respuesta:

He diseñado este simulador utilizando Particionamiento Fijo (Fixed Partitioning), que es la forma más clara de visualizar y comparar "Best Fit" vs "Worst Fit". En este modelo, el sistema operativo divide la memoria en bloques de tamaños específicos (que tú definirás) y los procesos deben ocupar un bloque entero (generando fragmentación interna si el proceso es menor que el bloque).

Aquí tienes el código completo. Puedes copiarlo, guardarlo como .html y abrirlo en tu navegador.

''''

HTML
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador de Gestión de Memoria: Best Fit vs Worst Fit</title>
    <style>
        /* =========================================
           CONFIGURACIÓN DE COLORES Y ESTILOS
           ========================================= */
        :root {
            --bg-color: #f0f2f5;
            --card-bg: #ffffff;
            --text-color: #333333;
            --accent-color: #2563eb; /* Azul principal */
            --success-color: #10b981; /* Verde (Best Fit) */
            --danger-color: #ef4444;  /* Rojo (Worst Fit / Fallos) */
            --block-free: #e2e8f0;    /* Gris claro */
            --block-occupied: #3b82f6; /* Azul proceso */
            --border-radius: 8px;
            --font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: var(--font-family);
            background-color: var(--bg-color);
            color: var(--text-color);
            padding: 20px;
            line-height: 1.6;
        }

        h1, h2, h3 { margin-bottom: 15px; font-weight: 700; }
        h1 { text-align: center; color: var(--accent-color); }

        /* Contenedores */
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: var(--border-radius);
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        /* Inputs y Botones */
        .input-group {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
            align-items: flex-end;
            flex-wrap: wrap;
        }

        .form-control {
            display: flex;
            flex-direction: column;
        }

        label { font-size: 0.9em; font-weight: 600; margin-bottom: 5px; }

        input {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1em;
        }

        button {
            padding: 10px 20px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: background 0.3s;
        }

        button:hover { background-color: #1d4ed8; }
        button.secondary { background-color: #64748b; }
        button:disabled { background-color: #cbd5e1; cursor: not-allowed; }

        /* Configuración de Bloques */
        #blocks-config-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 15px;
        }

        /* Simulación Visual */
        .simulation-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        @media (max-width: 768px) {
            .simulation-grid { grid-template-columns: 1fr; }
        }

        .algo-column {
            background: #fafafa;
            padding: 15px;
            border-radius: var(--border-radius);
            border: 1px solid #e5e7eb;
        }

        .algo-header {
            text-align: center;
            padding-bottom: 10px;
            border-bottom: 2px solid #eee;
            margin-bottom: 10px;
        }

        /* Visualización de la Memoria */
        .memory-container {
            display: flex;
            flex-direction: column;
            gap: 8px;
            min-height: 200px;
        }

        .memory-block {
            position: relative;
            height: 50px; /* Altura fija para visualización limpia */
            background-color: var(--block-free);
            border: 1px solid #cbd5e1;
            border-radius: 4px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            transition: all 0.5s ease;
            overflow: hidden;
        }

        .memory-block.occupied {
            background-color: #dbeafe; /* Fondo ligero para ocupado */
            border-color: var(--block-occupied);
        }

        /* Barra de progreso interna (Proceso) */
        .process-bar {
            height: 80%;
            background-color: var(--block-occupied);
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 0.8em;
            white-space: nowrap;
            transition: width 0.5s ease;
            width: 0%; /* Inicia en 0 para animación */
        }

        .block-info {
            position: absolute;
            right: 10px;
            font-size: 0.8em;
            color: #666;
        }

        /* Estadísticas */
        .stats-panel {
            margin-top: 15px;
            font-size: 0.9em;
            background: white;
            padding: 10px;
            border-radius: 4px;
        }
        .stat-row { display: flex; justify-content: space-between; margin-bottom: 5px; }
        .stat-val { font-weight: bold; }

        /* Consola */
        #console-log {
            background: #1e293b;
            color: #10b981;
            font-family: 'Courier New', Courier, monospace;
            padding: 15px;
            height: 150px;
            overflow-y: auto;
            border-radius: var(--border-radius);
            font-size: 0.85em;
        }
        .log-entry { margin-bottom: 5px; border-bottom: 1px solid #334155; padding-bottom: 2px; }
        .log-error { color: #ef4444; }
        .log-bf { color: #60a5fa; } /* Azul claro */
        .log-wf { color: #f472b6; } /* Rosa */

        /* Ganador */
        .winner-section {
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 100%);
            border: 2px solid var(--accent-color);
            margin-top: 20px;
            display: none; /* Oculto al inicio */
        }
        .winner-badge {
            font-size: 1.5em;
            font-weight: bold;
            color: var(--accent-color);
        }
        
        /* Utilidades */
        .hidden { display: none !important; }
        .fragmentation-visual {
            background: repeating-linear-gradient(
                45deg,
                rgba(0,0,0,0.05),
                rgba(0,0,0,0.05) 10px,
                rgba(0,0,0,0.1) 10px,
                rgba(0,0,0,0.1) 20px
            );
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Simulador de Memoria: Best Fit vs Worst Fit</h1>

    <div id="step-1" class="card">
        <h3>1. Configuración de Memoria</h3>
        <p>Define el tamaño total de la memoria y en cuántos bloques (particiones) quieres dividirla.</p>
        <div class="input-group">
            <div class="form-control">
                <label>Tamaño Total Memoria (KB)</label>
                <input type="number" id="total-mem" value="1000" min="100">
            </div>
            <div class="form-control">
                <label>Cantidad de Bloques</label>
                <input type="number" id="num-blocks" value="5" min="1" max="20">
            </div>
            <button onclick="generateBlockInputs()">Generar Bloques</button>
        </div>
        
        <div id="blocks-config-wrapper" class="hidden">
            <h4>Define el tamaño de cada bloque:</h4>
            <p style="font-size: 0.8em; color: #666;">La suma no debe superar el total. Si sobra espacio, se marcará como "Sistema".</p>
            <div id="blocks-config-container"></div>
            <div style="margin-top: 15px;">
                <span id="current-sum-display">Suma actual: 0 KB</span>
                <button onclick="initializeSimulation()" style="margin-left: 20px;">Iniciar Simulación</button>
            </div>
        </div>
    </div>

    <div id="step-2" class="card hidden">
        <div class="input-group" style="justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px;">
            <h3>Panel de Control</h3>
            <button class="secondary" onclick="resetSimulation()">Reiniciar Todo</button>
        </div>

        <div class="input-group">
            <div class="form-control">
                <label>ID Proceso</label>
                <input type="text" id="proc-id" placeholder="ej. P1">
            </div>
            <div class="form-control">
                <label>Tamaño Proceso (KB)</label>
                <input type="number" id="proc-size" placeholder="ej. 150">
            </div>
            <button onclick="addProcess()">Asignar Proceso</button>
        </div>

        <div class="simulation-grid">
            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--success-color)">Best Fit</h2>
                    <p>Busca el bloque más pequeño que sea suficiente.</p>
                </div>
                <div id="bf-container" class="memory-container"></div>
                
                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="bf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Libre):</span> <span id="bf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="bf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas de Asignación:</span> <span id="bf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>

            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--danger-color)">Worst Fit</h2>
                    <p>Busca el bloque más grande disponible.</p>
                </div>
                <div id="wf-container" class="memory-container"></div>

                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="wf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Libre):</span> <span id="wf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="wf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas de Asignación:</span> <span id="wf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>
        </div>

        <div id="winner-section" class="winner-section">
            <h3>🏆 Comparativa Final</h3>
            <p id="winner-text" class="winner-badge"></p>
            <p id="winner-reason" style="margin-top: 10px;"></p>
        </div>
    </div>

    <div class="card">
        <h3>System Logs</h3>
        <div id="console-log"></div>
    </div>
</div>

<script>
    /* =========================================
       LÓGICA DEL SIMULADOR
       ========================================= */

    // Estado global
    let memoryTotal = 0;
    let initialBlocksConfig = []; // {id, size}
    
    // Estado de las simulaciones
    let bfState = { blocks: [], fails: 0, processes: [] };
    let wfState = { blocks: [], fails: 0, processes: [] };
    
    let processCounter = 1;

    // Utilidad: Logger
    function log(msg, type = 'info') {
        const consoleDiv = document.getElementById('console-log');
        const entry = document.createElement('div');
        entry.classList.add('log-entry');
        
        const timestamp = new Date().toLocaleTimeString();
        let prefix = `[${timestamp}] `;
        
        if (type === 'error') {
            entry.classList.add('log-error');
            prefix += '❌ ';
        } else if (type === 'bf') {
            entry.classList.add('log-bf');
            prefix += '🟢 [BestFit] ';
        } else if (type === 'wf') {
            entry.classList.add('log-wf');
            prefix += '🔴 [WorstFit] ';
        } else {
            prefix += 'ℹ️ ';
        }

        entry.innerText = prefix + msg;
        consoleDiv.prepend(entry);
    }

    // PASO 1: Generar inputs para bloques
    function generateBlockInputs() {
        memoryTotal = parseInt(document.getElementById('total-mem').value);
        const count = parseInt(document.getElementById('num-blocks').value);
        const container = document.getElementById('blocks-config-container');
        
        if (!memoryTotal || !count) return alert("Por favor ingresa valores válidos.");
        
        container.innerHTML = '';
        const suggestedSize = Math.floor(memoryTotal / count);

        for (let i = 0; i < count; i++) {
            const div = document.createElement('div');
            div.className = 'form-control';
            // Variación aleatoria ligera para sugerir tamaños diferentes, pero editable
            const randomVar = Math.floor(Math.random() * 20) - 10; 
            div.innerHTML = `
                <label>Bloque ${i + 1} (KB)</label>
                <input type="number" class="block-input" data-index="${i}" value="${suggestedSize + randomVar}" onchange="updateSum()">
            `;
            container.appendChild(div);
        }

        document.getElementById('blocks-config-wrapper').classList.remove('hidden');
        updateSum();
    }

    function updateSum() {
        const inputs = document.querySelectorAll('.block-input');
        let sum = 0;
        inputs.forEach(inp => sum += parseInt(inp.value || 0));
        const display = document.getElementById('current-sum-display');
        display.innerText = `Suma actual: ${sum} KB / Total: ${memoryTotal} KB`;
        
        if(sum > memoryTotal) display.style.color = 'red';
        else display.style.color = 'green';
    }

    // PASO 2: Inicializar
    function initializeSimulation() {
        const inputs = document.querySelectorAll('.block-input');
        let sum = 0;
        initialBlocksConfig = [];

        // Validar y construir configuración
        for (let i = 0; i < inputs.length; i++) {
            const size = parseInt(inputs[i].value);
            if (size <= 0) return alert("Los tamaños de bloque deben ser positivos.");
            sum += size;
            initialBlocksConfig.push({
                id: i,
                size: size,
                occupied: false,
                processId: null,
                processSize: 0
            });
        }

        if (sum > memoryTotal) return alert(`La suma de bloques (${sum}) excede la memoria total (${memoryTotal}).`);

        // Copia profunda para estados independientes
        bfState.blocks = JSON.parse(JSON.stringify(initialBlocksConfig));
        wfState.blocks = JSON.parse(JSON.stringify(initialBlocksConfig));
        bfState.fails = 0;
        wfState.fails = 0;
        
        // UI Switch
        document.getElementById('step-1').classList.add('hidden');
        document.getElementById('step-2').classList.remove('hidden');
        
        log("Simulación inicializada con memoria particionada (Fixed Partitioning).");
        renderAll();
    }

    function resetSimulation() {
        location.reload();
    }

    // LÓGICA CORE: Asignar Proceso
    function addProcess() {
        const pIdInput = document.getElementById('proc-id');
        const pSizeInput = document.getElementById('proc-size');
        
        let pId = pIdInput.value || `P${processCounter}`;
        let pSize = parseInt(pSizeInput.value);

        if (!pSize || pSize <= 0) return alert("Tamaño de proceso inválido");

        log(`Intentando asignar Proceso ${pId} (${pSize} KB)...`);

        // 1. Ejecutar Best Fit
        runBestFit(pId, pSize);

        // 2. Ejecutar Worst Fit
        runWorstFit(pId, pSize);

        // 3. Actualizar UI
        processCounter++;
        pIdInput.value = `P${processCounter}`;
        pSizeInput.value = '';
        
        renderAll();
        checkWinner();
    }

    function runBestFit(id, size) {
        let bestIndex = -1;
        let minFragmentation = Infinity;

        // Lógica Best Fit: Buscar el bloque libre donde (bloque.size - proceso.size) sea MÍNIMO
        for (let i = 0; i < bfState.blocks.length; i++) {
            const block = bfState.blocks[i];
            if (!block.occupied && block.size >= size) {
                const diff = block.size - size;
                if (diff < minFragmentation) {
                    minFragmentation = diff;
                    bestIndex = i;
                }
            }
        }

        if (bestIndex !== -1) {
            // Asignar
            bfState.blocks[bestIndex].occupied = true;
            bfState.blocks[bestIndex].processId = id;
            bfState.blocks[bestIndex].processSize = size;
            log(`Asignado ${id} en Bloque ${bestIndex + 1} (Frag. Interna: ${minFragmentation} KB)`, 'bf');
        } else {
            bfState.fails++;
            log(`Fallo al asignar ${id}. No hay bloque adecuado.`, 'bf');
        }
    }

    function runWorstFit(id, size) {
        let worstIndex = -1;
        let maxFragmentation = -1;

        // Lógica Worst Fit: Buscar el bloque libre donde (bloque.size - proceso.size) sea MÁXIMO
        for (let i = 0; i < wfState.blocks.length; i++) {
            const block = wfState.blocks[i];
            if (!block.occupied && block.size >= size) {
                const diff = block.size - size;
                if (diff > maxFragmentation) {
                    maxFragmentation = diff;
                    worstIndex = i;
                }
            }
        }

        if (worstIndex !== -1) {
            // Asignar
            wfState.blocks[worstIndex].occupied = true;
            wfState.blocks[worstIndex].processId = id;
            wfState.blocks[worstIndex].processSize = size;
            log(`Asignado ${id} en Bloque ${worstIndex + 1} (Frag. Interna: ${maxFragmentation} KB)`, 'wf');
        } else {
            wfState.fails++;
            log(`Fallo al asignar ${id}. No hay bloque adecuado.`, 'wf');
        }
    }

    /* =========================================
       RENDERIZADO Y MÉTRICAS
       ========================================= */

    function renderAll() {
        renderContainer('bf-container', bfState.blocks);
        renderContainer('wf-container', wfState.blocks);
        
        updateStats(bfState, 'bf');
        updateStats(wfState, 'wf');
    }

    function renderContainer(containerId, blocks) {
        const container = document.getElementById(containerId);
        container.innerHTML = '';

        blocks.forEach((block, index) => {
            const div = document.createElement('div');
            div.className = `memory-block ${block.occupied ? 'occupied' : ''}`;
            
            // Cálculo de anchos para visualización
            let barWidth = 0;
            let internalFrag = 0;
            
            if (block.occupied) {
                // Porcentaje que ocupa el proceso dentro del bloque
                const pct = (block.processSize / block.size) * 100;
                barWidth = pct;
                internalFrag = block.size - block.processSize;
            }

            const content = block.occupied 
                ? `<div class="process-bar" style="width: ${barWidth}%">${block.processId} (${block.processSize}KB)</div>` 
                : `<span style="color: #999; font-style: italic; font-size: 0.8em;">Libre</span>`;

            div.innerHTML = `
                ${content}
                <div class="block-info">
                    <strong>B${index+1}</strong>: ${block.size}KB
                    ${block.occupied ? `<br><small style="color:red">F.Int: ${internalFrag}KB</small>` : ''}
                </div>
            `;
            container.appendChild(div);
        });
    }

    function updateStats(state, prefix) {
        // Métricas
        // 1. Utilización: Suma de tamaños de procesos / Total Memoria Sistema
        let totalUsedByProcess = 0;
        let totalFree = 0; // Fragmentación externa (suma de bloques libres)
        let maxFree = 0;

        state.blocks.forEach(b => {
            if (b.occupied) {
                totalUsedByProcess += b.processSize;
            } else {
                totalFree += b.size;
                if (b.size > maxFree) maxFree = b.size;
            }
        });

        const utilization = ((totalUsedByProcess / memoryTotal) * 100).toFixed(1);

        document.getElementById(`${prefix}-util`).innerText = `${utilization}%`;
        document.getElementById(`${prefix}-frag`).innerText = `${totalFree} KB`;
        document.getElementById(`${prefix}-max-free`).innerText = `${maxFree} KB`;
        document.getElementById(`${prefix}-fails`).innerText = state.fails;
    }

    function checkWinner() {
        const div = document.getElementById('winner-section');
        const badge = document.getElementById('winner-text');
        const reason = document.getElementById('winner-reason');
        
        div.style.display = 'block';

        // Criterio 1: Menos fallos
        if (bfState.fails < wfState.fails) {
            badge.innerText = "Ganador: BEST FIT";
            reason.innerText = `Best Fit ha tenido menos fallos de asignación (${bfState.fails} vs ${wfState.fails}). Aprovecha mejor los espacios ajustados.`;
            div.style.borderColor = "var(--success-color)";
        } else if (wfState.fails < bfState.fails) {
            badge.innerText = "Ganador: WORST FIT";
            reason.innerText = `Worst Fit ha tenido menos fallos (${wfState.fails} vs ${bfState.fails}). Al dejar huecos grandes, permitió entrar procesos futuros.`;
            div.style.borderColor = "var(--danger-color)";
        } else {
            // Empate en fallos, mirar fragmentación externa (más memoria libre disponible es mejor para el futuro?)
            // O mirar utilización (más utilización es mejor)
            
            // Calcular utilizaciones reales
            const bfUtil = parseFloat(document.getElementById('bf-util').innerText);
            const wfUtil = parseFloat(document.getElementById('wf-util').innerText);

            if (bfUtil > wfUtil) {
                badge.innerText = "Ganador Técnico: BEST FIT";
                reason.innerText = "Empate en fallos, pero Best Fit tiene mayor porcentaje de utilización de memoria.";
            } else if (wfUtil > bfUtil) {
                badge.innerText = "Ganador Técnico: WORST FIT";
                reason.innerText = "Empate en fallos, pero Worst Fit tiene mayor porcentaje de utilización de memoria.";
            } else {
                badge.innerText = "EMPATE";
                reason.innerText = "Ambos algoritmos se comportaron igual con esta carga de trabajo.";
                div.style.borderColor = "#999";
            }
        }
    }
</script>

</body>
</html>



''''

Características Clave de la Solución:
Arquitectura Visual (Best Fit vs Worst Fit):

Best Fit (Lado Izquierdo - Verde): Busca el bloque libre donde la "Fragmentación Interna" (el espacio sobrante) sea mínima.

Worst Fit (Lado Derecho - Rojo): Busca el bloque libre más grande, maximizando el espacio sobrante (con la teoría de que el sobrante sea útil para otro proceso, aunque en particionamiento estático esto suele ser contraproducente y solo genera más desperdicio interno).

Lógica de Memoria:

Implementé Particionamiento Fijo (Fixed Partitioning). Tú defines los "contenedores" al inicio (ej. Bloque de 100KB, Bloque de 500KB).

Si asignas un proceso de 80KB al bloque de 100KB, verás visualmente una barra azul (el proceso) y un espacio gris/blanco dentro del mismo bloque (la fragmentación interna).

Métricas Calculadas en Tiempo Real:

Utilización: Qué porcentaje de la RAM total está siendo usada realmente por datos de procesos.

Fragmentación Externa: Suma total de los bloques que están completamente vacíos.

Fragmentación Interna: Se muestra visualmente dentro de cada bloque y numéricamente en rojo ("F.Int").

Fallas: Contador de procesos que no pudieron entrar en ningún bloque.

Comparativa Final:

Abajo del todo aparecerá una sección dinámica que determina el ganador basándose principalmente en quién tuvo menos fallos de asignación (el objetivo principal de un OS es no rechazar procesos).

Para usarlo, simplemente guarda el código como un archivo .html (ej: simulador_memoria.html) y ábrelo en Chrome, Firefox o Edge. ¡Espero que te sirva para tus pruebas!

----

## Usuario: Astrit Airan Cetzal Cetzal

## IA: Gemini 3

## Proposito: mejorar el codigo que me proporcionó primero

## Promt:
Que el usuario pueda asignarle un tamaño especifico a la memoria y la cantidad de bloques que deben tener, recuerda que cada bloque debe tener un tamaño diferente (pero NO EL usuario debe asignar el tamaño de los bloques! porque seria más tardado ), no todos pueden tener la misma cantidad de memoria para todos los bloques antes de inicializar la asignacion

porfa para que sea mas fácil utiliza style dentro del head para que me sea más facil cambiarle los colores  

quiero ver los resultados, quien tuvo mas fragmentación , toma comi refeencia para la ejecucion el 2do codigo



-----


no podrias hacer que el usuario ingrese los valores que quiera y que luego cuando preciones un boton estos vayan poniendose y actualizando

modifica el siguiente código:

'''' 

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador de Gestión de Memoria: Best Fit vs Worst Fit</title>
    <style>
        /* =========================================
           CONFIGURACIÓN DE COLORES Y ESTILOS
           ========================================= */
        :root {
            --bg-color: #dba2f5c9;
            --card-bg: #aeece9;
            --text-color: #333333;
            --accent-color: #1d84b4; /* Azul principal */
            --success-color: #10b981; /* Verde (Best Fit) */
            --danger-color: #ef4444;  /* Rojo (Worst Fit / Fallos) */
            --block-free: #9dddb8;    /* Gris claro */
            --block-occupied: #3bf6d7; /* Azul proceso */
            --border-radius: 8px;
            --font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: var(--font-family);
            background-image: linear-gradient(to left, #ace5fffb, #79a2fc);
            color: var(--text-color);
            padding: 20px;
            line-height: 1.6;
        }

        h1, h2, h3 { margin-bottom: 15px; font-weight: 700; }
        h1 { text-align: center; color: var(--accent-color); }

        /* Contenedores */
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: var(--border-radius);
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }

        /* Inputs y Botones */
        .input-group {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
            align-items: flex-end;
            flex-wrap: wrap;
        }

        .form-control {
            display: flex;
            flex-direction: column;
        }

        label { font-size: 0.9em; font-weight: 600; margin-bottom: 5px; }

        input {
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1em;
        }

        button {
            padding: 10px 20px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            transition: background 0.3s;
        }

        button:hover { background-color: #14b2e2; }
        button.secondary { background-color: #d31616; }
        button:disabled { background-color: #cbd5e1; cursor: not-allowed; }

        /* Configuración de Bloques */
        #blocks-config-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 10px;
            margin-top: 15px;
        }

        /* Simulación Visual */
        .simulation-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }

        @media (max-width: 768px) {
            .simulation-grid { grid-template-columns: 1fr; }
        }

        .algo-column {
            background: #fafafa;
            padding: 15px;
            border-radius: var(--border-radius);
            border: 1px solid #e5e7eb;
        }

        .algo-header {
            text-align: center;
            padding-bottom: 10px;
            border-bottom: 2px solid #eee;
            margin-bottom: 10px;
        }

        /* Visualización de la Memoria */
        .memory-container {
            display: flex;
            flex-direction: column;
            gap: 8px;
            min-height: 200px;
        }

        .memory-block {
            position: relative;
            height: 50px; /* Altura fija para visualización limpia */
            background-color: var(--block-free);
            border: 1px solid #cbd5e1;
            border-radius: 4px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            transition: all 0.5s ease;
            overflow: hidden;
        }

        .memory-block.occupied {
            background-color: #dbeafe; /* Fondo ligero para ocupado */
            border-color: var(--block-occupied);
        }

        /* Barra de progreso interna (Proceso) */
        .process-bar {
            height: 80%;
            background-color: var(--block-occupied);
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 0.8em;
            white-space: nowrap;
            transition: width 0.5s ease;
            width: 0%; /* Inicia en 0 para animación */
        }

        .block-info {
            position: absolute;
            right: 10px;
            font-size: 0.8em;
            color: #666;
        }

        /* Estadísticas */
        .stats-panel {
            margin-top: 15px;
            font-size: 0.9em;
            background: white;
            padding: 10px;
            border-radius: 4px;
        }
        .stat-row { display: flex; justify-content: space-between; margin-bottom: 5px; }
        .stat-val { font-weight: bold; }

        /* Consola */
        #console-log {
            background: #1e293b;
            color: #10b981;
            font-family: 'Courier New', Courier, monospace;
            padding: 15px;
            height: 150px;
            overflow-y: auto;
            border-radius: var(--border-radius);
            font-size: 0.85em;
        }
        .log-entry { margin-bottom: 5px; border-bottom: 1px solid #334155; padding-bottom: 2px; }
        .log-error { color: #ef4444; }
        .log-bf { color: #60a5fa; } /* Azul claro */
        .log-wf { color: #f472b6; } /* Rosa */

        /* Ganador */
        .winner-section {
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #e0f2fe 0%, #f0f9ff 100%);
            border: 2px solid var(--accent-color);
            margin-top: 20px;
            display: none; /* Oculto al inicio */
        }
        .winner-badge {
            font-size: 1.5em;
            font-weight: bold;
            color: var(--accent-color);
        }
        
        /* Utilidades */
        .hidden { display: none !important; }
        .fragmentation-visual {
            background: repeating-linear-gradient(
                45deg,
                rgba(0,0,0,0.05),
                rgba(0,0,0,0.05) 10px,
                rgba(0,0,0,0.1) 10px,
                rgba(0,0,0,0.1) 20px
            );
        }
        footer {
            background-color: rgb(174, 218, 230);
            color: rgb(0, 0, 0); 
            padding: 20px; 
            width: 100%; 
            box-sizing: border-box;
            text-align: center;
            margin-top: 50px; 
            border-radius: 20px; 
        
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Simulador de Memoria: Best Fit vs Worst Fit</h1>

    <div id="step-1" class="card">
        <h3>1. Configuración de Memoria</h3>
        <p>Define el tamaño total de la memoria y en cuántos bloques (particiones) quieres dividirla.</p>
        <div class="input-group">
            <div class="form-control">
                <label>Tamaño Total Memoria (KB)</label>
                <input type="number" id="total-mem" value="1000" min="100">
            </div>
            <div class="form-control">
                <label>Cantidad de Bloques</label>
                <input type="number" id="num-blocks" value="5" min="1" max="20">
            </div>
            <button onclick="generateBlockInputs()">Generar Bloques</button>
        </div>
        
        <div id="blocks-config-wrapper" class="hidden">
            <h4>Define el tamaño de cada bloque:</h4>
            <p style="font-size: 0.8em; color: #666;">La suma no debe superar el total. Si sobra espacio, se marcará como "Sistema".</p>
            <div id="blocks-config-container"></div>
            <div style="margin-top: 15px;">
                <span id="current-sum-display">Suma actual: 0 KB</span>
                <button onclick="initializeSimulation()" style="margin-left: 20px;">Iniciar Simulación</button>
            </div>
        </div>
    </div>

    <div id="step-2" class="card hidden">
        <div class="input-group" style="justify-content: space-between; align-items: center; border-bottom: 1px solid #eee; padding-bottom: 15px;">
            <h3>Panel de Control</h3>
            <button class="secondary" onclick="resetSimulation()">Reiniciar Todo</button>
        </div>

        <div class="input-group">
            <div class="form-control">
                <label>ID Proceso</label>
                <input type="text" id="proc-id" placeholder="ej. P1">
            </div>
            <div class="form-control">
                <label>Tamaño Proceso (KB)</label>
                <input type="number" id="proc-size" placeholder="ej. 150">
            </div>
            <button onclick="addProcess()">Asignar Proceso</button>
        </div>

        <div class="simulation-grid">
            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--success-color)">Best Fit</h2>
                    <p>Busca el bloque más pequeño que sea suficiente.</p>
                </div>
                <div id="bf-container" class="memory-container"></div>
                
                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="bf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Libre):</span> <span id="bf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="bf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas de Asignación:</span> <span id="bf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>

            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--danger-color)">Worst Fit</h2>
                    <p>Busca el bloque más grande disponible.</p>
                </div>
                <div id="wf-container" class="memory-container"></div>

                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="wf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Libre):</span> <span id="wf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="wf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas de Asignación:</span> <span id="wf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>
        </div>

        <div id="winner-section" class="winner-section">
            <h3>🏆 Comparativa Final</h3>
            <p id="winner-text" class="winner-badge"></p>
            <p id="winner-reason" style="margin-top: 10px;"></p>
        </div>
    </div>

    <div class="card">
        <h3>System Logs</h3>
        <div id="console-log"></div>
    </div>
</div>

<script>
    /* =========================================
       LÓGICA DEL SIMULADOR
       ========================================= */

    // Estado global
    let memoryTotal = 0;
    let initialBlocksConfig = []; // {id, size}
    
    // Estado de las simulaciones
    let bfState = { blocks: [], fails: 0, processes: [] };
    let wfState = { blocks: [], fails: 0, processes: [] };
    
    let processCounter = 1;

    // Utilidad: Logger
    function log(msg, type = 'info') {
        const consoleDiv = document.getElementById('console-log');
        const entry = document.createElement('div');
        entry.classList.add('log-entry');
        
        const timestamp = new Date().toLocaleTimeString();
        let prefix = `[${timestamp}] `;
        
        if (type === 'error') {
            entry.classList.add('log-error');
            prefix += '❌ ';
        } else if (type === 'bf') {
            entry.classList.add('log-bf');
            prefix += '🟢 [BestFit] ';
        } else if (type === 'wf') {
            entry.classList.add('log-wf');
            prefix += '🔴 [WorstFit] ';
        } else {
            prefix += 'ℹ️ ';
        }

        entry.innerText = prefix + msg;
        consoleDiv.prepend(entry);
    }

    // PASO 1: Generar inputs para bloques
    function generateBlockInputs() {
        memoryTotal = parseInt(document.getElementById('total-mem').value);
        const count = parseInt(document.getElementById('num-blocks').value);
        const container = document.getElementById('blocks-config-container');
        
        if (!memoryTotal || !count) return alert("Por favor ingresa valores válidos.");
        
        container.innerHTML = '';
        const suggestedSize = Math.floor(memoryTotal / count);

        for (let i = 0; i < count; i++) {
            const div = document.createElement('div');
            div.className = 'form-control';
            // Variación aleatoria ligera para sugerir tamaños diferentes, pero editable
            const randomVar = Math.floor(Math.random() * 20) - 10; 
            div.innerHTML = `
                <label>Bloque ${i + 1} (KB)</label>
                <input type="number" class="block-input" data-index="${i}" value="${suggestedSize + randomVar}" onchange="updateSum()">
            `;
            container.appendChild(div);
        }

        document.getElementById('blocks-config-wrapper').classList.remove('hidden');
        updateSum();
    }

    function updateSum() {
        const inputs = document.querySelectorAll('.block-input');
        let sum = 0;
        inputs.forEach(inp => sum += parseInt(inp.value || 0));
        const display = document.getElementById('current-sum-display');
        display.innerText = `Suma actual: ${sum} KB / Total: ${memoryTotal} KB`;
        
        if(sum > memoryTotal) display.style.color = 'red';
        else display.style.color = 'green';
    }

    // PASO 2: Inicializar
    function initializeSimulation() {
        const inputs = document.querySelectorAll('.block-input');
        let sum = 0;
        initialBlocksConfig = [];

        // Validar y construir configuración
        for (let i = 0; i < inputs.length; i++) {
            const size = parseInt(inputs[i].value);
            if (size <= 0) return alert("Los tamaños de bloque deben ser positivos.");
            sum += size;
            initialBlocksConfig.push({
                id: i,
                size: size,
                occupied: false,
                processId: null,
                processSize: 0
            });
        }

        if (sum > memoryTotal) return alert(`La suma de bloques (${sum}) excede la memoria total (${memoryTotal}).`);

        // Copia profunda para estados independientes
        bfState.blocks = JSON.parse(JSON.stringify(initialBlocksConfig));
        wfState.blocks = JSON.parse(JSON.stringify(initialBlocksConfig));
        bfState.fails = 0;
        wfState.fails = 0;
        
        // UI Switch
        document.getElementById('step-1').classList.add('hidden');
        document.getElementById('step-2').classList.remove('hidden');
        
        log("Simulación inicializada con memoria particionada (Fixed Partitioning).");
        renderAll();
    }

    function resetSimulation() {
        location.reload();
    }

    // LÓGICA CORE: Asignar Proceso
    function addProcess() {
        const pIdInput = document.getElementById('proc-id');
        const pSizeInput = document.getElementById('proc-size');
        
        let pId = pIdInput.value || `P${processCounter}`;
        let pSize = parseInt(pSizeInput.value);

        if (!pSize || pSize <= 0) return alert("Tamaño de proceso inválido");

        log(`Intentando asignar Proceso ${pId} (${pSize} KB)...`);

        // 1. Ejecutar Best Fit
        runBestFit(pId, pSize);

        // 2. Ejecutar Worst Fit
        runWorstFit(pId, pSize);

        // 3. Actualizar UI
        processCounter++;
        pIdInput.value = `P${processCounter}`;
        pSizeInput.value = '';
        
        renderAll();
        checkWinner();
    }

    function runBestFit(id, size) {
        let bestIndex = -1;
        let minFragmentation = Infinity;

        // Lógica Best Fit: Buscar el bloque libre donde (bloque.size - proceso.size) sea MÍNIMO
        for (let i = 0; i < bfState.blocks.length; i++) {
            const block = bfState.blocks[i];
            if (!block.occupied && block.size >= size) {
                const diff = block.size - size;
                if (diff < minFragmentation) {
                    minFragmentation = diff;
                    bestIndex = i;
                }
            }
        }

        if (bestIndex !== -1) {
            // Asignar
            bfState.blocks[bestIndex].occupied = true;
            bfState.blocks[bestIndex].processId = id;
            bfState.blocks[bestIndex].processSize = size;
            log(`Asignado ${id} en Bloque ${bestIndex + 1} (Frag. Interna: ${minFragmentation} KB)`, 'bf');
        } else {
            bfState.fails++;
            log(`Fallo al asignar ${id}. No hay bloque adecuado.`, 'bf');
        }
    }

    function runWorstFit(id, size) {
        let worstIndex = -1;
        let maxFragmentation = -1;

        // Lógica Worst Fit: Buscar el bloque libre donde (bloque.size - proceso.size) sea MÁXIMO
        for (let i = 0; i < wfState.blocks.length; i++) {
            const block = wfState.blocks[i];
            if (!block.occupied && block.size >= size) {
                const diff = block.size - size;
                if (diff > maxFragmentation) {
                    maxFragmentation = diff;
                    worstIndex = i;
                }
            }
        }

        if (worstIndex !== -1) {
            // Asignar
            wfState.blocks[worstIndex].occupied = true;
            wfState.blocks[worstIndex].processId = id;
            wfState.blocks[worstIndex].processSize = size;
            log(`Asignado ${id} en Bloque ${worstIndex + 1} (Frag. Interna: ${maxFragmentation} KB)`, 'wf');
        } else {
            wfState.fails++;
            log(`Fallo al asignar ${id}. No hay bloque adecuado.`, 'wf');
        }
    }

    /* =========================================
       RENDERIZADO Y MÉTRICAS
       ========================================= */

    function renderAll() {
        renderContainer('bf-container', bfState.blocks);
        renderContainer('wf-container', wfState.blocks);
        
        updateStats(bfState, 'bf');
        updateStats(wfState, 'wf');
    }

    function renderContainer(containerId, blocks) {
        const container = document.getElementById(containerId);
        container.innerHTML = '';

        blocks.forEach((block, index) => {
            const div = document.createElement('div');
            div.className = `memory-block ${block.occupied ? 'occupied' : ''}`;
            
            // Cálculo de anchos para visualización
            let barWidth = 0;
            let internalFrag = 0;
            
            if (block.occupied) {
                // Porcentaje que ocupa el proceso dentro del bloque
                const pct = (block.processSize / block.size) * 100;
                barWidth = pct;
                internalFrag = block.size - block.processSize;
            }

            const content = block.occupied 
                ? `<div class="process-bar" style="width: ${barWidth}%">${block.processId} (${block.processSize}KB)</div>` 
                : `<span style="color: #999; font-style: italic; font-size: 0.8em;">Libre</span>`;

            div.innerHTML = `
                ${content}
                <div class="block-info">
                    <strong>B${index+1}</strong>: ${block.size}KB
                    ${block.occupied ? `<br><small style="color:red">F.Int: ${internalFrag}KB</small>` : ''}
                </div>
            `;
            container.appendChild(div);
        });
    }

    function updateStats(state, prefix) {
        // Métricas
        // 1. Utilización: Suma de tamaños de procesos / Total Memoria Sistema
        let totalUsedByProcess = 0;
        let totalFree = 0; // Fragmentación externa (suma de bloques libres)
        let maxFree = 0;

        state.blocks.forEach(b => {
            if (b.occupied) {
                totalUsedByProcess += b.processSize;
            } else {
                totalFree += b.size;
                if (b.size > maxFree) maxFree = b.size;
            }
        });

        const utilization = ((totalUsedByProcess / memoryTotal) * 100).toFixed(1);

        document.getElementById(`${prefix}-util`).innerText = `${utilization}%`;
        document.getElementById(`${prefix}-frag`).innerText = `${totalFree} KB`;
        document.getElementById(`${prefix}-max-free`).innerText = `${maxFree} KB`;
        document.getElementById(`${prefix}-fails`).innerText = state.fails;
    }

    function checkWinner() {
        const div = document.getElementById('winner-section');
        const badge = document.getElementById('winner-text');
        const reason = document.getElementById('winner-reason');
        
        div.style.display = 'block';

        // Criterio 1: Menos fallos
        if (bfState.fails < wfState.fails) {
            badge.innerText = "Ganador: BEST FIT";
            reason.innerText = `Best Fit ha tenido menos fallos de asignación (${bfState.fails} vs ${wfState.fails}). Aprovecha mejor los espacios ajustados.`;
            div.style.borderColor = "var(--success-color)";
        } else if (wfState.fails < bfState.fails) {
            badge.innerText = "Ganador: WORST FIT";
            reason.innerText = `Worst Fit ha tenido menos fallos (${wfState.fails} vs ${bfState.fails}). Al dejar huecos grandes, permitió entrar procesos futuros.`;
            div.style.borderColor = "var(--danger-color)";
        } else {
            // Empate en fallos, mirar fragmentación externa (más memoria libre disponible es mejor para el futuro?)
            // O mirar utilización (más utilización es mejor)
            
            // Calcular utilizaciones reales
            const bfUtil = parseFloat(document.getElementById('bf-util').innerText);
            const wfUtil = parseFloat(document.getElementById('wf-util').innerText);

            if (bfUtil > wfUtil) {
                badge.innerText = "Ganador Técnico: BEST FIT";
                reason.innerText = "Empate en fallos, pero Best Fit tiene mayor porcentaje de utilización de memoria.";
            } else if (wfUtil > bfUtil) {
                badge.innerText = "Ganador Técnico: WORST FIT";
                reason.innerText = "Empate en fallos, pero Worst Fit tiene mayor porcentaje de utilización de memoria.";
            } else {
                badge.innerText = "EMPATE";
                reason.innerText = "Ambos algoritmos se comportaron igual con esta carga de trabajo.";
                div.style.borderColor = "#999";
            }
        }
    }
</script>
    <footer>
        Astrit Airan Cetzal Cetzal - Sistemas Operativos - 14/02/2026 - Profesor: Jorge Javier Pedrozo Romero - Tecnológico de Software
    </footer>
</body>
</html>

quiero qie mi codigo haga lo kmismo que este  poque en este aumentan los bloques po la fragmentación 

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador de Algoritmos Best Fit vs Worst Fit</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
            margin: 0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            
            min-height: 100vh;
            padding: 20px;
            background-image: linear-gradient(to left, #ace5fffb, #79a2fc); /* Fondo con degradado de amarillo a naranja */
            
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            overflow: hidden;
        }

        header {
            background: linear-gradient(135deg, #69bcdd 0%, #137485 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .subtitle {
            opacity: 0.9;
            font-size: 1.1em;
        }

        .content {
            padding: 30px;
            background-color: #84a0b8;
        }

        .controls {
            background: #90b9e2;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 30px;
        }

        .control-section {
            margin-bottom: 25px;
        }

        .control-section h3 {
            color: #667eea;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .input-group {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            align-items: end;
        }

        .input-field {
            flex: 1;
            min-width: 150px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: 500;
        }

        input[type="number"] {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        input[type="number"]:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s;
            font-weight: 600;
        }

        .btn-primary {
            background: #667eea;
            color: white;
        }

        .btn-primary:hover {
            background: #5568d3;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-secondary:hover {
            background: #5a6268;
        }

        .btn-success {
            background: #28a745;
            color: white;
        }

        .btn-success:hover {
            background: #218838;
        }

        .btn-danger {
            background: #dc3545;
            color: white;
        }

        .btn-danger:hover {
            background: #c82333;
        }

        .algorithm-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        .algorithm-container {
            border: 2px solid #ddd;
            border-radius: 10px;
            padding: 20px;
            background: #fafafa;
        }

        .algorithm-container h2 {
            color: #667eea;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.5em;
        }

        .memory-display {
            background: white;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 15px;
            min-height: 400px;
            margin-bottom: 20px;
        }

        .memory-block {
            margin-bottom: 10px;
            border-radius: 5px;
            padding: 10px;
            position: relative;
            transition: all 0.5s ease;
            border: 2px solid #ddd;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.02);
            }
        }

        .memory-block.allocating {
            animation: pulse 0.6s ease-in-out;
        }

        .memory-block.free {
            background: linear-gradient(135deg, #84fab0 0%, #8fd3f4 100%);
            border-color: #4ecdc4;
        }

        .memory-block.occupied {
            background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
            border-color: #f093fb;
        }

        .memory-info {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .memory-label {
            font-weight: 600;
            color: #333;
        }

        .memory-size {
            font-size: 0.9em;
            color: #666;
        }

        .stats {
            background: white;
            border-radius: 8px;
            padding: 15px;
            border: 2px solid #ddd;
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }

        .stat-item:last-child {
            border-bottom: none;
        }

        .stat-label {
            color: #666;
            font-weight: 500;
        }

        .stat-value {
            color: #667eea;
            font-weight: 700;
        }

        .comparison {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 10px;
            margin-top: 30px;
        }

        .comparison h3 {
            color: #667eea;
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.5em;
        }

        .comparison-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
        }

        .comparison-card {
            background: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }

        .comparison-card h4 {
            color: #555;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .comparison-value {
            font-size: 2em;
            font-weight: 700;
            color: #667eea;
        }

        .winner {
            background: linear-gradient(135deg, #61c8cf 0%, #1779aa 100%);
        }

        .winner .comparison-value {
            color: #083813;
        }

        .process-queue {
            background: white;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 15px;
            margin-top: 20px;
        }

        .process-queue h4 {
            color: #667eea;
            margin-bottom: 10px;
        }

        .process-item {
            display: inline-block;
            background: #667eea;
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            margin: 5px;
            font-size: 0.9em;
            animation: slideIn 0.3s;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .log {
            background: #2d3748;
            color: #a0aec0;
            padding: 15px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            max-height: 200px;
            overflow-y: auto;
            margin-top: 20px;
        }

        .log-entry {
            margin-bottom: 5px;
            padding: 3px 0;
        }

        .log-success {
            color: #48bb78;
        }

        .log-error {
            color: #f56565;
        }

        .log-info {
            color: #4299e1;
        }

        @media (max-width: 768px) {
            .algorithm-section {
                grid-template-columns: 1fr;
            }

            .input-group {
                flex-direction: column;
            }

            .input-field {
                min-width: 100%;
            }
        }

        .tooltip {
            position: relative;
            display: inline-block;
        }

        .tooltip .tooltiptext {
            visibility: hidden;
            background-color: #555;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 5px 10px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -60px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 0.85em;
        }

        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }
        footer {
            background-color: rgb(68, 118, 158);
            color: rgb(0, 0, 0); 
            padding: 20px; 
            width: 100%; 
            box-sizing: border-box;
            text-align: center;
            margin-top: 50px; 
            border-radius: 20px; 
        
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🧠 Simulador de Gestión de Memoria</h1>
            <p class="subtitle">Comparación de algoritmos Best Fit vs Worst Fit</p>
        </header>

        <div class="content">
            <div class="controls">
                <div class="control-section">
                    <h3>📊 Configuración de Memoria</h3>
                    <div class="input-group">
                        <div class="input-field">
                            <label>Tamaño Total de Memoria (KB)</label>
                            <input type="number" id="totalMemory" value="1024" min="100">
                        </div>
                        <div class="input-field">
                            <label>Número de Bloques Iniciales</label>
                            <input type="number" id="numBlocks" value="5" min="1" max="10">
                        </div>
                        <button class="btn-primary" onclick="initializeMemory()">Inicializar Memoria</button>
                    </div>
                </div>

                <div class="control-section">
                    <h3>⚙️ Agregar Proceso</h3>
                    <div class="input-group">
                        <div class="input-field">
                            <label>ID del Proceso</label>
                            <input type="number" id="processId" value="1" min="1">
                        </div>
                        <div class="input-field">
                            <label>Tamaño del Proceso (KB)</label>
                            <input type="number" id="processSize" value="100" min="1">
                        </div>
                        <button class="btn-success" onclick="addProcess()">Agregar Proceso</button>
                    </div>
                </div>

                <div class="input-group">
                    <button class="btn-primary" onclick="executeAllocation()">▶️ Ejecutar Asignación</button>
                    <button class="btn-secondary" onclick="resetSimulation()">🔄 Reiniciar Simulación</button>
                    <button class="btn-danger" onclick="clearMemory()">🗑️ Limpiar Memoria</button>
                </div>
            </div>

            <div class="process-queue" id="processQueue" style="display: none;">
                <h4>Cola de Procesos Pendientes</h4>
                <div id="queueDisplay"></div>
            </div>

            <div class="algorithm-section">
                <div class="algorithm-container">
                    <h2>🎯 Best Fit</h2>
                    <div class="memory-display" id="bestFitMemory"></div>
                    <div class="stats" id="bestFitStats"></div>
                    <div class="log" id="bestFitLog"></div>
                </div>

                <div class="algorithm-container">
                    <h2>📈 Worst Fit</h2>
                    <div class="memory-display" id="worstFitMemory"></div>
                    <div class="stats" id="worstFitStats"></div>
                    <div class="log" id="worstFitLog"></div>
                </div>
            </div>

            <div class="comparison">
                <h3>📊 Comparación de Rendimiento</h3>
                <div class="comparison-grid" id="comparisonGrid"></div>
            </div>
        </div>
    </div>

    <script>
        class MemoryBlock {
            constructor(start, size, isFree = true, processId = null) {
                this.start = start;
                this.size = size;
                this.isFree = isFree;
                this.processId = processId;
            }
        }

        class MemoryManager {
            constructor(totalSize, algorithm) {
                this.totalSize = totalSize;
                this.algorithm = algorithm;
                this.blocks = [new MemoryBlock(0, totalSize, true)];
                this.allocations = 0;
                this.failures = 0;
                this.log = [];
            }

            initializeBlocks(numBlocks) {
                this.blocks = [];
                const blockSize = Math.floor(this.totalSize / numBlocks);
                let start = 0;

                for (let i = 0; i < numBlocks; i++) {
                    const size = i === numBlocks - 1 ? 
                        this.totalSize - start : 
                        blockSize + Math.floor(Math.random() * 50);
                    
                    this.blocks.push(new MemoryBlock(start, size, true));
                    start += size;
                }
            }

            allocate(processId, size) {
                let targetBlock = null;

                if (this.algorithm === 'bestfit') {
                    let minDiff = Infinity;
                    for (let block of this.blocks) {
                        if (block.isFree && block.size >= size) {
                            const diff = block.size - size;
                            if (diff < minDiff) {
                                minDiff = diff;
                                targetBlock = block;
                            }
                        }
                    }
                } else if (this.algorithm === 'worstfit') {
                    let maxSize = -1;
                    for (let block of this.blocks) {
                        if (block.isFree && block.size >= size && block.size > maxSize) {
                            maxSize = block.size;
                            targetBlock = block;
                        }
                    }
                }

                if (targetBlock) {
                    const index = this.blocks.indexOf(targetBlock);
                    
                    if (targetBlock.size === size) {
                        targetBlock.isFree = false;
                        targetBlock.processId = processId;
                    } else {
                        const newBlock = new MemoryBlock(
                            targetBlock.start, 
                            size, 
                            false, 
                            processId
                        );
                        const remainingBlock = new MemoryBlock(
                            targetBlock.start + size,
                            targetBlock.size - size,
                            true
                        );
                        
                        this.blocks.splice(index, 1, newBlock, remainingBlock);
                    }

                    this.allocations++;
                    this.addLog(`✓ Proceso P${processId} (${size}KB) asignado exitosamente`, 'success');
                    return true;
                } else {
                    this.failures++;
                    this.addLog(`✗ Proceso P${processId} (${size}KB) no pudo ser asignado`, 'error');
                    return false;
                }
            }

            deallocate(processId) {
                for (let block of this.blocks) {
                    if (!block.isFree && block.processId === processId) {
                        block.isFree = true;
                        block.processId = null;
                        this.mergeBlocks();
                        this.addLog(`↺ Proceso P${processId} liberado`, 'info');
                        return true;
                    }
                }
                return false;
            }

            mergeBlocks() {
                let i = 0;
                while (i < this.blocks.length - 1) {
                    if (this.blocks[i].isFree && this.blocks[i + 1].isFree) {
                        this.blocks[i].size += this.blocks[i + 1].size;
                        this.blocks.splice(i + 1, 1);
                    } else {
                        i++;
                    }
                }
            }

            getFragmentation() {
                let totalFree = 0;
                let largestFree = 0;
                let freeBlockCount = 0;

                for (let block of this.blocks) {
                    if (block.isFree) {
                        totalFree += block.size;
                        freeBlockCount++;
                        if (block.size > largestFree) {
                            largestFree = block.size;
                        }
                    }
                }

                const externalFragmentation = totalFree > 0 ? 
                    ((totalFree - largestFree) / totalFree * 100) : 0;

                return {
                    totalFree,
                    largestFree,
                    externalFragmentation: externalFragmentation.toFixed(2),
                    freeBlockCount
                };
            }

            getUtilization() {
                let used = 0;
                for (let block of this.blocks) {
                    if (!block.isFree) {
                        used += block.size;
                    }
                }
                return ((used / this.totalSize) * 100).toFixed(2);
            }

            addLog(message, type = 'info') {
                this.log.push({ message, type, timestamp: new Date() });
            }

            clearLog() {
                this.log = [];
            }
        }

        let bestFitManager;
        let worstFitManager;
        let processQueue = [];
        let nextProcessId = 1;

        function initializeMemory() {
            const totalMemory = parseInt(document.getElementById('totalMemory').value);
            const numBlocks = parseInt(document.getElementById('numBlocks').value);

            bestFitManager = new MemoryManager(totalMemory, 'bestfit');
            worstFitManager = new MemoryManager(totalMemory, 'worstfit');

            bestFitManager.initializeBlocks(numBlocks);
            worstFitManager.initializeBlocks(numBlocks);

            bestFitManager.addLog('Memoria inicializada', 'success');
            worstFitManager.addLog('Memoria inicializada', 'success');

            updateDisplay();
        }

        function addProcess() {
            const processId = parseInt(document.getElementById('processId').value);
            const processSize = parseInt(document.getElementById('processSize').value);

            processQueue.push({ id: processId, size: processSize });
            
            document.getElementById('processId').value = processId + 1;
            document.getElementById('processQueue').style.display = 'block';
            
            updateQueueDisplay();
        }

        function updateQueueDisplay() {
            const queueDisplay = document.getElementById('queueDisplay');
            queueDisplay.innerHTML = '';

            processQueue.forEach(process => {
                const processItem = document.createElement('div');
                processItem.className = 'process-item';
                processItem.textContent = `P${process.id}: ${process.size}KB`;
                queueDisplay.appendChild(processItem);
            });
        }

        async function executeAllocation() {
            if (processQueue.length === 0) {
                alert('No hay procesos en la cola');
                return;
            }

            if (!bestFitManager || !worstFitManager) {
                alert('Primero inicializa la memoria');
                return;
            }

            for (let process of processQueue) {
                await allocateWithAnimation(process);
            }

            processQueue = [];
            document.getElementById('processQueue').style.display = 'none';
            updateComparison();
        }

        async function allocateWithAnimation(process) {
            bestFitManager.allocate(process.id, process.size);
            worstFitManager.allocate(process.id, process.size);

            updateDisplay();
            
            // Highlight allocated blocks
            const bestFitBlocks = document.querySelectorAll('#bestFitMemory .memory-block');
            const worstFitBlocks = document.querySelectorAll('#worstFitMemory .memory-block');
            
            bestFitBlocks.forEach(block => {
                if (block.dataset.processId == process.id) {
                    block.classList.add('allocating');
                }
            });
            
            worstFitBlocks.forEach(block => {
                if (block.dataset.processId == process.id) {
                    block.classList.add('allocating');
                }
            });

            await new Promise(resolve => setTimeout(resolve, 600));
            
            bestFitBlocks.forEach(block => block.classList.remove('allocating'));
            worstFitBlocks.forEach(block => block.classList.remove('allocating'));
        }

        function updateDisplay() {
            if (!bestFitManager || !worstFitManager) return;

            updateMemoryDisplay('bestFitMemory', bestFitManager);
            updateMemoryDisplay('worstFitMemory', worstFitManager);

            updateStats('bestFitStats', bestFitManager);
            updateStats('worstFitStats', worstFitManager);

            updateLog('bestFitLog', bestFitManager);
            updateLog('worstFitLog', worstFitManager);
        }

        function updateMemoryDisplay(elementId, manager) {
            const container = document.getElementById(elementId);
            container.innerHTML = '';

            manager.blocks.forEach((block, index) => {
                const blockDiv = document.createElement('div');
                blockDiv.className = `memory-block ${block.isFree ? 'free' : 'occupied'}`;
                blockDiv.dataset.processId = block.processId;
                
                const heightPercent = (block.size / manager.totalSize) * 100;
                blockDiv.style.height = Math.max(heightPercent * 3, 30) + 'px';

                const info = document.createElement('div');
                info.className = 'memory-info';

                const label = document.createElement('span');
                label.className = 'memory-label';
                label.textContent = block.isFree ? 
                    `Bloque Libre #${index + 1}` : 
                    `Proceso P${block.processId}`;

                const size = document.createElement('span');
                size.className = 'memory-size';
                size.textContent = `${block.size}KB (${heightPercent.toFixed(1)}%)`;

                info.appendChild(label);
                info.appendChild(size);
                blockDiv.appendChild(info);

                container.appendChild(blockDiv);
            });
        }

        function updateStats(elementId, manager) {
            const container = document.getElementById(elementId);
            const frag = manager.getFragmentation();
            const util = manager.getUtilization();

            container.innerHTML = `
                <div class="stat-item">
                    <span class="stat-label">Utilización:</span>
                    <span class="stat-value">${util}%</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Memoria Libre:</span>
                    <span class="stat-value">${frag.totalFree}KB</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Bloque Libre Más Grande:</span>
                    <span class="stat-value">${frag.largestFree}KB</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Fragmentación Externa:</span>
                    <span class="stat-value">${frag.externalFragmentation}%</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Bloques Libres:</span>
                    <span class="stat-value">${frag.freeBlockCount}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Asignaciones Exitosas:</span>
                    <span class="stat-value">${manager.allocations}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">Asignaciones Fallidas:</span>
                    <span class="stat-value">${manager.failures}</span>
                </div>
            `;
        }

        function updateLog(elementId, manager) {
            const container = document.getElementById(elementId);
            container.innerHTML = '';

            manager.log.slice(-10).forEach(entry => {
                const logEntry = document.createElement('div');
                logEntry.className = `log-entry log-${entry.type}`;
                logEntry.textContent = `[${entry.timestamp.toLocaleTimeString()}] ${entry.message}`;
                container.appendChild(logEntry);
            });

            container.scrollTop = container.scrollHeight;
        }

        function updateComparison() {
            if (!bestFitManager || !worstFitManager) return;

            const bestFrag = bestFitManager.getFragmentation();
            const worstFrag = worstFitManager.getFragmentation();
            const bestUtil = parseFloat(bestFitManager.getUtilization());
            const worstUtil = parseFloat(worstFitManager.getUtilization());

            const grid = document.getElementById('comparisonGrid');
            grid.innerHTML = `
                <div class="comparison-card ${bestUtil >= worstUtil ? 'winner' : ''}">
                    <h4>Mejor Utilización</h4>
                    <div class="comparison-value">${bestUtil >= worstUtil ? 'Best Fit' : 'Worst Fit'}</div>
                    <p>${Math.max(bestUtil, worstUtil).toFixed(2)}%</p>
                </div>
                <div class="comparison-card ${parseFloat(bestFrag.externalFragmentation) <= parseFloat(worstFrag.externalFragmentation) ? 'winner' : ''}">
                    <h4>Menor Fragmentación</h4>
                    <div class="comparison-value">${parseFloat(bestFrag.externalFragmentation) <= parseFloat(worstFrag.externalFragmentation) ? 'Best Fit' : 'Worst Fit'}</div>
                    <p>${Math.min(parseFloat(bestFrag.externalFragmentation), parseFloat(worstFrag.externalFragmentation)).toFixed(2)}%</p>
                </div>
                <div class="comparison-card ${bestFitManager.failures <= worstFitManager.failures ? 'winner' : ''}">
                    <h4>Menos Fallas</h4>
                    <div class="comparison-value">${bestFitManager.failures <= worstFitManager.failures ? 'Best Fit' : 'Worst Fit'}</div>
                    <p>${Math.min(bestFitManager.failures, worstFitManager.failures)} fallas</p>
                </div>
                <div class="comparison-card ${bestFrag.largestFree >= worstFrag.largestFree ? 'winner' : ''}">
                    <h4>Mayor Bloque Libre</h4>
                    <div class="comparison-value">${bestFrag.largestFree >= worstFrag.largestFree ? 'Best Fit' : 'Worst Fit'}</div>
                    <p>${Math.max(bestFrag.largestFree, worstFrag.largestFree)}KB</p>
                </div>
            `;
        }

        function clearMemory() {
            if (!bestFitManager || !worstFitManager) return;

            bestFitManager.blocks.forEach(block => {
                block.isFree = true;
                block.processId = null;
            });

            worstFitManager.blocks.forEach(block => {
                block.isFree = true;
                block.processId = null;
            });

            bestFitManager.mergeBlocks();
            worstFitManager.mergeBlocks();

            bestFitManager.addLog('Memoria limpiada', 'info');
            worstFitManager.addLog('Memoria limpiada', 'info');

            updateDisplay();
            updateComparison();
        }

        function resetSimulation() {
            bestFitManager = null;
            worstFitManager = null;
            processQueue = [];
            
            document.getElementById('processQueue').style.display = 'none';
            document.getElementById('bestFitMemory').innerHTML = '';
            document.getElementById('worstFitMemory').innerHTML = '';
            document.getElementById('bestFitStats').innerHTML = '';
            document.getElementById('worstFitStats').innerHTML = '';
            document.getElementById('bestFitLog').innerHTML = '';
            document.getElementById('worstFitLog').innerHTML = '';
            document.getElementById('comparisonGrid').innerHTML = '';
        }

        // Initialize on load
        window.onload = function() {
            initializeMemory();
        };
    </script>

    <footer>
        Astrit Airan Cetzal Cetzal - Sistemas Operativos - 06/02/2026 - Profesor: Jorge Javier Pedrozo Romero - Tecnológico de Software
    </footer>
</body>
</html>

''''

## Archivos adjentos: N/A

## Respuesta:

Entendido perfectamente. He fusionado lo mejor de ambos mundos según tus instrucciones:

Estética y Estructura (Código 1): Mantuve los colores degradados (#dba2f5c9, #1d84b4), el diseño de tarjetas y el footer específico con tus datos.

Configuración (Código 1): El sistema genera tamaños aleatorios para los bloques iniciales, pero el usuario puede editarlos manualmente en los inputs antes de iniciar.

Lógica de Ejecución (Código 2 - Particionamiento Dinámico): Ahora, cuando un proceso entra en un bloque, divide el bloque. Si el bloque era de 500KB y entra un proceso de 100KB, el bloque se parte en dos: uno ocupado de 100KB y uno nuevo libre de 400KB (aumentando la cantidad total de bloques, tal como pediste).

Aquí tienes el código completo en un solo archivo:

''''

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simulador Avanzado: Best Fit vs Worst Fit (Dinámico)</title>
    <style>
        /* =========================================
           CONFIGURACIÓN DE COLORES Y ESTILOS
           ========================================= */
        :root {
            --bg-grad-start: #ace5fffb;
            --bg-grad-end: #79a2fc;
            --card-bg: #aeece9;
            --text-color: #333333;
            --accent-color: #1d84b4; /* Azul principal */
            --success-color: #10b981; /* Verde (Best Fit) */
            --danger-color: #ef4444;  /* Rojo (Worst Fit / Fallos) */
            --block-free: #9dddb8;    /* Verde claro libre */
            --block-occupied: #3bf6d7; /* Azul proceso */
            --border-radius: 12px;
            --font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }

        body {
            font-family: var(--font-family);
            background-image: linear-gradient(to left, var(--bg-grad-start), var(--bg-grad-end));
            color: var(--text-color);
            padding: 20px;
            line-height: 1.6;
            min-height: 100vh;
        }

        h1, h2, h3 { margin-bottom: 15px; font-weight: 700; }
        h1 { text-align: center; color: #0f4c68; text-shadow: 1px 1px 2px rgba(255,255,255,0.5); }

        /* Contenedores */
        .container {
            max-width: 1300px;
            margin: 0 auto;
        }

        .card {
            background: var(--card-bg);
            padding: 25px;
            border-radius: var(--border-radius);
            box-shadow: 0 8px 16px rgba(0,0,0,0.1);
            margin-bottom: 25px;
            border: 1px solid rgba(255,255,255,0.4);
        }

        /* Inputs y Botones */
        .input-group {
            display: flex;
            gap: 15px;
            margin-bottom: 15px;
            align-items: flex-end;
            flex-wrap: wrap;
        }

        .form-control {
            display: flex;
            flex-direction: column;
            flex: 1;
            min-width: 150px;
        }

        label { font-size: 0.9em; font-weight: 700; margin-bottom: 5px; color: #0e4b65; }

        input {
            padding: 12px;
            border: 2px solid #8ecae6;
            border-radius: 6px;
            font-size: 1em;
            background: rgba(255,255,255,0.9);
            transition: border 0.3s;
        }
        input:focus { border-color: var(--accent-color); outline: none; }

        button {
            padding: 12px 25px;
            background-color: var(--accent-color);
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 700;
            transition: transform 0.2s, box-shadow 0.2s;
            box-shadow: 0 4px 0 #155e82;
        }

        button:hover { transform: translateY(-2px); box-shadow: 0 6px 0 #155e82; background-color: #14b2e2; }
        button:active { transform: translateY(0); box-shadow: 0 2px 0 #155e82; }
        button.secondary { background-color: #d31616; box-shadow: 0 4px 0 #8f0e0e; }
        button.secondary:hover { background-color: #ff4d4d; }

        /* Configuración de Bloques Dinámicos */
        #blocks-config-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 10px;
            margin-top: 15px;
            background: rgba(255,255,255,0.3);
            padding: 15px;
            border-radius: 8px;
        }

        /* Simulación Visual */
        .simulation-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }

        @media (max-width: 850px) {
            .simulation-grid { grid-template-columns: 1fr; }
        }

        .algo-column {
            background: #f0fdfa; /* Fondo muy claro para contraste */
            padding: 20px;
            border-radius: var(--border-radius);
            border: 2px solid #bce3eb;
        }

        .algo-header {
            text-align: center;
            padding-bottom: 10px;
            border-bottom: 2px solid #ccc;
            margin-bottom: 15px;
        }

        /* Visualización de la Memoria (Estilo Pila/Stack) */
        .memory-container {
            display: flex;
            flex-direction: column;
            gap: 5px;
            min-height: 300px;
            background: #eef2f6;
            padding: 10px;
            border-radius: 8px;
            border: 1px inset #ccc;
        }

        .memory-block {
            position: relative;
            /* La altura se definirá dinámicamente según el tamaño */
            min-height: 35px; 
            border: 1px solid rgba(0,0,0,0.1);
            border-radius: 4px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0 10px;
            transition: all 0.4s ease;
            font-size: 0.85em;
            font-weight: 600;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }

        .memory-block.free {
            background-color: var(--block-free);
            color: #2c5e46;
            border-left: 5px solid #2c5e46;
        }

        .memory-block.occupied {
            background-color: var(--block-occupied);
            color: #0c4a6e;
            border-left: 5px solid #0c4a6e;
            animation: pulse 0.5s ease;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); box-shadow: 0 0 10px rgba(0,0,0,0.2); }
            100% { transform: scale(1); }
        }

        .block-info {
            display: flex;
            justify-content: space-between;
            width: 100%;
        }

        /* Estadísticas */
        .stats-panel {
            margin-top: 15px;
            font-size: 0.9em;
            background: white;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #ddd;
        }
        .stat-row { display: flex; justify-content: space-between; margin-bottom: 8px; border-bottom: 1px dashed #eee; padding-bottom: 2px; }
        .stat-val { font-weight: bold; color: var(--accent-color); }

        /* Consola */
        #console-log {
            background: #1e293b;
            color: #10b981;
            font-family: 'Courier New', Courier, monospace;
            padding: 15px;
            height: 180px;
            overflow-y: auto;
            border-radius: var(--border-radius);
            font-size: 0.85em;
            border: 2px solid #475569;
        }
        .log-entry { margin-bottom: 5px; border-bottom: 1px solid #334155; padding-bottom: 2px; }
        .log-error { color: #ef4444; }
        .log-bf { color: #60a5fa; } 
        .log-wf { color: #f472b6; } 

        /* Ganador */
        .winner-section {
            text-align: center;
            padding: 20px;
            background: white;
            border: 4px solid var(--accent-color);
            border-radius: 15px;
            margin-top: 20px;
            display: none;
            animation: slideUp 0.5s ease-out;
        }
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .winner-badge {
            font-size: 1.8em;
            font-weight: 800;
            color: var(--accent-color);
            text-transform: uppercase;
        }
        
        .hidden { display: none !important; }

        footer {
            background-color: rgba(255, 255, 255, 0.4);
            color: #000; 
            padding: 20px; 
            width: 100%; 
            box-sizing: border-box;
            text-align: center;
            margin-top: 50px; 
            border-radius: 20px; 
            font-weight: 600;
            border: 1px solid rgba(255,255,255,0.6);
        }
    </style>
</head>
<body>

<div class="container">
    <h1>Simulador de Gestión de Memoria Dinámica</h1>

    <div id="step-1" class="card">
        <h3>1. Configuración de Memoria</h3>
        <p>Define el tamaño total y los bloques iniciales. Luego, <strong>podrás editar manualmente</strong> los tamaños de los bloques antes de comenzar.</p>
        <div class="input-group">
            <div class="form-control">
                <label>Tamaño Total Memoria (KB)</label>
                <input type="number" id="total-mem" value="1024" min="100">
            </div>
            <div class="form-control">
                <label>Cantidad Inicial de Bloques</label>
                <input type="number" id="num-blocks" value="4" min="1" max="15">
            </div>
            <button onclick="generateBlockInputs()">Generar Bloques Editables</button>
        </div>
        
        <div id="blocks-config-wrapper" class="hidden">
            <h4>Ajuste Manual de Bloques:</h4>
            <p style="font-size: 0.9em; color: #444;">Modifica los valores si lo deseas. El sistema se ajustará al valor de "Suma Actual" al iniciar.</p>
            <div id="blocks-config-container"></div>
            <div style="margin-top: 20px; display: flex; align-items: center; justify-content: space-between; background: rgba(255,255,255,0.5); padding: 10px; border-radius: 8px;">
                <span id="current-sum-display" style="font-weight: bold; font-size: 1.1em;">Suma actual: 0 KB</span>
                <button onclick="initializeSimulation()" style="font-size: 1.1em;">🚀 Iniciar Simulación</button>
            </div>
        </div>
    </div>

    <div id="step-2" class="card hidden">
        <div class="input-group" style="justify-content: space-between; align-items: center; border-bottom: 2px solid rgba(255,255,255,0.5); padding-bottom: 15px;">
            <h3>Panel de Control</h3>
            <button class="secondary" onclick="resetSimulation()">🔄 Reiniciar Todo</button>
        </div>

        <div class="input-group" style="background: rgba(255,255,255,0.4); padding: 15px; border-radius: 8px;">
            <div class="form-control">
                <label>ID Proceso</label>
                <input type="text" id="proc-id" placeholder="ej. P1">
            </div>
            <div class="form-control">
                <label>Tamaño Proceso (KB)</label>
                <input type="number" id="proc-size" placeholder="ej. 150">
            </div>
            <button onclick="addProcess()">Asignar Proceso (+)</button>
        </div>

        <div class="simulation-grid">
            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--success-color)">Best Fit</h2>
                    <p>Elige el bloque donde sobra <strong>menos</strong> espacio. Divide el bloque seleccionado.</p>
                </div>
                <div id="bf-container" class="memory-container"></div>
                
                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="bf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Total Libre):</span> <span id="bf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloques Libres (Cantidad):</span> <span id="bf-free-count" class="stat-val">0</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="bf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas:</span> <span id="bf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>

            <div class="algo-column">
                <div class="algo-header">
                    <h2 style="color: var(--danger-color)">Worst Fit</h2>
                    <p>Elige el bloque <strong>más grande</strong>. Divide el bloque seleccionado.</p>
                </div>
                <div id="wf-container" class="memory-container"></div>

                <div class="stats-panel">
                    <div class="stat-row"><span>Utilización:</span> <span id="wf-util" class="stat-val">0%</span></div>
                    <div class="stat-row"><span>Frag. Externa (Total Libre):</span> <span id="wf-frag" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Bloques Libres (Cantidad):</span> <span id="wf-free-count" class="stat-val">0</span></div>
                    <div class="stat-row"><span>Bloque Libre Máx:</span> <span id="wf-max-free" class="stat-val">0 KB</span></div>
                    <div class="stat-row"><span>Fallas:</span> <span id="wf-fails" class="stat-val" style="color:red">0</span></div>
                </div>
            </div>
        </div>

        <div id="winner-section" class="winner-section">
            <h3>🏆 Resultados de la Fragmentación</h3>
            <p id="winner-text" class="winner-badge"></p>
            <p id="winner-reason" style="margin-top: 10px; font-size: 1.1em;"></p>
        </div>
    </div>

    <div class="card">
        <h3>Registro del Sistema (Logs)</h3>
        <div id="console-log"></div>
    </div>
</div>

<script>
    /* =========================================
       LÓGICA DEL SIMULADOR
       ========================================= */

    // Variables Globales
    let memoryTotalLimit = 0;
    let processCounter = 1;

    // Estado de los Algoritmos (Lista dinámica de bloques)
    // Estructura de bloque: { id, size, occupied, processId }
    let bfBlocks = [];
    let wfBlocks = [];
    
    let bfStats = { fails: 0 };
    let wfStats = { fails: 0 };

    // --- UTILERÍAS ---
    function log(msg, type = 'info') {
        const consoleDiv = document.getElementById('console-log');
        const entry = document.createElement('div');
        entry.classList.add('log-entry');
        
        const time = new Date().toLocaleTimeString();
        let prefix = `[${time}] `;
        
        if (type === 'error') {
            entry.classList.add('log-error'); prefix += '❌ ';
        } else if (type === 'bf') {
            entry.classList.add('log-bf'); prefix += '🟢 [BestFit] ';
        } else if (type === 'wf') {
            entry.classList.add('log-wf'); prefix += '🔴 [WorstFit] ';
        } else {
            prefix += 'ℹ️ ';
        }

        entry.innerText = prefix + msg;
        consoleDiv.prepend(entry);
    }

    // --- PASO 1: GENERACIÓN DE INPUTS (Configuración Manual) ---
    function generateBlockInputs() {
        memoryTotalLimit = parseInt(document.getElementById('total-mem').value);
        const count = parseInt(document.getElementById('num-blocks').value);
        const container = document.getElementById('blocks-config-container');
        
        if (!memoryTotalLimit || !count) return alert("Ingresa valores válidos.");

        container.innerHTML = '';
        
        // Generación de tamaños aleatorios "inteligentes" que sumen cerca del total
        let remaining = memoryTotalLimit;
        let sizes = [];
        
        for(let i=0; i<count-1; i++) {
            // Un tamaño aleatorio entre 10 y lo que queda dividido entre los bloques restantes
            let max = Math.floor(remaining / (count - i)) * 1.5; 
            let val = Math.floor(Math.random() * (max - 50)) + 50; 
            sizes.push(val);
            remaining -= val;
        }
        sizes.push(remaining); // El último se lleva el resto

        // Crear Inputs HTML
        sizes.forEach((size, i) => {
            const div = document.createElement('div');
            div.className = 'form-control';
            div.innerHTML = `
                <label>Bloque ${i+1} (KB)</label>
                <input type="number" class="block-input" value="${size}" oninput="updateSum()">
            `;
            container.appendChild(div);
        });

        document.getElementById('blocks-config-wrapper').classList.remove('hidden');
        updateSum();
    }

    function updateSum() {
        const inputs = document.querySelectorAll('.block-input');
        let sum = 0;
        inputs.forEach(inp => sum += parseInt(inp.value || 0));
        
        const display = document.getElementById('current-sum-display');
        display.innerText = `Suma actual: ${sum} KB`;
        
        if(sum > memoryTotalLimit) display.style.color = '#d31616'; // Rojo si se pasa
        else display.style.color = '#0e4b65';
    }

    // --- PASO 2: INICIALIZACIÓN DE LA MEMORIA ---
    function initializeSimulation() {
        const inputs = document.querySelectorAll('.block-input');
        let initialBlocks = [];
        let currentSum = 0;

        // Leer inputs del usuario
        for(let i=0; i<inputs.length; i++) {
            const size = parseInt(inputs[i].value);
            if(size <= 0) return alert("Los tamaños deben ser mayores a 0");
            initialBlocks.push({
                size: size,
                occupied: false,
                processId: null
            });
            currentSum += size;
        }

        // Actualizar el límite de memoria real basado en lo que configuró el usuario
        memoryTotalLimit = currentSum; 

        // Clonar para estados independientes
        bfBlocks = JSON.parse(JSON.stringify(initialBlocks));
        wfBlocks = JSON.parse(JSON.stringify(initialBlocks));
        
        bfStats.fails = 0;
        wfStats.fails = 0;

        // Cambiar vista
        document.getElementById('step-1').classList.add('hidden');
        document.getElementById('step-2').classList.remove('hidden');
        
        log(`Simulación iniciada. Memoria Total: ${memoryTotalLimit} KB. Bloques iniciales: ${initialBlocks.length}`);
        renderAll();
    }

    function resetSimulation() {
        location.reload();
    }

    // --- CORE: ASIGNACIÓN DINÁMICA (SPLITTING) ---
    function addProcess() {
        const pIdField = document.getElementById('proc-id');
        const pSizeField = document.getElementById('proc-size');
        
        const pId = pIdField.value || `P${processCounter}`;
        const pSize = parseInt(pSizeField.value);

        if(!pSize || pSize <= 0) return alert("Tamaño inválido");

        log(`Solicitud: ${pId} (${pSize} KB)...`);

        // 1. Ejecutar Best Fit
        allocateMemory(bfBlocks, bfStats, pId, pSize, 'bf');

        // 2. Ejecutar Worst Fit
        allocateMemory(wfBlocks, wfStats, pId, pSize, 'wf');

        // UI Updates
        processCounter++;
        pIdField.value = `P${processCounter}`;
        pSizeField.value = '';
        renderAll();
        determineWinner();
    }

    // Función genérica de asignación con división de bloques
    function allocateMemory(blocks, stats, pId, pSize, type) {
        let targetIndex = -1;
        
        if (type === 'bf') {
            // BEST FIT: Buscar bloque libre más pequeño que quepa
            let minDiff = Infinity;
            for (let i = 0; i < blocks.length; i++) {
                if (!blocks[i].occupied && blocks[i].size >= pSize) {
                    let diff = blocks[i].size - pSize;
                    if (diff < minDiff) {
                        minDiff = diff;
                        targetIndex = i;
                    }
                }
            }
        } else {
            // WORST FIT: Buscar bloque libre más grande que quepa
            let maxDiff = -1;
            for (let i = 0; i < blocks.length; i++) {
                if (!blocks[i].occupied && blocks[i].size >= pSize) {
                    let diff = blocks[i].size - pSize;
                    if (diff > maxDiff) {
                        maxDiff = diff;
                        targetIndex = i;
                    }
                }
            }
        }

        if (targetIndex !== -1) {
            // Bloque encontrado
            let originalBlock = blocks[targetIndex];
            
            // Asignar bloque
            // Modificamos el bloque actual para que sea el PROCESO
            let remainingSize = originalBlock.size - pSize;
            
            originalBlock.size = pSize;
            originalBlock.occupied = true;
            originalBlock.processId = pId;

            // Si sobró memoria, crear NUEVO bloque libre (Particionamiento Dinámico)
            if (remainingSize > 0) {
                let newBlock = {
                    size: remainingSize,
                    occupied: false,
                    processId: null
                };
                // Insertar el nuevo bloque justo después del actual
                blocks.splice(targetIndex + 1, 0, newBlock);
                log(`Asignado ${pId}. Bloque original dividido. Nuevo bloque libre de ${remainingSize}KB creado.`, type);
            } else {
                log(`Asignado ${pId}. Encaje exacto (0 fragmentación en este bloque).`, type);
            }
        } else {
            stats.fails++;
            log(`Fallo: No hay bloque contiguo suficiente para ${pId}`, type + ' error');
        }
    }

    // --- RENDERIZADO Y MÉTRICAS ---
    function renderAll() {
        renderContainer('bf-container', bfBlocks);
        renderContainer('wf-container', wfBlocks);
        updateStats('bf', bfBlocks, bfStats);
        updateStats('wf', wfBlocks, wfStats);
    }

    function renderContainer(id, blocks) {
        const container = document.getElementById(id);
        container.innerHTML = '';
        
        // Calcular altura proporcional (visual)
        // Máximo 400px altura total aprox para distribuir
        
        blocks.forEach(block => {
            const div = document.createElement('div');
            div.className = `memory-block ${block.occupied ? 'occupied' : 'free'}`;
            
            // Altura dinámica: mínimo 35px, máximo proporcional
            let heightPct = (block.size / memoryTotalLimit) * 100;
            div.style.flexGrow = block.size; // Flex grow usa el tamaño como proporción
            
            div.innerHTML = `
                <div class="block-info">
                    <span>${block.occupied ? '🔒 ' + block.processId : '🟢 Libre'}</span>
                    <span>${block.size} KB</span>
                </div>
            `;
            container.appendChild(div);
        });
    }

    function updateStats(prefix, blocks, stats) {
        let used = 0;
        let freeTotal = 0; // Fragmentación externa total
        let maxFree = 0;
        let freeCount = 0;

        blocks.forEach(b => {
            if (b.occupied) {
                used += b.size;
            } else {
                freeTotal += b.size;
                freeCount++;
                if (b.size > maxFree) maxFree = b.size;
            }
        });

        let utilPct = ((used / memoryTotalLimit) * 100).toFixed(1);

        document.getElementById(`${prefix}-util`).innerText = `${utilPct}%`;
        document.getElementById(`${prefix}-frag`).innerText = `${freeTotal} KB`;
        document.getElementById(`${prefix}-free-count`).innerText = `${freeCount}`;
        document.getElementById(`${prefix}-max-free`).innerText = `${maxFree} KB`;
        document.getElementById(`${prefix}-fails`).innerText = `${stats.fails}`;
    }

    function determineWinner() {
        const div = document.getElementById('winner-section');
        const text = document.getElementById('winner-text');
        const reason = document.getElementById('winner-reason');
        div.style.display = 'block';

        // Lógica de Ganador
        // 1. Menos Fallos es lo más importante
        if (bfStats.fails < wfStats.fails) {
            text.innerText = "GANADOR: BEST FIT";
            reason.innerText = "Best Fit logró asignar más procesos (menos fallos). Al dejar huecos pequeños, preservó los bloques grandes para procesos futuros.";
            div.style.borderColor = "var(--success-color)";
        } else if (wfStats.fails < bfStats.fails) {
            text.innerText = "GANADOR: WORST FIT";
            reason.innerText = "Worst Fit logró asignar más procesos. En este escenario específico, romper los bloques grandes fue beneficioso.";
            div.style.borderColor = "var(--danger-color)";
        } else {
            // Empate en fallos -> Ver Fragmentación (quien tiene bloques más grandes disponibles suele ser mejor)
            const bfMax = parseInt(document.getElementById('bf-max-free').innerText);
            const wfMax = parseInt(document.getElementById('wf-max-free').innerText);

            if (bfMax > wfMax) {
                text.innerText = "VENTAJA TÉCNICA: BEST FIT";
                reason.innerText = "Misma cantidad de fallos, pero Best Fit conservó un bloque libre más grande, lo cual es mejor para procesos futuros pesados.";
                div.style.borderColor = "var(--success-color)";
            } else if (wfMax > bfMax) {
                text.innerText = "VENTAJA TÉCNICA: WORST FIT";
                reason.innerText = "Misma cantidad de fallos, pero Worst Fit dejó un bloque disponible más grande (caso raro en particionamiento dinámico).";
                div.style.borderColor = "var(--danger-color)";
            } else {
                text.innerText = "EMPATE ABSOLUTO";
                reason.innerText = "Ambos algoritmos se comportaron idénticamente.";
                div.style.borderColor = "#666";
            }
        }
    }
</script>

<footer>
    Astrit Airan Cetzal Cetzal - Sistemas Operativos - 14/02/2026 - Profesor: Jorge Javier Pedrozo Romero - Tecnológico de Software
</footer>

</body>
</html>


''''
