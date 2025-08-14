# 🏢 Informe de Economía de Profesiones Principales

## 📋 Contenidos

* [Visión General](#visión-general)
* [Sistema de Dinero](#sistema-de-dinero)
* [Profesiones Principales Actuales](#profesiones-principales-actuales)
* [Parámetros Económicos](#parámetros-económicos)
* [Sistemas de Sueldo](#sistemas-de-sueldo)
* [Sistema de Turno (Duty)](#sistema-de-turno-duty)
* [Sistema de Llamadas de Servicio](#sistema-de-llamadas-de-servicio)
* [Seguimiento de Estadísticas](#seguimiento-de-estadísticas)
* [Integración Económica](#integración-económica)
* [Actualizaciones Propuestas](#actualizaciones-propuestas)

---

## 🎯 Visión General

El sistema de profesiones principales permite a los jugadores trabajar a tiempo completo y obtener ingresos regulares. A diferencia de las profesiones secundarias, este sistema ofrece mecanismos económicos más complejos y fuentes de ingresos sostenibles.

### 🏗️ Arquitectura del Sistema

* **Basado en Flags**: Cada profesión está representada por una flag
* **Sistema de Turno (Duty)**: Trabajar en estado de "duty"
* **Llamadas de Servicio**: Solicitudes de los clientes
* **Sistema de Habilidades**: Bonificaciones basadas en experiencia
* **Sistema de Contratos**: Restricciones para cambiar de profesión

---

## 💰 Sistema de Dinero

### 🪙 Sistema de Centavos

En este sistema, el dinero se almacena y procesa en **centavos**:

* **1 Dólar = 100 Centavos**
* **\$10.00 = 1000 centavos**
* **\$15.00 = 1500 centavos**

### 📊 Formateo de Dinero

```javascript
// Función Economy.formatMoney()
formatMoney(1000) // "$10.00"
formatMoney(1500) // "$15.00"
formatMoney(5000) // "$50.00"

// Función Economy.unformatMoney()
unformatMoney("$10.00") // 1000
unformatMoney("$15.00") // 1500
```

---

## 🚛 Profesiones Principales Actuales

### 1. 🚕 Taxista (Taxi Driver)

* **Flag**: `JOB_TAXI_DRIVER`
* **Sueldo por Turno**: 1500 centavos (\$15.00)
* **Sistema de Taxímetro**: Tarifas dinámicas
* **Características Especiales**:

  * Sistema de llamadas de clientes
  * Control del taxímetro
  * Tarifas basadas en la distancia
  * Límites de tarifa mínima/máxima

### 2. 🔧 Mecánico (Mechanic)

* **Flag**: `JOB_MECHANIC`
* **Sueldo por Turno**: 1000 centavos (\$10.00) + bonificación por habilidades
* **Llamadas de Servicio**: Solicitudes de clientes
* **Características Especiales**:

  * Sistema de reparación de vehículos
  * Venta de piezas
  * Servicios de modificación
  * Bonificaciones basadas en habilidades

### 3. 🚛 Conductor de Camión (Trucker)

* **Flag**: `JOB_TRUCKER`
* **Basado en Tareas**: Pago por cada viaje
* **Sistema de Contratos**: Trabajo basado en contratos
* **Características Especiales**:

  * Sistema de remolque
  * Transporte de cargas
  * Tareas basadas en rutas
  * Diferentes tipos de carga

### 4. 📦 Transportista de Carga (Cargo)

* **Flag**: `JOB_CARGO`
* **Dentro de la Ciudad**: Enfoque en entregas
* **Basado en Paquetes**: Pago por cada paquete entregado
* **Características Especiales**:

  * Entregas de paquetes
  * Tareas basadas en el tiempo
  * Sistema de direcciones

### 5. 🌾 Agricultor (Farmer)

* **Flag**: `JOB_FARMER`
* **Basado en Producción**: Enfoque en la cosecha
* **Límite Diario**: Límite en la compra de semillas
* **Características Especiales**:

  * Siembra de semillas
  * Sistema de cosecha
  * Venta de productos
  * Producción estacional

### 6. 🪓 Leñador (Lumberjack)

* **Flag**: `JOB_LUMBERJACK`
* **Producción de Madera**: Corte de árboles
* **Materia Prima**: Uso de recursos naturales
* **Características Especiales**:

  * Corte de árboles
  * Procesamiento de madera
  * Sistema de ventas

### 7. 🎣 Pescador (Fishing)

* **Flag**: `JOB_FISHER`
* **Pesca Dinámica**: Pesca de diferentes especies
* **Tipos de Pescado**: Diversidad de especies
* **Características Especiales**:

  * Sistema de pesca
  * Venta de pescado
  * Diversidad de tipos de pescado

### 8. 🔫 Vendedor de Armas (Arms Dealer)

* **Flag**: `JOB_ARMS_DEALER`
* **Venta de Armas**: Comercio legal de armas
* **Sistema de Licencias**: Control de permisos
* **Características Especiales**:

  * Venta de armas
  * Comercio de municiones
  * Control de licencias

### 9. 🚗 Chop Shop (Desguace)

* **Flag**: `JOB_CHOPSHOP`
* **Desguace de Vehículos**: Desmantelamiento de vehículos
* **Venta de Piezas**: Piezas de segunda mano
* **Características Especiales**:

  * Desmantelamiento de vehículos
  * Venta de piezas
  * Procesamiento de desechos

---

## 💰 Parámetros Económicos

### 📊 Tabla de Parámetros (En Centavos)

| Profesión               | Sueldo por Turno          | Sistema de Pago   | Bonificación por Habilidades | Duración del Contrato |
| ----------------------- | ------------------------- | ----------------- | ---------------------------- | --------------------- |
| **Taxi**                | 1500 centavos             | Taxímetro + Turno | No                           | 5 PayDays             |
| **Mecánico**            | 1000 centavos + Habilidad | Servicio + Turno  | Sí                           | 5 PayDays             |
| **Conductor de Camión** | Basado en Tareas          | Pago por Viaje    | No                           | 5 PayDays             |
| **Cargo**               | Basado en Tareas          | Pago por Entrega  | No                           | 5 PayDays             |
| **Agricultor**          | Basado en Producción      | Pago por Cosecha  | No                           | 5 PayDays             |
| **Leñador**             | Basado en Producción      | Pago por Madera   | No                           | 5 PayDays             |
| **Pescador**            | Basado en Pescado         | Pago por Pescado  | No                           | 5 PayDays             |
| **Vendedor de Armas**   | Basado en Ventas          | Comisión          | No                           | 5 PayDays             |
| **Chop Shop**           | Basado en Piezas          | Pago por Pieza    | No                           | 5 PayDays             |

### 🧮 Fórmula de Cálculo de Pago

```javascript
// Ejemplo de Taxi
const dutyPayout = 1500; // centavos
const fareMeterPayout = calculateFareMeter(); // centavos
const totalPayout = dutyPayout + fareMeterPayout;

// Ejemplo de Mecánico
const basePayout = 1000; // centavos
const skillBonus = player.character.skill.getJobBonuses('Mechanic', basePayout);
const servicePayout = calculateServiceCost(); // centavos
const totalPayout = basePayout + skillBonus + servicePayout;

// Integración Económica
const amount = Economy.request(totalPayout);
player.character.money.putInSalary(amount, `${jobName} Sueldo`);
```

---

## 💼 Sistemas de Sueldo

### 1. 🕐 Sueldo por Turno (Duty)

```javascript
// Taxista
case 'Taxi Driver': {
    salaryAmount = mp.world.constants.JOB_TAXI_DUTY_PAYOUT; // 1500 centavos
    break;
}

// Mecánico
case 'Mechanic': {
    salaryAmount = mp.world.constants.JOB_MECHANIC_DUTY_PAYOUT + 
                   player.character.skill.getJobBonuses('Mechanic', basePayout);
    break;
}
```

### 2. 🎯 Sueldo por Llamada de Servicio

* **Taxi**: Llamadas de clientes
* **Mecánico**: Solicitudes de reparación de vehículos
* **Tarifas Dinámicas**: Según la calidad del servicio

### 3. 📊 Sistema de Bonificación por Habilidades

```javascript
// Bonificación por habilidades del mecánico
const skillBonus = player.character.skill.getJobBonuses('Mechanic', basePayout);
const totalSalary = basePayout + skillBonus;
```

---

## 🕐 Sistema de Turno (Duty)

### 🔄 Control de Duty

```javascript
// Control de estado de turno
if(player.data.jobDuty) {
    player.character.data.jobDutyTime++;
    
    // Pago de sueldo después de cierto tiempo
    if(player.character.data.jobDutyTime >= DUTY_PAYOUT_TIME) {
        mp.events.call('triggerSalary', player, playerJob);
    }
}
```

### 📊 Estadísticas de Duty

* **Tiempo de Trabajo**: `jobDutyTime`
* **Ganancia**: `JOB_[JOB]_DUTY_EARNED`
* **Tiempo**: `JOB_[JOB]_DUTY_TIME`

---

## 📞 Sistema de Llamadas de Servicio

### 🎯 Gestión de Llamadas

```javascript
// Enviar llamada
jobReport.submit(flags.JOB_TAXI_DRIVER, player);

// Aceptar llamada
jobReport.resolve(player, counterId);

// Lista de llamadas
const serviceList = jobReport.getData(player.character.data.job);
```

### 📊 Parámetros de la Llamada

* **Llamante**: Información del cliente
* **Ubicación**: Punto de servicio
* **Teléfono**: Información de contacto
* **Estado**: Activo/En Espera/Completado

---

## 📈 Seguimiento de Estadísticas

### 📊 Métricas Seguimiento

#### **Estadísticas de Tiempo**

* `JOB_[JOB]_DUTY_TIME`: Total de tiempo de turno
* `JOB_[JOB]_DELAY`: Último tiempo de retraso

#### **Estadísticas de Desempeño**

* `JOB_[JOB]_DUTY_EARNED`: Ganancia total (en centavos)
* `JOB_[JOB]_DUTY_TIME`: Tiempo total de trabajo
* `JOB_[JOB]_MISSIONS_COMPLETED`: Número de misiones completadas

#### **Estadísticas Especiales**

* **Mecánico**: `JOB_MECHANIC_BUY_COMPONENT`, `JOB_MECHANIC_BUY_COMPONENT_SPENT`
* **Taxi**: `JOB_TAXI_FARE_EARNED`, `JOB_TAXI_MISSIONS_COMPLETED`
* **Conductor de Camión**: `JOB_TRUCKER_DELIVERIES`, `JOB_TRUCKER_EARNED`

### 📋 Ejemplo de Estadísticas (Mecánico)

```javascript
// Seguimiento de tiempo
player.character.stats.JOB_MECHANIC_DUTY_TIME += jobDutyTime;

// Seguimiento de desempeño (en centavos)
player.character.stats.JOB_MECHANIC_DUTY_EARNED += salaryAmount;
player.character.stats.JOB_MECHANIC_BUY_COMPONENT += componentQuantity;
player.character.stats.JOB_MECHANIC_BUY_COMPONENT_SPENT += componentCost;
```

---

## 🏦 Integración Económica

### 💸 Sistema de Dinero

```javascript
// Retiro de dinero del sistema económico (en centavos)
const amount = Economy.request(salaryAmount);

// Depósito en la cuenta de sueldo
player.character.money.putInSalary(amount, `${playerJob} Sueldo de Turno`);

// Formateo de dinero
const formattedAmount = Economy.formatMoney(amount); // "$XXX.XX"
```

### 📊 Impacto Económico

* **Generación de Dinero**: Agregar dinero al sistema económico
* **Control de Inflación**: Precios dinámicos
* **Equilibrio**: Oferta/demanda

---

## 🔄 Actualizaciones Propuestas

### 1. 🎯 Sistema de Sueldo Dinámico

```javascript
// Sistema propuesto (en centavos)
static calculateDutySalary(player, baseSalary) {
    const level = player.character.data.level;
    const skill = player.character.skill.getJobSkill(jobName);
    const economy = Economy.getInflationRate();
    const dutyTime = player.character.data.jobDutyTime;
    
    return Math.floor(baseSalary * (1 + (level * 0.01) + (skill * 0.005) + economy + (dutyTime * 0.001)));
}
```

### 2. 🌟 Sistema de Bonificación VIP

```javascript
// Integración de bonificación VIP (en centavos)
const vipBonus = Economy.calculateVIPBonus(player, salaryAmount);
const totalSalary = salaryAmount + vipBonus;
```

### 3. ⚖️ Sueldo Basado en Desempeño

```javascript
// Sueldo basado en desempeño (en centavos)
static calculatePerformanceSalary(player, baseSalary) {
    const completedMissions = player.character.stats.JOB_[JOB]_MISSIONS_COMPLETED;
    const performanceBonus = completedMissions * 50; // 50 centavos por misión
    return Math.floor(baseSalary + performanceBonus);
}
```

### 4. 📊 Mejoras en el Sistema de Habilidades

```javascript
// Sistema avanzado de habilidades (en centavos)
const skillLevel = player.character.skill.getJobSkill(jobName);
const skillBonus = skillLevel * 0.02; // 2% por nivel
const experienceBonus = player.character.stats.JOB_[JOB]_DUTY_TIME * 0.001; // 0.1% por hora
return Math.floor(baseSalary * (1 + skillBonus + experienceBonus));
```

### 5. 🎮 Gamificación

```javascript
// Sistema de logros
const achievements = {
    'SPEED_DEMON': 'Servicio rápido',
    'CUSTOMER_SATISFACTION': 'Alta satisfacción del cliente',
    'LONG_TERM_EMPLOYEE': 'Empleado de largo plazo',
    'TOP_PERFORMER': 'Mejor desempeño'
};
```

---

## 📋 Conclusión

El sistema de profesiones principales proporciona una simulación económica más compleja y sostenible que las profesiones secundarias. El sistema de turnos, las bonificaciones por habilidades y las llamadas de servicio ofrecen una experiencia de trabajo realista.

### 🎯 Objetivos Principales

1. **Sueldo Dinámico**: Sistema de pago basado en desempeño
2. **Integración de Habilidades**: Aumento del sueldo basado en experiencia
3. **Calidad del Servicio**: Bonificación basada en satisfacción del cliente
4. **Gamificación**: Sistema de logros y recompensas
5. **Equilibrio Económico**: Control de inflación y deflación

### 💡 Ventajas de las Profesiones Principales

* **Ingreso Sostenible**: Sistema de sueldos regulares
* **Desarrollo de Habilidades**: Progreso basado en experiencia
* **Llamadas de Servicio**: Solicitudes de clientes
* **Sistema de Turnos**: Experiencia de trabajo realista
* **Sistema de Contratos**: Restricciones para cambiar de profesión

---

*Este informe analiza el estado actual del sistema de profesiones principales basado en un sistema monetario en centavos y proporciona una hoja de ruta para futuras mejoras.*