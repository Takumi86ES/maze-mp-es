### Mejoras en el Inventario: Sistema de Imagen de Artículos y Valor/Mercado (Desgaste)

Este documento explica dos nuevos sistemas y sus efectos en el entorno de roleplay:

* Asignación, compartición y visualización de imágenes en artículos
* Asignación de valor a los artículos y desgaste (wear float) con valor de mercado dinámico

---

### 1) Sistema de Imagen de Artículos

* **Objetivo**: Permitir que los jugadores asignen una imagen a ciertos artículos mediante una URL, compartirla con jugadores cercanos e inspeccionarla a través de CEF.
* **Tipos soportados**: Outfit, Packaging, Drink, Food, Generic

#### Flujo de Uso

* **Asignar Imagen**: Haz clic derecho en el inventario → Asignar Imagen → Ingresa la URL → Asignada al artículo.
* **Inspeccionar Imagen**: Si el artículo tiene imagen, se abre en la ventana de CEF. Se cierra con ESC / Backspace.
* **Compartir Imagen**: Si el artículo tiene imagen, se muestra al jugador objetivo (ID del jugador ingresada, dentro de 5 metros).

#### UI

* Opciones del menú contextual:

  * Asignar Imagen
  * Compartir Imagen (si tiene imagen)
  * Inspeccionar Imagen (si tiene imagen)

#### Detalles Técnicos

* **Almacenamiento de Datos**: `SpawnedItem.extra.imageUrl`
* **Validación**:

  * HTTP/HTTPS obligatorio
  * Extensiones permitidas: .png, .jpg, .jpeg, .gif, .webp
  * Longitud máxima: 300 caracteres
* **Control de cercanía**: Para compartir, 5m y en la misma dimensión
* **Visualización**: Se abre con `CEFBrowser:openImage` en CEF HUD

#### Efectos en el Roleplay

* Productos como empaques/comida/bebidas con marca, contenido y presentación estética
* Roles de transmisión de imágenes como prueba, carteles, folletos, catálogos de productos
* Aumento de la interacción social entre jugadores a través del intercambio de imágenes

---

### 2) Sistema de Valor y Mercado (Desgaste)

* **Objetivo**: Registrar el monto pagado por los productos como "valor"; generar un rango dinámico de "valor de mercado" mediante desgaste (float).

#### Flujo de Pedido y Asignación de Valor

* En pedidos realizados en negocios (individuales/múltiples):

  * El total pagado por el cliente se agrega a la caja del negocio.
  * El 50% del costo de producción se deduce automáticamente de la caja del negocio.
  * Al agregar el producto al inventario del jugador, se escribe la siguiente metadata:

    * `extra.valueCents`: Precio unitario (centavos)
    * `extra.marketFloat`: Desgaste (float) inicial entre 0.05–0.45
* **Nota**: De esta forma, cada artículo gana un "valor personal"; el historial de precios tiene importancia en RP.

#### Capas de Desgaste (Wear Float)

* El desgaste del artículo se muestra en 5 niveles:

  * **Nuevo**: 0.00–0.07
  * **Ligeramente Desgastado**: 0.07–0.15
  * **Moderadamente Desgastado**: 0.15–0.38
  * **Fuertemente Desgastado**: 0.38–0.45
  * **Desgastado**: 0.45–1.00

#### Cálculo del Valor de Mercado

* **Visualización**: "Valor" + "Desgaste (float)" + "Valor de Mercado" (rango min–max)
* **Factores (multiplicador del valor)**:

  * **Nuevo**: 0.95–1.20
  * **Ligeramente Desgastado**: 0.85–1.05
  * **Moderadamente Desgastado**: 0.70–0.90
  * **Fuertemente Desgastado**: 0.55–0.75
  * **Desgastado**: 0.35–0.60

#### Integración de UI

* Inventario → Clic derecho → Información:

  * Valor: ej. \$300.00
  * Desgaste: ej. Moderadamente Desgastado (0.22)
  * Valor de Mercado: ej. \$210.00 – \$270.00
* `SpawnedItem.basicData()` agrega estos campos al `extra`; el menú contextual de React los muestra automáticamente.

#### Efectos en el Roleplay y Economía

* **Envejecimiento de productos**: Puede ampliarse con uso/proceso; se pueden agregar sistemas de mantenimiento/reparación a futuro.
* **Variedad de Precios**: Incluso artículos del mismo tipo pueden tener diferentes rangos de mercado debido a su valor/desgaste.
* **Dinámicas de Negocios**:

  * **Ingreso**: El pago entra directamente a la caja al momento de la compra
  * **Gasto**: El costo de producción (50%) se deduce automáticamente
  * **Margen de Ganancia**: Enriquecerá el RP de selección de productos y marketing
* **Colección/Premium**: Los artículos con bajo desgaste (Nuevo) pueden convertirse en "coleccionables".

---

### Ideas para Expansión

* **Actualización del Desgaste**: Actualización dinámica del float con uso, daño, efectos ambientales, mantenimiento/reparación
* **Mercado**: Los valores pueden destacarse en el UI para ventas jugador a jugador
* **Certificados**: Verificación del `valueCents` y la fuente con factura/certificado
* **Analítica**: Métricas como valor promedio de venta y distribución del desgaste en el panel de negocios

---

### Resumen Breve

* **Sistema de Imagen**: Se asignan imágenes a los tipos adecuados; se pueden revisar/marcar; mejora la visualización en RP.
* **Sistema de Valor y Mercado**: El precio de compra se convierte en valor; el desgaste (float) genera un rango de mercado; diversificación económica y en RP.