# FELINUXS

**Un núcleo de contención para agentes de IA sobre Linux.**

Cuando un agente ejecuta algo, ese algo corre *encerrado*, no puede comprometer el host,
y queda *registrado*. Esa es la promesa. Nada más — y nada menos.

---

## La idea en una frase

Vivimos la época en que los agentes de IA **ejecutan código**: por MCP, por CLI, por
automatizaciones, por lo que venga. La mayoría de sistemas intentan **controlar** lo que
el agente puede hacer. FELINUXS parte de una premisa distinta:

> El control puede fallar. Por eso, además de controlar, hay que **contener las
> consecuencias** cuando falla.

No es prevención perfecta. Es **contención a prueba de fallos**.

---

## Cómo evolucionó este proyecto

FELINUXS no nació siendo lo que es hoy. Ha pasado por tres etapas, y contarlas con
honestidad es parte del proyecto.

### Etapa 1 — Servidor MCP (origen)

Empezó como un servidor MCP: una forma de poner herramientas y recursos al alcance de
agentes. La etapa `0.1` de este repositorio pertenece a ese momento y explora una
dirección distinta —la gobernanza interna de modelos— que **ya no es el foco actual**.
Se conserva como registro histórico del recorrido.

### Etapa 2 — Motor de control

La segunda visión fue más ambiciosa: no solo exponer herramientas, sino **verificar,
autorizar y limitar** lo que un agente puede ejecutar. El foco pasó de «conectar» a
«gobernar la ejecución».

### Etapa 3 — Arquitectura de contención (actual)

La etapa actual asume algo incómodo pero real: **los mecanismos de prevención pueden
fallar**. Por eso incorpora una **frontera de aislamiento proporcionada por el propio
sistema operativo**, de modo que —aunque un proceso consiga eludir el control— **queda
confinado**.

Y aquí está la separación que define el proyecto:

> **El motor de contención se desacopla de MCP.** MCP deja de *definir* lo que FELINUXS
> es, y pasa a ser **una puerta de entrada** más. El mismo núcleo puede contener
> distintas clases de procesos ejecutados por agentes.

El problema que FELINUXS aborda **no pertenece a MCP**. Un agente ejecuta código por
muchos caminos; la contención debe funcionar para todos ellos.

---

## Los cuatro verbos

El núcleo se organiza alrededor de cuatro pasos que ocurren en **cada ejecución**:

| Verbo | Pregunta que responde |
|---|---|
| **VERIFICAR** | ¿Es lo que esperaba? |
| **AUTORIZAR** | ¿Tiene permiso para esto? |
| **CONTENER** | ¿Dónde corre, y qué puede tocar? |
| **EVIDENCIAR** | ¿Qué ocurrió, y se puede demostrar? |

Estos cuatro verbos son **independientes del protocolo**: no dependen de MCP.
Son una función central del motor, no una capacidad suelta de una interfaz.

---

## Qué garantiza (y qué no)

**Lo que se busca garantizar:**

- Un proceso contenido **no modifica** el sistema anfitrión.
- **Sin acceso a la red por defecto.**
- Sujetos a **límites de memoria y tiempo**.
- Un proceso comprometido queda **confinado dentro de la frontera**.
- Cada ejecución deja **evidencia verificable**.

**Lo que NO se promete:**

- No es **prevención perfecta**. Es contención *fail-safe*.
- No cubre vulnerabilidades del **kernel** ni canales laterales.
- Las pruebas actuales son **evidencia inicial demostrada**, **no** un certificado de
  seguridad de producción. Falta endurecimiento y auditoría.

---

## Qué es aportación y qué no

Ser claro en esto es parte del diseño.

**No es aportación de este proyecto:**

- El aislamiento mediante namespaces de Linux.
- Las jaulas o sandboxes del sistema operativo.
- La verificación por hash, las listas de control o los registros de auditoría.

Todas esas piezas **ya existían** y las hacen, mejor y más maduras, proyectos como
`bubblewrap`, Docker, Firejail, gVisor o Firecracker. Este proyecto **no las reinventa**.

**Lo que este proyecto explora:**

- Una **arquitectura integrada** para agentes de IA que reúne verificación,
  autorización, contención a nivel de sistema operativo y evidencia auditable
  **en un mismo acto de ejecución**.
- Con el **motor desacoplado del protocolo**, de modo que MCP sea *una puerta*, no *el todo*.
- Con la hipótesis de trabajo explícita: **asumir que la prevención falla** y diseñar
  en consecuencia.

La aportación, si la hay, está en la **integración** — no en cada tecnología por separado.

---

## Estado

| Frente | Estado |
|---|---|
| Concepto y arquitectura | Definidos y documentados |
| Núcleo en funcionamiento | En desarrollo, ejecutable y probado |
| Evidencia de contención | Pruebas iniciales superadas |
| Garantía de producción | **Todavía no** — requiere endurecimiento y auditoría |

---

## Sobre el código

Este repositorio conserva la **etapa `0.1`** como registro del recorrido del proyecto.

La implementación del **núcleo de contención actual** no está publicada aquí. Lo que se
comparte públicamente es **qué hace** el sistema y **qué garantiza** — no la combinación
interna con la que se consigue.

---

## Autor

**Félix José Martínez González**

- GitHub: [@felinuxs](https://github.com/felinuxs)
- Web del proyecto: [felinuxs.github.io](https://felinuxs.github.io)
- Email: [felinuxs@gmail.com](mailto:felinuxs@gmail.com)

---

*FELINUXS — de conectar agentes con herramientas, a contener las consecuencias cuando
el control falla.*
