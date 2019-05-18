# albraga.github.io
Sve
<! DOCTYPE HTML PUBLIC "- // W3C // DTD HTML 4.0 Transitional // EN" >
< html > < head > < title > NBoard Protocol </ title >
		
	< cabeza >
	< estilo >
	código , pre { font-size : 110 % ; color de fondo : #FFE ;}
	</ estilo >
	</ cabeza > </ cabeza >

	< body  alink = " # ff00ff "  bgcolor = " # ffffc0 "  link = " # 0000ff "  text = " # 000000 "  vlink = " # 800080 " >
		< h1 > Protocolo NBoard </ h1 >
		< p > Esto describe el protocolo utilizado por la GUI de NBoard Othello cuando
			Comunicándose con los motores. </ p >
		< p > El motor se ejecuta como un proceso separado que es
			iniciado por la GUI; La comunicación entre los dos programas es a través de la NBoard.
			Protocolo. El protocolo está diseñado para ser fácil de implementar para el motor.
		</ p >
		< h2 > Sesión de ejemplo </ h2 >
		< pre >
& lt ; nboard 2
& lt ; configurar el juego (; GM [Othello] PC [NBoard] DT [2014-02-21 20:52:27 GMT] PB [./ mEdax] PW [chris] RE [?] TI [15:00] TY [8] BO [8 --------------------------- O * ------ * O ---------- ----------------- *] B [F5] W [F6] B [D3] W [C5] B [E6] W [F7] B [E7] W [F4 ];)
& lt ; establecer profundidad 6
& lt ; ping 1
& lt ; ir

> set myname Edax6
> pong 1
> estado Edax está pensando
> nodestats 35805 0.00
> === d6 -1.00 0.0
> estado Edax está esperando
</ pre >			
		Puede ver un ejemplo de una comunicación NBoard ejecutando NBoard y 
		examinando debugLog.txt en el directorio NBoard. Los comandos al motor son
		precedido por ' & gt ; 'y las respuestas del motor están precedidas por' & lt ; '.
		< h2 > Mecanismo de comunicación </ h2 >
		El motor se comunica con la GUI a través de la entrada y salida de la consola (es decir, stdin 
		y stdout, cerr y cout). Esto suena fácil, y lo es, pero hay dos
		Cosas a tener en cuenta:
		< ol >
			< li >
				La comunicación se realiza a través de tuberías, por lo que la prueba de entrada puede no funcionar en el 
				igual que una verdadera aplicación de consola. En particular bajo Windows el
				La función _kbhit () no funcionará. Simplemente puede hacer búsquedas en profundidad y
				ignorar al usuario que intenta abortar la búsqueda, o usar un segundo hilo simple que 
				lee stdin y señala el primero cuando un comando ha entrado.
				< p > </ p >
			</ li > < li >
				La respuesta del motor a NBoard no se enviará hasta que el búfer de salida sea 
				enrojecido Hay muchas maneras de hacer esto. En C ++ las opciones viables incluyen
				< ul >
					< li >
					llame a cout.flush () después de cada línea
					</ li > < li >
					termina tus líneas con std :: endl en lugar de "\ n"
					</ li > < li >
					establecer cout a sin búfer
					</ li > < li >
						Salida a Cerr, que se vacía automáticamente cada vez que termina la línea.
					</ li >
				</ ul >
				Espero que al menos una de estas opciones esté disponible en otros idiomas.
			</ li >
		</ ol >
		< h2 > Comandos de NBoard al motor </ h2 >
		Todos los comandos de NBoard al motor están en una sola línea.
		< p >
			Esta es una lista de los comandos en la versión actual del protocolo. Más voluntad
			Es probable que se agregue a medida que el protocolo evolucione. Si lo consigues
			un comando que no entiendes debes ignorar toda la línea.
		</ p >
		< p >
			Las GUI deben enviar el comando "nboard {versión}" como su primer comando al motor. GUIs
			también debe enviar el comando "establecer profundidad" y el comando "configurar juego" antes de emitir 
			Comandos "hint" y "go". Los motores pueden asumir que las GUIs hacen esto correctamente.
		</ p >
		< table  border = " 1 " >
			< tbody > < tr >
				< th >
					nboard {version: int} </ th >
				< td >
					< p > Información de la versión enviada al principio de la sesión. </ p >
					< p > < strong > Requerido: </ strong > El motor debe ingresar al "Modo NBoard" y todo lo demás
						Los comandos estarán en formato NBoard. </ p >
					< p > < strong > Nota: </ strong > La versión actual del protocolo es la versión 2. Para referencia, instrucciones
						para el protocolo, la versión 1 se incluye en el historial de revisiones de este documento. </ p >
				</ td >
			</ tr >
			< tr >
				< th >
					establecer profundidad {maxDepth: int} </ th >
				< td >
					< p > Establecer la profundidad de búsqueda en el medio juego del motor. </ p >
					< p > < strong > Opcional: </ strong > Establece la profundidad del juego intermedio en {maxDepth}. Las profundidades de los finales están en el motor.
						discreción del autor. </ p >
				</ td >
			</ tr >
			< tr >
				< th >
					configurar juego {GGF} </ th >
				< td > Dígale al motor que todos los comandos adicionales se relacionan con la posición al final de
					El juego dado, en formato GGF.
					< p > < strong > Requerido: </ strong > El motor debe actualizar su estado de juego almacenado. </ p >
				</ td >
			</ tr >
			< tr >
				< th >
					establecer desacato {desprecio: int} </ th >
				< td > < p > Configura el factor de desacato del motor. </ p >
					< p > < strong > Opcional: </ strong > Indica al motor que los sorteos de libros deben considerarse como un valor dado,
					Desde el punto de vista del negro. 100 = dibuja a negro (+100 discos), -100 = dibuja a blanco (por 100
					 discos), 0 = los sorteos se valoran en 0. < p >
						 < p > Si no se emite el comando 'establecer desacato', el programa debe usar un valor de desacato de 0. </ p >
					< p > < strong > Desde: </ strong > Protocolo versión 2. </ p >
				</ td >
			</ tr >
			< tr >
				< th >
					move {move: string} / {eval: float or blank} / {time: float} </ th >
				< td >
					< p > Indique al motor que todos los comandos adicionales se relacionan con la posición después de la dada
						movimiento. El movimiento es de 2 caracteres, por ejemplo, "F5". Eval se encuentra normalmente en centi-discos. Tiempo es
						en segundos. Eval y el tiempo puede ser omitido. Si se omite eval, se asume que es "desconocido";
						si se omite el tiempo, se asume que es 0. </ p >
					< p > < strong > Requerido: </ strong > Actualiza el estado del juego haciendo el movimiento. No se requiere respuesta. </ P >
					< p > < strong > Desde: </ strong > Versión de protocolo 2. En la versión de protocolo 1, la GUI acaba de enviar "F5" en lugar de "mover F5". </ p >
				</ td >
			</ tr >
			< tr >
				< th >
					sugerencia {n: int} </ th >
				< td > Dígale al motor que dé evaluaciones para la posición dada. n dice cuántos
					movimientos para evaluar, por ejemplo, 2 significa dar evaluaciones para las 2 primeras posiciones. Esto es usado
					Cuando el usuario está analizando un juego. Con el comando "sugerencia", el motor no está CONSTRUIDO por el tiempo restante en el juego.
					< p > < b > Requerido: </ b > El motor envía una evaluación para su movimiento superior </ p >
					< p > < b > Mejor: </ b > El motor envía una evaluación para aproximadamente la parte superior n
						se mueve Si el motor busca mediante profundización iterativa, también debe enviar evaluaciones durante la búsqueda, lo que
						hace que la GUI se sienta más receptiva al usuario. </ p >
						< p > Dependiendo de si la evalación proviene de un libro o una búsqueda,
						el motor envía de vuelta
						</ P > < código > Búsqueda {pv: < un  href = " #PV " > PV </ a >} {eval: < un  href = " #Eval " > Eval </ a > 0} {profundidad: < una  href = " #Depth " > Profundidad </ a >} {texto de forma libre} </ código >
						< Br /> o < br />
						< Código > {pv libro: < un  href = " #PV " > PV </ a >} {eval: < un  href = " #Eval " > Eval </ a >} {juegos número: larga} {profundidad: < a  href = " #Depth " > Profundidad </ a >} {texto de forma libre: cadena} </ código >
					< P > < un  nombre = " PV " > < b > PV </ b >: El pv debe comenzar con dos caracteres que representan el movimiento considerado (por ejemplo,
						"F5" o "PA") y no debe contener espacios en blanco. "F5d6C3" y "F5-D6-C3" son
						PV válidos pero "F5 D6 C3" considerará que D6 es la evaluación.
					</ p >
					< P > < un  nombre = " Eval " > < b > Eval </ b >: El eval es desde el punto de vista del jugador para mover y es una
						doble. A opción del motor, también puede ser un par ordenado de dobles separados por una coma:
						{valor de dibujo a negro}, {valor de dibujo a blanco}. </ p >
						< P > < un  nombre = " Profundidad " > < b > La profundidad </ b >: La profundidad es la profundidad de búsqueda. Debe comenzar con un entero
							pero puede terminar con otros personajes;
							por ejemplo, "100% W" es una profundidad válida. La profundidad no puede contener espacios.
						</ p >
							Dos códigos de profundidad tienen un significado especial para NBoard: "100% W" le dice a NBoard que el motor tiene
							resuelto para ganar / perder / empate y el signo de la evaluación coincide con el signo de la evaluación devuelta.
							"100%" le dice a NBoard que el motor ha hecho una resolución exacta.
						</ p >
					< p > El texto de forma libre puede ser cualquier otra información que el motor quiera transmitir.
						NBoard 1.1 y 2.0 no muestran esta información, pero es posible que las versiones posteriores u otras GUI. </ P >
				</ td >
			</ tr >
			< tr >
				< th >
					ir </ th >
				< td > Dígale al motor que decida qué movimiento jugará. Esto se usa cuando el motor está jugando en un juego.
					Con el comando "ir", la computadora está limitada por la profundidad máxima de búsqueda y la 
												Tiempo restante en el juego.
					< p > < b > Requerido: </ b > El motor responde con "< código > === {mover} </ código >" donde mover
						es por ejemplo "F5"
					</ p >
					< p > < b > Mejor: </ b > El motor responde con "< código > === {mover: Cadena} / {eval: float} / {time: float} </ code >".
						Eval puede omitirse si el movimiento es forzado. El motor también devuelve el pensamiento.
						salida como en el comando "sugerencia". </ p >
					< p > < b > Importante: </ b > El motor < em > no </ em > actualiza la placa con este movimiento,
						en cambio, espera un comando de "mover" de NBoard. Esto es porque el usuario puede
						Han modificado el tablero mientras el motor pensaba. </ p >
					< p > < b > Nota: </ b > Para que sea más fácil para el autor del motor, The NBoard gui establece el estado del motor en ""
						cuando recibe la respuesta. El motor puede anular este comportamiento.
						enviando un comando de "estado" inmediatamente después de la respuesta. </ p >
					< p > < b > Desde: </ b > Versión de protocolo 1, pero el motor que está limitado por el tiempo restante es desde la versión de Protocolo 2. </ p >	
				</ td >
			</ tr >
			< tr >
				< th >
					ping {ping: int} </ th >
				< td > Asegure la sincronización cuando la posición de la placa esté a punto de cambiar.
					< p > < b > Requerido: </ b > Deja de pensar y responde con "pong n". Si el motor esta
						analizando una posición que debe dejar de analizar antes de enviar "pong n" de lo contrario 
						NBoard pensará que el análisis se relaciona con la posición actual. </ P >
				</ td >
			</ tr >
			< tr >
				< th >
					aprender </ th >
				< td > Aprende el juego actual.
					< p > < b > Requerido: </ b > Responda "aprendido". </ p >
					< p > < b > Mejor: </ b > Agrega el juego actual al libro. </ p >
					< p > < b > Nota: </ b > Para que sea más fácil para el autor del motor, The NBoard gui establece el estado del motor en ""
						cuando recibe la respuesta "aprendida". El motor puede anular este comportamiento.
						enviando un comando de "estado" inmediatamente después de la respuesta. </ p >
				</ td >
			</ tr >
			< tr >
				< th > analizar </ th >
				< td > Realizar un análisis retrógrado del juego actual.
					< p > < b > Opcional: </ b > Realizar un análisis retrógrado del juego actual. Para cada posición del tablero que ocurra en el juego, la
						el motor devuelve una línea del análisis de forma < código > {movesMade: int} {eval: double} </ code >. movesMade = 0 corresponde
						a la posición inicial. Los pases cuentan para los movimientos realizados, por lo que los movimientos pueden ser superiores a 60. </ p >
					< p > < b > Desde: </ b > Protocolo versión 2. </ b > </ p >
				</ td >
			</ tr >
				
		</ tbody > </ table >
		< h2 > Comandos del motor a NBoard </ h2 >
		< table  border = " 1 " >
			< tbody > < tr >
				< th >
					status {text} </ th > < td > Establece la línea de estado que se muestra en la GUI de NBoard. </ td >
			</ tr >
			< tr >
				< th >
					set myname {text} </ th > < td > Establece el nombre del motor como se muestra en la GUI. </ td >
			</ tr >
			< tr >
				< th >
					nodestats {cantidad de nodos: largo} {tiempo: flotar} </ th >
					< td > Establece la información de conteo de nodos del motor como se muestra en la GUI.
					< p > < b > conteo de nodos </ b >: número de nodos desde el comienzo de la búsqueda actual </ p >
					< p > < b > time </ b >: número de segundos desde el comienzo de la búsqueda actual </ p >
					< p > < strong > Desde: </ strong > Protocolo versión 2. </ p >
					</ td >
			</ tr >
		</ tbody > </ table >
		< h2 > Código de ejemplo </ h2 >
		Este es el código utilizado por NTest a partir de NBoard 1.1. Incluye Windows específico
		multihilo Probablemente requerirá modificación para trabajar en otros.
		programas
		< pre > // Copyright 2004 Chris Welty
// Todos los derechos reservados

#include "GameX.h"
#include & lt ; deque & gt ;
#include & lt ; sstream & gt ;
#include "windows.h"

/////////////////////////////////////
// CGame2
/////////////////////////////////////

//! Los comandos almacenados de NBoard.
static std :: deque & lt ; std :: string & gt ; líneas;
//! Este evento se establece cuando hay una línea de entrada disponible

//! Una sección crítica maneja el acceso a un recurso. Sólo un hilo puede poseerlo a la vez.
clase CriticalSection {
público:
	Sección crítica(); 
	~ CriticalSection ();

	void Enter ();
	dejar vacío ();
privado:
	CRITICAL_SECTION m_cs;
} cs;

//! Construye el objeto de la sección crítica.
CriticalSection :: CriticalSection () {
 	:: InitializeCriticalSection ( & amp ; m_cs);
 }

//! Destruye la sección crítica.
CriticalSection :: ~ CriticalSection () {
	:: DeleteCriticalSection ( & amp ; m_cs);
}

//! Bloquea hasta que la sección crítica esté disponible; Entonces toma el control de ello.
void CriticalSection :: Enter () {
	:: EnterCriticalSection ( & amp ; m_cs);
}

//! Control de liberación de la sección crítica.
void CriticalSection :: Leave () {
	:: LeaveCriticalSection ( & amp ; m_cs);
}

//! Un evento de Windows
//!
//! Este es un evento de Windows sin nombre, por lo que otros procesos
//! (por ejemplo, múltiples copias de ntest) no puede afectar el evento.
Evento de clase {
público:
	Evento();
	~ Evento ();

	void Set ();
	void Reset ();
	void Wait (tiempo de espera u4);
privado:
	HANDLE m_event;
} eventInput;

Evento :: Evento () {
	m_event = CreateEvent (NULL, true, false, NULL);
}

Evento :: ~ Evento () {
	CloseHandle (m_event);
}

//! Establecer un evento en true.
Evento nulo :: Set () {
	SetEvent (m_event);
}

//! Establecer un evento en falso
void Event :: Reset () {
	ResetEvent (m_event);
}

//! Espere un evento con el tiempo de espera especificado, o siempre si el tiempo de espera es == INFINITE
Evento nulo :: Espere (tiempo de espera de u4) {
	WaitForSingleObject (m_event, timeout);
}

//! Esta función devuelve verdadero si hay entrada esperando el motor.
//! Está destinado a ser utilizado en la función de búsqueda.
//!
//! Actualmente se usa solo cuando se usa un visor externo con GameX.
//! \ todo prueba para ver si esto ralentiza la búsqueda. Si es así necesita un mecanismo más rápido.
bool HasInput () {
	cs.Enter ();
	bool fHasInput =! lines.empty ();
	cs.Leave ();
	return fHasInput;
}

//! Agregue una línea de entrada al deque y establezca eventInput si el deque estaba vacío antes
estático void AddStringToDeque (const std :: string & amp ; s) {
	cs.Enter ();
	if (lines.empty ()) {
		eventInput.Set ();
	}
	lines.push_back (s);
	cs.Leave ();
}

//! Trabajo del hilo: añadir cosas al deque.
DWORD WINAPI MoveCinToDeque estático (void *) {
	std :: string sLine;
	while (getline (std :: cin, sLine))
		AddStringToDeque (sLine);

	// por último, publica un mensaje para dejar de fumar. Normalmente obtenemos una del espectador.
	// pero a veces no hay oportunidad antes de la terminación.
	AddStringToDeque ("quit");
	devuelve 0;
}

//! Obtenga una línea de entrada del hilo que está analizando las líneas para nosotros.
GetLineFromThread estático bool (std :: string & amp ; sLine) {
	eventInput.Wait (INFINITE);
	cs.Enter ();
	sLine = lines.front ();
	lines.pop_front ();
	if (lines.empty ())
		eventInput.Reset ();
	cs.Leave ();
	devuelve verdadero
}

//! Crea y ejecuta un juego utilizando la clase de juego alternativa para los espectadores externos
//!
//! Comandos de usuario:
//! - modo & lt ; n & gt ; : 0 = computadora inactiva, 1 = computadora juega blanco, 2 = computadora juega negro, 3 = computadora juega ambos
CGameX :: CGameX (CComputerDefaults cd) {
	CPlayerComputer * pcomp = NULL;

	int nboardVersion = 0;
	cd.fsPrint = -1 & amp ; ~ CSearchInfo :: kPrintMove & amp ; ~ CSearchInfo :: kPrintGameAnalysis;
	cd.fsPrintOpponent = -1;
	u4 fLearn = CPlayer :: kNoAddSoloUnsolvedToBook;

	// Inicializar con un tablero básico. De esa manera estamos garantizados para tener siempre un juego legal.
	Inicializar ("8");

	// Iniciar el hilo que nos dará mensajes.
	u4 threadId;
	CreateThread (NULL, 0, MoveCinToDeque, NULL, 0, & amp ; threadId);

	std :: string sLine;
// while (getline (std :: cin, sLine)) {
	while (GetLineFromThread (sLine)) {
		// guarda el valor de GameOver para que sepamos si aprender el juego
		const bool fGameWasOver = GameOver ();

		std :: istringstream is (sLine);
		std :: string sCommand;
		es & gt ; & gt ; sCommand;

		if (sCommand == "go") {
			// motor le dice al espectador qué movimiento haría.
			// NO actualice la placa, el motor no tiene idea de si el espectador cree que la computadora debería moverse
			// (p. ej., en nboard, el usuario podría cambiar al modo "el usuario juega con ambos colores" mientras el motor está pensando).
			// cualquier actualización de la placa viene dada por un mensaje de movimiento estándar.
			if (pcomp) {
				COsMoveListItem mli;
				pcomp- & gt ; GetMoveAndTime (* this, CPlayer :: kMyMove | fLearn, mli);
				std :: cout & lt ; & lt ; "===" & lt ; & lt ; mli & lt ; & lt ; std :: endl;
			}
			else {
				std :: cout & lt ; & lt ; "advertencia Debe seleccionar una profundidad con \" establecer profundidad & lt ; n & gt ; \ "primero" & lt ; & lt ; std :: endl;
			}
		}
		else if (sCommand == "hint") {
			int nBest = 1;
			es & gt ; & gt ; nBest
			// Si no es el movimiento de la computadora, él puede dar pistas.
			// COsMoveListItem mli;
			// pcomp- & gt ; GetMoveAndTime (* this, CPlayer :: kAnalyze | fLearn, mli);
			std :: cout & lt ; & lt ; "Estado analizando" & lt ; & lt ; std :: endl;
			pcomp- & gt ; Sugerencia (CQPosition (pos.board), nBest);
			std :: cout & lt ; & lt ; "estado" & lt ; & lt ; std :: endl;
		}
		si no (sCommand == "aprender") {
			pcomp- & gt ; EndGame (* esto);
			std :: cout & lt ; & lt ; "aprender" & lt ; & lt ; std :: endl;
		}
		else if (sCommand == "nboard") {
			es & gt ; & gt ; nboardVersion;
		}
		else if (sCommand == "new") {
			// este comando no es parte del estándar de interfaz, pero es útil para la prueba.
			std :: string sBoardType ("8");
			es & gt ; & gt ; sBoardType;
			Inicializar (sBoardType.c_str ());
		}
		else if (sCommand == "ping") {
			int n;
			es & gt ; & gt ; norte;
			std :: cout & lt ; & lt ; "pong" & lt ; & lt ; n & lt ; & lt ; std :: endl;
		}
		else if (sCommand == "quit") {
			descanso;
		}
		else if (sCommand == "remove_tree") {
			si (pcomp & amp ;&erio ; pcomp- & gt ; libro) {
				pcomp- & gt ; libro- & gt ; RemoveTree (CQPosition (pos.board) .BitBoard ());
			}
		}
		else if (sCommand == "draw_tree") {
			si (pcomp & amp ;&erio ; pcomp- & gt ; libro) {
				std :: cout & lt ; & lt ; "--- Dibujar árbol --- \ nDespués de";
				para (size_t i = 0; i & lt ; ml.size (); i ++)
					std :: cout & lt ; & lt ; ml [i] .mv & lt ; & lt ; "";
				std :: cout & lt ; & lt ; "\norte";

				pcomp- & gt ; libro- & gt ; PrintDrawTree (CQPosition (pos.board));
			}
		}
		else if (sCommand == "set") {
			std :: string param;
			es & gt ; & gt ; param
			if (param == "game") {
				// el tablero está cambiando, necesita negamax el juego anterior para asegurarse de que los valores se mantienen consistentes
				si (pcomp & amp ;&erio ; pcomp- & gt ; libro)
					pcomp- & gt ; libro- & gt ; NegamaxGame (* esto);
				En (es);
			}
			si no (param == "profundidad") {
				std :: istringstream iscp (cd.sCalcParams.c_str ());
				char c = 's';
				profundidad int = 12;
				iscp & gt ; & gt ; c & gt ; & gt ; profundidad;

				es & gt ; & gt ; profundidad;

				std :: ostringstream os;
				os & lt ; & lt ; c & lt ; & lt ; profundidad;
				cd.sCalcParams = os.str ();

				si (pcomp)
					eliminar pcomp;
				pcomp = new CPlayerComputer (cd);
				std :: cout & lt ; & lt ; "\norte";
				std :: cout & lt ; & lt ; "set myname Ntest" & lt ; & lt ; profundidad & lt ; & lt ; std :: endl;
			}
			si no (param == "desprecio") {
				desprecio flotante = 0;
				es & gt ; & gt ; desprecio;

				// actualizar los valores predeterminados de la computadora (usados ​​para computadoras nuevas) y la computadora actual.
				cd.vContempts [1] = CComputerDefaults :: FloatToContempt (desprecio);
				cd.vContempts [0] = - cd.vContempts [1];
				if (pcomp) {
					pcomp- & gt ; cd.vContempts [0] = cd.vContempts [0];
					pcomp- & gt ; cd.vContempts [1] = cd.vContempts [1];
				}
			}
			else {
				getline (es, param);
			}
		}
		else if (sCommand == "move") {
			COsMoveListItem mli;
			es & gt ; & gt ; mli;
			Actualización (mli);
		}
		si no (sCommand.size () == 2) {
			COsMoveListItem mli;
			mli.mv = COsMove (sCommand);
			Actualización (mli);
		}
	}
}

		</ pre >
	</ body > </ html >
