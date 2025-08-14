## Guía del Sistema Weazel News

### Visión General

Weazel News es la entidad que maneja los anuncios, anuncios y transmisiones en vivo dentro del servidor. Esta guía explica cómo utilizar los sistemas tanto para jugadores como para el personal de Weazel, sin entrar en detalles técnicos.

* **Sistema de Anuncios**: Publicación de anuncios instantáneos, flujo de ofertas/aceptaciones, tarifas y tiempo de espera.
* **Anuncios Recurrentes**: Anuncios repetitivos a intervalos definidos.
* **Zona de Eventos (Área de Transmisión en Vivo)**: Creación de áreas para transmisiones en vivo, nombrado de áreas y el inicio/fin de transmisiones.
* **Características de la Facción Weazel**: Equipamiento (chaleco antibalas), marcadores de mapa (blips de Weazel), integración con llamadas y teléfonos.

---

### Roles y Permisos

* **Ciudadanos**

  * Pueden publicar anuncios (se aplican tarifas y condiciones).
  * Pueden ver el flujo de anuncios en la interfaz telefónica y llamar a Weazel.
* **Personal de Weazel**

  * Pueden publicar anuncios gratuitos mientras están de servicio.
  * Pueden gestionar transmisiones en vivo utilizando los comandos de la Zona de Eventos, invitar o finalizar transmisiones de personas.
  * Pueden utilizar chalecos antibalas y marcadores de la facción (blips).

---

### Sistema de Anuncios

**Objetivo:** Enviar un mensaje de anuncio o aviso a todos los jugadores del servidor y compartir el número de contacto.

* **Visualización**: Los anuncios aparecerán en el chat del juego con la etiqueta “Anuncio:”; la lista de anuncios en el teléfono se actualiza en tiempo real.

* **Comandos (Uso General)**

  * `/reklam [mensaje]`

    * **Cuenta VIP**: Se puede usar desde cualquier lugar.
    * **Cuenta Normal**: El jugador debe estar en un punto de anuncio (`AdvertisementPoint`).
    * **Costo**: Depende de la tarifa de `Weazel Reklam Ücreti` en la economía del servidor (efectivo o banco).
    * **Tiempo de espera**: 60 segundos de espera (para prevenir el spam).
  * **Teléfono**: La lista de anuncios se actualiza en tiempo real en el teléfono.

* **Comandos (Weazel en Servicio)**

  * `/reklam [mensaje]` → Gratis, se publica inmediatamente y aparece en la lista telefónica.

* **Oferta/Aceptación de Anuncio (Servicio Weazel en el Campo)**

  * `/reklamteklifi [ID jugador] [precio] [mensaje]` → Envía una oferta de anuncio pagada a un jugador objetivo.
  * El jugador objetivo puede aceptar el anuncio con `/reklamkabul` y paga. El anuncio se publica.

    * **Pago**: Se deduce automáticamente del efectivo o cuenta bancaria del jugador.
    * El mensaje en vivo muestra el nombre del jugador y su número de teléfono activo.

* **Información de Contacto**

  * El número de teléfono que aparece en el anuncio es el número activo del dispositivo (proveedor) conectado del jugador.

* **Reglas/Sugerencias**

  * El texto debe ser claro, breve y relevante.
  * Está prohibido hacer spam o compartir contenido inapropiado.
  * Incluso siendo VIP, debe haber un tiempo de espera de 60 segundos entre anuncios.

---

### Anuncios Recurrentes (Automáticos)

Publica anuncios programados automáticamente a intervalos específicos.

* **Comandos**

  * `/toplureklam [cantidad] [intervalo (minutos)] [mensaje]`

    * Ejemplo: `/toplureklam 5 10 ¡La subasta comienza!` → Publica un anuncio cada 10 minutos, un total de 5 veces.
  * `/reklamlistesi` → Lista los anuncios recurrentes activos.

* **Notas**

  * Los anuncios recurrentes se almacenan en la base de datos; el número restante y el tiempo se siguen automáticamente.
  * En caso de abuso o uso no autorizado, se aplican las reglas de administración.

---

### Zona de Eventos (Área de Transmisión en Vivo)

Permite la realización de transmisiones en vivo de manera ordenada y controlada. Los jugadores autorizados que ingresen en el área de eventos serán notificados, y podrán iniciar o invitar a otros a la transmisión.

* **Reglas del Área**

  * El radio de acción debe estar entre 5–50 (por defecto 10).

* **Comandos (En Español)**

  * `/olaybolgesi ekle [radio]` → Crea una nueva Zona de Eventos en la ubicación actual.
  * `/olaybolgesi isim [nuevo_nombre]` → Cambia el nombre de la Zona de Eventos en la que te encuentras.
  * `/olaybolgesi bilgi` → Muestra información sobre la Zona de Eventos en la que te encuentras.
  * `/olaybolgesi liste` → Lista todas las Zonas de Eventos.
  * `/olaybolgesi sil onayla` → Elimina la Zona de Eventos en la que te encuentras (requiere confirmación).
  * Nota: Por compatibilidad hacia atrás, también funciona el comando antiguo `/livearea`.

* **Comandos de Transmisión**

  * `/haberler baslat` → Inicia la transmisión en la Zona de Eventos en la que te encuentras.
  * `/haberler davet [jugador]` → Inicia la transmisión del jugador objetivo en la misma Zona de Eventos.
  * `/haberler durdur` o `/haberler bitir` → Detiene tu propia transmisión.
  * `/haberler durdur [jugador]` → Detiene la transmisión del jugador objetivo en la misma Zona de Eventos.
  * `/haberler hepsinidurdur` o `/haberler hepsinibitir` → Detiene todas las transmisiones en la misma Zona de Eventos.

* **Comportamiento**

  * **Ingreso al área**: Los jugadores autorizados verán una notificación de la "Zona de Eventos" y se conectarán a la zona.
  * **Salida del área**: Se desconecta la zona; si el jugador está transmitiendo, la transmisión se detiene automáticamente.
  * **Desconexión del jugador**: La transmisión actual se detiene automáticamente, y la conexión se limpia.

---

### Características de la Facción Weazel

* **Equipamiento (Chaleco Antibalas)**

  * En los puntos de chaleco antibalas en el área de eventos, puedes acceder al menú con `/ekipman`.
  * La opción “Devolver Equipamiento” permite devolver todos los equipos pertenecientes a la facción.
  * El equipo seleccionado en el menú se añade al inventario.
  * Los objetos de facción tienen un número de serie: `WEAZEL-XXXX-XXXX`.

* **Weazel Blip (Marcadores de Mapa)**

  * `/weazelblip add [sprite] [color] [duración] [nombre]` → Añade un marcador temporal (ej. 15m, 1h).
  * `/weazelblip remove [id]` → Elimina un marcador.
  * `/weazelblip list` → Lista los marcadores de Weazel cercanos.
  * Uso: Señalar puntos de disparo, eventos, ubicaciones de noticias. El marcador desaparece automáticamente al final del tiempo.

* **Integración con Teléfono**

  * **Ciudadano**: Los ciudadanos pueden ver la lista de anuncios en su teléfono y llamar a Weazel mediante la opción "Llamar a Weazel" (existe un tiempo de espera contra el abuso de esta opción).
  * **Weazel**: El número de Weazels en servicio se reflejará en la interfaz telefónica.

* **Servicio (Duty)**

  * Los miembros de Weazel pueden entrar y salir del servicio con el comando `/isbasi`.
  * Durante el servicio, los anuncios son gratuitos y se publican en nombre de Weazel.

---

### Flujos de Ejemplo

* **Publicación de Anuncio por Ciudadano**

  1. Si es VIP: `/reklam Vendo mi Sultan, precio negociable.`
  2. Si no es VIP: Va a un punto de anuncio y usa el mismo comando.
  3. Se cobra el costo, el anuncio se publica y la lista del teléfono se actualiza.

* **Anuncio por Weazel en Servicio**

  1. Entra en servicio con `/isbasi`.
  2. Usa `/reklam Estamos en vivo a esta hora, llame para más detalles.` → Se publica gratuitamente.

* **Zona de Eventos y Transmisión**

  1. El editor crea un área con `/olaybolgesi ekle 20`.
  2. El reportero entra y ve la notificación emergente.
  3. El editor usa `/haberler davet [jugador]` para iniciar la transmisión del reportero.
  4. Al finalizar, se detienen todas las transmisiones con `/haberler hepsinidurdur`.

---

### Preguntas Frecuentes

* **¿Cuánto cuesta un anuncio?** → Se aplica la tarifa definida por `Weazel Reklam Ücreti`, la cual depende de la economía del servidor.
* **¿Por qué existe un tiempo de espera?** → Para evitar el spam y asegurar una visibilidad justa.
* **¿Por qué es necesario el área de eventos?** → Para gestionar las transmisiones en vivo de manera ordenada y facilitar las invitaciones y cierres de transmisiones.