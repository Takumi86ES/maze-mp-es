# Informe Económico de Profesiones Secundarias

## 📋 Contenido

* [Visión General](#visión-general)
* [Sistema Monetario](#sistema-monetario)
* [Profesiones Secundarias Actuales](#profesiones-secundarias-actuales)
* [Parámetros Económicos](#parámetros-económicos)
* [Sistemas de Bonificación](#sistemas-de-bonificación)
* [Mecanismos de Retraso](#mecanismos-de-retraso)
* [Seguimiento de Estadísticas](#seguimiento-de-estadísticas)
* [Integración Económica](#integración-económica)
* [Actualizaciones Recomendadas](#actualizaciones-recomendadas)

---

## 🎯 Visión General

El sistema de profesiones secundarias permite que los jugadores ganen ingresos adicionales a través de trabajos temporales junto con sus profesiones principales. Este sistema proporciona una simulación económica realista, permitiendo que los jugadores tengan diversas fuentes de ingresos.

### 🏗️ Arquitectura del Sistema

* **Estructura Modular**: Cada profesión secundaria es un módulo independiente.
* **Parámetros Dinámicos**: Ajustables mediante variables globales.
* **Seguimiento de Estadísticas**: Métricas detalladas de rendimiento.
* **Sistema de Retrasos**: Protección contra el spam y mantenimiento del equilibrio.

---

## 💰 Sistema Monetario

### 🪙 Sistema de Centavos

En este sistema, el dinero se guarda y se procesa en **centavos**:

* **1 Dólar = 100 Centavos**
* **\$9.50 = 950 centavos**
* **\$25.00 = 2500 centavos**

### 📊 Formato de Dinero

```javascript
// Función Economy.formatMoney()
formatMoney(950) // "$9.50"
formatMoney(2500) // "$25.00"
formatMoney(47500) // "$475.00"

// Función Economy.unformatMoney()
unformatMoney("$9.50") // 950
unformatMoney("$25.00") // 2500
```

---

## 🚛 Profesiones Secundarias Actuales

### 1. 🚌 Conductor de Autobús (Bus Driver)

* **ID del Propietario del Vehículo**: 1
* **Sistema Basado en Rutas**: Distancia dinámica y pago
* **Características Especiales**:

  * Múltiples opciones de rutas
  * Pago basado en distancia
  * Sistema de finalización de rutas

### 2. 🗑️ Recolector de Basura (Trash Collector)

* **ID del Propietario del Vehículo**: 2
* **Número de Tareas**: 30 cubos de basura
* **Pago**: 950 centavos/tarea (\$9.50) + bono de 2500 centavos (\$25.00)
* **Ganancia Total**: 31,000 centavos (\$310.00)

### 3. 🧹 Barredor de Calles (Street Sweeper)

* **ID del Propietario del Vehículo**: 3
* **Basado en Rutas**: Sistema de pago dinámico
* **Bono**: 0 centavos (sin bono)
* **Características Especiales**: Pago basado en distancia

### 4. 🏊 Cazador de Tesoros (Treasure Collector)

* **ID del Propietario del Vehículo**: 4
* **Número de Tareas**: 20 puntos
* **Pago**: 1625 centavos/tarea (\$16.25) + bono de 2500 centavos (\$25.00)
* **Ganancia Total**: 35,000 centavos (\$350.00)
* **Riesgo/Recompensa**: Alto riesgo, alta recompensa

### 5. 🌱 Cortacésped (Lawn Mower)

* **ID del Propietario del Vehículo**: 5
* **Pago Máximo**: 22,500 centavos (\$225.00)
* **Bono**: 2500 centavos (\$25.00)
* **Características Especiales**: Sistema basado en áreas

### 6. 🚚 Repartidor (Delivery Driver)

* **ID del Propietario del Vehículo**: 6
* **Número de Tareas**: 15 entregas
* **Pago**: 3750 centavos/tarea (\$37.50) + bono de 2500 centavos (\$25.00)
* **Ganancia Total**: 58,750 centavos (\$587.50)

### 7. 💰 Transportista de Dinero (Money Transporter)

* **ID del Propietario del Vehículo**: 7
* **Número de Tareas**: 10 cajeros automáticos
* **Pago**: 4750 centavos/tarea (\$47.50) + bono de 2500 centavos (\$25.00)
* **Ganancia Total**: 50,000 centavos (\$500.00)
* **Nivel de Riesgo**: Alto

### 8. ⚡ Electricista (Electrician)

* **ID del Propietario del Vehículo**: 8
* **Número de Tareas**: 12 puntos de falla
* **Pago**: 11250 centavos/tarea (\$112.50) + bono de 5000 centavos (\$50.00)
* **Ganancia Total**: 140,000 centavos (\$1,400.00)

---

## 💰 Parámetros Económicos

### 📊 Tabla de Parámetros (En Centavos)

| Profesión                   | Pago por Tarea  | Máximo Tareas | Bono de Finalización | Ganancia Total   | Retraso por Tarea | Retraso Estándar |
| --------------------------- | --------------- | ------------- | -------------------- | ---------------- | ----------------- | ---------------- |
| **Autobús**                 | Basado en Rutas | Variable      | 2500 centavos        | Basado en Rutas  | Basado en Rutas   | 5 minutos        |
| **Basurero**                | 950 centavos    | 30            | 2500 centavos        | 31,000 centavos  | 30 minutos        | 5 minutos        |
| **Barredor**                | Basado en Rutas | 1 ruta        | 0 centavos           | Basado en Rutas  | 720 minutos       | 3 minutos        |
| **Cazador de Tesoros**      | 1625 centavos   | 20            | 2500 centavos        | 35,000 centavos  | 60 minutos        | 5 minutos        |
| **Cortacésped**             | Dinámico        | 30+           | 2500 centavos        | 22,500 centavos  | 900 minutos       | 5 minutos        |
| **Repartidor**              | 3750 centavos   | 15            | 2500 centavos        | 58,750 centavos  | 15 minutos        | 5 minutos        |
| **Transportista de Dinero** | 4750 centavos   | 10            | 2500 centavos        | 50,000 centavos  | 360 minutos       | 5 minutos        |
| **Electricista**            | 11250 centavos  | 12            | 5000 centavos        | 140,000 centavos | 30 minutos        | 5 minutos        |

### 🧮 Fórmula de Cálculo de Pago

```javascript
// Cálculo básico de pago (en centavos)
const basePayout = PAY_PER_OBJECTIVE * completedObjectives;
const finishBonus = finished ? FINISH_BONUS : 0;
const totalPayout = basePayout + finishBonus;

// Integración económica
const amount = Economy.request(totalPayout);
player.character.money.putInSalary(amount, `Profesión Secundaria: ${jobName}`);

// Formateo del dinero
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
```

---

## 🎁 Sistemas de Bonificación

### 1. 🏆 Bono de Finalización

* **Cantidad**: 2500 centavos (\$25.00) - para la mayoría de las profesiones
* **Electricista**: 5000 centavos (\$50.00) - bono especial
* **Barredor**: 0 centavos - sin bono
* **Condición**: Completar todas las tareas
* **Objetivo**: Incentivar a los jugadores a completar las tareas

### 2. 🚀 Bono por Múltiples Tareas

* **Sistema**: Algunas profesiones tienen bonificación por completar múltiples tareas
* **Bono**: Pago extra o puntos de experiencia
* **Ejemplo**: Completar rutas de autobús

### 3. ⚡ Bono por Velocidad

* **Sistema**: Completar en un tiempo determinado
* **Bono**: Pago adicional basado en el tiempo
* **Riesgo**: Apresurarse para completar rápidamente

---

## ⏰ Mecanismos de Retraso

### 🔒 Cálculo de Retraso

```javascript
const delay = STANDARD_DELAY + (DELAY_PER_OBJECTIVE * completedObjectives);
player.character.stats[sidejob.delayKey] = player.character.data.playTime + delay;
```

### 📊 Tabla de Retrasos

| Profesión                   | Retraso Estándar | Retraso por Tarea | Retraso Máximo  |
| --------------------------- | ---------------- | ----------------- | --------------- |
| **Autobús**                 | 5 minutos        | Basado en Rutas   | Basado en Rutas |
| **Basurero**                | 5 minutos        | 30 minutos        | 15 horas        |
| **Barredor**                | 3 minutos        | 720 minutos       | 12 horas        |
| **Cazador de Tesoros**      | 5 minutos        | 60 minutos        | 20 horas        |
| **Cortacésped**             | 5 minutos        | 900 minutos       | 15 horas        |
| **Repartidor**              | 5 minutos        | 15 minutos        | 4.25 horas      |
| **Transportista de Dinero** | 5 minutos        | 360 minutos       | 60 horas        |
| **Electricista**            | 5 minutos        | 30 minutos        | 6 horas         |

### 🛡️ Protección contra Spam

* **Objetivo**: Evitar que los jugadores realicen continuamente tareas secundarias
* **Mecanismo**: No se puede realizar otra tarea hasta que termine el tiempo de retraso
* **Control**: `player.character.stats[sidejob.delayKey] > player.character.data.playTime`

---

## 📈 Seguimiento de Estadísticas

### 📊 Métricas Seguidas

#### **Estadísticas de Tiempo**

* `SIDEJOB_[JOB]_TIME`: Tiempo total de trabajo
* `SIDEJOB_[JOB]_DELAY`: Último tiempo de retraso

#### **Estadísticas de Rendimiento**

* `SIDEJOB_[JOB]_LOADED/DELIVERED`: Número de tareas completadas
* `SIDEJOB_[JOB]_EARNED`: Ganancia total (en centavos)
* `SIDEJOB_[JOB]_TODAY`: Número de tareas realizadas hoy
* `SIDEJOB_[JOB]_DONE`: Número de tareas completadas

### 📋 Ejemplo de Estadísticas (Basurero)

```javascript
// Seguimiento de tiempo
player.character.stats.SIDEJOB_TRASH_TIME += Math.ceil((now.getTime() - this.startTime.getTime()) / 1000);

// Seguimiento de rendimiento (en centavos)
player.character.stats.SIDEJOB_TRASH_LOADED += this.objective;
player.character.stats.SIDEJOB_TRASH_EARNED += payout; // 950 * objective + 2500
player.character.stats.SIDEJOB_TRASH_TODAY++;
if(finished) player.character.stats.S
```


IDEJOB\_TRASH\_DONE++;

````

---

## 🏦 Integración Económica

### 💸 Sistema Monetario
```javascript
// Retiro de dinero desde el sistema económico (en centavos)
const amount = Economy.request(payout);

// Ingreso al salario
player.character.money.putInSalary(amount, `Profesión Secundaria: ${jobName} - ${description}`);

// Formateo del dinero
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
````

### 📊 Efectos en la Economía

* **Generación de Dinero**: Agregar dinero al sistema económico
* **Control de Inflación**: Precios dinámicos
* **Equilibrio**: Balance entre oferta/demanda

---

## 🔄 Actualizaciones Recomendadas

### 1. 🎯 Precios Dinámicos

```javascript
// Sistema propuesto (en centavos)
static calculatePayPerObjective(player, basePay) {
    const level = player.character.data.level;
    const skill = player.character.skill.getJobSkill(jobName);
    const economy = Economy.getInflationRate();
    
    return Math.floor(basePay * (1 + (level * 0.01) + (skill * 0.005) + economy));
}
```

### 2. 🌟 Sistema de Bonificación VIP

```javascript
// Integración de bonificación VIP (en centavos)
const vipBonus = Economy.calculateVIPBonus(player, payout);
const totalPayout = payout + vipBonus;
```

### 3. ⚖️ Sistema de Riesgo/Recompensa

```javascript
// Sistema de riesgo para el transportista de dinero (en centavos)
static calculateRiskReward(player, basePay) {
    const successRate = player.character.stats.SIDEJOB_MONEY_TRANSPORTER_SUCCESS_RATE;
    const riskMultiplier = 1 + (successRate * 0.1);
    return Math.floor(basePay * riskMultiplier);
}
```

### 4. 📊 Sistema de Habilidades

```javascript
// Pago basado en la experiencia (en centavos)
const skillLevel = player.character.skill.getJobSkill(jobName);
const skillBonus = skillLevel * 0.02; // 2% por nivel
return Math.floor(basePay * (1 + skillBonus));
```

### 5. 🎮 Gamificación

```javascript
// Sistema de logros
const achievements = {
    'SPEED_DEMON': 'Finalización rápida',
    'PERFECTIONIST': 'Finalización sin errores',
    'MARATHON_RUNNER': 'Trabajo largo'
};
```

---

## 📋 Conclusión

El sistema actual de profesiones secundarias funciona con el sistema monetario basado en centavos. Este sistema es ideal para cálculos de dinero precisos y controla la inflación.

### 🎯 Objetivos Principales

1. **Precios Dinámicos**: Precios que cambian según las condiciones del mercado.
2. **Integración de Habilidades**: Aumento del pago basado en la experiencia.
3. **Riesgo/Recompensa**: Mayor pago para profesiones más riesgosas.
4. **Gamificación**: Sistema de logros y recompensas.
5. **Equilibrio Económico**: Control de inflación y deflación.

### 💡 Ventajas del Sistema de Centavos

* **Precisión**: Cálculos precisos en centavos.
* **Rendimiento**: Operaciones con números enteros.
* **Consistencia**: La misma moneda en todo el sistema.
* **Control de Inflación**: Ajustes precisos de precios.

---

*Este informe analiza el sistema actual de profesiones secundarias usando un sistema monetario basado en centavos y presenta una hoja de ruta para futuras actualizaciones.*
