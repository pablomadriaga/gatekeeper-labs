# TMC / OPA Gatekeeper Labs

Laboratorios y pruebas de políticas OPA Gatekeeper utilizadas con
VMware Tanzu Mission Control Self-Managed.

## Labs

### Required Labels

Permite requerir labels organizacionales sobre los recursos Kubernetes.

Los siguientes labels pueden activarse o desactivarse desde los parámetros
de la Custom Policy en TMC:

```text
requireApp          ON/OFF
requireOwner        ON/OFF
requireEnvironment  ON/OFF
requireCostCenter   ON/OFF
requireTeam         ON/OFF
```

También se pueden agregar labels adicionales a demanda. 

La policy puede utilizarse con distintos modos de enforcement, por ejemplo:

- Warn: permite crear el recurso y muestra una advertencia si faltan labels.
- Deny: bloquea la creación del recurso si faltan labels requeridos.
