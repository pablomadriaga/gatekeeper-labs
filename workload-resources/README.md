# Workload Resources

Validación de `requests` y `limits` de CPU y memoria para workloads Kubernetes.

Actualmente la policy utiliza dos `ConstraintTemplate` independientes:

- `warning.yaml`: genera advertencias cuando un workload supera los valores recomendados.
- `deny.yaml`: bloquea workloads que superan los límites máximos permitidos o que no definen `requests` y `limits`.

## Modelo de funcionamiento

### Warning policy

La policy definida en `warning.yaml` utiliza los siguientes parámetros configurables desde TMC:

- `WarnCpu`: valor de CPU a partir del cual se genera una advertencia.
- `WarnMemory`: valor de memoria a partir del cual se genera una advertencia.

Ejemplo:

```text
WarnCpu:    200m
WarnMemory: 350Mi
```

Superar estos valores no bloquea el workload.

TMC debe configurar esta policy con:

```text
Enforcement: WARN
```

### Deny policy

La policy definida en `deny.yaml` utiliza los siguientes parámetros:

- `MaxCpu`: máximo de CPU permitido.
- `MaxMemory`: máximo de memoria permitido.

Ejemplo:

```text
MaxCpu:    300m
MaxMemory: 512Mi
```

Además, esta policy requiere que los containers tengan definidos:

- `resources.requests.cpu`
- `resources.requests.memory`
- `resources.limits.cpu`
- `resources.limits.memory`

TMC debe configurar esta policy con:

```text
Enforcement: DENY
```

## Comportamiento esperado

### CPU

```text
0 ───────────── 200m ───────────── 300m ─────────────>
      OK                WARN                 DENY
```

### Memory

```text
0 ───────────── 350Mi ──────────── 512Mi ─────────────>
      OK                WARN                 DENY
```

Ejemplos:

```text
CPU 100m / Memory 256Mi
→ permitido
→ sin advertencias
```

```text
CPU 250m / Memory 400Mi
→ permitido
→ warning de CPU
→ warning de memoria
```

```text
CPU 400m
→ warning por superar el valor recomendado
→ deny por superar el máximo permitido
```

```text
Memory 600Mi
→ warning por superar el valor recomendado
→ deny por superar el máximo permitido
```

```text
requests o limits ausentes
→ deny
```

## Excepciones

Se contempla incorporar excepciones explícitas para workloads que no puedan cumplir temporalmente la policy.

Una excepción deberá ser visible y justificar su existencia, por ejemplo:

```yaml
metadata:
  labels:
    policy.company.com/resource-policy: exempt
  annotations:
    policy.company.com/resource-policy-exception: "INC-12345 - Legacy application pending resource tuning"
```

El objetivo de una excepción es resolver casos extraordinarios y temporales.

No debe utilizarse como alternativa habitual al cumplimiento de la policy.

En una evolución posterior se podrá exigir que la referencia de excepción cumpla un formato aprobado, por ejemplo un ticket `INC-*`, `CHG-*` o equivalente, e incorporar controles adicionales sobre quién puede autorizarla.
