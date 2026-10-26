# recepcionista-ia — roadmap

Recepcionista telefónica con IA de **RobinnovaLab** (la empresa de Carlos: automatización e IA para empresas, robótica y programación para jóvenes, formación en IA para profesionales). Contesta, averigua quién llama y qué necesita, y lo pasa al agente del área correcta con el contexto, sin volver a preguntar. Es a la vez la recepcionista real que le falta a RobinnovaLab y su mejor demo: un cliente que pide "agentes de IA para atención" la puede probar llamando. (Cambio del 2026-10-26: antes era una empresa ficticia.) Nota en el vault: `01 Proyectos/recepcionista-ia.md`.

## Reglas
- **Se escribe desde cero.** Se inspira en la arquitectura de `agente-voz` (trabajo en CICSA), pero no se copia código, prompts, datos, cuentas ni credenciales de ese repo ni de la empresa. Nada que mencione a CICSA.
- Cuentas propias: Vapi y Twilio (número propio) a nombre de Carlos. Las de la demo de CICSA son de la empresa.
- La única persona real a la que se pasa algo es Carlos (aviso o transferencia, por decidir). Nada de datos de clientes en el repo: las llamadas y leads van a almacenamiento propio ignorado por git.
- Repo en la cuenta `CPerrufo24` (comprobar `git config user.email` = perrufo.cyv@gmail.com antes del primer commit).

## Arquitectura (por decidir en detalle)
- Voz: Vapi pone audio, STT y TTS; el número de Twilio propio se importa a Vapi.
- Backend FastAPI como "director": recibe los eventos de Vapi y responde con `assistant-overrides` (los guiones viven en el código y se cambian sin tocar Vapi).
- Router: un agente recepcionista saca nombre, empresa y motivo platicando, y pasa a especialistas (ventas, soporte, quejas, recados) con esos datos inyectados.
- Después: panel por departamento (Next.js), WhatsApp, patrones de resiliencia (circuit breaker, store & forward). A futuro, opción de mover la voz a la pila de TrivVOIP (Asterisk ARI) para bajar costos.
- Despliegue: el Servidor propio (Lenovo, Cloudflare Tunnel) cuando esté listo; mientras, local con un túnel.

## Áreas de RobinnovaLab (propuesta)
Salen del formulario de contacto de la landing, para que llamada, chatbot y formulario hablen el mismo idioma:
- **Recepción:** saluda como RobinnovaLab, saca nombre, empresa o escuela, contacto y motivo, y enruta.
- **Empresas (transformación operativa):** entiende el problema (Excel, WhatsApp, personas clave), lo califica y agenda un diagnóstico con Carlos. Tono B2B, sin dar precios.
- **Programas STEAM para jóvenes (9 a 18 años):** habla con padres o escuelas: edad, nivel (básico, intermedio, avanzado), presencial o en línea, robótica con Arduino y LEGO, programación. Deja el interés registrado.
- **Formación en IA para profesionales:** docentes y profesionales sin conocimientos técnicos; talleres presenciales o en línea.
- **Recados y otros:** toma el recado y avisa a Carlos.
Respuesta prometida igual que en la web: menos de 24 horas en días hábiles.

## Fases
1. Cuentas propias de Vapi y Twilio; número gratuito de la cuenta de prueba de Twilio, importado a Vapi y con el cel de Carlos verificado. **(Carlos, pendiente)**
2. Guiones de RobinnovaLab a partir de la landing (`Robinnovalab-page`): recepcionista + áreas (ver abajo).
3. Backend mínimo + router entre áreas: un número que contesta y clasifica.
4. Registro de llamadas y panel por departamento.
5. Despliegue en el Servidor y enlace para compartir.

## Pendientes al retomar
- Nada de código todavía. Repo `CPerrufo24/recepcionista-ia` creado y `main` subido (remoto por el alias `github-personal`). Sin `.env` ni servicios corriendo.
- Decidido 2026-10-26: la recepcionista es la de RobinnovaLab (ya no hay empresa ficticia).
- Decisiones del 2026-10-26:
  - Se llama **Robi**, como el chatbot de la web.
  - **Número:** el gratuito de la cuenta de prueba de Twilio (de EE. UU.). Mientras la cuenta siga en prueba, solo pueden llamar números verificados en Twilio y antes de conectar suena un aviso de "trial account". Sirve para desarrollar; para clientes reales hay que subir la cuenta a pago (y, si se quiere, un número mexicano con su bundle regulatorio).
  - **Al terminar la llamada:** solo aviso a Carlos con un resumen (nombre, área, qué necesita); nunca transfiere.
  - **Leads:** en el backend propio (SQLite y luego Postgres en el Servidor), que alimenta el panel.
- Abrir cuentas de Vapi y Twilio.
