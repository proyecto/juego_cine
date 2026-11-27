ESPECIFICACIÓN DE JUEGO: PLATÓ 28 – HOLLYWOOD, 1954 (6 JUGADORES)

Usa el archivo gato.html como plantilla técnica exacta (mantén el mismo sistema de sincronización en tiempo real con Paho MQTT + BroadcastChannel, el panel de anfitrión para Rafa, el sistema de contraseñas, el ranking de votos en vivo por ronda y la estructura visual de tarjetas intel-block), para crear un nuevo archivo HTML llamado plato28.html ambientado en el Hollywood de 1954 para 6 jugadores.

1. REGLAS CRÍTICAS DE DISEÑO Y SEGURIDAD

Regla Crítica 1: El asesino no sabe que lo es hasta la Ronda 3

Inocencia aparente en Rondas 1 y 2: En la ficha permanente (subtitle, fachada, secreto, rencillas, alibi) y en las pistas de Ronda 1 y Ronda 2, TODOS los personajes (incluido el asesino real) deben estar escritos como inocentes que creen no haber cometido el crimen, aunque todos tengan motivos oscuros de vida o muerte, líos comprometedores y secretos que ocultar.

Desbloqueo automático en Ronda 3 (#killer-reveal):

Al verdadero asesino: Le muestra un aviso secreto en rojo revelándole que él/ella es el asesino real, explicándole brevemente cómo cometió el crimen (decapitación de Arthur Vance y ocultación de la cabeza en la caja de FX) y dándole instrucciones para defenderse y desviar sospechas durante toda la Ronda 3 antes de la votación final.

Al resto de jugadores: Les muestra un aviso en verde confirmando que son inocentes y advirtiendo de que el verdadero asesino acaba de ser notificado y va a intentar engañarles.

Regla Crítica 2: Modo Ciego Total (Cero spoilers para Rafa)

Rafa va a jugar como un participante más (Jack Miller).

Elige en secreto al asesino entre los 6 jugadores. Anne Harper NUNCA puede ser la asesina.

NO digas quién es el culpable en el chat ni en comentarios del código.

Codifica en Base64 tanto la identidad del culpable (CIPHER_CULPRIT) como los textos del aviso secreto de la Ronda 3 (#killer-reveal) para que Rafa no pueda leerlos por accidente si abre el archivo HTML.

Al finalizar la generación del archivo, muestra únicamente la lista de contraseñas de los 6 personajes para repartirlas en mesa.

2. ARQUITECTURA TÉCNICA Y REGLAS DE EQUILIBRIO

Partida cerrada de 6 jugadores: Elimina cualquier referencia a un séptimo personaje. Todo el diseño, las pistas y los enredos giran exclusivamente en torno a los 6 personajes fijos.

Duración, Pausa y Fases del Juego:

Temporizador de 12 minutos por ronda (configurable entre 10 y 15 minutos) para las Rondas 1, 2 y 3.

Incluye un botón de Pausa / Reanudar en el panel del anfitrión que congele el reloj en tiempo real para todos los jugadores conectados.

Fases exactas (5 botones en el panel de anfitrión): Ronda 1 → Ronda 2 → Ronda 3 (Revelación) → Alegato Final (30s–1 min) → Votación Final.

Fase de Alegato Final: Al activar esta fase, el reloj cambia automáticamente a un temporizador de 1 minuto (60 segundos) (con botón de reinicio rápido en el panel del anfitrión para ir dando turno a cada uno de los 6 jugadores) y la pantalla muestra un aviso destacado en dorado indicando que cada sospechoso tiene entre 30 segundos y 1 minuto mirando a los ojos a la mesa para defender su inocencia y acusar directamente a otra persona, manteniendo bloqueados los botones de voto definitivo hasta pasar a la fase de Votación Final.

Cambia el MQTT_TOPIC a uno exclusivo (ej. plato28_hollywood_1954/game).

Paridad Total de Sospecha (3 señalados por ronda, empate técnico en Ronda 3):

En cada ronda, las pistas y hallazgos ponen pruebas directas en contra de 3 participantes distintos, garantizando que al finalizar la Ronda 3 absolutamente los 6 jugadores hayan recibido acusaciones graves y tengan pruebas físicas y motivos sólidos en su contra (ej. Ronda 1: Al, Jack, Betty; Ronda 2: Evelyn, Irma, Jack/Al; Ronda 3: Anne, Betty/Evelyn, Irma).

Prohibido el "candidato obvio": Ninguna pista debe señalar de forma inequívoca al asesino real ni exculpar por completo a nadie. Al llegar a la Ronda 3, todos deben tener exactamente el mismo nivel de sospecha objetiva sobre la mesa, de modo que la votación final dependa exclusivamente de la psicología, la capacidad de mentir o defenderse y los cruces de acusaciones en vivo.

Coartadas Espaciales Cruzadas (Paradero Declarado 22:30 – 23:30):

Cada ficha de personaje debe incluir un bloque destacado con su Paradero Declarado entre las 22:30 y las 23:30 (franja exacta del crimen), diseñado con huecos de tiempo y contradicciones (como el desmayo por champán de Evelyn frente a las salidas de Betty) para que ninguna pareja quede blindada.

3. AMBIENTACIÓN, ENREDOS Y EVENTOS DE SERIE B (globalStories)

Título: Plató 28 – Hollywood, 1954 (Último día de rodaje de «Sombra en el Paraíso»).

Estética: Cine negro años 50 (negro, dorado envejecido, rojo oscuro).

El misterio detrás de la película: Nadie en Hollywood daba un duro por «Sombra en el Paraíso»: una estrella venida a menos (Evelyn), una guionista arruinada con fama de informal (Betty) y una directora novel (Irma). Para las tres era su gran oportunidad y las únicas que creían en el éxito. El resto de la industria sabía que aquello no prometía nada… lo que abre la gran pregunta de la noche: ¿por qué Arthur Vance financió y rodó realmente esta película y de quién era el dinero?

Enredos de Camerino (Bisexualidad y Celos en el Rodaje): Todos los personajes del reparto —a excepción de Jack Miller— son bisexuales y, aunque nadie mantiene una pareja formal dentro del juego, durante los meses de rodaje han surgido encuentros clandestinos, romances esporádicos y ataques de celos cruzados entre ellos (Evelyn con Betty y Al; Betty con Evelyn e Irma; Al con Evelyn e Irma; Irma con Betty, Al y Anne; Anne con Irma). Estas aventuras nocturnas sirven tanto de coartada comprometedora como de detonante de sospechas cuando alguien intenta ocultar con quién estuvo antes del crimen.

Desarrollo por Fases

Ronda 1 — El Hallazgo en la Caja de FX y el Maletín de Chicago:

"Se acabó el rodaje. El Plató 28 es un caos de cables, focos apagados, decorados a medio desmontar y camerinos vaciándose. Vosotros sois los últimos que quedáis dentro recogiendo el equipo. Jack Miller (Rafa, el vigilante de seguridad) hace su última ronda por la zona de tramoya antes de cerrar las puertas blindadas. Ve una caja de atrezzo mal cerrada, con la etiqueta «FX – Desechar», goteando un líquido espeso y oscuro sobre el hormigón. Al levantar la tapa pensando que es un molde de látex roto, descubre entre virutas de embalaje y sangre todavía tibia la cabeza decapitada de Arthur Vance, el productor y máximo inversor de la película, con los ojos abiertos y un corte limpio en el cuello. Jack activa el cierre de seguridad del plató. Nadie entra y nadie sale. El asesino sigue aquí dentro.
Sobre la mesa del despacho de Vance ha quedado abierto un maletín vacío con el membrete de un banco de Chicago y un libro de cuentas abierto. Todas las miradas se clavan automáticamente en Albert «Al» Sterling, el contable del estudio, que es el primero en tener que explicar a toda la mesa de quién era realmente el dinero de esta película."

(Nota global visible en todas las rondas: avisar a todos los jugadores de que en cada ronda Anne Harper leerá dos anotaciones literales de su cuaderno de continuidad: una es rigurosamente cierta y otra es un error suyo. Anne tampoco sabe cuál es cuál).

Ronda 2 — El Torso en la Tramoya, el Busto Equivocado y el Teléfono Rojo:

Hallazgo macabro: Empieza a gotear sangre desde lo alto de la tramoya; al bajar la polea aparece el resto del cuerpo decapitado de Arthur Vance. Junto a él cae el busto de escayola equivocado (un molde de cabeza de FX partido con restos de maquillaje real y pelo arrancado, señal de que el asesino probó el golpe o intentó fabricar un señuelo, dejando rastros compatibles tanto con fuerza bruta como con experiencia mercenaria o destreza manual).

Evento de tensión (Mitad de ronda): Suena el teléfono rojo de producción en la centralita del plató. Son los inversores de Chicago preguntando por Vance y lanzando un ultimátum: a medianoche enviarán a «los limpiadores» a recuperar su dinero y castigar a quien haya saboteado su operación.

Ronda 3 — El Arma en FX, la Cinta Magnetofónica y la Toma Falsa:

Hallazgo del arma: En el taller de atrezzo aparece la herramienta ensangrentada escondida entre botes de sangre artificial (Kensington Gore).

La cinta magnetofónica del camerino: En el despacho de Vance se recupera un magnetófono de bobina abierta que grababa en silencio durante el ataque. El zumbido eléctrico tapa el nombre del agresor, pero captura los segundos previos al golpe con detalles ambiguos que encajan por igual con todos los presentes.

La toma falsa de última hora: Una cámara secundaria se quedó rodando por error en plano fijo hacia el fondo del decorado durante 15 segundos. En el fotograma borroso se ve una silueta cruzando hacia tramoya con una prenda larga y un destello metálico en la mano que encaja con cualquiera de los presentes.

Bloque #killer-reveal activo para toda la mesa.

Fase 4 — Alegato Final (30 segundos a 1 minuto por jugador):

Se cierra el debate libre. Por turnos (cronometrados a 1 minuto máximo), cada sospechoso dispone de entre 30 segundos y 1 minuto mirando a los ojos a la mesa para defender su inocencia y acusar abiertamente a otra persona explicando sus motivos. Nadie puede interrumpir durante el turno de palabra.

Fase 5 — Votación Final:

Se desbloquean los botones de voto definitivo en los móviles para emitir el veredicto y revelar el ranking final antes de que lleguen los hombres de Chicago.

4. MECÁNICAS ESPECIALES OBLIGATORIAS

Poder de Irma Cole — «¡Silencio en el Plató!»:

En cada ronda la web muestra un panel y botones exclusivos para Irma con dos modos a elegir:

Modo Privado (1 pregunta): Llama aparte a 1 jugador (1 a 1, sin ruido) como una nota de dirección y le hace una pregunta confidencial. Solo ella escucha la respuesta.

Modo Público (2 preguntas): Grita «¡Silencio en el plató!», hace 2 preguntas en la mesa (a dos personas o a la misma) y la web lanza un aviso global indicando que el resto de jugadores tiene prohibido hablar o interrumpir mientras pregunta y le responden.

Incluye en la ficha de Irma 2 preguntas sugeridas (opcionales) por ronda para ayudarle a arrancar si quiere.

Mecánica de Anne Harper — «El Cuaderno de Continuidad Doble»:

Anne NUNCA es elegida como asesina.

En cada una de las 3 rondas (intel[1], intel[2], intel[3]), recibe 2 pistas públicas obligatorias redactadas como dos frases exactas, muy cortas y listas para leer en voz alta ante toda la mesa (Nota A y Nota B).

Regla 1 Verdad + 1 Mentira por turno: En cada ronda, exactamente 1 de las dos notas es verdadera y demoledora, y la otra es falsa (un despiste o cruce de horas en sus apuntes que confunde a la mesa).

Orden aleatorio y ciego: Alterna en cada ronda cuál va primero (ej. Ronda 1: Verdadera / Falsa; Ronda 2: Falsa / Verdadera; Ronda 3: Verdadera / Falsa) sin marcar en su ficha cuál es la buena, para que Anne las lea con total convicción y el resto tenga que cruzarlas con los paraderos declarados para descubrir cuál falla.

Añade en su ficha una excusa muy sencilla por si alguien la interroga a ella.

5. REPARTO Y HABILIDADES (LOS 6 JUGADORES ESTADOUNIDENSES)

(Sustituye el bloque "Parejas" de gato.html por "Relaciones y Rencillas en el Plató". Cada ficha incluye: Fachada, Secreto Oscuro, Relaciones y Rencillas, Paradero Declarado 22:30–23:30, Objeto que llevas encima y Habilidad Especial).

Jack Miller — Vigilante de Seguridad y Mercenario a Sueldo (Jugador: Rafa / Anfitrión):

Perfil, culpa e inocencia: Expolicía despedido del cuerpo que trabaja como vigilante nocturno del estudio; encuentra la cabeza y cierra el plató. Es un mercenario que ha hecho trabajos sucios tanto para la mafia como para Vance y sabe perfectamente cómo matar y descuartizar a alguien si hace falta. Vance lo extorsionaba con su historial y sabía de sus ataques de ira, pero además esta misma noche Vance le había contratado a él para «hacer desaparecer» a alguien del plató (sin revelarle aún el nombre) dejándole un fajo de billetes como adelanto. Al encontrar decapitado a su propio cliente, Jack cierra el plató por pura supervivencia: alguien se le ha adelantado o intenta cargarle el muerto. (Al margen de los líos bisexuales del reparto, pero como vigilante lo ha visto todo en los pasillos).

Habilidad («Registro de Bolsillos»): Elige a 1 jugador y le obliga a leer en voz alta el apartado "Objeto que llevas encima" de su ficha.

Evelyn Brooks — Actriz Principal (Jugadora: Encarni):

Perfil, culpa e inocencia: Antigua gran estrella venida a menos tras varios fracasos; cinéfila apasionada que idolatra a Billy Wilder y veía esta película como su resurgir. En los años 40 su exmarido (productor rival de Vance) murió en un sospechoso «accidente de caza» del que salió absuelta por falta de pruebas; Vance guardaba en su caja fuerte el informe forense original que demostraba que Evelyn manipuló el rifle y planeaba entregarlo mañana a la prensa mientras la sustituía por una actriz veinte años más joven. Tiene sangre fría y manejo de armas. Paradero roto: Declaró estar con Betty en su camerino desde las 22:30, pero se quedó dormida por el champán y unas gotas para los nervios hacia las 22:45 y no sabe cuánto tiempo salió Betty ni quién entró. Ha mantenido un romance secreto con Betty y un flirteo con Al, y está muerta de celos por los rumores sobre la nueva actriz.

Habilidad («Primer Plano»): Hace 1 pregunta directa a un jugador y ese jugador solo puede responder "SÍ" o "NO", sin derecho a excusas ni explicaciones.

Betty Donovan — Guionista (Jugadora: Blanca):

Perfil, culpa e inocencia: Genio caída en desgracia por el alcohol y las fiestas, arruinada y con fama de informal; extrovertida, poco mitómana, vende manualidades en mercadillos para sobrevivir y vive en un pequeño apartamento con dos gatos que se odian entre sí. El verdadero motivo de su veto en Hollywood es que fue investigada por el Comité de Actividades Antiamericanas (caza de brujas de McCarthy) y Vance la amenazaba con delatarla al FBI como simpatizante comunista —lo que supondría la cárcel y la ruina total—, además de robarle los derechos de su guion. Tiene destreza manual con alambres y herramientas, pero matar a Vance antes de cobrar los tres meses de sueldo en metálico que le debía la deja completamente sin blanca. Paradero roto: Salió del camerino de Evelyn a por hielo hacia las 22:55 y, al volver, juraría que Evelyn acababa de llegar agitada del pasillo con el abrigo de visón puesto. Ha tenido encuentros apasionados con Evelyn y una noche íntima con Irma, generando tensión y celos entre las tres.

Habilidad («Careo de Guion»): Señala a 2 jugadores (ideal para quienes intentan pasar desapercibidos) y les obliga a acusarse mutuamente durante un minuto diciendo por qué desconfían el uno del otro.

Albert «Al» Sterling — Contable y Banquero Impuesto por la Mafia de Chicago (Jugador: Alberto):

Perfil, culpa e inocencia: Extrovertido, fiestero, amante del cine español y europeo, conocido en todas las fiestas de Hollywood por codearse con estrellas como Frank Sinatra o Marlon Brando. Celoso de su intimidad y obsesionado con su aspecto físico (estilo John Travolta en Grease: revisa constantemente pelo, camisa y pañuelo). Fue impuesto por el sindicato de Chicago para lavar dinero en la película; decidía cómo se gastaba cada dólar y desviaba parte a su bolsillo. Vance lo chantajeaba con fotos en locales clandestinos de cabaret y drag queens y amenazaba con destapar su desfalco. Ha tenido escarceos nocturnos con Evelyn e Irma. Clave de la trama: Como hombre de Chicago y gestor real de la caja, es el único que sabe de dónde salió exactamente el dinero de la película y a quién pertenecía.

Habilidad («Pausa de Espejo»): Puede atusarse el pelo o el pañuelo para esquivar 1 pregunta incómoda sin responderla y rebotársela directamente a otro jugador.

Irma Cole — Directora Novel (Jugadora: Inma):

Perfil, culpa e inocencia: Directora observadora y mordaz cuando habla; tiene un gato, le apasiona Corea y la cultura asiática y defiende el cine extranjero subtitulado (NO mencionar timidez, introversión ni ningún problema de audición). En realidad está vinculada a una red de contrabando de la Costa Oeste y Hong Kong/Corea (rival directa de los socios de Chicago de Al) y utilizaba las latas de película del rodaje para sacar microfilms y mensajes codificados hacia Asia. Vance había descubierto el contrabando y planeaba entregarla a los federales esta noche. Tiene frialdad calculada y conoce la tramoya al dedillo, aunque la muerte de Vance congela el estreno de su película. Bajo la presión del rodaje tuvo encuentros clandestinos con Betty, Al y Anne.

Habilidad («¡Silencio en el Plató!»): Elige entre Modo Privado (1 pregunta 1 a 1 aparte) o Modo Público (2 preguntas con silencio absoluto en la mesa).

Anne Harper — Script / Continuidad y Archivera (Jugadora: Ana):

Perfil, culpa e inocencia: Estudió filología, ama los libros densos e intelectuales y apunta detalles obsesivos de continuidad en silencio desde una esquina. Vive en su mundo y a veces suelta comentarios incoherentes, pero registra detalles clave sin darse cuenta. Antes trabajó como archivera en un sanatorio psiquiátrico del que fue despedida tras un incendio en el ala de registros, y sufre una fijación por «corregir los errores de la realidad». Vance descubrió su historial psiquiátrico falso y ordenó cerrar el archivo para echarla mañana a la calle tras humillarla en público. Nadie vigila a la chica silenciosa de la esquina, aunque su complexión y sus propias notas de continuidad juegan en su contra. Tuvo un discreto romance de madrugada con Irma y guarda celos contenidos al ver los escarceos de Irma con Betty y Al. (NUNCA elegirla como asesina).

Habilidad («El Cuaderno de Continuidad Doble»): Lee en voz alta sus 2 pistas públicas obligatorias en cada ronda (1 verdadera y 1 falsa por turno).

6. INSTRUCCIÓN DE ENTREGA FINAL

Genera plato28.html completo partiendo de gato.html y dime únicamente la lista de contraseñas de los 6 personajes para repartirlas, sin revelarme ningún detalle sobre quién es el asesino ni en comentarios del código.