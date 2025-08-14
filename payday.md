### Sistema PayDay — Guía en Español — MAZE MP ES

Esta guía resume, de manera clara y no técnica, los componentes que conforman el monto que los jugadores reciben en su cuenta durante el PayDay, y cómo varían en diferentes situaciones. Los ejemplos se dan en dólares, con dos decimales (1 unidad = 100 centavos = 1.00\$).

### ¿Cómo Funciona?

* **Soporte gratuito (Nuevo Jugador)**: Durante los primeros 50 PayDays, se agrega un soporte de 3,000.00\$ al jugador. Normalmente no se aplica impuesto en este período, pero en jugadores casados se podría aplicar un descuento de al menos el 1% en impuestos.
* **Cuenta de salario**: El salario acumulado del jugador se transfiere a su banco durante el PayDay y se reinicia.
* **Ganancias por horas extras**: Se calculan en función del tiempo trabajado, a razón de 5,000 unidades por hora.
* **Interés bancario**: Se agrega un interés basado en el saldo bancario antes del PayDay. A medida que los activos totales aumentan, la tasa de interés disminuye progresivamente (aproximadamente del 0.5% al 0.1%).
* **Impuesto sobre la renta**: Se aplica un impuesto entre el 1% y el 10% sobre el ingreso bruto. A medida que aumentan los activos totales, la tasa de impuestos sube. Los jugadores casados tienen un descuento del 10% en esta tasa, pero en la práctica nunca baja del 1%.
* **Inversión neta**: Se deduce el impuesto del ingreso bruto y el monto neto se deposita en el banco.
* **Información de nivel**: Se asigna un nombre de nivel informativo según la tasa de impuestos aplicada (Bajo, Medio, etc.). Esto es solo para fines de informes/etiquetado.

### Constantes del Sistema y Efectos

* **Soporte gratuito**: Se puede configurar en el sistema predeterminado. En esta guía, se ha usado 3,000.00\$ (primeros 50 PayDays).
* **INTERÉS\_BANCARIO\_MIN / MAX**: Rango de tasas de interés bancario (del 0.1% al 0.5%). A medida que los activos aumentan, la tasa se acerca al límite superior.
* **TASA\_DE\_IMPUESTO\_MIN / MAX**: Rango de tasas de impuestos sobre la renta (del 1% al 10%). A medida que aumentan los activos, la tasa se acerca al límite inferior.
* **DESCUENTO\_IMPUESTO\_CASADO**: Descuento de impuesto para jugadores casados (10%). Sin embargo, la tasa nunca será inferior al 1%.
* **Tarifa horaria (Horas extras)**: 5,000 unidades/hora. El monto en dólares se calcula según esta tarifa.

### Cálculo Matemático (Resumen)

* **Activos Totales**: V = efectivo + banco + valor de la casa + valor del vehículo
* **Tasa de interés**: r = max(min\_interés, max\_interés − disminución\_tasa × piso(V / umbral\_disminución))
* **Tasa de impuesto**: t = min(max\_impuesto, min\_impuesto + aumento\_tasa × piso(V / umbral\_aumento))
* **Descuento por matrimonio**: t := max(min\_impuesto, t − t × descuento\_matrimonio)
* **Ingresos por horas extras**: A\_horas\_extra = piso(tiempo\_trabajo × tarifa\_horaria / 3600)
* **Interés bancario**: B = piso(saldo\_bancario × r)
* **Ingreso bruto**: G = (salario + soporte\_gratuito + A\_horas\_extra) + B
* **Impuesto**: Impuesto = G × t
* **Neto**: Neto = G − Impuesto

### Escalas de Impuestos (Informativas)

| Nombre del Nivel | Límite de la tasa de impuesto |
| ---------------- | ----------------------------- |
| Bajo             | 0%                            |
| Bajo-Medio       | 2%                            |
| Medio            | 3.5%                          |
| Medio-Alto       | 5%                            |
| Bajo-Elite       | 6.5%                          |
| Medio-Elite      | 8%                            |
| Más Alto         | 10%                           |

### Umbrales de Entrada de los Niveles (Basado en los Activos Totales)

Los rangos siguientes se calculan con base en un jugador "soltero" y sin soporte gratuito. La fórmula es: t = %1 + %0.1 × piso(Activos Totales / 1,000,000\$), donde t tiene un límite superior del 10%.

| Nivel       | Tasa de Impuesto Aplicada | Rango de Activos Totales (soltero) |
| ----------- | ------------------------: | ---------------------------------- |
| Bajo        |                   < 2.00% | 0\$ – 9,999,999.99\$               |
| Bajo-Medio  |         ≥ 2.00% y < 3.50% | 10,000,000.00\$ – 24,999,999.99\$  |
| Medio       |         ≥ 3.50% y < 5.00% | 25,000,000.00\$ – 39,999,999.99\$  |
| Medio-Alto  |         ≥ 5.00% y < 6.50% | 40,000,000.00\$ – 54,999,999.99\$  |
| Bajo-Elite  |         ≥ 6.50% y < 8.00% | 55,000,000.00\$ – 69,999,999.99\$  |
| Medio-Elite |        ≥ 8.00% y < 10.00% | 70,000,000.00\$ – 89,999,999.99\$  |
| Más Alto    |                  ≥ 10.00% | 90,000,000.00\$ y más              |

**Notas**:

* El descuento por matrimonio (10%) puede reducir la tasa de impuestos, lo que podría hacer que el jugador pase a un nivel inferior, pero la tasa nunca será inferior al 1%.
* Durante el período de soporte gratuito, el impuesto normalmente es 0%; en jugadores casados, se aplica un mínimo del 1%, lo que mantiene el nivel de "Bajo".
* Los rangos están basados en las constantes del sistema (INTERÉS\_BANCARIO\_MIN/MAX, INC\_RATE, INC\_VALUE); si estos valores cambian, la tabla debe actualizarse.

### Clases de Impuestos (taxClasses) y Límites

Los valores de límite se almacenan en centavos en el código; los siguientes valores están en dólares.

| Nivel       |     Límite (\$) | Impuesto sobre Vivienda | Impuesto sobre Vehículos | Interés Bancario | Impuesto sobre Ingresos |
| ----------- | --------------: | ----------------------: | -----------------------: | ---------------: | ----------------------: |
| Bajo        |    200,000.00\$ |                   0.04% |                    0.08% |            1.00% |                      0% |
| Bajo-Medio  |    500,000.00\$ |                   0.08% |                    0.12% |            0.85% |                   2.00% |
| Medio       |  1,000,000.00\$ |                   0.12% |                    0.15% |            0.70% |                   3.50% |
| Medio-Alto  |  2,500,000.00\$ |                   0.16% |                    0.20% |            0.55% |                   5.00% |
| Bajo-Elite  |  5,000,000.00\$ |                   0.20% |                    0.25% |            0.40% |                   6.50% |
| Medio-Elite | 10,000,000.00\$ |                   0.25% |                    0.30% |            0.25% |                   8.00% |
| Más Alto    |   No hay límite |                   0.30% |                    0.40% |            0.10% |                  10.00% |

**Notas**:

* El "Límite" se refiere al límite superior de activos para cada nivel; aquellos que superen el límite pasarán al siguiente nivel. No hay límite en el último nivel.
* La tabla refleja la configuración de `taxClasses`; estos valores deben interpretarse junto con otros cálculos económicos en el sistema.

### Escenarios (en dólares)

**Nota**: Los ejemplos a continuación están en dólares y se muestran con dos decimales.

#### C-1: Nuevo Jugador (Soltero, primer PayDay)

* No tiene saldo en efectivo ni en el banco, sin activos.
* Soporte gratuito: 3,000.00\$, sin impuestos.
* Neto: 3,000.00\$
* Nivel: Bajo

#### C-2: Trabajador (Soltero, activos medios, 2 horas extras)

* Ejemplo: Banco con 200,000 unidades, efectivo con 50,000 unidades, salario de 3,000 unidades, 2 horas extras.
* Interés bancario: 1,000.00\$
* Ganancia por horas extras: 10,000.00\$
* Transferencia de salario: 3,000.00\$
* Bruto: 14,000.00\$
* Impuesto (1%): 140.00\$
* Neto: 13,860.00\$
* Nivel: Bajo

#### C-3: Persona Adinerada (Casado, activos altos, 1 hora extra)

* Ejemplo: Banco con 5,000,000 unidades, efectivo con 500,000 unidades, activos altos (casa/vehículo), 1 hora extra.
* Interés bancario: 21,500.00\$ (la tasa disminuye con los activos)
* Ganancia por horas extras: 5,000.00\$
* Bruto: 26,500.00\$
* Impuesto (aproximadamente 2.43%, después del descuento por matrimonio): 643.95\$
* Neto: 25,856.05\$
* Nivel: Bajo-Medio

#### C-4: Caso límite — Casado + Soporte Gratuito

* No tiene saldo en efectivo ni en el banco, casado, dentro de los primeros 50 PayDays.
* Soporte gratuito: 3,000.00\$
* Impuesto (se aplica al menos un 1%): 30.00\$
* Neto: 2,970.00\$
* Nivel: Bajo

### Tabla Resumen

| Personaje         | Bruto (\$) | Tasa de Impuesto | Impuesto (\$) | Neto (\$) | Nivel      |
| ----------------- | ---------: | ---------------: | ------------: | --------: | ---------- |
| C-1 Nuevo         |   3,000.00 |               0% |          0.00 |  3,000.00 | Bajo       |
| C-2 Trabajador    |  14,000.00 |             1.0% |        140.00 | 13,860.00 | Bajo       |
| C-3 Adinerado     |  26,500.00 |          \~2.43% |        643.95 | 25,856.05 | Bajo-Medio |
| C-4 Casado+Gratis |   3,000.00 |             1.0% |         30.00 |  2,970.00 | Bajo       |

### Notas de Campo

* El interés bancario solo se calcula según el saldo bancario antes del PayDay. Los montos añadidos en PayDay generarán interés en el siguiente período.
* El salario acumulado se transfiere al banco en PayDay y se reinicia.
* No existe una situación en la que el pago neto sea negativo con las tasas actuales; la tasa de impuesto tiene un límite superior del 10%.