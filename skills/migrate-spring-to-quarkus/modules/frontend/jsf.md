# Module: Frontend / View Layer — JSF / Jakarta Faces

Migrate JSF (Jakarta Faces) view layer from Spring to Quarkus.

## Strategy Resolution

Read `<target>/migration-spec.yaml` at module start if it exists:

| Condition | Strategy | Sub-module to Execute |
|---|---|---|
| `decisions.view_layer == 'myfaces'` | Maintain JSF with Quarkus MyFaces | [jsf-myfaces.md](jsf-myfaces.md) |
| `decisions.view_layer == 'qute'` | Migrate JSF to Quarkus Qute | [jsf-qute.md](jsf-qute.md) |
| Standalone run (< 5 view files) | Migrate to Quarkus Qute | [jsf-qute.md](jsf-qute.md) |
| Standalone run (>= 5 view files) | Maintain JSF with Quarkus MyFaces | [jsf-myfaces.md](jsf-myfaces.md) |

## Strategy Execution

1. **If `<target>/migration-spec.yaml` exists**, follow `decisions.view_layer` directly:
   - If `decisions.view_layer == 'myfaces'` → load and execute [jsf-myfaces.md](jsf-myfaces.md)
   - If `decisions.view_layer == 'qute'` → load and execute [jsf-qute.md](jsf-qute.md)
2. **If running standalone without a spec**, evaluate the file count heuristic:
   - Count the `.xhtml` files across `<source>` (`src/main/webapp/`, `src/main/resources/`, etc.).
   - If total `.xhtml` views < 5 → load and execute [jsf-qute.md](jsf-qute.md)
   - If total `.xhtml` views >= 5 → load and execute [jsf-myfaces.md](jsf-myfaces.md)
