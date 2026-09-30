# Module: Frontend / View Layer — FreeMarker

Migrate or preserve the FreeMarker view layer from Spring to Quarkus.

## Strategy Resolution

Read `<target>/migration-spec.yaml` at module start if it exists:

| Condition | Strategy | Sub-module to Execute |
|---|---|---|
| `decisions.view_layer == 'qute'` | Migrate FreeMarker to Qute | [freemarker-qute.md](freemarker-qute.md) |
| `decisions.view_layer == 'freemarker'` | Preserve FreeMarker with Quarkus | [freemarker-quarkus.md](freemarker-quarkus.md) |
| Standalone run (< 5 `.ftl` / `.ftlh` / `.ftlx` view files) | Migrate to Qute | [freemarker-qute.md](freemarker-qute.md) |
| Standalone run (>= 5 `.ftl` / `.ftlh` / `.ftlx` view files) | Preserve with quarkus-freemarker | [freemarker-quarkus.md](freemarker-quarkus.md) |

## Strategy Execution

1. **If `<target>/migration-spec.yaml` exists**, follow `decisions.view_layer` directly:
   - If `decisions.view_layer == 'qute'` → load and execute [freemarker-qute.md](freemarker-qute.md)
   - If `decisions.view_layer == 'freemarker'` → load and execute [freemarker-quarkus.md](freemarker-quarkus.md)
2. **If running standalone without a spec**, evaluate the file count heuristic:
   - Count the `.ftl`, `.ftlh`, and `.ftlx` files across `<source>` (`src/main/resources/templates/` and any other template directories).
   - If total FreeMarker view files < 5 → load and execute [freemarker-qute.md](freemarker-qute.md)
   - If total FreeMarker view files >= 5 → load and execute [freemarker-quarkus.md](freemarker-quarkus.md)
