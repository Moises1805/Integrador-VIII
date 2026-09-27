 # FICHA TÉCNICA Y ESTADO DEL PROYECTO INTEGRADOR

---

## 1. Descripción del Proyecto

 
* **Organización:** Empresa Municipal Aguas Claras (Ubicada en el departamento de Carazo, Nicaragua).
* **Contexto Operativo:** Operación de producción, distribución, micromedición y facturación de agua potable para 28,600 conexiones activas distribuidas en 9 sectores hidráulicos de 4 municipios de Carazo. El análisis se focaliza en 5 sectores hidráulicos principales: Diriamba, Dolores, Jinotepe Norte, Jinotepe Sur y San Marcos .
* **Problema Principal:** Escenario de alto riesgo operativo caracterizado por una **tasa de fugas confirmadas del 35.6%** entre los casos con resultado conocido y una referencia de **Agua No Contabilizada (ANC) del 28%**. Esta situación se agrava por la baja calidad e integración de los datos: inconsistencias semánticas (*"ESTIMACIÓN"* vs. *"Estimación"*), datos de consumo nulos, registros fuera de rango operativo y cierres heterogéneos de órdenes de trabajo.
* **Decisión Institucional a Apoyar:** Priorizar mensualmente las inspecciones técnicas de fugas y el programa de revisión/recambio de medidores con base en una matriz objetiva de riesgo operativo físico.
* **Unidad de Análisis y Periodo:** La relación **conexión-mes**, abarcando el periodo histórico desde enero de 2024 hasta junio de 2026  
---

## 2. Integrantes y Estructura Académica

* **Institución:** Universidad Nacional Autónoma de Nicaragua (UNAN-Managua, CUR Carazo).
* **Unidad Académica:** Departamento de Ciencias, Tecnología y Salud.
* **Carrera / Componente Curricular:** Ingeniería en Sistemas de Información / Integrador VIII - Gobernanza de Datos.
* **Equipo de Trabajo:** Equipo #10.
* **Integrantes (Estudiantes):**
  * **Jeanelly Tatiana Rodríguez Cárdenas**.
  * **Moisés Gabriel Rodríguez Mendieta**.
* **Docentes Asignados:**
  * **MSc. Yulieth Nohemí CasaNova**.
  * **Profesor Eddy Galán**.
  * **Profesor Wuilber Matus**.
	

---

## 3. Requisitos del Marco de Gobierno de Datos

El marco cumple estrictamente con los siguientes estándares internacionales y entregables metodológicos:

### A. Referentes Normativos Exigidos
* **ISO/IEC 38505-1 (Gobernanza de Datos de TI):** Para guiar la definición de principios prácticos de gobierno vinculados a acciones concretas de control.
* **ISO/IEC 25012:2008 (Calidad de Datos):** Para evaluar la completitud, consistencia, exactitud y trazabilidad del conjunto transaccional.
* **DAMA-DMBOK (2.ª ed.):** Para estructurar los dominios de datos, el catálogo de metadatos, la gestión de calidad y la asignación de roles.
* **COBIT 2019 / ISACA:** Para definir la Matriz RACI con un único *Accountable* (A) no delegable por actividad y alinear el tratamiento de riesgos con objetivos de gestión como **APO11** (Calidad), **APO12** (Riesgos) y **APO13** (Seguridad).
* **NIST Privacy Framework:** Para la catalogación del ecosistema de procesamiento, control de accesos RBAC y seudonimización con la clave `id_conexion_mes`.
* **ISO/IEC 19510 / BPMN 2.0 e ISO 9001:2015:** Para la modelación gráfica del proceso actual (Mapa AS-IS) y el diseño del Sistema de Gestión de Calidad.

### B. Entregables y Componentes Obligatorios
1. **Ficha de Contexto y Matriz de Hechos, Supuestos y Vacíos**.
2. **Diagrama de Causa-Efecto (Ishikawa)** adaptado a las 6 dimensiones de gobernanza de datos.
3. **Catálogo/Inventario de Datos Críticos:** Cobertura de las 8 variables clave (D01 a D08) con ID, descripción, uso, sensibilidad e importancia.
4. **Mapa de Actores y Matriz RACI:** Con asignación transparente de responsabilidades entre Comercial, Acueductos, Mantenimiento, Catastro/TI y Gerencia Operativa.
5. **Diez Políticas Prioritarias de Datos (POL-01 a POL-10):** Regulando accesos, catálogos cerrados, cuarentena informática y linaje.
6. **Matriz de Riesgos y Matriz de Alineación Estratégica:** Evaluación de impacto, probabilidad y COBIT.
7. **Diseño Analítico Inicial:** Matriz de preguntas analíticas, técnica de clasificación supervisada y métricas de evaluación SMART.

---

## 4. Instrucciones de Ejecución Metodológica

Para la operativización del proyecto y la transformación de datos, se ejecuta la siguiente secuencia técnica:

1. **Ingesta e Integración de Silos Transaccionales:** Extraer los datos desde Comercial (SQL), SCADA (API/eventos), Mantenimiento (XLSX) y Catastro GIS (CSV), unificándolos bajo la clave `id_conexion_mes`.
2. **Normalización Semántica (Pipeline ETL):** Sustituir los campos de texto libre por catálogos cerrados y listas desplegables obligatorias en las app móviles comerciales para eliminar inconsistencias de captura (*"Estimación"* vs. *"ESTIMACIÓN"*).
3. **Validación y Filtrado Operativo de Calidad:** Configurar scripts automáticos de validación técnica en base de datos para bloquear consumos negativos (&lt;0 m³) o superiores a 180 m³, y presiones ilógicas fuera de la franja operativa de 12 a 72 PSI.
4. **Gestión de Cuarentena e Inyección de Linaje:** Enviar a cuarentena informática los registros con nulos críticos e inyectar de forma obligatoria los metadatos de auditoría `sistema_origen` y `fecha_carga`.
5. **Ejecución del Modelo Predictivo:** Entrenar el algoritmo de **Clasificación Supervisada** utilizando la variable categórica binaria `fuga_confirmada` (1 = Fuga; 0 = No Fuga), priorizando la métrica de **Exhaustividad (Recall)** para reducir las pérdidas no detectadas.
6. **Despliegue Operativo:** Automatizar mensualmente el cálculo del KPI **Tasa de Fuga Confirmada (TFC)** para alimentar el tablero de la Gerencia Operativa y guiar la programación de las cuadrillas de campo.

---

## 5. Estado del Proyecto

| Corte / Hito | Semanas | Alcance y Entregables | Estado |
| :--- | :---: | :--- | :---: |
| **Corte I: Diagnóstico y Gobernanza Inicial** | **Semanas 1 - 5** | Consolidación del documento **`marco-gobierno-datos-v1.docx`** y presentación gerencial (`Primer Corte semana 5.pptx`), cubriendo contexto, Ishikawa, principios ISO 38505-1, catálogo D01-D08, RACI y políticas iniciales. | **COMPLETADO** |
| **Corte II: Calidad de Procesos, ETL y Perfil** | **Semanas 6 - 10** | **Fase Actual:** Análisis Exploratorio de Datos (EDA), diseño gráfico del **`flujo_diseno_integrado.png`**, formalización de las matrices de riesgo/alineación estratégica S6 y S7, elaboración del documento **`entregables-y-presentacion-s7-completo.docx`** y diseño del Sistema de Gestión de Calidad (Mapa AS-IS, indicadores ICD/PLR/TFC y Plan de Mejora v1). | **EN CURSO** |
| **Corte III: Modelado, Predicción y Cierre** | **Semanas 11 - 16** | Entrenamiento del algoritmo de clasificación supervisada, optimización de métricas (Recall/AUC-ROC), integración con el mapa de procesos propuesto (TO-BE), matriz de trazabilidad final y defensa académica del proyecto final. | **PENDIENTE** |

 
