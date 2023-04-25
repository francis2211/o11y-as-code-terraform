---
slug: lab-workloads
id: mduxblhrjf9f
type: challenge
title: 'Lab: Workloads'
teaser: Utilice las cargas de trabajo para organizar sus recursos
notes:
- type: text
  contents: |-
    # Utilice Cargas de trabajo para organizar sus recursos.

    En este desafío, se le ha encomendado:
    - Crear una carga de trabajo para organizar todos sus recursos en una vista (Full Stack).
    - Enlazarlo con su carga de trabajo y generar un permalink.
tabs:
- title: Editor
  type: code
  hostname: docker-vm
  path: /newrelic/o11y
- title: Terminal
  type: terminal
  hostname: docker-vm
  workdir: /newrelic/o11y
difficulty: basic
timelimit: 600
---
🧪 Paso 1: Crear una Carga de Trabajo
=======================

- Una Carga de Trabajo es una colección de todo lo que usted o su equipo son responsables de monitorear, solucionar problemas y  mejorar.
- Las Cargas de Trabajo se crean usando una etiqueta común para agrupar todos los recursos juntos.
- Agregue este fragmento de código después de `# TODO: Create a workload using the team tag`

```
resource "newrelic_workload" "O11yAsCode" {
  name = var.MY_TEAM_WORKLOAD_NAME
  account_id = (var.NEW_RELIC_ACCOUNT_ID)

  # Include entities with a set of tags.
  entity_search_query {
    query = var.MY_TEAM_WORKLOAD_QUERY
  }

  entity_guids = [
    newrelic_one_dashboard_json.imported-dashboard.guid,
    newrelic_one_dashboard_json.custom-dashboard.guid,
  ]
}
```

- Recuerde guardar el archivo.
- Revise `TF_VAR_MY_TEAM_WORKLOAD_QUERY` y `TF_VAR_TAGS` en `o11y/terraform.tfvars`
- Asegúrese de que las `TF_VAR_TAGS` que cree se reflejen en `TF_VAR_MY_TEAM_WORKLOAD_QUERY`

🧪 Step 2: Link to your workload
=======================

- Cree un enlace a su carga de trabajo produciendo el permalink.
- Agregue este fragmento de código después de `# TODO: Output the permalink to the workload`

```
output "my-team-workload" {
  value = newrelic_workload.O11yAsCode.permalink
}
```

- Recuerde guardar el archivo.

🏁 Step 3: Finish
=======================

- En la pestaña Terminal, previsualice los cambios con el siguiente comando:

```
terraform plan
```

- Cuando esté listo, aplique los cambios:

```
terraform apply
```

- Para completar el desafío, presione **Check**
