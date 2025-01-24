<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Examen de Conocimientos</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #ffffff;
            position: relative;
            user-select: none;
            -webkit-user-select: none;
            background-image: url('https://static.vecteezy.com/ti/vetor-gratis/p1/14477343-uso-de-icone-de-drone-em-qualquer-projeto-gratis-vetor.jpg');
            background-size: 80%;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
        }

        .container {
            width: 90%;
            max-width: 700px;
            background-color: #fff;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            padding: 20px;
            box-sizing: border-box;
            position: relative;
            transition: box-shadow 0.3s ease;
        }

        .container:hover {
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
        }

        header {
            background-color: #043870;
            color: white;
            text-align: center;
            padding: 20px;
            border-radius: 10px;
        }

        header h1 {
            margin: 0;
            font-size: 1.4rem;
        }

        .section {
            padding: 20px;
            display: none;
        }

        .section.active {
            display: block;
        }

        .form-group {
            margin-bottom: 12px; 
        }

        .form-group label {
            display: block;
            margin-bottom: 4px; 
            font-weight: 500;
            color: #555;
            font-size: 0.85rem;
        }

        .form-group input {
            width: 100%;
            padding: 10px; 
            border: 1px solid #ddd;
            border-radius: 12px;
            font-size: 1rem;
            box-sizing: border-box;
            background-color: #f9f9f9;
            transition: border-color 0.3s ease;
        }

        .form-group input:focus {
            border-color: #043870;
            outline: none;
        }

        button {
            background-color: #043870;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 12px;
            font-size: 1rem;
            cursor: pointer;
            transition: background-color 0.3s;
            width: 100%;
        }

        button:hover {
            background-color: #0b9627;
        }

        .question-card {
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
            display: block;
            gap: 15px;
            transition: box-shadow 0.3s ease;
        }

        .question-card:hover {
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }

        .question-card p {
            font-size: 0.9rem;
            margin-bottom: 15px;
            color: #333;
        }

        .question-card label {
            font-size: 1rem;
            display: block;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #ddd;
            background-color: #fff;
            margin-bottom: 12px;
            cursor: pointer;
            transition: background-color 0.3s, border-color 0.3s;
        }

        .question-card label:hover {
            background-color: #f1f1f1;
            border-color: #043870;
        }

        .question-card input[type="radio"] {
            margin-right: 10px;
        }

        #timer {
            font-size: 1.1rem;
            color: #0d0101cd;
            font-weight: bold;
            position: fixed;
            top: 20px;
            right: 20px;
            background-color: #9e9a98b1;
            padding: 12px 20px;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            transition: box-shadow 0.3s ease;
        }

        #timer:hover {
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
        }

        .results-box {
            background-color: #f9f9f9;
            border: 1px solid #ddd;
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
        }

        .results-box h2 {
            margin-top: 0;
            font-size: 1.2rem;
        }

        @media (max-width: 600px) {
            .question-card p {
                font-size: 0.85rem;
            }

            .question-card label {
                font-size: 0.8rem;
            }

            button {
                padding: 10px;
                font-size: 1rem;
            }
        }

        .logo-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 0; 
        }

        .logo {
            width: 100px;
            height: auto;
        }
    </style>
</head>
<body>
    <div class="logo-container">
        <img src="c:\Users\JUAN CAMILO SERNA\Pictures\Captura de pantalla 2025-01-17 160624.png" alt="Logo" class="logo">
    </div>

    <div id="timer">Tiempo restante: <span id="contador">40:00</span></div>
    <div class="container">
        <header>
            <h1>Grupo Drones y Movilidad Urbana Aérea</h1>
            <p>Secretaría de Autoridad Aeronáutica</p>
        </header>

        <div id="claveAcceso" class="section active">
            <div class="form-group">
                <label for="clave">Ingrese la contraseña</label>
                <input type="text" id="clave" placeholder="Escriba la contraseña">
            </div>
            <button onclick="verificarClave()">Verificar Clave</button>
        </div>

        <div id="datosEstudiante" class="section">
            <div class="form-group">
                <label for="nombre">Nombre Completo</label>
                <input type="text" id="nombre" placeholder="Escriba su nombre completo">
            </div>
            <div class="form-group">
                <label for="documento">Número de Documento y Ciudad de expedición</label>
                <input type="text" id="documento" placeholder="Escriba su número de documento">
            </div>
            <button onclick="iniciarExamen()">Comenzar Examen</button>
        </div>

        <div id="examen" class="section">
            <form id="formularioExamen">
            </form>
            <button onclick="mostrarResultados()">Finalizar Examen</button>
        </div>

        <div id="resultados" class="section">
            <div class="results-box">
                <h2>Resultados del Examen</h2>
                <p><strong>Nombre:</strong> <span id="resultNombre"></span></p>
                <p><strong>Número de Documento:</strong> <span id="resultDocumento"></span></p>
                <p><strong>Respuestas Correctas:</strong> <span id="resultCorrectas"></span> de <span id="totalPreguntas"></span></p>
                <p><strong>Puntaje:</strong> <span id="resultPuntaje"></span>%</p>
                <p><strong>Fecha y Hora:</strong> <span id="fechaHora"></span></p>
            </div>
        </div>
    </div>

    <script>
        const fechaActual = new Date();
        const fechaHoraFormateada = fechaActual.toLocaleString();
        document.getElementById('fechaHora').textContent = fechaHoraFormateada;
    </script>

    <script>
        const clavesValidas = ["grupodrones2025**", "secretariadeautoridad2025**", "gdmua4386**", "inglaterra2025**", "soporte2025**", "autoridadaeronautica2025**", "drones2025**", "aviacionnotripulada**"]; 

        function verificarClave() {
            const claveIngresada = document.getElementById('clave').value;

            if (clavesValidas.includes(claveIngresada)) {
                document.getElementById('claveAcceso').classList.remove('active');
                document.getElementById('datosEstudiante').classList.add('active');
            } else {
                alert("Clave incorrecta. Intente nuevamente.");
            }
        }

        function iniciarExamen() {
            document.getElementById('datosEstudiante').classList.remove('active');
            document.getElementById('examen').classList.add('active');
        }

        function mostrarResultados() {
            document.getElementById('examen').classList.remove('active');
            document.getElementById('resultados').classList.add('active');
        }
    </script>
</body>
</html>


    <script>
        let nombreEstudiante = "";
        let documentoEstudiante = "";
        let puntajeTotal = 0;
        const DURACION_EXAMEN = 40 * 60; 
        let tiempoRestante = DURACION_EXAMEN;
        let temporizador;

       
        const preguntas = {
            derechoAereo: [
                
            { pregunta: "La seguridad operacional en el espacio aéreo y la seguridad de las personas en tierra y su privacidad, son aspectos relevantes que se tienen en cuenta para el establecimiento de las Normas para aeronaves no tripuladas a nivel mundial.  Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué requisitos son básicos y se requiere cumplir para volar un UAS en el espacio aéreo de un país?", opciones: ["Ningún permiso ni licencia, ya que son no tripulados.", "Un registro del UAS y el cumplimiento de las regulaciones específicas.", "Sólo se pueden operar en áreas deshabitadas, sin regulaciones adicionales."], respuesta: 1 },
            { pregunta: "¿Cuál es uno de los propósitos principales de las regulaciones de UAS?", opciones: ["Restringir el acceso público a la tecnología de UAS.", "Garantizar la seguridad de las operaciones y proteger la integridad del espacio aéreo.", "Facilitar la adquisición de UAS por parte de particulares sin restricciones."], respuesta: 1 },
            { pregunta: "¿Cuál es la sigla del Organismo de Autoridad de la Aviación Civil a nivel mundial?", opciones: ["FAA.", "EASA.", "OACI."], respuesta: 2 },
            { pregunta: "¿Cuál es la sigla del Organismo de Autoridad de la Aviación Civil en Colombia?", opciones: ["AAAE.", "UAEAC.", "CIAC."], respuesta: 1 },
            { pregunta: "La normatividad aeronáutica válida en Colombia se encuentra compilada en:", opciones: ["NAN  Normatividad Aeronáutica Nacional.", "RAC  Reglamentos Aeronáuticos de Colombia.", "LAR  Reglamentos Aeronáuticos Latinoamericanos."], respuesta: 1 },
            { pregunta: "¿Cuál de las siguientes normas aplicables en Colombia regulan la actividad aérea con aeronaves no tripuladas?", opciones: ["RAC 100.", "RAC 61.", "Parte 101 y 102 de la OACI."], respuesta: 0 },
            { pregunta: "¿Cuál es el objetivo principal del marco normativo de la aviación mundial?", opciones: ["Ordena implementar la seguridad operacional más elevada posible para todos los estados sean signatarios o no.", "Lograr y conservar el nivel uniforme de seguridad operacional más elevado posible.", "Que los diferentes estados signatarios cumplan a cabalidad las reglamentaciones internacionales emitidas por la OACI."], respuesta: 1 },
            { pregunta: "El Objetivo del marco normativo emitido por la OACI en sus 19 Anexos, radica específicamente en dar pautas de la reglamentación internacional aplicable a los estados signatarios, los cuales tienen que cumplir de forma obligatoria al pie de la letra. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Cuál es el objetivo general y principal de los RAC?", opciones: ["Dar pautas para el desarrollo de toda la aviación en Colombia.", "Sugerir diferentes formas de operación aérea para organizar las actividades entre Aviación Civil y Aviación de Estado.", "Regular la actividad aérea civil en el país y proporcionar una base sólida y legal en las actuaciones administrativas y operativas propias de la aviación."], respuesta: 2 },
            { pregunta: "¿Qué se entiende por la Sigla SARP’s?", opciones: ["Recopilación de Procedimientos,  Normas y Métodos Ordenados para la Aviación Civil Internacional.", "Énfasis para la aplicación de Procedimientos, Normas y Métodos Asistidos para la Aviación Civil.", "Estudio de Procedimientos y Redacción de Normas y Métodos Recomendados para la Aviación Civil Internacional."], respuesta: 2 },
            { pregunta: "¿Cuál es la relación entre las SARP´s de la OACI y las regulaciones nacionales de aviación? ", opciones: ["Las SARP’s reemplazan por completo las regulaciones nacionales.", "Las SARP’s son recomendaciones y los estados pueden adoptarlas de manera voluntaria. ", "Las SARP’s se aplican sólo a las aeronaves militares."], respuesta: 1 },
            { pregunta: "La Reglamentación Aeronáutica Colombiana (RAC-100) se realizó en concordancia con los SARP’s emitidos por la OACI, y está determinada para mantenimiento y preservación de la seguridad operacional con los más altos estándares.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Cuál de las siguientes legislaciones colombianas no requiere ser observada para el desarrollo de la Aviación No Tripulada en el país? ", opciones: ["Código Nacional de Policía y Convivencia: Ley 1801/2016.", "Código Nacional de Tránsito: Ley 769 de 2002.", "Código de Comercio de Colombia: Decreto 410/1971."], respuesta: 1 },
            { pregunta: "El uso indebido o irresponsable de aeronaves no tripuladas, podrá ser sancionado únicamente por la Autoridad Aeronáutica competente. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Qué aspecto importante relacionado con la aviación, debemos conocer sobre el Código del Comercio?", opciones: ["Los detalles de cómo regular nuestra actividad económica.", "Las cauciones que se deben formalizar para la actividad aérea comercial con aeronaves de peso inferior a 1000 kilogramos.", "Los deberes y Obligaciones contractuales como Explotador UAS."], respuesta: 1 },
            { pregunta: "El Código del Comercio Indica que solamente aeronaves con peso superior a 1000 kilogramos deben constituir una caución (póliza) que garantice la indemnización por eventos aéreos (incidentes o accidentes) de los cuales se genere muerte, lesiones personales, daños y perjuicios a terceras personas. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "El Código del Comercio determina que para aeronaves con peso máximo hasta de 1000 kilogramos, se debe establecer una caución para la Indemnización de terceros en caso de muerte o lesiones personales.  Este valor es el equivalente a:", opciones: ["30.300 kilogramos de oro puro.", "33.333 gramos de oro puro.", "33.333 libras de oro puro."], respuesta: 1 },
            { pregunta: "En el proceso de autorización de solicitudes de vuelo UAS, la Aerocivil acepta pólizas RCE de aseguradoras internacionales por periodos inferiores a un año. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué condiciones o alcances debe tener una póliza internacional, para que sea aceptada por la Aerocivil en el proceso de autorización de solicitudes de vuelo de Aeronaves no tripuladas?", opciones: ["Debe indicar claramente que tiene cobertura en todo el territorio colombiano y que el beneficiario con la cobertura sea el mismo Explotador UAS inscrito.", "Indiquen las Horas y días de la cobertura.", "Debe traer una certificación de la empresa aseguradora donde detalle que las condiciones de la póliza están en conformidad con la Legislación del país donde se expide el documento."], respuesta: 0 },
            { pregunta: "Para vuelos realizados con aeronaves no tripuladas en la categoría “abierta” la Aerocivil ordena que los operadores de UAS cuenten con una póliza de cubrimiento por daños a terceros producidos como consecuencia de una operación aérea.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "De acuerdo con lo estipulado en la Ley 1801/2016 “Código Nacional de Policía y Convivencia”, las autoridades competentes y actividad de policía podrán suspender e incautar una aeronave no tripulada, cuando con ella se estén infringiendo normas legales. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Cuál de las siguientes opciones es la más acertada en relación con la privacidad al operar un UAS?", opciones: ["No existe ninguna consideración de privacidad, ya que no tienen tripulación a bordo.", "Debe obtenerse el consentimiento por escrito de todas las personas que se encuentren en la cercanía antes de operarlo.", "Respetar la privacidad de las personas y evitar la vigilancia no autorizada."], respuesta: 2 },
            { pregunta: "De acuerdo con lo estipulado en la Ley 1523/2012 Sistema Nacional de Gestión del Riesgo de Desastres, un piloto de UAS que realice vuelos de asistencia AID con aeronaves no tripuladas en el sitio del desastre, debe ostentar la capacitación requerida y suficiente para estar desarrollando esta labor.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué es el PMU?  ", opciones: ["Puesto de Mando Unificado. Hace referencia al lugar físico donde se concentra e implementa la coordinación para asuntos operacionales de un determinado incidente o evento. ", "Puesto Mandatorio Universal. Se refiere al lugar físico donde se concentra e implementan los vehículos y ayudas humanitarias para asuntos de un determinado incidente o evento.", "Es la Jerarquía de los organismos estatales que se convocan para solucionar asuntos operacionales de un determinado incidente o evento."], respuesta: 0 },
            { pregunta: "De acuerdo con la Ley 356/1994, “Estatuto de Seguridad y Vigilancia Privada” Toda empresa de vigilancia que realice actividades con UAS, requiere:", opciones: ["Pedir permiso de operación aérea a la Superintendencia de seguridad y vigilancia privada.", "Tener un permiso de la Superintendencia de seguridad y vigilancia privada para el empleo de facilidades tecnológicas aprobadas.", "Que el gerente General haya realizado un curso de operación de aeronaves no tripuladas."], respuesta: 1 },
            { pregunta: "Una empresa de seguridad y vigilancia privada que emplee UAS en el desarrollo de su objeto social, debe tener el debido permiso expedido por la Superintendencia de Seguridad y Vigilancia Privada para su uso.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "A los pilotos UAS que violen o incumplan las normas establecidas en los RAC, les aplica lo dispuesto en el RAC 13 “Régimen sancionatorio”. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué significa la Sigla “OACI”?", opciones: ["Organización Internacional de Aviación Civil.", "Conglomerado de las Naciones para la Aviación Civil.", "Convención de Aviación Civil Internacional."], respuesta: 0 },
            { pregunta: "La OACI tiene potestad sobre los Estados miembros para realizar acciones punitivas  por incumplimiento a las normas aeronáuticas proferidas por ellos. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "De acuerdo al RAC 91, es adecuado emplear sustancias como Alcohol y Alucinógenos, ya que éstas no representan un uso problemático en las actividades de vuelo.  Este postulado es:", opciones: ["Verdadero ", "Falso",], respuesta: 1 },
            { pregunta: "En una  aeronave no tripulada, no es permitido realizar trabajos en la modificación del diseño original de la aeronave, que afecten el centro de gravedad o las características de vuelo de dicha aeronave sin permiso del fabricante.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "Los documentos de la OACI nombrados Partes 101 y 102 del 2020,  establecen un modelo de reglamentación para UAS de Categoría abierta y Categoría específica que sugiere la OACI, para que  adopten los Estados miembros para el control de este tipo de aviación.  Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué significa la sigla UAEAC?", opciones: ["Agencia Administrativa Estatal de Aerodinámica Civil ", "Unidad Administrativa Especial de Aeronáutica Civil.", "Ninguna de las anteriores."], respuesta: 1 },
            { pregunta: "¿Cuáles de los siguientes, es un documento que ha publicado la Aerocivil para el control de la Aviación no tripulada en Colombia?", opciones: ["Circular 008/2014 (Requisitos Generales de Aeronavegabilidad y operaciones para RPAS).", "Resolución 02401/2017 -Apéndice 11 RAC 90- (Operación de Sistemas de Aeronaves Tripuladas UAS).", "Ninguna de las anteriores"], respuesta: 2 },
            { pregunta: "¿Qué tipo de sanciones se pueden imponer la Aerocivil por el incumplimiento de las regulaciones para UAS?", opciones: ["Multas económicas e  incluso acciones legales.", "Nada, ya que las regulaciones de UAS son puramente voluntarias.", "Pérdida de la licencia para conducirlos."], respuesta: 0 },
            { pregunta: "¿Qué RAC  indica el regimen sancionatorio aplicado a los diferentes Explotadores aéreos por cometer actos ilícitos o que vayan en contra de los Reglamentos Aeronáuticos de Colombia?", opciones: ["RAC 91", "RAC 13", "RAC 141"], respuesta: 1 },
            { pregunta: "¿Cuál de las siguientes opciones constituye una violación expresa de las normas?", opciones: ["Volar en los parámetros de autorización emitidos por la Autoridad Aeronáutica.", "Volar desconociendo el espacio aéreo en donde estoy volando.", "Extralimitar las restricciones e indicaciones descritas en la autorización de vuelo."], respuesta: 2 },
            { pregunta: "De acuerdo con el RAC 13 “Infracciones Aeronáuticas” ¿Cuáles son los dos tipos de infracciones aeronáuticas que se le pueden imponer a un Explotador UAS que viole la reglamentación?", opciones: ["Infracciones generales e infracciones particulares", "Infracciones de orden técnico e infracciones de orden administrativo.", "Infracciones de la norma y Sanciones del procedimiento"], respuesta: 1 },
            { pregunta: "Las Sanciones aeronáuticas impuestas por la Aerocivil, que tengan relación directa con acciones u omisiones que atenten contra la seguridad aérea y pongan en peligro la seguridad operacional de las aeronaves está considerada como una sanción:", opciones: ["De Orden nacional", "De Orden Técnico.", "De Orden Gerencial"], respuesta: 1 },
            { pregunta: "La Policía Nacional puede suspender o impedir todas aquellas actividades con UAS o incautar los dispositivos de aeronaves no tripuladas, cuando con ellos no se estén violando ninguna de las normas o leyes legales del país. Este postulado es:", opciones: ["VERDADERO", "Falso",], respuesta: 1 },
            
            ],
            rac100: [
            { pregunta: "¿Cuál es el título de la norma RAC 100?", opciones: ["Generalidades de las aeronaves no tripuladas - UAS.", "Operación de sistemas de aeronaves no tripuladas - UAS.", "Reglamento de utilización de aeronaves no tripuladas - UAS."], respuesta: 1 },
            { pregunta: "¿A quiénes aplica la reglamentación de la norma RAC 100?", opciones: ["A toda persona natural o jurídica en el país que realice operaciones con UAS con fines comerciales únicamente y para los CIAC y aeroclubes que tengan previsto prestar servicios de capacitación y entrenamiento en la operación de UAS.", "A aeronaves no tripuladas que realicen operaciones en territorio colombiano; y para cualquier tipo de centro de instrucción que tenga previsto prestar servicios de capacitación y entrenamiento en la operación de UAS.", "A toda persona natural o jurídica, pública o privada, nacional o extranjera, que planee realizar operaciones con UAS sin ánimo de lucro, con fines comerciales y a todo CIAC que tenga previsto prestar servicios de instrucción en la operación de UAS."], respuesta: 2 },
            { pregunta: "La norma RAC 100 contiene, entre otros, los requisitos para: ", opciones: ["Los impuestos legales para los UAS y equipos tecnológicos asociados a ellas.", "La obtención del certificado de idoneidad como piloto UAS. ", "La obtención del permiso de funcionamiento de un centro de instrucción de UAS."], respuesta: 1 },
            { pregunta: "¿Qué ventaja tiene una UA registrada?", opciones: ["Se puede operar dentro de la legalidad.", "Son las únicas que pueden volar a 500 ft AGL.", "Son las únicas que deben cumplir los RAC, en general."], respuesta: 0 },
            { pregunta: "La bitácora de vuelo es un documento donde se lleva el histórico de los vuelos realizados por una persona en formato libre, el cual debe contener como mínimo los siguientes datos: nombre del piloto UAS, fecha del vuelo, hora de despegue, tiempo total de vuelo y modelo del equipo UAS registrado. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "El certificado de idoneidad de piloto UAS es un documento expedido por la Aerocivil por medio del cual se otorgan a una persona privilegios para operar UAS en la categoría específica. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "El libro de vuelo y mantenimiento de una aeronave no tripulada es un documento de cada una de las aeronaves no tripuladas registradas ante la Aerocivil, en el cual se registran todos los datos, condiciones y reportes de vuelo, así como la información correspondiente a problemas de funcionamiento y trabajos de mantenimiento realizados a cada una de ellas. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Cuál de las siguientes postulaciones  hace parte de la deficnición del observador UA?", opciones: ["Es una persona común y corriente quien, mediante observación visual directa de la aeronave no tripulada, ayuda al piloto UAS en la realización segura del vuelo, especialmente en operaciones VLOS.", "Es una persona capacitada y competente, quien, mediante observación visual directa de la aeronave no tripulada, ayuda al piloto UAS en la realización segura del vuelo, especialmente en operaciones VLOS y EVLOS.", "Es cualquier persona designada por el Explotador UAS, para que acompañe al piloto de UAS en la realización de un vuelo."], respuesta: 1 },
            { pregunta: "¿Qué significa la sigla VLOS?", opciones: ["Visual Line of Sight / Visibilidad en linea de vista.", "Virtual Line of Sight / Visibilidad en linea de vista virtual.", "Visual Line Operation Safety / Visibilidad en linea de vista de operación segura."], respuesta: 0 },
            { pregunta: "¿Qué significa la sigla BVLOS?", opciones: ["Beyond Virtual Line of Sight / Visibilidad  más allá de la línea virtual de vista.", "Basic Visual Line Operation Safety / Visibilidad en línea basica de operación segura.", "Beyond Visual Line of Sight / Visibilidad más allá de la linea de vista."], respuesta: 1 },
            { pregunta: "¿Qué significa la sigla EVLOS?", opciones: ["Eventual Visual Line of Sight / Visibilidad en línea de vista eventual.", "Extended Visual Line of Sight / Visibilidad en línea de vista extendida.", "Extreme Visual Line Operation Safety / Visibilidad en linea de operación extrema segura. "], respuesta: 1 },
            { pregunta: "En las operaciones en condiciones visuales VLOS está permitido el uso de instrumentos electrónicos, mecánicos, electromagnéticos, ópticos y/o electroópticos para no perder de vista la aeronave en vuelo. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "La definición de EVLOS es: Operación más allá de la línea de vista, en la cual el piloto UAS opera un UAS sin mantener contacto visual directo con la UA. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "Un sistema tecnológico de gestión de vuelo UAS, es aquella plataforma que integra, entre otras, facilidades tecnológicas, la gestión en tiempo real la operación de la aeronave no tripulada, garantizando el control operacional del vuelo sobre un sistema de información geográfica  GIS. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "El manual de control de mantenimiento *MCM* es el mismo manual del fabricante. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "Se denomina operador UAS:", opciones: ["A la persona que manipula los mandos de control de una UA en categoría abierta, quien no cuenta con certificado de idoneidad como piloto UAS.", "A la persona que manipula los mandos de control de una UA en cualquier categoría y quien conoce a profundidad el manual del usuario de la aeronave.", "En la norma RAC 100 no se emplea el término “operador UAS”."], respuesta: 0 },
            { pregunta: "¿Qué significa la sigla FPV?", opciones: ["Follow Plane View / Seguimiento del plano visual.", "Facilidad para volar.", "First Person View / Vista en primera persona."], respuesta: 2 },
            { pregunta: "La sigla ZNVD significa Zona Norte para Vuelo de Drones. Este postulado es: ", opciones: ["Verdadero.", "falso.",], respuesta: 1 },
            { pregunta: "¿Qué tipo de aeronaves no tripuladas deben registrarse en categoria abierta ante la Aerocivil?", opciones: ["Todas aquellas cuyo PMBO sea 250 gramos.", "Todos aquellos sistemas de aeronaves no tripuladas en los que la aeronave tenga un peso igual o superior a 200 gramos.", "Solamente aquellas aeronaves no tripuladas que sean empleadas para actividades comerciales o profesionales."], respuesta: 1 },
            { pregunta: "En el caso en que se celebren contratos de arrendamiento sobre un UAS, la responsabilidad operacional recaerá sobre el arrendatario, dado que estos acuerdos lo convierten en explotador UAS.", opciones: ["Verdadero, siempre y cuando el contrato sea puesto en conocimiento del asunto a la Aerocivil.", "Verdadero, sin condiciones.", "Falso, el propietario siempre responderá por lo operacional."], respuesta: 0 },
            { pregunta: "Es obligatorio que toda UA registrada tenga una etiqueta de identificación y que contenga datos mínimos del propietario o explotador UAS. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué es la categoría “abierta”?", opciones: ["Corresponde a las aeronaves no comerciales y con un PMBO de hasta 15 kilogramos, incluyendo todos los elementos que estén a bordo en el despegue.", "Corresponde a las operaciones aéreas comerciales y con un PMBO de hasta 25 kilogramos, incluyendo todos los elementos que estén a bordo en el despegue.", "Corresponde a las operaciones aéreas no comerciales y con un PMBO de hasta 25 kilogramos, incluyendo todos los elementos que estén a bordo en el despegue."], respuesta: 2 },
            { pregunta: "¿Cuál de las siguientes expresiones define mejor la categoría “específica”, según el RAC 100?", opciones: ["Corresponde a las operaciones con una UA con finalidades comerciales, indiferente de su peso, y hasta 250 kilogramos de peso (masa) bruto en el despegue incluyendo todos los elementos a bordo.", "Corresponde a las operaciones de vuelo con una UA empleada en actividades diferentes a las comerciales y hasta 250 kilogramos de peso general, incluyendo todos los elementos a bordo.", "Corresponde a las aeronaves no tripuladas que se empleen en actividades comerciales, desde 25 Kilogramos y hasta 250 kilogramos de peso máximo, incluyendo todos los elementos a bordo."], respuesta: 0 },
            { pregunta: "La Categoría Certificada corresponde a las operaciones de sistemas de aeronaves remotamente piloteadas RPAS, cuyas condiciones de vuelo y fines de utilización son similares a las realizadas en la aviación tripulada. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "Planear el desarrollo de la operación, conocer las diferentes clasificaciones del espacio aéreo, operar un UA de manera responsable y segura, operar la UA dentro de las limitaciones establecidas por el fabricante y garantizar que la UA y sus correspondientes sistemas se encuentran en condiciones aptas para realizar un vuelo seguro, son algunas de las responsabilidades tanto de un operador UA, como de un piloto a distancia UA. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "La distancia horizotal máxima permitida para operar una UA en VLOS es:", opciones: ["500 mts.", "750 mts.", "500 ft."], respuesta: 2 },
            { pregunta: "El RAC 100 permite que las operaciones aéreas con UAS se puedan efectuar por encima de la primera capa de nubes, siempre y cuando estas se encuentren a no más de 500 ft de altura.", opciones: ["Falso", "Verdadero",], respuesta: 0 },
            { pregunta: "El RAC 100 limita la cantidad de observadores UAS a uno solo por operación aérea, cuando se realicen operaciones en condición EVLOS. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "Para la categoría específica, la condición de vuelo nocturno la puede realizar cualquier piloto UAS, siempre y cuando tenga al día su certificado de aprobación del curso básico de piloto UAS en un CIAC autorizado por la Aerocivil. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Cuáles de las siguientes postulaciones son condiciones a cumplir al  realizar actividades de vuelo en zona urbana? /1-Límite horizontal de 30 m en cercanía a una persona ajena a la operación./2-No se puede volar por encima de 400 ft./3-Únicamente en condiciones VLOS.", opciones: ["Solo el  numeral 3 es correcto", "Los numerales 1 y 3  son correctos ", "Los numerales 1, 2 y 3 son correctos"], respuesta: 2 },
            { pregunta: "Cuales de los siguientes Vuelos Especiales con UAS, son considerados dentro del RAC 100:", opciones: ["Vuelo nocturno, en zona urbana, autónomo, para demostraciones comerciales o de capacidad tecnologica UAS, en competencias y actividades deportivas.", "Vuelo acrobático, en zona rural, automático, para demostraciones y bajo techo.", "Vuelo pesado, urbano, acrobático, bajo techo y de paisajismo."], respuesta: 0 },
            { pregunta: "De acuerdo con el RAC 100 para una inspección operacional , todo operador UA debe tener siempre a la mano unicamente certificado de inscripción de la UA ante la Aerocivil y copia del libro de vuelo y mantenimiento. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Con respecto al consumo de sustancias que perjudiquen las facultades humanas en su desempeño, la norma establece que no se podrá operar una UA, estando bajo su influencia, o dentro de las 36 horas siguientes a su consumo, bien sea de alcohol u otra sustancia psicoactiva. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Las sanciones que expresamente detalla el RAC 100 por la comisión de un acto prohibido o por incumplimiento de lo descrito en ella acarreará entre otras:", opciones: ["Suspender o revocar cualquier certificado o autorización aprobado previamente por la Aerocivil o negar cualquier solicitud elevada ante ella. ", "Iniciar actos administrativos sancionatorios según lo dispuesto en el RAC 13 sin perjuicio de la responsabilidad civil, penal, policiva o administrativa inherente al hecho. ", "Las dos opciones son correctas."], respuesta: 2 },
            { pregunta: "En caso de un evento donde por la operación de la UA una persona haya resultado lesionada, el explotador está obligado a reportarlo a la autoridad de investigación de accidentes de aviación. Con relación a esta afirmación, podemos decir que:", opciones: ["Si, esto es completamente obligatorio .", "No es obligatorio, se realiza si el usuario ve la necesidad de reportarlo.", "Sí se debe reportar, pero solo en el caso de requerirse para adelantar la gestión para el cobro de la póliza."], respuesta: 0 },
            { pregunta: "Teniendo en cuenta que las aeronaves no tripuladas que realicen operaciones aéreas en la categoría abierta no requieren pedir permiso ante la Aerocivil, el RAC 100 no contempla las especificaciones requeridas y las reglas de operación para esta categoría. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Las condiciones específicas de operación con UAS en Colombia según el RAC 100, en categoría abierta y categoría específica, son, entre otras:", opciones: ["Altura máxima 400 ft., VLOS 750 m, VMC, separación mínima de personas 30 m, consulta de espacios aéreos.", "Altura máxima 400 m, VLOS 500 ft, IMC, separación mínima de personas a 300 m, consulta de meteorología.", "Ninguna de las anteriores, para la categoría abierta no se exigen condiciones de operación."], respuesta: 0 },
            { pregunta: "¿Cuáles de las siguientes son consideradas restricciones para la operación de la categoría abierta? /1-Volar en zonas restringidas, prohibidas, peligrosas, ZNVD y BVLOS./2-Actividades de transporte, delivery o comerciales./3-Actividades recreativas o de deporte./4-Volar en zonas despobladas o determinadas para el uso de aeromodelos./5-Volar en cercanía de: Presidente, unidades militares y aeródromos.", opciones: ["Los numerales 1, 2 y 3 con correctos", "Los numerales 3, 4 y 5 son correctos", "Los numerales 1, 2 y 5  son correctos"], respuesta: 2 },
            { pregunta: "Un operador de una UA en categoría abierta deberá demostrar capacitación, entre otras, de las siguientes áreas de conocimiento:", opciones: ["Manual de operación del fabricante, conocimiento de las UA y conciencia situacional.", "Procedimientos de operación y seguridad del fabricante, cuidados y mantenimiento, aerodinámica aplicada y conocimiento de las UA, meteorología y navegación aplicada, actuación humana, distracciones y conciencia situacional.", "Solamente basta con conocer el funcionamiento de cada botón y palancas de control remoto de la aeronave."], respuesta: 1 },
            { pregunta: "Las consideraciones que indica el RAC100 para una operación en categoría específica son:", opciones: ["Que la operación sea realizada para vuelos de hobby, recreación o deporte.", "Que la operación sea realizada con fines comerciales y que la operación exceda las condiciones y limitaciones dispuestas para la categoría abierta.", "Que el piloto quiera realizar operaciones en esta categoría, por las bondades que ofrece."], respuesta: 1 },
            { pregunta: "Las operaciones de vigilancia y seguridad privada con UAS las puede realizar cualquier persona en la Categoría Abierta, siempre y cuando lo haga sin ánimo de lucro, en apoyo a una labor social y en coordinación directa con el cuadrante de la Policía Nacional que opera en el sector. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Las actividades de instrucción propia de los CIAC, aunque están catalogadas como operaciones de la categoría específica, no requieren cumplir el total de los formalismos relacionados para esta categoría, teniendo en cuenta que se encuentran bajo condiciones muy controladas de seguridad. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Para que un Explotador UAS pueda realizar una operación aérea de conformidad con las disposiciones legales del RAC 100, es requisito : ", opciones: ["Contar con un Certificado de Explotador UAS expedido por la Aerocivil.", "No haber inscrito ante la Aerocivil los equipos especiales que empleará.", "No es necesario contar con la póliza de responsabilidad civil."], respuesta: 0 },
            { pregunta: "Para que un Explotador UAS pueda realizar una operación aérea de conformidad con las disposiciones legales del RAC 100 es requisito: ", opciones: ["Es opcional contar con el manual de operaciones y del fabricante.", "Es voluntario realizar el respectivo análisis de riesgos de seguridad operacional.", "Obtener las autorizaciones de vuelo correspondientes."], respuesta: 2 },
            { pregunta: "En caso de ser requerido por un Explotador UAS realizar modificaciones estructurales a una de sus UA, lo podrá hacer para brindar un mejor servicio a sus clientes. El anterior postulado es:", opciones: ["Falso, nunca se puede hacer.", "Verdadero, siempre y cuando se tenga la respectiva autorización por parte de la Aerocivil.", "Verdadero, siempre y cuando estén expresamente aprobadas por el fabricante."], respuesta: 2 },
            { pregunta: "Dado el caso en que el piloto automático de la UA que se está volando presente fallas es necesario:", opciones: ["Suspender la operación aérea, para no incurrir en un accidente o incidente.", "Deshabilitar el piloto automático del UA y continuar en vuelo manual.", "Terminar rápidamente el trabajo que se está realizando, para no perder tiempo."], respuesta: 0 },
            { pregunta: "Las acciones de mitigación de riesgos procuradas por el explotador UAS en cuanto a la pérdida de la conexión de comunicación entre la UA y la estación en tierra deberán enfocarse en minimizar los daños en caso de falla del enlace C2; estas acciones deben estar debidamente consignadas en el MO. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "Para el caso específico de un UAS de 60 kg de PMBO utilizado en operaciones de aspersión agrícola en beneficio de un predio de su mismo propietario, su piloto debe: ", opciones: ["Pedir permiso a la Aerocivil para ejecutar los vuelos.", "Contar con el certificado de idoneidad y las adiciones correspondientes para el caso específico.", "Contar con la matriz de análisis y mitigación de riesgos."], respuesta: 1 },
            { pregunta: "Para el caso específico de un UAS de 60 kg de PMBO utilizado en operaciones de aspersión agrícola en beneficio de un predio de su mismo propietario, su piloto deberá solicitar siempre permiso a la Aerocivil. Este postulado es: ", opciones: ["Falso.", "Verdadero.",], respuesta: 0 },
            { pregunta: "Uno de los requisitos expresados en el RAC 100 y que es de suma importancia para poder solicitar un permiso de vuelo para realizar operaciones de enjambre con UAS, es: ", opciones: ["Ser ingeniero de sistemas especializado en el software que controla el enjambre.", "Contar con una adición en su certificado de idoneidad con base en un documento válido que soporte las habilidades y competencias necesarias para efectuar este tipo de operaciones.", "Poseer un sistema de protección especial para evitar incidentes o accidentes en caso de que fallen y se desplomen algunas aeronaves."], respuesta: 1 },
            { pregunta: "¿Qué significa una operación “dron delivery”?", opciones: ["Es una operación especial de topografía.", "Es una operación de transporte y entrega de pequeñas cargas.", "Es una operación de transporte de personas 'taxi'."], respuesta: 1 },
            { pregunta: "Un explotador UAS que pretenda hacer operaciones aéreas “dron delivery” está en la obligación de demostrar que el personal designado para efectuar este tipo de labor cuenta con la capacitación correspondiente del fabricante de la aeronave en cuanto a la manipulación y operación deL UAS. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Que el personal involucrado en la manipulación de la carga tenga capacitación certificada en cuanto a transporte seguro de mercancías peligrosas por vía aérea es un requisito obligatorio para poder ejecutar operaciones *dron delivery*.  Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "¿Qué límite debe ser excedido para poder considerar una operación de una UA como operación BVLOS?", opciones: ["Superar la distancia horizontal entre el piloto UAS y la UA de 3 km o antes si pierde linea directa de vista. ", "Superar la distancia horizontal entre el Piloto UAS y la UA de 1.500 m.", "Solamente disponer de un sistema de administración en tiempo real de la aeronave para poder volar."], respuesta: 0 },
            { pregunta: "Una operación BVLOS puede llevarse a cabo en cualquier lugar, no requiere condiciones especiales para su vuelo; solamente se requiere que el Explotador UAS realice una solicitud ordinaria ante la Aerocivil. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Las operaciones aéreas que sean realizadas en condiciones BVLOS por parte de un explotador UAS requieren que este cuente con una autorización expresa para este tipo de operación y un área específica determinada para el efecto.  Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "¿Qué condiciones especiales debe tener en cuenta un explotador UAS para volar BVLOS?/1-Máxima altura de 400 ft y en VMC./2-Falta de conciencia situacional permanente en la ubicación de la UA en vuelo./3-Maxima desviación permitida es de 30 m entre la ruta de los WP./4-Pérdida del enlace C2 se considera operación normal./5-Visualización de la telemetría y sistema de administración del espacio en tiempo real./6-Monitorización parcial y esporádica de la meteorología.", opciones: ["Los numerales 1, 2 y 3 son correctos.", "Los numerales 4, 5 y 6 son correctos.", "Los numerales 1, 3 y 5 son correctos."], respuesta: 2 },
            { pregunta: "El certificado como explotador UAS expedido por la Aerocivil para la categoría específica permite:", opciones: ["Que el explotador UAS cuente con autorización por parte de la Aerocivil para poder prestar un determinado servicio de aviación civil con el uso de UAS.", "Que el explotador UAS pueda determinar de mejor forma las tarifas de su servicio.", "Que el explotador UAS relacione sin restricción los pilotos de UAS que requiera la empresa."], respuesta: 0 },
            { pregunta: "Algunos de los requisitos que necesita una empresa para poder gestionar ante la Aerocivil un certificado como explotador UAS son:", opciones: ["Contar con un registro mercantil válido .", "Obtener resultado satisfactorio en la inspección operacional por parte de la Aerocivil.", "Ambas opciones son válidas."], respuesta: 2 },
            { pregunta: "¿Con qué lapso de tiempo un explotador UAS debe reportar cambios en su información de registro para evitar inconsistencias que ocasionen la suspensión de su certificado de explotador UAS?", opciones: ["Mínimo semestralmente, el último día hábil de cada periodo. ", "Dentro de los 15 días siguientes a la ocurrencia del cambio.", "Solamente se requiere el registro inicial, no hay necesidad de reportar cambios."], respuesta: 1 },
            { pregunta: "Mantener al día el libro de vuelo y mantenimiento de cada UA, así como emitir y mantener actualizado el Manual de Operación (MO), hacen parte integral de las responsabilidades que el Explotador UAS certificado, Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "No es necesario que el explotador UAS certifique el tiempo de vuelo acumulado a cada piloto UAS que trabaje en la empresa, teniendo en cuenta que la Aerocivil lleva este registro por medio de los permisos de vuelo tramitados. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Es responsabilidad de cada uno de los pilotos UAS que trabaja con un explotador UAS mantener sus competencias de entrenamiento para cumplir con los diferentes tipos de operación que realiza la empresa, realizando por cuenta propia los cursos de repaso y verificaciones correspondientes. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "¿Cuáles son los parámetros que la Aerocivil tendrá en cuenta para suspender o cancelar un certificado de explotador UAS?/1-El incumplimiento de requisitos y condiciones establecidos en la reglamentación./2-Efectuar operaciones aéreas que pongan en riesgo la seguridad operacional./3-La incapacidad técnica para realizar actividades de mantenimiento./4-El abandono de la actividad autorizada sin justificación por más de un año.", opciones: ["Los numerales 1 y 4 son correctos.", "Los numerales 2 y 3 son correctos.", "Todos los numerales son correctos."], respuesta: 2 },
            { pregunta: "Un explotador UAS que tenga registrado bajo su dominio tres *3* o más UAS, ¿qué cargos debe registrar y designar ante la Aerocivil?", opciones: ["Una persona en el cargo de Jefe de Mantenimiento de UA y otra persona en el cargo de Gerente de Proyectos.", "Una persona en el cargo de Jefe de Pilotos UA y otra persona en el cargo de Gerente de Seguridad Operacional.", "Una persona en el cargo de Secretaría para UAS y otra persona en el cargo de Gerente de Seguridad de los “Vertipuertos”."], respuesta: 1 },
            { pregunta: "¿Cuál de las siguientes afirmaciones no corresponde a la experiencia que debe ostentar un Jefe de Pilotos?", opciones: ["Contar con capacitación como piloto UAS en al menos una de las operaciones aéreas autorizadas al explotador UAS.", "Contar con experiencia administrativa de al menos cien (100) horas de trámites de vuelo para UAS.", "Contar con capacitación certificada por CIAC, de mínimo cuarenta *40* horas, en el sistema de gestión de la seguridad operacional - SMS."], respuesta: 1 },
            { pregunta: "El aseguramiento de la adecuada asignación y utilización de cada UA y de cada piloto UAS de acuerdo con las competencias requeridas para el desarrollo de la operación autorizada al explotador UAS certificado es una función expresa del Jefe de Pilotos. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Monitorear los estándares operativos y la eficiencia de cada piloto UAS designado es una de las funciones principales del Gerente de Seguridad Operacional. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "De las siguiente cualificaciones y experiencias del Gerente de Seguridad Operacional, ¿Cuál es la correcta?", opciones: ["Contar con un curso básico sobre el Sistema de Gestión de Calidad, certificado por ICONTEC, de mínimo cuarenta (40) horas.", "Tener formación acreditada en áreas del sector aeronáutico.", "Experiencia administrativa contable acreditada respecto de las funciones y naturaleza de la empresa explotadora UAS."], respuesta: 1 },
            { pregunta: "La responsabilidad de la identificación de los peligros y el análisis y gestión de los riesgos en cuanto a la operación con aeronaves no tripuladas es una función inherente al Jefe de Pilotos.  Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Monitorear que se lleven a cabo las acciones correctivas *planes de acción* de un Explotador UAS, es una función inherente al Gerente de la Seguridad Operacional. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "¿Cuál es el nombre del documento expedido por la Aerocivil que permite a los pilotos UA desarrollar operaciones de vuelo con aeronaves no tripuladas en la categoría específica?", opciones: ["Licencia de piloto a distancia.", "Certificado de idoneidad de piloto UAS.", "Licencia de operación de UAS."], respuesta: 1 },
            { pregunta: "¿Cuál de los requisitos a continuación aplica para solicitar un certificado de idoneidad?", opciones: ["Haber culminado satisfactoriamente con Acta de Grado los estudios de básica secundaria en una institución reconocida nacionalmente.", "Haber culminado satisfactoriamente el contenido del curso básico de piloto UAS de aeronaves no tripuladas en un CIAC aprobado por la Aerocivil.", "Pagar un Objeto Virtual de Aprendizaje para reforzar los conocimientos de UAS."], respuesta: 1 },
            { pregunta: "¿Cuál de los siguientes es requisito para poder volar una UA en categoría específica?", opciones: ["Contar con un certificado de idoneidad como piloto UAS expedido por la Aerocivil.", "Contar con una aeronave no tripulada sin registro ante la Aerocivil.", "Solicitar una autorización de vuelo no requiere presentar la poliza RCE."], respuesta: 0 },
            { pregunta: "El certificado de idoneidad obtenido por una persona podrá ser transferido a otra, de acuerdo con la solicitud expresa de un explotador UAS en un determinado momento y bajo unas circunstancias específicas. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Para poder obtener el certificado de idoneidad de piloto UA en categoría específica, se requiere contar con un certificado médico con las siguientes características:", opciones: ["Médico Ocupacional: Vigencia de dos años, optometría, audiometría, tensión arterial, neurología, psicología e integridad de extremidades inferiores.", "Médico Ocupacional: Vigencia de un año, optometría, audiometría, lenguaje verbal e integridad de extremidades superiores.", "Médico Aeronáutico: Vigencia de tres años, optometría, audiometría, oftalmología, neurología, psicología y coeficiente intelectual."], respuesta: 1 },
            { pregunta: "La estructura academica del curso de piloto UAS, contiene las siguientes áreas de conocimiento entre otras:/1-Aerodinámica aplicada./2-Despacho de aeronaves./3-Regulaciones aeronáuticas./4-Peso y balance./5-Meteorología aeronáutica./6-Navegación aérea./7-Asistente en vuelo.", opciones: ["Los numerales 1, 3, 5 y 6 son correctos.", "Los numerales 2, 4, 6 y 7 son correctos.", "Todos los numerales son correctos."], respuesta: 0 },
            { pregunta: "Para la planificación del vuelo, se requiere del uso practico de GIS. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Actividades como la dispersión, aspersión e instrucción de vuelo UAS, son considerados como adiciones al certificado de idoneidad. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Actividades de fotogrametría y modelamiento digital del terreno son considerados como adiciones al certificado de idoneidad. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "Los requisitos generales para obtener una adición al certificado de idoneidad como piloto UAS son:", opciones: ["Ser titular de una aeronave que requiera de las especificaciones de la adición; demostrar horas de práctica relacionada con la correspondiente adición; pago de la compensación económica de la adición.", "Ser titular de un certificado de idoneidad de piloto UAS otorgado por la Aerocivil; demostrar capacitación teórica y práctica relacionada con la correspondiente adición; pago de los derechos de la respectiva adición.", "No tienen requisitos generales  y se solicita a la Dirección de Servicios de Navegación Aérea."], respuesta: 1 },
            { pregunta: "La suspensión o cancelación de un certificado de idoneidad o de sus adiciones se origina por:/1-A solicitud del interesado. /2-El titular no reúne los requisitos que dieron origen a su otorgamiento. /3-Como sanción en caso de infracción a los Reglamentos Aeronáuticos de Colombia./4-Suspensión provisional por riesgo inminente contra la seguridad operacional en flagrancia.", opciones: ["Los numerales 2 y 3 son correctos.", "Los numerales 1 y 4 son correctos.", "Todos los numerales son correctos."], respuesta: 2 },
            { pregunta: "El Sistema De Gestión de la Seguridad Operacional  SMS es de cumplimiento opcional para los explotadores UAS. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "El Sistema de Gestión de la Seguridad Operacional  SMS es de obligatorio cumplimiento para los explotadores UAS y requisito fundamental para obtener el certificado como explotador UAS. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Tres *3* documentos requeridos para realizar una solicitud de autorización de vuelo en categoría específica ante la Aerocivil son:", opciones: ["Formato de solicitud de vuelo, matriz SMS y póliza.", "Manual de operaciones, factura de compra, manual del fabricante.", "Todas las opciones son correctas."], respuesta: 0 },
            { pregunta: "Es requisito fundamental para tramitar el certificado de explotador UAS contar con el manual de operaciones (MO) aprobado por la Aerocivil. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
            { pregunta: "Los documentos mínimos requeridos para solicitar un certificado de idoneidad como piloto UAS son:/1-Certificado del curso básico de piloto UAS expedido por un CIAC aprobado./2-Copia del registro civil de nacimiento./3-Copia del documento de identificación./4-Copia de la declaración de renta./5-Copia de la constancia de realización del OVA./6-Copia del certificado de aprobación del examen teórico./7-Copia de la licencia de conducción./8-Copia del certificado médico ocupacional vigente.", opciones: ["Los numerales 1, 3, 5, 6 y 8 son requeridos.", "Los numerales 2, 4, 5 y 7 no son requeridos.", "Todos los numerales son requeridos."], respuesta: 0 },
            { pregunta: "Los documentos mínimos requeridos para la solicitud de registro de una UA contemplan: las fotografías de la aeronave, la factura de compra, la declaración de importación, paz y salvo de la DIAN y el documento de identificación del propietario. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "El procedimiento correcto para informar a la Aerocivil de que se requiere o se realizó una cesión de dominio de un UAS de un propietario a un explotador UAS que compró o alquiló la aeronave se realiza:", opciones: ["Por medio de carta dirigida al Grupo Drones y Movilidad Urbana Aérea firmada por el propietario del registro.", "Tramitando el formato reporte de desuso o solicitud cambio de propiedad de UAS o equipo tecnológico, adjuntando para el efecto la documentación solicitada.", "No se requiere informar a la Aerocivil de la novedad."], respuesta: 0 },
            { pregunta: "Los únicos documentos requeridos para iniciar el proceso de certificación de explotador UAS son la carta de cumplimiento y el manual de operaciones con SMS. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "De las siguientes opciones, determine la fases para obtener la certificación como Explotador UAS (seleccione la correcta).", opciones: ["Solicitud, Aprobación de manuales, Inspección y Certificado.", "Presolicitud, Evaluación documental, Solicitud formal, Demostración y Certificado.", "Presolicitud, Solicitud, Evaluación Documental, Inspección y demostración y Emisión del certificado."], respuesta: 2 },
            { pregunta: "Toda solicitud de autorización de vuelo que involucre el uso de espacio aéreo restringido, peligroso o prohibido debe ser solicitado a la Aerocivil, con copia dirigida a la FAC. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "¿Qué requisito es necesario si un explotador UAS va a realizar un vuelo que esté dentro de una ZNVD?", opciones: ["Requerirá obligatoriamente el pago de los derechos para poder operar en una ZNVD.", "Requerirá obligatoriamente una autorización escrita de la entidad responsable de la ZNVD.", "Requerirá obligatoriamente una carta de confidencialidad exclusiva de la Fiscalía General de la Nación."], respuesta: 1 },
            { pregunta: "¿Qué es y que significa la sigla CDM?", opciones: ["CDM: Toma de decisiones en colaboracion.", "CDM: Coordinación de Datos Monitoreados.", "CDM: Compilación De Maniobras integradas."], respuesta: 0 },
            { pregunta: "¿Qué sigifica la sigla - MCM?", opciones: ["MCM: Maniobras controladas por el manual.", "MCM: Monitoreo de control manual.", "MCM: Manual de control de mantenimiento."], respuesta: 2 },


            ],
            aerodinamica: [
            { pregunta: "La aerodinámica es el estudio del movimiento de las masas de aire y sus efectos en la tierra. Este postulado es: ", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
            { pregunta: "La definición mas acertada para *AERODINÁMICA* es:", opciones: ["El estudio del comportamiento del aire en movimiento al interactuar con un objeto.", "El estudio de las propiedades químicas de los gases que componen el aire.", "El movimiento del aire en la tierra."], respuesta: 0 },
            { pregunta: "¿Cuál de las siguientes opciones describe adecuadamente las tres leyes de Newton?", opciones: ["Ley de la termodinámica, ley de la física y y ley de la presión.", "Ley de la inercia, ley de la dinámica y y ley de la acción y reacción.", "Ley del flujo, ley de la estática y ley de la reacción."], respuesta: 1 },
            { pregunta: "Una de las leyes de Newton, que es uno de los principios aplicados a la aerodinámica presente en los UAS, es:", opciones: ["Ley de conservación de la energía.", "Ley de acción y reacción.", "Ley de la termodinámica"], respuesta: 1 },
            { pregunta: "El teorema de Bernoulli describe que todo cuerpo sumergido en un líquido experimenta una fuerza hacia arriba equivalente al peso del volumen desalojado. Este postulado es:.", opciones: ["Falso.", "Verdadero.",], respuesta: 0 },
            { pregunta: "¿De qué trata el teorema de Bernoulli?", opciones: ["Describe el comportamiento de un objeto con respecto a un fluido.", "Describe los cambios de velocidad por la temperatura de un fluido.", "Describe la conservación de la energia relacionando con la presión y velocidad de un fluido."], respuesta: 2 },
            { pregunta: "¿Cual de los siguientes postulados es verdadero?", opciones: ["A mayor velocidad relativa del aire, mayor presión sobre el plano aerodinámico de la aeronave, por lo tanto mayor sustentación.", "A mayor velocidad relativa del aire, menor presión sobre el plano aerodinámico de la aeronave, por lo tanto mayor sustentación.", "A mayor velocidad relativa del aire, menor colchón de aire bajo el plano aerodinámico de la aeronave, por lo tanto mayor sustentación."], respuesta: 1 },
            { pregunta: "¿Qué es un perfil aerodinámico?", opciones: ["La capacidad de una aeronave para realizar maniobras acrobáticas.", "La forma y las características del perfil transversal de una superficie sustentadora.", "La velocidad máxima que puede alcanzar una aeronave."], respuesta: 1 },
            { pregunta: "La capa de la atmósfera donde se desarrolla principalmente la aviación es:", opciones: ["La mesosfera.", "La exosfera.", "La troposfera."], respuesta: 2 },
            { pregunta: "Son los movimientos angulares naturales de una aeronave sobre sus ejes:", opciones: ["Guiñada, torsión y alabeo.", "Guiñada, alabeo y cabeceo.", "Guiñada, bamboleo y torsión."], respuesta: 1 },
            { pregunta: "¿Qué consideraciones se tienen para el cálculo del PMBO?", opciones: ["Potencia motriz, presión atmosférica y temperatura del aire.", "Peso potencial de inercia.", "Variación de la presión por temperatura."], respuesta: 0 },
            { pregunta: "¿Cuál es el función principal del borde de ataque de un perfil aerodinámico?", opciones: ["Parte del perfil aerodinámico donde se manifiestan los vectores de fuerza.", "La presión del aire ejerce fuerza de sustentación.", "Recibe el aire de impacto y lo divide para recorrer el perfil aerodinámico."], respuesta: 2 },
            { pregunta: "¿Cuál es la principal función que identifica el borde de fuga o borde de salida de un perfil aerodinámico?", opciones: ["Allí la sustentación ejerce su fuerza.", "Allí cambia la presión del aire.", "Allí, los flujos superior e inferior abandonan el ala."], respuesta: 2 },
            { pregunta: "¿A qué se denomina cuerda alar o línea de cuerda en un perfil aerodinámico?", opciones: ["Línea que recorre un perfil por su borde superior.", "Línea recta que va desde el borde de ataque hasta el borde de fuga.", "Línea que mide el espesor máximo del perfil."], respuesta: 1 },
            { pregunta: "¿Qué es un perfil aerodinámico simétrico?", opciones: ["Perfil en donde la línea de curvatura media coincide con la cuerda alar.", "Perfil que produce sustentación con ángulo de ataque cero.", "Perfil de medidas iguales entre el espesor máximo y la cuerda."], respuesta: 0 },
            { pregunta: "¿Qué es un perfil aerodinámico asimétrico?", opciones: ["Perfil en donde el extrados y el intrados son iguales.", "Perfil que produce sustentación con ángulo de ataque cero.", "Perfil similar en medidas entre borde de fuga y borde de ataque."], respuesta: 1 },
            { pregunta: "¿Cuáles son los vectores de fuerza resultantes que actúan en una aeronave?", opciones: ["Sustentación, peso, empuje y resistencia.", "Sustentación, elevación, empuje y resistencia.", "Elevación, gravedad, empuje y potencia."], respuesta: 0 },
            { pregunta: "¿Cómo se podría describir la fuerza sustentadora *lift* para una aeronave?", opciones: ["La fuerza resultante que principalmente hala a una aeronave hacia arriba.", "La fuerza resutante que impulsa a una aeronave hacia adelante.", "La fuerza resultante que se opone a la resistencia al avance de una aeronave."], respuesta: 0 },
            { pregunta: "¿Cómo se podría describir la resistencia en una aeronave?", opciones: ["La fuerza que mantiene una aeronave en el aire.", "La dificultad que experimenta el avance de una aeronave.", "La capacidad que tiene una aeronave para mantenerse en vuelo."], respuesta: 1 },
            { pregunta: "¿Cómo afecta la forma del ala a su aerodinámica?", opciones: ["Determina la velocidad máxima de vuelo.", "Influye directamente en la sustentación y la resistencia.", "Determina la altura máxima de servicio de una aeronave."], respuesta: 1 },
            { pregunta: "¿Cual es la característica del centro de gravedad de un multicóptero?", opciones: ["Que se ubica en cada uno de los motores de la aeronave.", "Que se ubica cerca del centro geométrico de la aeronave, dependiendo de la distribución de los motores .", "Los multicópteros no tienen centro de gravedad definido."], respuesta: 1 },
            { pregunta: "¿En dónde se debería ubicar el centro de gravedad de un avión?", opciones: ["En el tren de aterrizaje.", "En la cola del avión.", "En el centro de presión de las alas."], respuesta: 2 },
            { pregunta: "El centro de gravedad de una aeronave generalmente se expresa en términos de posición en el sistema de referencia de la aeronave, que incluye los ejes longitudinal, lateral y vertical. Estas “coordenadas” permiten determinar la ubicación precisa del punto del centro de gravedad. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué sucede si el centro de gravedad de una UA se encuentra por fuera de los límites establecidos por el fabricante?", opciones: ["Afecta negativamente la capacidad de control y estabilidad de la UA en el aire.", "Se aprovecha para poder hacer vuelos acrobáticos con más facilidad.", "El sistema advierte la condición y no permite el despegue de la UA."], respuesta: 0 },
            { pregunta: "¿Qué es el ángulo de ataque?", opciones: ["Ángulo formado entre la cuerda alar y el viento relativo.", "Ángulo formado entre el borde de ataque y la cuerda alar.", "Ángulo formado entre la línea de curvatura media alar y el viento relativo."], respuesta: 0 },
            { pregunta: "¿Por qué se produce la pérdida aerodinámica?", opciones: ["Por aumento de velocidad del aire en el intrados.", "Por acercarse a una velocidad subsónica.", "Por exceder el ángulo de ataque."], respuesta: 2 },
            { pregunta: "¿Cuál de las siguientes opciones corresponde a superficies hipersustentadoras?", opciones: ["Alas rotatorias.", "Spoilers", "Flaps"], respuesta: 2 },
            { pregunta: "¿Cómo influye la temperatura en el vuelo de un UA a una presión constante?", opciones: ["A mayor temperatura, más difícil volar, menos tiempo de vuelo.", "A menor temperatura, más difícil volar, menos tiempo de vuelo.", "A menor temperatura, más fácil volar, menos tiempo de vuelo."], respuesta: 0 },
            { pregunta: "¿Cómo se contrarresta el torque de las hélices en un multirrotor?", opciones: ["Todas las hélices giran en sentido de las manecillas del reloj.", "Un solo motor no se ve afectado por el torque.", "Las hélices se contrarrestan por pares girando en sentidos contrarios."], respuesta: 2 },
            { pregunta: "¿Qué tipos de resistencia aerodinámica existen?", opciones: ["Contorno, de superficie, de presión.", "Inducida y parásita.", "Parásita, inducida y de presión."], respuesta: 1 },
            { pregunta: "Entre los efectos aerodinámicos que tienen ocurrencia en una superficie alar, ¿qué es la pérdida?", opciones: ["La pérdida de sustentación por disminución de la densidad del aire.", "La pérdida de sustentación por alto ángulo de ataque.", "La pérdida de velocidad de la aeronave."], respuesta: 1 },
            { pregunta: "¿Cuál de los siguientes elementos no es considerado una superficie sustentadora?", opciones: ["Hélices.", "Flaps* y *slats*.", "Alerones."], respuesta: 2 },




            ],
            meteorologia: [

            { pregunta: "¿Qué es la meteorología?", opciones: ["Es el estudio de los fenómenos que ocurren el la atmósfera. ", "Es el estudio de las condiciones marítimas que tienen influencia en el viento y la lluvia.", "Es el comportamiento del tiempo y clima de un lugar específico."], respuesta: 0 },
            { pregunta: "¿En cuáles campos se hace uso de aplicación de la meteorología?", opciones: ["Experimental, sinóptica, agrícola, marítima y aeronáutica.", "Forestal aerodinámica y agropecuaria.", "Regional, local y oceánica."], respuesta: 0 },
            { pregunta: "¿A qué se le conoce como clima?", opciones: ["Descripción estadística de las condiciones meteorológicas más frecuentes de una región, en un determinado período de tiempo.", "Variación diaria de las condiciones atmosféricas que se presentan en una región específica.", "Variaciones del viento en cuanto a velocidad y dirección que se presentan en una región específica."], respuesta: 0 },
            { pregunta: "¿A qué se le conoce como (tiempo meteorológico)?", opciones: ["Descripción estadística de las condiciones meteorológicas más frecuentes de una región, en un determinado periodo de tiempo.", "Variación diaria o de tiempos muy cortos de análisis de las condiciones atmosféricas que se presentan en una región específica.", "Variaciones del viento en cuanto a velocidad y dirección que se presentan en una región específica."], respuesta: 1 },
            { pregunta: "¿Cuál es la diferencia entre tiempo meteorológico y clima?", opciones: ["No hay diferencia, realmente son lo mismo.", "El tiempo meteorológico son las condiciones atmosféricas predominantes de una región amplia y se determina por periodos largos de tiempo. El clima es un estado de la atmosfera en un momento determinado, en una locación específica y cambia constantemente.", "El tiempo meteorológico es un estado de la atmósfera en un momento determinado, en una ubicación específica y cambia constantemente. El clima son las condiciones atmosféricas predominantes de una región amplia y se determina por períodos largos de tiempo."], respuesta: 2 },
            { pregunta: "¿Qué aspectos contribuyen a que se determinen los parámetros de clima en un lugar determinado?", opciones: ["Latitud y orografía.", "Posición geográfica relativa con respecto a continentes y océanos.", "Las dos opciones son correctas."], respuesta: 2 },
            { pregunta: "De las siguientes opciones, ¿Qué instrumentos meteorológicos, se emplean para capturar información del tiempo meteorológico?/1-Indicador de velocidad y dirección de viento. /2-Termómetros de altas y alcohol./3-Odómetro./4-Sensor de humedad./5-Sensor presión ATM./6-Tensiómetro./7-Ceilómetro./8-Variómetro./9-Horizonte artificial./10-Manómetro.", opciones: ["Los numerales 2, 4, 6, 8 y 10 son correctos", "Los numerales 1, 3, 6, 8, 9 y 10 son correctos.", "Los numerales 1, 2, 4, 5 y 7 son correctos."], respuesta: 2 },
            { pregunta: "La observación meteorológica consiste en la medición de todos los elementos meteorológicos que en conjunto representan las condiciones del estado de la atmósfera. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué es la atmósfera?", opciones: ["Es el conjunto de gases y nubes que envuelven a la tierra.", "Es manto de vapor de agua que rodea a la tierra.", "Ambas opciones son correctas."], respuesta: 0 },
            { pregunta: "¿Cuál es la composición estándar del aire?", opciones: ["Nitrógeno 78% - Oxígeno 21% - Otros gases 1%", "Nitrógeno 70% - Oxígeno 25% - Otros gases 5%", "Nitrógeno 80% - 0xígeno 19% - Otros gases 1%"], respuesta: 0 },
            { pregunta: "Además de los elementos gaseosos estándar del aire, ¿qué otras moléculas conforman la atmósfera?", opciones: ["Agua en sus tres estados.", "Núcleos higroscópicos.", "Solamente agua en estado gaseoso."], respuesta: 0 },
            { pregunta: "Las capas de la atmósfera según la composición química del aire son homósfera y heterósfera. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Cuál de las siguientes es una característica de la troposfera?", opciones: ["Disminución abrupta de la temperatura con el incremento de altitud. ", "Contiene toda la humedad de la atmósfera. ", "La altitud promedio del tope de la atmósfera es alrededor de 6 millas."], respuesta: 1 },
            { pregunta: "La ionosfera es una capa de la atmósfera no clasificada según temperatura, la cual contiene una gran cantidad de iones que son importantes para procesos electromagnéticos. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué característica tiene la ionósfera?", opciones: ["Permite la reflexión de las ondas largas de radio HF.", "Permite la refracción de las ondas de radio HF.", "Permite la difracción de las ondas de radio VHF."], respuesta: 0 },
            { pregunta: "¿Qué es el viento?", opciones: ["Es el movimiento de una masa de aire en sentido vertical.", "Es el movimiento de una masa de aire en sentido horizontal.", "Es el movimiento de una masa de aire sin importar su sentido."], respuesta: 1 },
            { pregunta: "¿Cuáles son las unidades empleadas para poder medir la velocidad del viento?", opciones: ["(m/s) metros por segundo y (km/h) kilómetros por hora.", "(kt) nudos.", "Todas las opciones son verdaderas."], respuesta: 2 },
            { pregunta: "El movimiento vertical de una masa de aire, inducido por elaumento de su temperatura se denomina: ", opciones: ["Estratificación.", "Convección. ", "Efecto de Coriolis."], respuesta: 1 },
            { pregunta: "Los vientos catabáticos son identificados como:", opciones: ["Vientos que viajan de los picos hacia las faldas de las montañas. ", "Vientos que viajan desde los valles hacia la cima de las montañas.", "Vientos que viajan por las costas."], respuesta: 0 },
            { pregunta: "El movimiento desordenado del aire originado por diferentes causas se le conoce como:", opciones: ["Turbulencia. ", "Viento geostrófico. ", "Corriente de chorro."], respuesta: 0 },
            { pregunta: "¿Qué es la turbulencia?", opciones: ["Es el desplazamiento de un fluido de forma ordenada y laminar con respecto a su dirección e intensidad.", "Es el desplazamiento de un fluido de forma desordenada con respecto a su dirección e intensidad.", "Es una situación de desorden presentado por un elemento en general."], respuesta: 1 },
            { pregunta: "Para la aviación no tripulada, ¿por qué es peligrosa una situación de turbulencia del aire?", opciones: ["Porque interrumpe el flujo laminar sobre las superficies sustentadoras, causando desplome.", "Porque existiendo la condición turbulenta, no se puede ver a simple vista.", "Las dos opciones son correctas."], respuesta: 0 },
            { pregunta: "¿Qué es temperatura?", opciones: ["Es un concepto teórico basado en las sensaciones del cuerpo humano.", "Es la comparación entre la sensación de frío y calor.", "Es la medida de la energía interna de un cuerpo."], respuesta: 2 },
            { pregunta: "El calor es la energía manifestada por el aumento de la temperatura en un cuerpo determinado.  Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué es radiación solar?", opciones: ["Es la energía emitida por el sol.", "Son las crestas de fuego que produce el sol.", "Se le conoce como la corona solar cuando hay un eclipse de sol."], respuesta: 0 },
            { pregunta: "La radiación solar se compone de radiación infrarroja y radiación ultravioleta únicamente. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Cuál es la principal causa de la variación climatológica y del estado de la meteorología?", opciones: ["Cambios en la presión del aire sobre la superficie de la tierra. ", "Movimientos de las masas de aire de las áreas húmedas a las áreas secas. ", "Variaciones de la energía solar en la superficie terrestre."], respuesta: 2 },
            { pregunta: "¿A qué se le conoce como meteoro?", opciones: ["A un fenómeno atmosférico sólido (granizo, nieve, etc.).", "A cualquier fenómeno atmosférico. ", "A un fenómeno atmosférico luminoso."], respuesta: 1 },
            { pregunta: "¿A qué se le conoce como meteorito?", opciones: ["Cualquier fenómeno atmosférico. ", "Cualquier fragmento de materia sólida procedente del espacio exterior.", "Las dos opciones son correctas."], respuesta: 1 },
            { pregunta: "Las nubes son las manifestaciones visibles del agua contenida en la atmósfera, indicando saturación y condensación. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿A qué se le conoce como (precipitación)?", opciones: ["Caída de agua líquida o sólida desde la atmósfera hacia la superficie terrestre.", "Cuando alguien realiza una acción de forma acelerada.", "Evaporación del agua de la superficie."], respuesta: 0 },
            { pregunta: "Cuando la temperatura actual del aire se acerca a la temperatura del punto de rocío identificamos que:", opciones: ["Hay menor probabilidad de formación de niebla o nubes bajas. ", "Hay mayor probabilidad de formación de niebla, neblina o nubes bajas.", "No hay probabilidad de precipitación."], respuesta: 1 },
            { pregunta: "Las nubes tipo estratos (ST), cúmulos (CU) y estratocúmulos *SC* son consideradas:", opciones: ["Nubes de capa baja.", "Nubes de capa media.", "Nubes de tormenta."], respuesta: 0 },
            { pregunta: "Las nubes tipo cirros, cirroestratos y cirrocúmulos son consideradas:", opciones: ["Nubes bajas.", "Nubes altas.", "Nubes medias."], respuesta: 1 },
            { pregunta: "La clasificación de las nubes según su apariencia es:", opciones: ["Estratiformes, bancos de niebla y cirriformes. ", "Estratiformes, cumuliformes y cirriformes.", "De formación vertical y formación horizontal."], respuesta: 1 },
            { pregunta: "¿Cuál es el tipo de nube que produce mayor turbulencia y es potencialmente peligrosa para la aviación? ", opciones: ["CS - Cirrostratos", "CB - Cumulonimbos", "Todas las nubes son peligrosas para la aviación."], respuesta: 1 },
            { pregunta: "¿Qué tipo de nubes se consideran de desarrollo vertical?", opciones: ["Torrecúmulos (TCU) y cumulonimbos (CB).", "Torrecúmulos (TCU) y nimboestratos (NS).", "Cumulonimbos (CU) y nimboestratos (NS)."], respuesta: 0 },
            { pregunta: "El término FEW empleado para determinar condiciones de nubosidad corresponde a: ", opciones: ["1 a 2 octas. ", "Cielo despejado.", "3 a 4 octas."], respuesta: 0 },
            { pregunta: "El término empleado para referirse a un cielo totalmente cubierto (8 Octas) por condiciones de nubosidad se le llama:", opciones: ["Scattered.", "Overcast.", "CAVOK."], respuesta: 1 },
            { pregunta: "En Colombia, la visibilidad horizontal se mide en:", opciones: ["Pies.", "Metros.", "Millas terrestres."], respuesta: 1 },
            { pregunta: "¿Cuáles son los mínimos meteorológicos aplicables a las reglas de vuelo visual VFR?", opciones: ["Visibilidad de más de 500 mts. y techo de nubes de más de 5000 ft.", "Visibilidad de 5 km o más y techo de nubes no menor de 1.500 ft.", "Visibilidad de más de 10 km y techo de nubes de más de 1.500 ft."], respuesta: 1 },
            { pregunta: "Se le llama al fenómeno compuesto en su mayoría por partículas de agua en estado líquido o sólido que opalizan el aire, reduciendo la visibilidad por debajo de 1 km: ", opciones: ["HZ *Bruma*. ", "GR *Granizo*.", "FG *Niebla*."], respuesta: 2 },
            { pregunta: "¿Cuál de las siguientes es considerada nube de tormenta?", opciones: ["CC (Cirrocúmulos). ", "ST (Estratos).", "CB (Cumulonimbos)."], respuesta: 2 },
            { pregunta: "¿Qué es la presión atmosférica?", opciones: ["Peso de una columna de aire desde el punto de medición hasta el límite de la troposfera sobre una superficie determinada.", "Presión de una columna de aire desde el nivel medio del mar hasta el límite superior de la atmósfera sobre una superficie estándar de un centímetro cuadrado.", "Fuerza que ejerce el peso de una columna de aire desde el punto de medición hasta el límite superior de la atmósfera por unidad de superficie."], respuesta: 2 },
            { pregunta: "Fuerza que ejerce peso de una columna de aire sobre una unidad de superficie, que se extiende desde la superficie en la cual se realiza la medición hasta el límite superior de la atmósfera.", opciones: ["Presión barométrica.", "Fuerza atmosférica.", "Presión atmosférica."], respuesta: 2 },
            { pregunta: "En cuanto a la presión atmosférica, ¿cuál de las siguientes relaciones es la correcta?", opciones: ["A mayor altura, menor presión atmosférica.", "A mayor altura, mayor presión atmosférica.", "A menor altura, menor presión atmosférica."], respuesta: 0 },
            { pregunta: "En cuanto a la densidad del aire, se determina que:", opciones: ["A menor presión atmosférica. mayor densidad del aire.", "A mayor presión atmosférica. mayor densidad del aire.", "Sin importar la presión atmosférica.  la densidad del aire será siempre igual."], respuesta: 1 },
            { pregunta: "Cuando se habla de VFR, nos referimos a las condiciones meteorológicas visuales. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "Un vuelo para una aeronave no tripulada debe ser efectuado de acuerdo con:", opciones: ["Reglas de vuelo instrumentos y en condiciones IMC.", "Reglas de vuelo visual y en condiciones VMC.", "Reglas de vuelo visual y en condiciones IMC."], respuesta: 1 },
            { pregunta: "Las unidades para la medición de la temperatura son grados Celsius, Kelvin y Fahrenheit. Este postulado es: ", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "¿Qué es la humedad?", opciones: ["Es la cantidad de agua presente en la atmósfera.", "Es la cantidad de agua presente en los océanos.", "Es el vapor de agua que se puede encontrar en la tierra."], respuesta: 0 },
            { pregunta: "¿Cómo se define el (punto de rocío)?", opciones: ["Temperatura del aire a la cual se condensa el vapor de agua que hay en la atmósfera.", "Temperatura del aire a la cual se evaporan las moléculas de agua.", "Presión del aire a la cual se condensa el vapor de agua."], respuesta: 0 },
            { pregunta: "METAR, SPECI y TAF son:", opciones: ["Reportes meteorológicos aeronáuticos asociados a un aeródromo. ", "Reportes meteorológicos aeronáuticos de tiempo real.", "Información documentada de las condiciones meteorológicas de un determinado lugar."], respuesta:  0},
            { pregunta: "Dentro de la información que se maneja en la aviación, ¿qué es un METAR?", opciones: ["Reporte meteorológico de condiciones de altura.", "Reporte meteorológico de actualidad del aeródromo.", "Pronóstico meteorológico del aeródromo."], respuesta: 1 },
            { pregunta: "En los reportes METAR el término NSW significa:", opciones: ["Chubascos en la vecindades.", "No existen cambios significativos en la meteorología respecto del informe anterior.", "Precaución de tormenta en el sector."], respuesta: 1 },
            { pregunta: "En los reportes METAR el termino CAVOK significa:", opciones: ["Condiciones de cielo (techo) y visibilidad buenas.", "Estamos todos bien.", "Cielo completamente libre de nubes."], respuesta: 0 },
            { pregunta: "Se le llama al fenómeno compuesto en su mayoría por partículas sólidas suspendidas en la atmósfera que la oscurecen: ", opciones: ["HZ (Bruma). ", "BR (Neblina).", "FG (Niebla)."], respuesta: 0 },
            { pregunta: "Se le llama al fenómeno compuesto en su mayoría por partículas de agua en estado líquido o sólido que opalizan el aire, reduciendo la visibilidad por debajo de 5 km: ", opciones: ["HZ (Bruma). ", "BR (Neblina).", "FG (Niebla)."], respuesta: 1 },



            ],
            navegacion: [

            { pregunta: "¿Cuál de las siguientes opciones se ajusta mas a la definición de espacio aéreo?", opciones: ["Es aquella porción de la atmósfera terrestre, sobre tierra o agua, que está sometida y regulada a la soberanía y jurisdicción de un estado en particular, en el cual se prestan los servicios de tránsito aéreo.", "Es aquella porción del aire, sobre tierra de un país que se emplea para facilitar el tránsito aéreo, sin restricciones de ninguna clase para cualquier aeronave que la requiera sobrevolar.", "Cualquiera de las opciones es correcta."], respuesta: 0 },
            { pregunta: "El espacio aéreo controlado es:", opciones: ["Zona del espacio aéreo de un país donde su Autoridad Aeronáutica solamente presta servicios de reglamentación y asesoría para el vuelo.", "Porción del espacio atmosférico con límites definidos donde se presta el servicio de control de tránsito aéreo.", "Una porción de la atmósfera determinada en donde las aeronaves están obligadas a pedir permiso para volar."], respuesta: 1 },
            { pregunta: "El espacio aéreo controlado es una porción de la atmósfera especialmente diseñado para que los UAS puedan realizar operaciones legales y dentro de los más altos estándares de seguridad operacional. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "En Colombia, el espacio aéreo controlado comprende:/1-Zonas de tránsito de aeródromo (ATZ)./2-Zonas prohibidas. /3-Areas de control terminal (TMA)./4-Zonas de entrenamiento./5-Zonas de control (CTR)./6-Áreas de control./7-Zonas restringidas.", opciones: ["Los numerales 1, 2, 3 y 4 son correctos.", "Los numerales 1, 3, 5 y 6 son correctos.", "Los numerales 2, 4 y 7 son correctos."], respuesta: 1 },
            { pregunta: "El espacio aéreo no controlado es un tipo de espacio aéreo con dimensiones conocidas donde se facilitan los servicios completos de tránsito aéreo. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "El espacio aéreo no controlado es:", opciones: ["Porción del espacio atmosférico con límites definidos donde se facilitan servicios de información y asesoramiento únicamente.", "Un concepto de espacio aéreo que incluye áreas restringidas, peligrosas y prohibidas.", "Están clasificados como espacios aéreos clase B y C."], respuesta: 0 },
            { pregunta: "El espacio aéreo no controlado en Colombia comprende:", opciones: ["Espacios aéreos ATZ.", "Espacios aéreos con clasificación F y G.", "Espacios aéreos segregados."], respuesta: 1 },
            { pregunta: "En las áreas o zonas restringidas están absolutamente prohibidas toda clase de vuelos. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "Las áreas o zonas prohibidas están administradas únicamente por la Autoridad de Aviación de Estado. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Cuál es la definición de rumbo?", opciones: ["Es el camino general que se traza en una carta de navegación.", "Es el ángulo formado entre el norte geográfico y la posición en donde me encuentro con respecto a donde quiero llegar. ", "Es la dirección respecto al norte magnético en la que una aeronave se desplaza en vuelo."], respuesta: 2 },
            { pregunta: "¿A qué se le conoce como *HEADING*?", opciones: ["La dirección a la cual apunta la nariz de la aeronave en vuelo.", "La dirección que se estima a donde llegará la aeronave posterior al vuelo.", "La dirección hacia donde se traslada la aeronave en vuelo."], respuesta: 0 },
            { pregunta: "La Rosa de los Vientos es un símbolo en forma de círculo que tiene marcado alrededor los rumbos en que se divide la circunferencia del horizonte, así mismo se representan en letras los puntos cardinales y está referenciado con respecto al norte geográfico. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "De acuerdo con la rosa de los vientos, los cuatro puntos cardinales principales son:", opciones: ["NNW, SSW, ENE, WNW.", "N, S, E, W.", "NW, NE, SE, SW."], respuesta: 1 },
            { pregunta: "Seleccione los tipos de navegación según la técnica de utilización:/1-Visual./2-Marítima./3-A la estima./4-Espacial./5-Astronómica./6-Radionavegación./7-Aérea./8-Satelital./9-Terrestre.", opciones: ["Los numerales 1, 2, 3, 4 y 7 son correctos.", "Los Numerales 1, 3, 5, 6 y 8 son correctos.", "Los numerales 2, 4,7 y 9 son correctos."], respuesta: 1 },
            { pregunta: "La navegación aérea se define como el conjunto de técnicas y procedimientos que permiten guiar de manera eficiente una aeronave de un punto de partida hasta un punto de destino, respecto a la superficie de la tierra, manteniendo en todo momento la ruta deseada. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 0 },
            { pregunta: "Para poder volar una aeronave no tripulada con seguridad, es requisito indispensable que el piloto UAS tenga conocimiento y entrenamiento en técnicas de navegación por instrumentos. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "La palabra usada para definir la distancia vertical comprendida entre el nivel medio del mar y la posición de una aeronave en el aire es:", opciones: ["Altura.", "Elevación.", "Altitud."], respuesta: 2 },
            { pregunta: "¿Qué significa la sigla GNSS?", opciones: ["Global Navigation Satellite System.", "Ground Navigation Syncronic System.", "Global New Positioning System."], respuesta: 0 },
            { pregunta: "Los satélites de comunicaciones fueron diseñados para determinar las coordenadas geográficas de un receptor sin importar si está en el mar, en el aire o en una montaña. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Qué es la navegación GNSS?", opciones: ["Es un tipo de navegación que se comunica con todos los satélites en el mundo, proporcionando referencias de coordenadas en lugares específicos de la tierra. ", "Es un tipo de navegación que emplea sistemas de posicionamiento global pasivos de navegación basados en las emisiones de radiofrecuencia de los satélites, los cuales proporcionan una referencia espacio-temporal.", "Es un tipo de navegación que emplea sistemas retroactivos de emisión de radiofrecuencia con satélites de comunicaciones, proporcionando referencias de coordenadas en cualquier lugar de la tierra."], respuesta: 1 },
            { pregunta: "Para la aviación no tripulada, los sistemas de navegación satelital son considerados como:", opciones: ["Un complemento de la navegación visual.", "Un suplemento de la navegación a la estima.", "El sistema de navegación principal."], respuesta: 2 },
            { pregunta: "El sistema de recepción de satélites de una aeronave no tripulada en Colombia solamente puede ver satélites de las constelaciones autorizadas por la Aerocivil. Este postulado es:", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            { pregunta: "¿Cuál es la definición más acertada para meridianos y paralelos?", opciones: ["Conceptos geográficos que consisten en líneas imaginarias trazadas sobre el globo terrestre y que se utilizan para poder ubicar puntos sobre la superficie de la tierra.", "Son líneas isogónicas trazadas sobre la superficie del globo terráqueo, con la cual se establece la posición de un objetivo.", "Es la cuadrícula estructurada sobre los mapas referenciada con el norte magnético que nos da una idea cercana de donde nos podemos encontrar."], respuesta: 0 },
            { pregunta: "Los paralelos dividen a la tierra en dos partes iguales, y son los que nos dan referencia del día y la noche. Este postulado es:.", opciones: ["Verdadero", "Falso",], respuesta: 1 },
            

            
            ],
            comunicaciones: [
            { pregunta: "¿En qué bandas de frecuencia operan las comunicaciones aeronáuticas?", opciones: ["VLF Muy Baja Frecuencia.", "VHF Muy Alta Frecuencia.", "UHF Ultra Alta Frecuencia."], respuesta: 1 },
            { pregunta: "¿Cuál es la frecuencia de emergencia?", opciones: ["118,0 MHz.", "121,5 MHz.", "122,9 KHz."], respuesta: 1 },
            { pregunta: "¿En dónde se pueden verificar las frecuencias aeronáuticas de comunicación de un aeródromo?", opciones: ["118,0 MHz.", "121,5 MHz.", "122,9 KHz."], respuesta: 1 },
            { pregunta: "¿Qué es interferencia?", opciones: ["Propagación de muchas ondas de radio.", "Intermitencia de una onda de frecuencia.", "Cuando dos señales en la misma onda se interrumpen entre sí."], respuesta: 2 },
            { pregunta: "¿Qué tipo de Interferencias existen?", opciones: ["Ruido atmosférico.", "Ruido producido por el hombre.", "Ambas opciones son correctas."], respuesta: 2 },
            { pregunta: "¿Cuál es el alfabeto utilizado para deletrear en la aviación?", opciones: ["Código “Q” de comunicaciones.", "Lenguaje militar táctico.", "Alfabeto fonético internacional OACI."], respuesta: 2 },
            { pregunta: "De acuerdo con el alfabeto fonético OACI, ¿cuál es el correcto deletreo de la palabra “VUELO”?", opciones: ["Vaca – Uva – Enano – Limón – Opera.", "Victor – Uniform – Eco – Lima – Oscar.", "Vision – Uniform – Eco - Liceo – Omar."], respuesta: 1 },
            { pregunta: "Según el alfabeto fonético de la OACI, la letra equis (x) se pronuncia:", opciones: ["Ex-ruy", "Ex-rey", "Ex-trey"], respuesta: 1 },
            { pregunta: "¿Cómo se verifica que la información suministrada por radio fue correctamente recibida?", opciones: ["Obturando el PTT tres veces al terminar el mensaje.", "Colacionando la información.", "Respondiendo “RECIBIDO” al terminar de escucharla."], respuesta: 1 },
            { pregunta: "¿Qué no puede existir en el proceso de la comunicación? ", opciones: ["Dudas, confusión y ambigüedad.", "Que la información sea veraz.", "Que el idioma sea el mismo."], respuesta: 0 },
            { pregunta: "¿Qué significa PAN-PAN?", opciones: ["Señal de aviso de urgencia.", "Señal de aviso de emergencia.", "Aviso de información aeronáutica."], respuesta: 0 },
            { pregunta: "¿Qué significa MAY DAY - MAY DAY - MAY DAY?", opciones: ["Señal de aviso de Urgencia.", "Señal de aviso de emergencia.", "Aviso de información aeronáutica."], respuesta: 1 },
            { pregunta: "Cuando una aeronave se encuentra en una situación de emergencia, radiotelefónicamente utiliza las palabras:", opciones: ["MAYDAY, MAYDAY, MAYDAY.", "PAN, PAN, PAN.", "SOS."], respuesta: 0 },
            { pregunta: "Cuando una aeronave se encuentra en una situación de urgencia, radiotelefónicamente utiliza las palabras:", opciones: ["MAYDAY, MAYDAY, MAYDAY.", "PAN, PAN, PAN.", "SOS."], respuesta: 1 },
            
                
            ],

             factoreshumanos: [

            { pregunta: "¿Cuál de los siguientes factores humanos afecta significativamente la actuación en la aviación no tripulada?", opciones: ["Altitud.", "Fatiga.", "Peso de las antenas del control remoto."], respuesta: 1 },
            { pregunta: "¿Cuál es un ejemplo adecuado de la carga de trabajo en la aviación no tripulada?", opciones: ["La cantidad de combustible en un UAS.", "La demanda cognitiva y física impuesta a un piloto UAS.", "El peso máximo que un UAS puede llevar."], respuesta: 1 },
            { pregunta: "¿Cuál es el fin de la capacitación en actuaciones humanas?", opciones: ["Reducir los costos operativos.", "Aumentar la velocidad de vuelo.", "Tomar decisiones seguras y efectivas durante las operaciones."], respuesta: 2 },
            { pregunta: "Los sistemas de apoyo digitales (apps), respecto a la toma de decisiones en la operación con UAS:", opciones: ["Automatizan completamente las operaciones de UAS.", "Ayudan a los operadores y pilotos a tomar decisiones informadas.", "Realizan mantenimiento en tiempo real de los UAS."], respuesta: 1 },
            { pregunta: "La fatiga puede afectar la actuación de los pilotos de UAS:", opciones: ["Aumentando la toma de decisiones efectivas por el cansancio.", "Mejorando la concentración en la medida que progresa el vuelo.", "Reduciendo la atención y el tiempo de reacción."], respuesta: 2 },
            { pregunta: "¿Cuál de las siguientes opciones no constituye un factor que afecte la carga de trabajo mental para los pilotos UAS?", opciones: ["Toma de decisiones.", "Demanda cognitiva.", "Altitud de vuelo."], respuesta: 2 },
            { pregunta: "¿Qué tipo de entrenamiento se debe fortalecer para mejorar la actuación del piloto UAS en situaciones de emergencia en la operación de vuelo?", opciones: ["Entrenamiento físico intensivo (Gimnasio).", "Entrenamiento de resistencia (Ditching).", "Practica de reacciones de emergencia en escenarios de entrenamiento."], respuesta: 2 },
            { pregunta: "¿Qué tecnología ayuda a mitigar la carga de trabajo en los pilotos y operadores de UAS?", opciones: ["Inteligencia artificial y automatización.", "Cámaras de alta resolución.", "Sistemas anticolisión, ADS-B."], respuesta: 0 },
            { pregunta: "¿Qué impacto puede tener el estrés en la actuación de los pilotos y operadores de UAS?", opciones: ["Aumenta la adrenalina y propicia la claridad mental.", "Aumenta exponencialmente los errores y reduce la eficiencia.", "Facilita la comunicación y el nivel de concentración."], respuesta: 1 },
            { pregunta: "¿Qué rol juegan las habilidades de liderazgo en la aviación no tripulada?", opciones: ["Son esenciales para los pilotos UAS, pero no lo son para los operadores de UAS.", "Son importantes para la toma de decisiones y organización del equipo de trabajo.", "Solo son relevantes en operaciones militares."], respuesta: 1 },
            { pregunta: "¿Cuál es la importancia de la comunicación dentro del equipo de trabajo en la operación UAS?", opciones: ["No es relevante, ya que los UAS operan de forma automática según la planificación del vuelo gestionada.", "Es vital para coordinar las operaciones y garantizar las acciones de seguridad operacional.", "La comunicación se utiliza sólo en situaciones de emergencia."], respuesta: 1 },
            { pregunta: "¿Cuál de los siguientes factores humanos es clave para la actuación segura en la aviación no tripulada?", opciones: ["La elección de rutas de vuelo.", "La capacitación del piloto.", "La velocidad del viento en vuelo."], respuesta: 1 },
            { pregunta: "¿Qué factor o comportamiento humano es fundamental para evitar la fatiga del piloto en operaciones de vuelo?", opciones: ["Cumplimiento de regulaciones de tiempo de vuelo y descanso.", "Realizar múltiples tareas durante el vuelo.", "Uso de estimulantes en la medida que el piloto los necesite."], respuesta: 0 },
            { pregunta: "¿Qué es la ergonomía cognitiva aplicada a la aviación no tripulada?", opciones: ["Es el estudio de la postura de los operadores y pilotos cuando están en operaciones aéreas con sus aeronaves.", "Es el mejoramiento de la relación entre máquinas y personas para entrelazar factores como la comunicación, trabajo en equipo, percepción, memoria, razonamiento e interrelacionarlo con las capacidades cognitivas humanas de cada persona.", "Es el proceso de mejora de las condiciones y resistencia física de los pilotos y operadores de aeronaves no tripuladas."], respuesta: 1 },
            { pregunta: "¿Cómo puede colaborar la ergonomía cognitiva para mejorar la actuación en vuelo de un piloto UAS?", opciones: ["Optimizando la interfaz de usuario de software.", "Diseñando asientos más cómodos para poder operar.", "Aumentando las cargas intelectuales de trabajo."], respuesta: 0 },
            { pregunta: "¿De las siguientes apreciaciones cuáles constituyen falla humana en contra de la seguridad operacional?", opciones: ["Operar un dron desconociendo las regulaciones y legislaciones que aplican en el desarrollo de las operaciones de vuelo.", "Maniobrar mi dron de forma irresponsable y temeraria en espacios públicos y el empleo de sustancias psicoactivas en la realización de operaciones de vuelo.", "Todas las opciones son correctas."], respuesta: 2 },
            { pregunta: "¿Cuál es el propósito de las regulaciones de tiempo de vuelo y descanso en la aviación?", opciones: ["Aumentar la carga de trabajo de los operadores.", "Evitar la fatiga de los pilotos.", "Aumentar el tiempo de vuelo de los UAS."], respuesta: 1 },
        


             ],


             sms:[

             { pregunta: "Es lo que significa la sigla SMS:", opciones: ["Sistema de la seguridad mixta en operaciones.", "Manejo de riesgos para la seguridad operacional aérea. ", "Sistema de gestión de la seguridad operacional."], respuesta: 2 },
             { pregunta: "Uno de los 4 componentes del SMS en la aviación aplicable a los UAS es:", opciones: ["Manual de calidad del sistema.", "Gestión del riesgo de la seguridad operacional.", "Manual de operaciones."], respuesta: 1 },
             { pregunta: "Estado en el que los riesgos asociados a las actividades de aviación relativas a la operación de las aeronaves se reducen y controlan a un nivel aceptable. Esta definición que corresponde al concepto de:", opciones: ["Nivel de aceptabilidad.", "Seguridad operacional.", "Sistema de gestión de la seguridad operacional."], respuesta: 1 },
             { pregunta: "¿De qué consta la estructura del SMS?", opciones: ["Consta de cuatro (4) componentes y doce (12) elementos.", "Consta de doce (12) componentes y cuatro (4) elementos.", "Ninguna de las opciones es correcta."], respuesta: 1 },
             { pregunta: "¿Cuáles son los componentes del sistema de gestión de la seguridad operacional?", opciones: ["Alcances; Determinación de peligros; Mantenimiento y evaluación.", "Tareas generales; Tareas específicas; Evaluación y mejora.", "Política y objetivos; Gestión de riesgos; Aseguramiento y promoción."], respuesta: 0 },
             { pregunta: "Dentro del componente de políticas y objetivos de la seguridad operacional, el SMS designa la responsabilidad de un ejecutivo de la empresa.", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "EL SMS tiene alcance a_______________ de  la empresa que participa de manera directa e indirecta en las operaciones de la aviación no tripulada.", opciones: ["Todo personal de pilotos.", "Todo personal operativo.", "Todo el personal."], respuesta: 2 },
             { pregunta: "En el SMS no es necesario que un explotador UAS cuente con una política de compromiso con su implementación y desarrollo. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "De las siguientes opciones, ¿cuales son objetivos de la seguridad operacional que debe tener todo explotador UAS?", opciones: ["Reducir y mitigar los riesgos operativos.", "Capacitar y mantener entrenado a todo el personal de la empresa. ", "Todas las anteriores."], respuesta: 2 },
             { pregunta: "La rendición de cuentas es un elemento que no se considera en la implementación del SMS del explotador UAS. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "La observación y medición del rendimiento en materia de seguridad operacional es un elemento del SMS que invita a verificar el sistema mediante:", opciones: ["Estrategias, indicadores y metas de rendimiento. ", "Indicadores y metas de rendimientos.", "Estrategias e indicadores."], respuesta: 0 },
             { pregunta: "Un análisis de riesgos realizado para un vuelo UAS debe contemplar la gestión de riesgos de seguridad operacional del tipo de operación UAS y la condición de vuelo que pretende realizar. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "Un Incidente de aviación se puede identificar como un evento o suceso que involucra a una aeronave sin daños graves, lesiones significativas a personas o pérdida de vidas humanas.", opciones: ["Falso.", "Verdadero.",], respuesta: 0 },
             { pregunta: "¿Cuál de las siguientes opciones se ajusta más a la definición de accidente aéreo?", opciones: ["Todo suceso relacionado con la utilización de una aeronave, que  en el caso de una aeronave no tripulada, que ocurre entre el momento en que la aeronave está lista para desplazarse con el propósito de realizar un vuelo y el momento en que se detiene, al finalizar el vuelo, y se apaga su sistema de propulsión principal, durante el cual cualquier persona sufre lesiones mortales o graves, la aeronave sufre daños o roturas estructurales o la aeronave desaparece o es totalmente inaccesible.", "Sucesos infortunado que, relacionado con la utilización de una aeronave, altera la marcha normal de los acontecimientos y, como consecuencia, hay daños materiales y fatalidades entre las personas involucradas.", "Actuaciones inesperadas por parte del piloto que alteran la marcha normal de los acontecimientos y, como consecuencia, hay daños materiales y fatalidades entre las personas involucradas."], respuesta: 0 },
             { pregunta: "¿Qué se busca con la implementación de la gestión de la seguridad operacional?", opciones: ["El cumplimiento de las normas y procedimientos aeronáuticos, por parte de las aeronaves para evitar posibles colisiones en vuelo, preservando de esta forma la vida de las personas.", "Mitigar proactivamente riesgos de la seguridad operacional antes de que resulten en accidentes o incidentes de aviación. Las actividades de seguridad operacional se deben gestionar de una manera disciplinada, integral y enfocada. ", "Que todas aquellas actuaciones de conciencia situacional sean realizadas por todas las personas, para evitar posibles problemas con las aeronaves."], respuesta: 1 },
             { pregunta: "En general, ¿qué es un sistema de gestión de la seguridad operacional (SMS)?", opciones: ["Conjunto de reglamentos y acciones para evitar hurtos o pérdidas de equipo.", "Conjunto de reglamentos y acciones para mejorar la seguridad en la operación.", "Sistema para mejorar la seguridad física de las instalaciones."], respuesta: 1 },
             { pregunta: "¿Qué características tiene el SMS?", opciones: ["Estructurado, sistemático y proactivo.", "Reactivo, proactivo y predictivo.", "Analítico, reactivo y sancionatorio."], respuesta: 0 },
             { pregunta: "La empresa debe garantizar la cultura del reporte en el SMS y para ello debe realizar:", opciones: ["Procedimientos.", "Manuales.", "Capacitaciones."], respuesta: 2 },
             { pregunta: "Parte del compromiso que debe tener el explotador UAS en el SMS es el de:", opciones: ["Sancionar.", "Promocionar la cultura del reporte.", "Implementar protocolos y procedimientos."], respuesta: 1 },
             { pregunta: "El medio oficial de comunicación de la seguridad operacional que debe implementar el explotador UAS debe ser tan claro que garantice:", opciones: ["Que todo el personal conozca el SMS, con arreglo al puesto de trabajo que ocupe. ", "Que mantiene en reserva la información crítica para la seguridad operacional.", "Que las medidas de seguridad operacional que se adopten son implementadas sin dar indicios del por qué se tomaron."], respuesta: 0 },
             { pregunta: "La empresa definirá y mantendrá un proceso para identificar los cambios que puedan afectar al nivel de riesgo de seguridad operacional asociado a sus operaciones UAS, así como para identificar y manejar los riesgos de seguridad operacional que puedan derivarse de esos cambios. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "El SMS determina que se debe establecer un procedimiento interno de notificación e investigación de sucesos. Esto puede incluir los MOR, que significan:", opciones: ["Reportes obligatorios de eventos.", "Manejo oportuno de reportes.", "Reportes operacionales mínimos."], respuesta: 0 },
             { pregunta: "Dentro del SMS se realizan revisiones periódicas a la operación para la identificación de peligros y la evaluación de riesgos.  Participar en la gestión de los riesgos es responsabilidad de:", opciones: ["Los clientes.", "Los auditores.", "Los pilotos."], respuesta: 2 },
             { pregunta: "La empresa deberá nombrar un _______________, que será el responsable de la implementación y mantenimiento del SMS.", opciones: ["Coordinador aéreo.", "Director del sistema.", "Gerente de seguridad operacional."], respuesta: 2 },
             { pregunta: "Es requisito de la norma contar con documentación para el sistema SMS; entre otros, con:", opciones: ["Código de SMS y listas de verificación.", "Manual de SMS o capítulo SMS en el MO.", "Plan de SMS y formato de registro de UAS."], respuesta: 1 },
             { pregunta: "La implementación apropiada del SMS garantiza que las auditorías internas, la rendición de cuentas y el seguimiento a los planes, programas y procedimientos mediante indicadores, aporten:", opciones: ["Mejora continua y gestión del cambio. ", "Cumplimiento de los cronogramas.", "Identificación de peligros."], respuesta: 0 },
             { pregunta: "¿Cuáles son los métodos para la identificación de los peligros?", opciones: ["Método descriptivo, método reactivo y método rotativo.", "Método predictivo, método proactivo y método reactivo.", "Método predictivo, método descriptivo y método rotativo."], respuesta: 1 },
             { pregunta: "El método predictivo para la identificación de los peligros se enfoca en tomar medidas preventivas para reducir la probabilidad de que ocurran incidentes o accidentes. Esto implica la implementación de políticas, procedimientos y controles diseñados para mitigar riesgos conocidos o identificados. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "El método reactivo se aplica después de que ha ocurrido un incidente o accidente y se centra en responder a las situaciones de emergencia para tomar medidas correctivas y evitar que incidentes similares vuelvan a ocurrir en el futuro. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "La definición más acertada de peligro en el contexto de la seguridad operacional es:", opciones: ["Condición u objeto que potencialmente puede causar lesiones al personal y/o daños o destrucción del equipo.", "Condición nerviosa frente a una actividad.", "Medida, en términos de severidad y probabilidad, de que algo pueda ocurrir y sus consecuencias."], respuesta: 0 },
             { pregunta: "El peligro es la evaluación de las consecuencias de la posibilidad de que el piloto pierda el control de la aeronave, expresada en términos de probabilidad y severidad. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "¿Cuáles son las fuentes más comunes para la identificación de peligros?", opciones: ["Reportes de incidentes / Accidentes y revisión de documentación.", "Investigación de accidentes, regulaciones.", "Todas las opciones son correctas."], respuesta: 2 },
             { pregunta: "¿Defina qué es riesgo en el contexto de la seguridad operacional?", opciones: ["Condición nerviosa frente a una actividad.", "Nivel de incertidumbre ante la ocurrencia de un suceso y que este pueda tener componentes perjudiciales.", "Probabilidad y gravedad proyectada de la consecuencia o el resultado de una situación o peligro existente."], respuesta: 2 },
             { pregunta: "Los elementos del componente de gestión del riesgo del SMS son: Identificación de peligros, y evaluación y mitigación de seguridad operacional. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "El proceso de gestión de la seguridad operacional inicia con:", opciones: ["La obtención de los datos.", "La implementación de las estrategias.", "La identificación de los peligros."], respuesta: 2 },
             { pregunta: "En el contexto de la seguridad operacional, la definición más acertada para 'probabilidad' es:", opciones: ["Posibles efectos de un evento o condición insegura.", "Consecuencias de un riesgo.", "Calificación de la frecuencia de posibilidad de que un evento ocurra."], respuesta: 2 },
             { pregunta: "En el contexto de la seguridad operacional, ¿qué es severidad del riesgo?", opciones: ["La calificación de las consecuencias posibles de un evento tomando como referencia el peor escenario previsible.", "Consecuencias de un peligro.", "Posibilidad que un evento no pueda ocurrir."], respuesta: 0 },
             { pregunta: "En el contexto de la seguridad operacional, según la OACI, ¿cuáles son las clases de severidad?", opciones: ["Depende del explotador UAS la forma cómo sean determinadas. ", "Catastrófico, peligroso, mayor, menor, insignificante.", "Frecuente, ocasional, remoto, improbable, extremadamente improbable."], respuesta: 1 },
             { pregunta: "En el contexto de la seguridad operacional, ¿qué es mitigación?", opciones: ["Reducir la posibilidad de daño por descuido.", "Disminuir la actividad operacional.", "Medidas que eliminan o reducen la probabilidad o severidad del riesgo."], respuesta: 2 },
             { pregunta: "Los propósitos generales perseguidos por la implementación del SMS abarcan: 1-Protección de la seguridad pública e integración segura en el espacio aéreo. 2-Protección de la privacidad y prevención de accidentes y daños. 3-Gestión de riesgos y cumplimiento legal y regulatorio. 4-Fomento de una cultura de seguridad e investigación y análisis de incidentes.", opciones: ["Los numerales 1, 2 y 3 son correctos.", "Todos los numerales son correctos.", "Los numerales 2 y 3 son incorrectos."], respuesta: 1 },
             { pregunta: "¿Cuál es el objetivo de la seguridad operacional que se aborda con la capacitación adecuada y la gestión de la fatiga?", opciones: ["Gestión del tránsito aéreo.", "Errores humanos.", "Cultura de seguridad física."], respuesta: 1 },
             { pregunta: "¿Cuál es el objetivo de la Seguridad Operacional que se aborda mediante la coordinación acertada del flujo de aeronaves y el garantizar un espacio aéreo seguro?", opciones: ["Gestión del tránsito aéreo.", "Mantenimiento y fiabilidad de las aeronaves.", "Cultura de seguridad física."], respuesta: 0 },
             { pregunta: "El ABC del análisis del peligro, es:", opciones: ["Establecer el peligro genérico (formulación), identificar los componentes específicos del peligro y orientar a la tripulación para evitar los riesgos específicos.", "Establecer el riesgo específico (formulación), identificar los componentes de ese riesgo específico y orientar a la tripulación para evitar actividades que desencadenen en peligros.", "Identificar el peligro, analizar y calificar el riesgo, mitigar el riesgo."], respuesta: 0 },
             { pregunta: "La información documentada no es considerada un proceso indispensable en el sistema de mitigación de la seguridad operacional. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "La documentación de los peligros es una necesidad de estandarización al interior de la empresa y, para ello, incluye la definición y comprensión específica de un tipo de peligro, acompañado de su aplicación, reporte, medición y gestión específica del riesgo, como política de seguridad común y general. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "La identificación de peligros es un proceso continuo del SMS; debe ser parte de un ciclo de mejora continua de la seguridad operacional. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "En el contexto de la seguridad operacional, ¿cuáles son las clases de severidad?", opciones: ["Depende del explotador UAS el cómo serán determinadas. ", "Únicamente peligroso e insignificante.", "Frecuente, ocasional, remoto, improbable, extremadamente improbable."], respuesta: 0 },


             ],


             conocimientosgenerales:[


             { pregunta: "De acuerdo con la norma RAC 1, la definición de aeronave es:", opciones: ["Toda nave o aparato que sin importar su peso puede surcar el cielo y está destinada a volar con o sin piloto.", "Toda máquina que puede sustentarse en la atmósfera por reacciones del aire que no sean las reacciones del mismo contra la superficie de la tierra.", "Ambas definiciones son correctas."], respuesta: 1 },
             { pregunta: "En el mundo aeronáutico, ¿a que se refiere la expresión 'dron'?", opciones: ["Palabra genérica empleada para referirse a cualquier aeronave no tripulada o pilotada a distancia.", "Abejorro o zángano, por el 'zumbido' de los rotores.", "Cualquier tipo de vehículo aéreo tripulado o aeromodelo."], respuesta: 2 },
             { pregunta: "La sigla “RPAS” se emplea genéricamente para referirnos a cualquier clase de aeronaves no tripuladas. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 1 },
             { pregunta: "¿Qué significa la sigla “UAS”?", opciones: ["Unmmaned Aircraft System / Sistema de aeronave no tripulada.", "Aerial Aircraft Support / Aeronave no tripulada. ", "Aerial Vehicle System / Vehículo aéreo no tripulado."], respuesta: 1 },
             { pregunta: "¿Qué significa la sigla “RPAS”? ", opciones: ["Remotely Piloted Aircraft Software / Aeronaves piloteadas remotamente por software.", "Remotely Pylon Aerial System / Aeronaves pilotadas a la distancia.", "Remotely Piloted Aircraft System / Sistema de aeronave remotamente pilotada."], respuesta: 2 },
             { pregunta: "¿Qué significa la sigla UAV?", opciones: ["Unmmaned Aircraft Visual / Sistema visual aéreo no tripulado. ", "Unmmaned Aerial System / Sistemas de aeronaves remotamente piloteadas. ", "Ummaned Aerial Vehicle / Vehículo aéreo no tripulado."], respuesta: 2 },
             { pregunta: "De las siguientes opciones, seleccione la que contenga componentes que NO forman parte de un UAS:", opciones: ["Fuselaje, baterías, antenas, tren de aterrizaje, satélites.", "Chasis, baterías, planta(s) de potencia, tarjeta controladora.", "Chasis, computadora, sensores, baterías y control remoto."], respuesta: 0 },
             { pregunta: "¿Qué tipo de motores eléctricos empleados por los UA son más eficientes?", opciones: ["Motores trifásicos con escobillas.", "Motores monofásicos estriados.", "Motores trifásicos sin escobillas."], respuesta: 2 },
             { pregunta: "¿Qué tipo de baterías empleadas por los UA son las más comunes?", opciones: ["Li-Fe.", "Ni-Cd.", "Li-Po."], respuesta: 2 },
             { pregunta: "¿Cuál es la principal precaución que se debe tener cuando se inicia un ciclo de carga de las baterías?", opciones: ["Sobrepasar el tiempo de carga.", "Supervisarlas siempre mientras estas se cargan.", "Cargarlas inmediatamente después del vuelo."], respuesta: 1 },
             { pregunta: "¿Cuál es la funcionalidad del ESC en un sistema de propulsión eléctrico?", opciones: ["Control de velocidad electrónico, para medir la fuerza del motor.", "Electronic Speed Controller, que envía la corriente necesaria para mantener las revoluciones de los motores exigidas por la tarjeta controladora.", "Electronic Speed Controller, que controla la corriente que produce el generador."], respuesta: 1 },
             { pregunta: "¿Qué función realiza la computadora de vuelo del UA?", opciones: ["Controla la carga de las baterías.", "Controla el funcionamiento en vuelo de la UA.", "Programa el control remoto."], respuesta: 1 },
             { pregunta: "¿Para qué se usa un sistema RTK (Real Time Kinetic)?", opciones: ["Aumentar la precisión de la UA con base en una antena en tierra.", "Aumentar la señal de los satélites.", "Emitir una señal que evita la interferencia electrónica."], respuesta: 1 },
             { pregunta: "¿Qué es el OSD?", opciones: ["Sensor de obstáculos direccional.", "On Screen Display, mezcla la imagen de la cámara con la información de telemetría.", "On Screen Display, transmite únicamente la señal de la cámara a la pantalla."], respuesta: 1 },
             { pregunta: "¿Cuál es la frecuencia más común en la señal de comunicación de una UA con la estación de tierra?", opciones: ["326 GHz.", "2,4 GHz.", "1,5 GHz."], respuesta: 1 },
             { pregunta: "¿Cuáles de las siguientes frecuencias de transmisión de la señal desde el control son las mas comunes?", opciones: ["2,4 GHz a 5,8 GHz.", "2,4 MHz a 5,8 MHz.", "118 MHz a 2,4 GHz."], respuesta: 1 },
             { pregunta: "¿Qué función cumple el 'gimbal'?", opciones: ["Aumenta la precisión del GPS. ", "Mejora la señal de transmisión de video.", "Estabiliza el movimiento de la cámara."], respuesta: 2 },
             { pregunta: "¿Qué precaución hay que tener con los sensores ópticos?", opciones: ["Solo funcionan con buena luminosidad.", "Deben estar alejados de la luz fuerte o láser porque los puede dañar.", "Las dos opciones son correctas."], respuesta: 2 },
             { pregunta: "En la región de América del Sur, para la configuración del movimiento de las palancas de la estación terrena, ¿qué modo debe ser seleccionado?", opciones: ["Modo uno.", "Modo dos.", "Modo cine, normal, sport."], respuesta: 1 },
             { pregunta: "¿Cuál es la característica de operación del comando RTH?", opciones: ["La UA mantiene su posición cuando pierde señal.", "La UA regresa automáticamente al origen.", "La UA regresa a su última posición de vuelo."], respuesta: 1 },
             { pregunta: "¿Mínimo con cuántos satélites enlazados al sistema de navegación se recomienda volar en modo de asistencia satelital?", opciones: ["Tres satélites.", "Doce satélites.", "Cinco satélites."], respuesta: 1 },
             { pregunta: "En zonas de despegue, ¿qué tipos de superficies pueden generar interferencia en la operación de la UA?", opciones: ["Superficies lisas.", "Superficies metálicas.", "Superficies de madera."], respuesta: 1 },
             { pregunta: "¿Cual es la carga de voltaje nominal medio que tiene cada celda en una batería Li-Po?  ", opciones: ["3,7 voltios.", "12 voltios.", "3,5 voltios."], respuesta: 0 },
             { pregunta: "¿Qué es el índice KP?", opciones: ["La cantidad de satélites que puede alinear el dron.", "El índice geomagnético planetario.", "La cantidad de luminosidad del día."], respuesta: 1 },
             { pregunta: "¿Con qué porcentaje de carga de batería se deben almacenar las baterías Li-Po para evitar su deterioro?", opciones: ["0 %.", "20 %.", "50 a 60 %."], respuesta: 2 },
             { pregunta: "¿Qué es el enlace C2?", opciones: ["Es la vía de comunicación que conecta la UA con su control y permite la transmisión de datos en ambas direcciones. ", "Es el canal que permite el control de la UA, pero no tiene retroalimentación de las condiciones de la aeronave en tiempo real.", "Es una tecnología automatizada que permite recopilar, desarrollar y transmitir información de un dispositivo electrónico a otro."], respuesta: 0 },
             { pregunta: "Al sistema de medición de magnitudes físicas que permite transmitir los datos obtenidos a un observador lejano se le conoce como:", opciones: ["Transmisión de datos.", "Telemetría.", "Enlace C2."], respuesta: 1 },
             { pregunta: "La estación de control en tierra de una aeronave no tripulada, permite al operador UA o piloto UAS dirigir el vuelo de la UA. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "La función “ALTITUDE HOLD” hace referencia a:", opciones: ["Ayuda a mantener siempre la misma altura, sin importar los comandos que le dé el piloto.", "Ayuda a mantener la altura establecida por el piloto en el RTH.", "Corrige y mantiene automáticamente la altura de vuelo de la UA a la última altura establecida por el piloto en el vuelo."], respuesta: 2 },
             { pregunta: "¿Qué significa el modo “RTH” y para qué sirve?", opciones: ["Reset to House. Permite regresar la configuración del UA a la de la casa fabricante.", "Return to Home. Permite que la UA retorne a las coordenadas previas de despegue.", "Re-Start and Hold. Permite reencender el dron en vuelo y mantenerlo en espera."], respuesta: 1 },
             { pregunta: "De las siguientes opciones, seleccione la que actualmente aplica para los UAS: ¿Qué parámetros requiere el modo RTH?", opciones: ["Establecer las coordenadas de salida por parte del piloto.", "Solamente se debe establecer la altura segura de regreso.", "No requiero parametrizar el RTH, ha sido establecido de fábrica."], respuesta: 1 },
             { pregunta: "En algunos modelos de UAS, el modo RTH es el mismo modo RTL de otros modelos. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "De las siguientes opciones, seleccione las tecnologías que permiten la detección de obstáculos en tiempo real para un UAS:", opciones: ["Sistemas de radar, sensores ópticos y 'LiDAR'.", "Sistemas de mensajería instantánea.", "Códigos QR."], respuesta: 0 },
             { pregunta: "¿Cuál de las siguientes tecnologías NO se utiliza para el control de operaciones aéreas con UAS?", opciones: ["5G.", "GPS.", "Radiocontrol."], respuesta: 1 },
             { pregunta: "¿Qué significa la sigla VTOL?", opciones: ["Vertical Take Off and Landing / Aeronave de despegue y aterrizaje vertical.", "Visual Talk Off Line / Aeronave de despegue y aterrizaje horizontal.", "Virtual Takeoff and Landing / Despegue y aterrizaje virtual."], respuesta: 0 },
            


             ],


             planificaciondevuelo:[


             { pregunta: "¿Qué se entiende por la sigla NOTAM?", opciones: ["Noticias para el hombre del mar. ", "Informes operacionales periódicos.", "Aviso a los aviadores. Información de carácter de temporal e importante para las operaciones aéreas."], respuesta: 2 },
             { pregunta: "¿Qué es la AIP?", opciones: ["Publicación de Información Aeronáutica.", "Aerodrome Instrument Procedures.", "Aplicación Informativa Periódica."], respuesta: 0 },
             { pregunta: "¿Qué limitaciones de la UA debemos contemplar en la planificación del vuelo?", opciones: ["Estados de ansiedad del piloto u operador.", "Limitaciones de seguridad: Altura máxima, distancia máxima, rango de operación y PMBO.", "Limitaciones físicas y psicológicas del piloto."], respuesta: 1 },
             { pregunta: "Con respecto a los espacios aéreos, ¿cuál es una buena práctica antes de planificar un vuelo?", opciones: ["Revisar la meteorología, para estar seguros de contar con las condiciones favorables para nuestro vuelo.", "Revisar las condiciones normativas, para poder realizar el permiso de vuelo acorde con el trabajo que se requiere hacer.", "Revisar el área en donde se va a realizar la operación para determinar si se podría estar incurriendo en algún área de control o zona especial."], respuesta: 2 },
             { pregunta: "¿Cuál de las siguientes tareas no corresponde a una actividad de preparación operacional de un vuelo UAS?", opciones: ["Analizar los espacios aéreos y zonas de control.", "Reunión final del vuelo.", "Diseño de las misiones de vuelo y ciclos de baterías."], respuesta: 1 },
             { pregunta: "De las siguientes, ¿cuáles son las prácticas que contribuyen a la seguridad operacional del vuelo con UAS que todo piloto UAS debe aplicar?", opciones: ["Capacitación y certificación, planificación de vuelo y mantenimiento regular.", "Comprobaciones post-vuelo.", "Entrega de trabajo final y reporte de misión cumplida."], respuesta: 0 },
             { pregunta: "De las siguientes, ¿cuáles son las prácticas que contribuyen a la seguridad operacional de vuelo con UAS que todo explotador-piloto UAS debe aplicar?", opciones: ["Actualización de firmware y software; plan de emergencia.", "Seguimiento visual; gestión de la batería.", "Todas las opciones son correctas."], respuesta: 2 },
             { pregunta: "Las limitaciones operacionales están dadas por las características técnicas de la aeronave, el pronóstico meteorológico y el diseño de las maniobras de vuelo para administrar apropiadamente las condiciones de riesgo. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "¿Cuál de las siguientes consideraciones es crucial al planificar un vuelo con UAS en zona urbana?", opciones: ["La altitud máxima permitida.", "La densidad de población y la clase de espacio aéreo.", "La capacidad de carga de la aeronave."], respuesta: 1 },
             { pregunta: "¿Cuál es el objetivo principal de la seguridad operacional en la aviación no tripulada?", opciones: ["Garantizar la seguridad de las operaciones con UAS y su integración segura en el espacio aéreo.", "Promover una cultura de seguridad y cumplimiento de las regulaciones.", "Las dos opciones son correctas."], respuesta: 2 },
             { pregunta: "¿Cuál es el propósito principal de una operación de vuelo UAS?", opciones: ["Cumplir con los objetivos de la misión.", "Garantizar que el dron tenga suficiente combustible.", "Definir las restricciones de altura máxima."], respuesta: 0 },
             { pregunta: "Algunos requisitos qué se deben incluir en una solicitud de autorización de vuelo UAS son: ", opciones: ["Color del equipamiento del personal operacional en campo.", "El equipo de protección personal del piloto UAS.", "La información del análisis de riesgos - SMS, áreas geográficas de vuelo, marca y modelo de la UA, pilotos UAS."], respuesta: 2 },
             { pregunta: "¿Por qué es importante conocer, entender y verificar la regulación antes de planificar un vuelo UAS?", opciones: ["Para evitar violaciones de las restricciones consignadas en la norma, de espacio aéreo y maximizar la seguridad operacional.", "Para asegurarse de que la aeronave pueda cumplir con las restricciones determinadas en la norma.", "Para determinar el monto de las tarifas que nos pueden aplicar por el trámite administrativo y operacional del UAS."], respuesta: 0 },
             { pregunta: "¿Cuál de las siguientes fuentes de información es esencial para planificar un vuelo seguro con un UAS?", opciones: ["Listados de actualizaciones de aeronaves no tripuladas expedidos por la página oficial del fabricante.", "Diarios oficiales con las ultimas noticias del país e información económica que afecte el mercado de aeronaves no tripuladas.", "Espacios aéreos, pronóstico meteorológico actualizado y NOTAMS aplicables al lugar donde se realizará la operación, entre otros."], respuesta: 2 },
             { pregunta: "¿Cuál NO sería una consideración al seleccionar una ubicación de despegue y aterrizaje para una UA?", opciones: ["El color de la superficie del terreno.", "El tiempo de vuelo, según la cantidad de baterías o combustible disponible.", "La dirección e intensidad del viento al momento del despegue."], respuesta: 0 },
             { pregunta: "De las características técnicas de una UA en cuanto a sus limitaciones operacionales, ¿qué aspectos se deben tener en cuenta para realizar una excelente planificación de vuelo?", opciones: ["Velocidad máxima, autonomía de vuelo y color de la UA.", "FPV, altura máxima, EPP del piloto UA y frecuencia de operación.", "Altura máxima, velocidad máxima y PMBO de la UA."], respuesta: 2 },
             { pregunta: "¿Cuáles son algunos de los aspectos que se deben verificar antes de encender una UA con el propósito de volarla?", opciones: ["Si está bien embalada en su contenedor.", "Si se cuenta con la cantidad de baterías suficientes para poder concluir la misión exitosamente.", "El estado y la funcionalidad de la aeronave, incluyendo fuente de potencia y sensores."], respuesta: 2 },
             { pregunta: "¿Qué debe hacerse si se encuentra con condiciones meteorológicas adversas durante un vuelo con UAS?", opciones: ["Aumentar la velocidad para completar la misión rápidamente.", "Aterrizar de manera segura y suspender la operación hasta que las condiciones mejoren.", "Llevar en vuelo el dron hacia una zona donde haya mejores condiciones meteorológicas."], respuesta: 1 },
             { pregunta: "¿Cuál es una consideración al desarrollar una misión de vuelo con un UAS que requiera operar cerca de aeropuertos o helipuertos?", opciones: ["Aumentar la altitud de la UA para evitar colisiones y tener la capacidad de realizar maniobras evasivas rápidas.", "Realizar un CDM (si aplica) y obtener los permisos especiales correspondientes de la Aerocivil.", "Contar con un sistema de mantenimiento en tiempo real para la UA."], respuesta: 1 },
             { pregunta: "El propósito principal de consultar los NOTAMS de un sector específico en relación con la planificación del vuelo con UAS es enterarse de las alertas, restricciones del espacio aéreo y situaciones especiales con suficiente anticipación. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0 },
             { pregunta: "El propósito principal de consultar los NOTAMS de un sector específico en relación con la planificación del vuelo con UAS es enterarse de alertas de fenómenos meteorológicos significativos con suficiente anticipación. Este postulado es:", opciones: ["Verdadero.", "Falso.",], respuesta: 0},
            


             ]
    
        };



function seleccionarPreguntasAleatorias(categoria, cantidad) {
    const preguntasAleatorias = [];
    const indicesSeleccionados = new Set();

    
    if (categoria.length < cantidad) {
        alert(`La categoría no tiene suficientes preguntas. Se seleccionarán solo ${categoria.length} preguntas.`);
        cantidad = categoria.length;  
    }

    while (preguntasAleatorias.length < cantidad) {
        const indiceAleatorio = Math.floor(Math.random() * categoria.length);
        if (!indicesSeleccionados.has(indiceAleatorio)) {
            preguntasAleatorias.push(categoria[indiceAleatorio]);
            indicesSeleccionados.add(indiceAleatorio);
        }
    }

    console.log(`Preguntas seleccionadas: ${preguntasAleatorias.length}`);
    return preguntasAleatorias;
}


function obtenerPreguntasSeleccionadas() {
    preguntasSeleccionadas = [];  
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.derechoAereo, 4));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.rac100, 20));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.aerodinamica, 2));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.meteorologia, 6));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.navegacion, 7));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.comunicaciones, 2));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.factoreshumanos, 2));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.sms, 2));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.conocimientosgenerales, 3));
    preguntasSeleccionadas.push(...seleccionarPreguntasAleatorias(preguntas.planificaciondevuelo, 2));


    return preguntasSeleccionadas;
}


function iniciarExamen() {
    nombreEstudiante = document.getElementById('nombre').value;
    documentoEstudiante = document.getElementById('documento').value;

    if (nombreEstudiante === "" || documentoEstudiante === "") {
        alert("Por favor, ingrese su nombre, número de documento y Correo electónico.");
        return;
    }

   
    document.getElementById("datosEstudiante").classList.remove("active");
    document.getElementById("examen").classList.add("active");

   
    cargarPreguntas();

   
    iniciarTemporizador();
}


function cargarPreguntas() {
    const preguntasSeleccionadas = obtenerPreguntasSeleccionadas();
    const formularioExamen = document.getElementById('formularioExamen');
    formularioExamen.innerHTML = '';

    
    if (preguntasSeleccionadas.length === 0) {
        alert("No se han seleccionado preguntas.");
        return;
    }

    preguntasSeleccionadas.forEach((pregunta, index) => {
        const card = document.createElement('div');
        card.className = 'question-card';
        card.innerHTML = ` 
            <p><strong>${index + 1}. ${pregunta.pregunta}</strong></p>
            ${pregunta.opciones.map((opcion, i) => ` 
                <label>
                    <input type="radio" name="pregunta${index}" value="${i}">
                    ${opcion}
                </label>
            `).join('')}`;
        formularioExamen.appendChild(card);
    });
}


function iniciarTemporizador() {
    let tiempoRestante = 60 * 40; 
    let temporizador = setInterval(() => {
        const minutos = Math.floor(tiempoRestante / 60);
        const segundos = tiempoRestante % 60;
        document.getElementById('contador').innerText = `${String(minutos).padStart(2, '0')}:${String(segundos).padStart(2, '0')}`;

        if (tiempoRestante === 0) {
            clearInterval(temporizador);
            mostrarResultados();
        } else {
            tiempoRestante--;
        }
    }, 1000);
}

n
function mostrarResultados() {
    const formularioExamen = document.getElementById('formularioExamen');
    const preguntas = formularioExamen.getElementsByClassName('question-card');
    let puntajeTotal = 0;
    let respuestasCorrectas = 0;

    
    Array.from(preguntas).forEach((preguntaCard, index) => {
        const selectedOption = preguntaCard.querySelector('input[type="radio"]:checked');
        const correctAnswer = preguntasSeleccionadas[index].respuesta;

        if (selectedOption) {
            if (parseInt(selectedOption.value) === correctAnswer) {
                respuestasCorrectas++;
            }
        }
    });

    puntajeTotal = Math.round((respuestasCorrectas / preguntasSeleccionadas.length) * 100);

  
    document.getElementById("examen").classList.remove("active");
    document.getElementById("resultados").classList.add("active");

   
    document.getElementById("resultNombre").innerText = nombreEstudiante;
    document.getElementById("resultDocumento").innerText = documentoEstudiante;
    document.getElementById("resultCorrectas").innerText = respuestasCorrectas;
    document.getElementById("totalPreguntas").innerText = preguntasSeleccionadas.length;
    document.getElementById("resultPuntaje").innerText = puntajeTotal;

}

</script>
