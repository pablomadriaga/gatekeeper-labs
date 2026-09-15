# TMC / OPA Gatekeeper Labs

Laboratorios y pruebas de políticas OPA Gatekeeper utilizadas con
VMware Tanzu Mission Control Self-Managed.

## Labs

### Deployment resources

Validación de requests y limits para Deployments.

- Warning si CPU > 200m
- Warning si memory > 350Mi
- Deny si CPU > 300m
- Deny si memory > 512Mi
- Deny si requests no están definidos
- Deny si limits no están definidos

