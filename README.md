# Gatekeeper Labs

Laboratorios y pruebas de políticas OPA Gatekeeper utilizadas con
VMware Tanzu Mission Control Self-Managed.

El objetivo de este repositorio es mantener ejemplos simples, reproducibles
y orientados a casos reales de gobierno, validación y control de recursos
Kubernetes.

## Objetivo del repositorio

Este repositorio busca funcionar como una colección de patrones reutilizables
para políticas de Kubernetes basadas en OPA Gatekeeper.

La idea es que cada laboratorio permita entender:

- qué problema intenta resolver;
- qué recurso Kubernetes valida;
- qué comportamiento aplica;
- cómo probarlo;
- y qué resultado se espera.

## Estructura

Cada laboratorio contiene, según corresponda:

- uno o más `ConstraintTemplate`;
- manifiestos de prueba;
- un `README.md` con el comportamiento esperado;
- ejemplos válidos e inválidos para verificar la policy.

