# recepcionista-ia — roadmap

Demo personal de una recepcionista telefónica con IA para una empresa ficticia: contesta, averigua quién llama y qué necesita, y lo pasa al agente del área correcta con el contexto, sin volver a preguntar. Sirve para mandarla a reclutadores y clientes y como pieza de portafolio. Nota en el vault: `01 Proyectos/recepcionista-ia.md`.

## Reglas
- **Se escribe desde cero.** Se inspira en la arquitectura de `agente-voz` (trabajo en CICSA), pero no se copia código, prompts, datos, cuentas ni credenciales de ese repo ni de la empresa. Nada que mencione a CICSA.
- Cuentas propias: Vapi y Twilio (número propio) a nombre de Carlos. Las de la demo de CICSA son de la empresa.
- Sin transferencias a personas reales; las llamadas de prueba se quedan en almacenamiento propio.
- Repo en la cuenta `CPerrufo24` (comprobar `git config user.email` = perrufo.cyv@gmail.com antes del primer commit).

## Arquitectura (por decidir en detalle)
- Voz: Vapi pone audio, STT y TTS; el número de Twilio propio se importa a Vapi.
- Backend FastAPI como "director": recibe los eventos de Vapi y responde con `assistant-overrides` (los guiones viven en el código y se cambian sin tocar Vapi).
- Router: un agente recepcionista saca nombre, empresa y motivo platicando, y pasa a especialistas (ventas, soporte, quejas, recados) con esos datos inyectados.
- Después: panel por departamento (Next.js), WhatsApp, patrones de resiliencia (circuit breaker, store & forward). A futuro, opción de mover la voz a la pila de TrivVOIP (Asterisk ARI) para bajar costos.
- Despliegue: el Servidor propio (Lenovo, Cloudflare Tunnel) cuando esté listo; mientras, local con un túnel.

## Fases
1. Cuentas propias de Vapi y Twilio y número propio. **(Carlos, pendiente)**
2. Empresa ficticia: nombre, giro, áreas y guiones nuevos. Propuesta: servicios industriales.
3. Backend mínimo + router entre áreas: un número que contesta y clasifica.
4. Registro de llamadas y panel por departamento.
5. Despliegue en el Servidor y enlace para compartir.

## Pendientes al retomar
- Nada de código todavía; la carpeta solo tiene este archivo (sin `git init` ni repo en GitHub).
- Decidir nombre y giro de la empresa ficticia.
- Abrir cuentas de Vapi y Twilio.
