# PROYECTO: **VaR-Aire Monterrey**
### Sistema de Pronóstico de Riesgo Ambiental mediante Métodos Cuantitativos Financieros  

---

## 1. PROBLEMA & OPORTUNIDAD

### Contexto
Monterrey es la ZMM con mayor incertidumbre en calidad del aire por:

- **Inversiones térmicas (octubre-febrero):** incrementos de 300% en PM2.5 en <6 horas  
- **Contingencias industriales:** apagones de precatdoras, quemas agrícolas  

Actualmente, el **SIMA** utiliza modelos determinísticos con **RMSE ≈ 15-20 μg/m³**, pero sin intervalos de confianza útiles para decisiones de salud pública (ej. cierre de escuelas).

### Gap
Los modelos de Deep Learning (LSTM, CNN) predicen bien la **media**, pero fallan en **cuantificar riesgo de cola** y son *“cajas negras”* para técnicos ambientales.

### Oportunidad
Aplicar **Value-at-Risk (VaR)** y **simulaciones Monte Carlo** de la industria financiera para crear **pronósticos probabilísticos calibrados** que SIMA pueda operar.

---

## 2. INSIGHTS CLAVE DE LOS DATOS SIMA 2020-2025

### 2.1 Perfil de Estaciones (15 activas)

**Estación Benchmark:**  
- **CE (Obispado, Centro, Monterrey, 562 msnm)** – ubicación representativa y datos más completos.

**Estaciones Estratégicas por Zona:**
- **SE2 (Juárez, 387 msnm):** Sureste industrial, alta volatilidad PM2.5  
- **SO2 (San Pedro, 636 msnm):** Suroeste residencial, menor volatilidad pero sensible a transporte  
- **NO2 (García, 702 msnm):** Noroeste industrial, máxima elevación (inversiones tempranas)  
- **NE2 (Apodaca, 432 msnm):** Noreste industrial-automotriz  

**Gradiente Altitudinal Crítico:**  
334 msnm (SE3, Cadereyta) → 702 msnm (NO2, García)  
Permite modelar **efecto topográfico en dispersión**.

---

### 2.2 Contaminantes & Variables

**Criterio:**  
PM2.5, PM10, O₃, SO₂, NO₂, CO, NO, NOx  

**Meteorológicos:**  
Temperatura (ºC), Humedad (%), Radiación Solar (kW/m²), Precipitación (mm/hr), Presión (mmHg), Viento Velocidad (km/hr), Viento Dirección (0-360°)

---

### 2.3 Calidad de Datos & Flags (CRÍTICO)

**15 tipos de flags afectan validez:**

- **Missingness:** P (falla eléctrica), C (calibración), D (apagado), B (malas condiciones), n (falla comunicación)  
- **Outliers:** m (positivo sobre rango), l (negativo sobre rango), o (PM10 > 900), f (PM10 salto 3x)  
- **Censura:** a (PM < 5 μg/m³), r (comparativo PM10 vs PM2.5)  
- **Especiales:** En SE2, valores flag `l` → **0.36** (no 0) por sensor específico  

**Impacto en VaR:**  
Los flags invalidan ~15-30% de los datos horarios.  
Se requiere **MICE-Estación** (imputación por estación), no *bulk imputation*.

---

## 3. JUSTIFICACIÓN (¿Por Qué Finanzas?)

Los mercados financieros y la contaminación en Monterrey comparten:

- **Volatilidad clustering:** días malos seguidos (*autocorrelación condicional*)  
- **Eventos de cola:** *exceedances* comparables con *crashes bursátiles*  
- **Datos con ruido y missing values:** comunes desde los 1980s  
- **Decisión bajo incertidumbre:** un *trader* y un director de salud pública necesitan saber “¿qué tan mal puede ponerse?”

**Ventaja:**  
En 4 meses podemos entregar un sistema que diga  
> “15% probabilidad de exceder 75 μg/m³ mañana”  
vs. un modelo DL que solo dice “pronóstico: 55 μg/m³ (±20)”.

---

## 4. OBJETIVOS

### Objetivo General
Desarrollar un **framework de pronóstico de riesgo ambiental** para la ZMM que cuantifique incertidumbre usando **métodos de finanzas cuantitativas**, entregando probabilidades de *exceedance* calibradas para soporte de decisiones de salud pública.

### Objetivos Específicos
- **Modelado de Volatilidad:** Calcular “volatilidad implícita” de PM2.5/O₃ usando **GARCH**.  
- **Simulación Monte Carlo:** Generar 10,000 trayectorias de concentración con dependencias entre contaminantes vía **Copulas**.  
- **Teoría de Valor Extremo:** Estimar probabilidad de eventos extremos (AQI > 150).  
- **Backtesting:** Validar modelo con datos 2023-2024 mediante **Kupiec** y **Christoffersen tests**.  
- **Dashboard SIMA:** Entregar herramienta interactiva con **bandas VaR(95%)** y alertas automáticas.

---

## 5. PLAN DE CALIDAD DE DATOS (Específico SIMA)

### 5.1 Protocolo de Limpieza por Flag
```python
# Pseudocódigo específico
for estacion in ['CE', 'SE2', 'SO2', 'NO2']:
    df = cargar_datos(estacion)
    
    # Flags inválidos → Missing
    invalid_flags = ['p','c','d','b','m','l','z','o','s','r','e','a','f','h','n','u','x']
    if estacion == 'SE2':
        invalid_flags.remove('l')  # l es válido pero transformar a 0.36
    
    df[df['flag'].isin(invalid_flags)] = np.nan
    
    # Imputación MICE-Estación: usa últimas 72 horas de la misma estación
    df = MICE_imputacion_horaria(df, max_lag=72)
```

---

### 5.2 Tratamiento de Outliers (Rangos 2020–2025)
| Variable | Regla de Winsorización |
|-----------|-----------------------|
| PM2.5 | >350 μg/m³ → "circuit breaker" |
| PM10 | >820 μg/m³ |
| Temperatura | <-5°C o >45°C |
| Presión | <687 mmHg o >740 mmHg |

---

### 5.3 Estructura de Datos Final

| Campo | Tipo | Descripción |
|--------|------|-------------|
| fecha_hora | datetime | Timestamp completo |
| estacion_id | str | CE, SE2, SO2, etc. |
| PM2.5 | float | Concentración imputada |
| PM2.5_flag | str | Flag original |
| PM2.5_confianza | float | 1 - (% missing en ventana 24h) |
| VaR_95 | float | Límite superior riesgo |
| volatilidad_historica | float | Rolling std 24h |

---

## 6. METODOLOGÍA (Framework "Quantitative Risk")

### Fase 1: Análisis Exploratorio de Series Financieras
- Transformación:  
  \( r_t = \log(rac{PM2.5_t}{PM2.5_{t-1}}) \)
- Tests de estacionariedad: ADF, KPSS  
- Identificación de regímenes: Modelos **Markov-Switching**

---

### Fase 2: Arquitectura de Riesgo
```python
# Pipeline conceptual
Raw Data (SIMA) 
   → Preprocess (MICE imputación, winsorización)
   → Feature Engineering (volatilidad móvil, lags meteorológicos)
   → Modelo Híbrido:
       ├─ GARCH(p,q): Volatilidad condicional
       ├─ Copula: Dependencia PM2.5-O3-NO2
       └─ EVT: Probabilidad de exceedance
   → Simulación Monte Carlo (10k trayectorias)
   → VaR Ambiental: Percentil 95 de distribución simulada
```

---

### Fase 3: Validación Financiera
- **Kupiec Test:** calibración (% de días que exceden VaR ≈ 5%)  
- **Christoffersen Test:** independencia de violaciones  
- **Walk-Forward:** ventanas deslizantes de 30 días para evitar *look-ahead bias*
