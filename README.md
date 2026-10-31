# CalidadIA

Sistema de aprendizaje de **Gestión de la Calidad y la Seguridad Agroalimentaria (3490)**, Máster Universitario en Ingeniería Agronómica, Universidad Miguel Hernández de Elche. Aplicación web de un solo fichero, construida a partir de la Guía Docente 2026-2027.

**Usar la app:** https://fborrasumh.github.io/calidadia/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23843518.svg)](https://doi.org/10.5281/zenodo.23843518)

**Idiomas:** español (por defecto), inglés y portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Qué hace

- **Práctica adaptativa por resultado de aprendizaje (RA).** 48 preguntas (3 por cada uno de los 16 RA de la guía), con práctica de recuperación y repaso espaciado (intervalos de 1, 2, 4, 8 y 16 días). Un modelo de dominio por RA, con olvido en el tiempo, elige la siguiente pregunta y muestra siempre el motivo. Mismas respuestas → misma ruta.
- **Simulacro con la regla literal de la guía:** test al 60 % del examen («cuatro preguntas incorrectas restarán una correcta»), dos casos prácticos al 20 % cada uno y mínimo de 4 para que el examen cuente. Calculadora de la nota final (50/20/20/10) y cálculo de la esperanza de responder al azar.
- **Casos con solución calculada por el código**, con datos nuevos en cada intento (semilla reproducible) y diagnóstico de errores típicos: probabilidad de aceptación de un plan de muestreo por atributos; dictamen con un criterio microbiológico de tres clases (n, c, m, M); trazabilidad hacia delante con balance de masas; límites de un gráfico X̄-R y puntos fuera de control; capacidad de proceso (Cp, Cpk).
- **Laboratorio APPCC** sobre dos diagramas de flujo ficticios (zumo pasteurizado, lechuga de IV gama): el estudiante identifica peligros y responde al árbol de decisión; el código aplica el árbol, comprueba que cada PCC tiene límite crítico con valor, vigilancia con frecuencia y acción correctora, y que hay verificación y registros (los 7 principios), y compara con una referencia orientativa. Exporta el plan a Word.
- **IA opcional** (clave propia de OpenAI, Google Gemini o Anthropic Claude): comenta el plan APPCC o explica una pregunta de otra forma. **Nunca pone nota**: las frases con notas o puntuaciones se retiran por código. Cada cita que la IA hace del plan se verifica por código contra el texto del estudiante y las cifras que no están en el plan se señalan.
- **Panel del profesorado:** analítica de preguntas a partir de exportaciones anónimas del alumnado (dificultad, discriminación 27 %/27 %, distractores que nadie elige, dominio medio por RA) con propuestas de revisión que decide el profesorado; exportación del banco a Moodle XML (penalización −25 %), GIFT y CSV; análisis de la Guía Docente.
- **Ejemplo resuelto sin clave** (plan APPCC del zumo con un comentario de la IA precalculado que pasa por las mismas comprobaciones).

## Cómo se usa la IA

Con la propia clave de cada persona, guardada solo en su navegador. Se elige el modelo de entre los disponibles en la clave. No hace falta servidor.

## Privacidad

Todo (respuestas, progreso, planes) se guarda solo en el navegador (IndexedDB). A la IA solo sale lo que la persona pide que comente, con correos, teléfonos y documentos de identidad enmascarados y tras ver una muestra de lo que sale. La exportación anónima lleva un seudónimo aleatorio, las opciones elegidas y el dominio por RA, sin nombre, sin textos libres y sin la hora de cada respuesta; incluye su diccionario de datos.

## Límites

- Las preguntas, los casos y los diagramas de flujo los ha redactado la app para practicar: **no son el examen real** ni sustituyen a los materiales de la asignatura. Los valores de los criterios microbiológicos de los casos son ficticios.
- La correspondencia entre RA y unidades didácticas no la declara la guía: es una propuesta editable.
- El dominio por RA es una estimación orientativa, no una nota. La referencia APPCC es orientativa: un mismo peligro puede gestionarse como PCC o con prerrequisitos.
- La IA puede equivocarse; la normativa debe consultarse siempre en su versión vigente (EUR-Lex).
- **Investigación:** la app genera datos, no evidencia publicable. Usar exportaciones del alumnado para publicar requiere aprobación ética (en la UMH, la Oficina de Investigación Responsable), consentimiento informado, RGPD y, idealmente, un diseño preregistrado con grupo de comparación.
- Probado con IA simulada de los tres proveedores; no se ha probado con claves reales.

## Pruebas realizadas (v1.0.0)

46 pruebas de la lógica pura en Node (reglas de la guía, binomial, tres clases, árbol de decisión, 300 variantes por tipo de caso, determinismo de la ruta adaptativa, analítica, Moodle XML/GIFT) y 77 en navegador (Playwright): flujos completos en es/en/pt, IA simulada que inventa citas y pone nota, exportaciones (Word abierto con python-docx, también sin CDN), **axe-core sin infracciones WCAG 2.2 A/AA** en las 7 pantallas y los 3 idiomas, navegación con teclado, funcionamiento **sin red** tras la carga, móvil de 390 px sin desborde y **CPU ×4**: primera pantalla útil en menos de 3 s. Contraste del texto secundario ≥ 7:1 sobre blanco; sin límites de tiempo.

## Análisis de la Guía Docente (resumen)

La guía declara 16 RA, 14 unidades, 3 metodologías y 4 instrumentos de evaluación, pero no los relaciona entre sí; el RA de sostenibilidad y economía circular no tiene unidad propia; 12 de 16 RA empiezan por «Conocer» (verbo no observable); con 4 opciones por pregunta, la penalización de 1/4 no anula el azar (esperanza +0,0625; la corrección neutra sería 1/3); la bibliografía más reciente es de 2012 (hoy rigen BRCGS Food Safety Issue 9, IFS Food 8, ISO 22000:2018, y el Reglamento (UE) 2024/1143 sustituyó al 1151/2012); no constan horas, cronograma ni convocatoria extraordinaria. La app ataca primero el 50 % de la nota que depende del examen.

## Adaptarla a otra asignatura o universidad

Todo el contenido está en `src/curriculum.js` del proyecto (ficha, RA, unidades, banco de preguntas, procesos APPCC, reglas de evaluación). Cambiando ese fichero y los diccionarios (`tools/tr.py`) se obtiene otra app con la misma lógica.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) y María José Frutos Fernández (Universidad Miguel Hernández de Elche).

Construida a partir de la Guía Docente 2026-2027 de la asignatura 3490, de la que María José Frutos Fernández es profesora responsable.

Roles (CRediT): Fernando Borrás Rocher — conceptualización, software, metodología, validación; María José Frutos Fernández — recursos (Guía Docente y asignatura), conceptualización docente, validación del contenido.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · María José Frutos Fernández [0000-0003-0620-5050](https://orcid.org/0000-0003-0620-5050)

## Fundamentos

- Roediger, H. L., y Karpicke, J. D. (2006). Test-enhanced learning. *Psychological Science*, 17(3), 249-255. https://doi.org/10.1111/j.1467-9280.2006.01693.x
- Cepeda, N. J., Pashler, H., Vul, E., Wixted, J. T., y Rohrer, D. (2006). Distributed practice in verbal recall tasks. *Psychological Bulletin*, 132(3), 354-380. https://doi.org/10.1037/0033-2909.132.3.354
- Dunlosky, J., Rawson, K. A., Marsh, E. J., Nathan, M. J., y Willingham, D. T. (2013). Improving students' learning with effective learning techniques. *Psychological Science in the Public Interest*, 14(1), 4-58. https://doi.org/10.1177/1529100612453266
- Codex Alimentarius. CXC 1-1969, Principios Generales de Higiene de los Alimentos.

## Cómo citar

Borrás Rocher, F. y Frutos Fernández, M. J. (2026). *CalidadIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23843518](https://doi.org/10.5281/zenodo.23843518)

## Licencia

MIT. Véase [LICENSE](LICENSE). Ambos autores han dado su conformidad con publicar bajo MIT.
