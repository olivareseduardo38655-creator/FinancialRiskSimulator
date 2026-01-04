# Financial Risk Simulator (Monte Carlo Engine)

![Java](https://img.shields.io/badge/Java-17%2B-ed8b00?style=for-the-badge&logo=java&logoColor=white)
![Build](https://img.shields.io/badge/Build-Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)
![Architecture](https://img.shields.io/badge/Architecture-Clean-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## Descripción Ejecutiva

Este proyecto implementa un motor de simulación estocástica de alto rendimiento diseñado para la modelización de riesgos financieros. Utilizando el Método de Monte Carlo y el Movimiento Browniano Geométrico (GBM), el sistema proyecta miles de escenarios de precios futuros de activos para cuantificar la exposición al riesgo de mercado.

El objetivo principal es proveer una herramienta backend robusta que permita calcular métricas críticas como el VaR (Value at Risk) con alta precisión computacional, desacoplando la lógica de simulación de la capa de persistencia.

## Objetivos Técnicos

1.  **Inmutabilidad de Datos:** Implementación estricta de `records` de Java 14+ para garantizar la integridad de los parámetros de configuración y los resultados de la simulación.
2.  **Arquitectura en Capas:** Separación clara de responsabilidades entre el Motor de Cálculo (Engine), el Modelo de Dominio (Model) y la Entrada/Salida (IO).
3.  **Optimización de Memoria:** Uso de arrays primitivos para el manejo eficiente de grandes volúmenes de escenarios simulados (10,000+ iteraciones).
4.  **Persistencia Agnóstica:** Módulo de exportación diseñado para interoperabilidad con herramientas de análisis de datos externas (Excel, Python/Pandas) mediante formato CSV estándar.

## Arquitectura del Sistema

El flujo de datos sigue un diseño lineal y determinista, asegurando la trazabilidad desde la configuración inicial hasta la generación de métricas de riesgo.

```mermaid
graph LR
    A[SimulationConfig] -->|Parámetros| B(MonteCarloEngine)
    B -->|Cálculo Estocástico| C[SimulationResult]
    C -->|Array de Precios| D{RiskCalculator}
    C -->|Raw Data| E[ResultsExporter]
    D -->|Métricas VaR| F[Consola / Reporte]
    E -->|Persistencia| G[simulation_results.csv]
