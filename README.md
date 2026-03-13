# Predictor abandono

## Proyecto de Predicción de Abandono de Empleados

Desarrollo de un sistema completo de predicción de abandono de empleados que combina análisis de datos exploratorio, modelado de machine learning y visualización interactiva para generar insights accionables y cuantificar el impacto económico en la organización.

### Visión General

Se realiza un EDA exhaustivo para generar insights y predecir las implicaciones económicas del abandono de empleados. Se contemplan varios modelos de machine learning del state of art para predecir el abandono y finalmente se genera un reporte interactivo en Tableau.

### Stack Tecnológico

- **Python**: Pandas, NumPy, Matplotlib, Seaborn
- **Machine Learning**: Scikit-learn, XGBoost, LightGBM, CatBoost
- **Optimización**: RandomizedSearchCV, Scikit-optimize
- **Visualización**: Tableau (dashboard interactivo)
- **Procesamiento**: Pipeline, ColumnTransformer, OneHotEncoder

## Dashboard de Tableau

<div class='tableauPlaceholder' id='viz1740899400000' style='position: relative'>
  <noscript>
    <a href='https://public.tableau.com/app/profile/brian.alex.fuentes.acu.a/viz/dashBoardTest/Dashboard1'>
      <img alt='Dashboard 1' src='https://public.tableau.com/static/images/da/dashBoardTest/Dashboard1/1.png' style='border: none' />
    </a>
  </noscript>
  <object class='tableauViz' style='display:none;'>
    <param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' />
    <param name='embed_code_version' value='3' />
    <param name='site_root' value='' />
    <param name='name' value='dashBoardTest/Dashboard1' />
    <param name='tabs' value='no' />
    <param name='toolbar' value='yes' />
    <param name='static_image' value='https://public.tableau.com/static/images/da/dashBoardTest/Dashboard1/1.png' />
    <param name='animate_transition' value='yes' />
    <param name='display_static_image' value='yes' />
    <param name='display_spinner' value='yes' />
    <param name='display_overlay' value='yes' />
    <param name='display_count' value='yes' />
    <param name='language' value='es-ES' />
  </object>
</div>


 **[Ver Dashboard Interactivo Completo](https://public.tableau.com/app/profile/brian.alex.fuentes.acu.a/viz/dashBoardTest/Dashboard1)**

---

##  Análisis Exploratorio y Limpieza de Datos

### Dataset y Preprocesamiento
- **Dataset**: 1,470 registros con 31 variables iniciales
- **Limpieza estratégica**: Eliminación de variables con alto porcentaje de nulos y sin variabilidad
- **Imputación inteligente**: Basada en distribución de frecuencias para variables categóricas

### Insights Clave del EDA
- **Tasa de abandono**: 16.1% de los empleados abandonaron
- **Perfil de riesgo**: Empleados que viajan frecuentemente, en ventas/RRHH, con baja satisfacción laboral
- **Variables críticas**: Horas extra, satisfacción laboral, nivel educativo y salario

---

## Modelado de Impacto Económico

### Metodología de Costos
Implementación basada en estándares del *Center for American Progress*:
- Empleados < $30k: 16.1% de su salario
- Empleados $30k-50k: 19.7% de su salario  
- Empleados $50k-75k: 20.4% de su salario
- Empleados > $75k: 21% de su salario

### Resultados de Negocio
- **Impacto anual**: $2.7M en costos por abandono
- **Potencial de ahorro**: 
  - Reducir 10% = $271,900 anuales
  - Reducir 20% = $543,801 anuales
  - Reducir 30% = $815,701 anuales

---

## Pipeline de Machine Learning

### Arquitectura del Modelo
```python
# Pipeline completo con preprocesamiento y modelado
pipeline = Pipeline([
    ('preprocessing', ColumnTransformer([
        ('scaler', StandardScaler(), numeric_features),
        ('encoder', OneHotEncoder(drop='if_binary'), categorical_features)
    ])),
    ('classifier', RandomForestClassifier(max_depth=9, n_estimators=50))
])
```

### Modelos Evaluados y Optimizados
| Modelo | AUC-ROC | Estado |
|--------|---------|---------|
| Decision Tree | 0.66 | Baseline |
| **Random Forest** | **0.78** | ⭐ Mejor rendimiento |
| XGBoost | Optimizado | RandomizedSearchCV |
| LightGBM | Optimizado | RandomizedSearchCV |
| CatBoost | Optimizado | RandomizedSearchCV |
| Logistic Regression | Referencia | Modelo lineal |

### Técnicas de Optimización
- **RandomizedSearchCV** con 100 iteraciones y validación cruzada (5-fold)
- **Optimización bayesiana** para hiperparámetros
- **Balance de clases** con estratificación en train/test split

---

## Métricas y Variables Predictivas

### Performance del Modelo
- **AUC-ROC**: 0.78 (Random Forest optimizado)
- **Validación cruzada**: 5-fold para robustez estadística
- **Feature importance**: Identificación de variables predictivas clave

### Variables Más Influyentes
1. **Horas extra** (correlación positiva fuerte)
2. **Satisfacción laboral** (correlación inversa)
3. **Nivel educativo y salario** (impacto significativo)
4. **Departamento y puesto** (factores contextuales)

---

## Impacto y Aplicaciones

### Valor de Negocio Generado
- **Reducción de costos**: Identificación temprana permite intervención proactiva
- **Optimización de recursos**: Focalización en empleados de alto riesgo
- **Toma de decisiones**: Base cuantitativa para estrategias de RRHH
- **Proyecciones financieras**: Modelado de escenarios para presupuesto

### Casos de Uso Implementados
1. **Sistema de alerta temprana** para empleados en riesgo
2. **Programas de retención** personalizados por perfil
3. **Optimización de presupuesto** de capacitación y beneficios
4. **Métricas KPI** para seguimiento de rotación

---

## Habilidades Demostradas

### Data Science & Analytics
- **EDA completo**: Análisis univariado y bivariado con visualizaciones normalizadas
- **Feature engineering**: Selección y transformación de variables
- **Análisis de negocio**: Cuantificación de impacto económico

### Machine Learning
- **Modelado predictivo**: Comparación de múltiples algoritmos
- **Optimización**: Hiperparámetros con RandomizedSearchCV
- **Validación**: Métricas robustas y validación cruzada

### Business Intelligence
- **Dashboard interactivo**: Tableau con visualizaciones dinámicas
- **Comunicación**: Traducción de resultados técnicos a valor de negocio
- **Storytelling**: Insights accionables para stakeholders

---

## Estructura del Proyecto

```
├── ds_simulacion.ipynb    # Notebook principal con análisis completo
├── AbandonoEmpleados.csv  # Dataset original
└── README.md             # Documentación del proyecto
```

### Contenido del Notebook
1. **Carga y limpieza de datos**
2. **Análisis exploratorio univariado y bivariado**
3. **Generación de insights de negocio**
4. **Cuantificación del impacto económico**
5. **Desarrollo y evaluación de modelos ML**
6. **Optimización de hiperparámetros**

---

Este proyecto demuestra la capacidad de transformar datos brutos en insights accionables con impacto económico medible, combinando técnicas avanzadas de machine learning con visualización interactiva para la toma de decisiones estratégicas.
