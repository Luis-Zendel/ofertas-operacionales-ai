# Entendimiento del problema.

Rappi tiene repartidores trabajando en tiempo real en diferentes zonas en 9 paises. 

Cuando la oferta y demanda no estan balanceadas suceden 2 escenarios:

## 1) SATURACIÓN ( + ordenes - repartidores activos )
Consecuencia: clientes esperan más, ordenes se pierden NPS cae

## 2) SOBRE OFERTA ( - ordenes + repartidores activos )
Consecuencia: ineficiencia operacional, costo sin retorno 

## Metrica central de balance operacional 
Ratio = Ordenes / repartidores conectados 
Si ratio es menor a 0.5 Sobre-oferta (ineficiencia de costo)
Si ratio es 0.9 a 1.2 es un rango saludable 
Si ratio es mayor a 1.8 (pérdida de órdenes)

## Estado actual:
El equipo operations actualmente gestiona el balance de forma reactiva

## Objetivo:
Construir un sistema de gestion de balance de forma proactiva
Para:
    - Enbiar alartas accionables con recomendaciones concretas al euipo a través de Telegram.

## MÓDULOS ESPECIFICOS

### Módulo 1 - Diagnóstico Operacional (25%)
DESCRIPCIÓN:
Analiza el dataset histórico e identifica los factores que afectan la operación. 
Se deben de responder las siguientes preguntas

PREGUNTAS A RESPONDER: 
P1. ¿En qué horas del día y en qué zonas la operación alcanza niveles críticos de saturación? Cuantifica.
- Evaluar el ratio por hora y zona, ya que el número de ordenes y número de repartidores activos se relacionan a esos 2 parámetros
P2. ¿Qué variable externa del dataset se correlaciona con el deterioro del ratio operacional? Describe el mecanismo.
- El dataset cuenta con **PRECIPITATION_MM** que es una variable externa meteorológica.
P3. ¿Todas las zonas responden igual a esa variable? Identifica las más vulnerables y explica por qué tienen mayor sensibilidad.
- 
P4. ¿El nivel de earnings (incentivos) está bien calibrado a lo largo del mes? ¿Detectas periodos con gasto ineficiente? Muestra los días exactos.
P5. ¿Qué relación tiene el nivel de earnings con la saturación operacional? ¿Es una relación simple o depende de otras condiciones?

ENTREGABLE:
Notebook o script reproducible con el análisis completo (Python recomendado).
Visualizaciones para cada hallazgo (el gráfico correcto para cada tipo de pregunta).
Resumen de hallazgos en máximo 1 página: patrones encontrados + impacto cuantificado en la operación.

### Módulo 2 - Motor de alertas tempranas con API de clima (35%)
DESCRIPCIÓN:
Basado en los patrones del módulo 1. Construye un sistema que monitoree las condiciones climáticas en tiempo real.