---
slug: lab-dashboards
id: lmkvcmjjmi2u
type: challenge
title: 'Lab: Dashboards'
teaser: Trabajando con Dashboards
notes:
- type: text
  contents: |-
    # Lab: Dashboards

    En este desafío, se le asigna la tarea de
    - Importar un panel de control desde New Relic.
    - Enlazar a ese panel de control importado.
    - Crear un panel de control dinámico basado en un archivo de plantilla.
    - Enlazar a ese panel de control personalizado.
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
🧪 Paso 1: Importar un dashboard de New Relic
=======================

1. Navegue a New Relic y cree un dashboard.
2. Copie el dashboard preconstruido como un archivo json.
3. Guarde el archivo como `o11y/dashboard/import.json`

- Después de esos pasos, cree un recurso de dashboard para el dashboard importado.
- En `o11y/main.tf` agregue este fragmento de código después de `# TODO: Import a dashboard from a JSON file`

```
resource "newrelic_one_dashboard_json" "imported-dashboard" {
  json = file("dashboards/import.json")
}
```

- Cree un enlace a su dashboard importado
- En `o11y/main.tf` agregue este fragmento de código después de `# TODO: Output the permalink to the imported dashboard`

```
output "my-team-imported-dashboard" {
  value = newrelic_one_dashboard_json.imported-dashboard.permalink
}
```

- Recuerde guardar el archivo.
- Utilizando la pestaña Terminal, previsualice los cambios utilizando el siguiente comando:

```
terraform plan
```

- Una vez que esté satisfecho con los cambios, ejecute el siguiente comando para aplicar los cambios.

```
terraform apply
```

🧪 Paso 2: Crear un Dashboard dinámico
=======================

- Utilizando la pestaña Editor, revise `o11y/dashboards/custom.json.tftpl`
- Observe las variables utilizadas `${nombre_variable}`
- Las variables pueden pasarse a la plantilla.
- Cree un recurso de dashboard personalizado utilizando variables.
- Agregue este fragmento de código después de `# TODO: Create a dashboard from a template file`

```
resource "newrelic_one_dashboard_json" "custom-dashboard" {
  json = templatefile("dashboards/custom.json.tftpl", {
    account_id = var.NEW_RELIC_ACCOUNT_ID,
    applications = var.APPS,
    dashboard_name: "O11yAsCode Dashboard (TF)",
  })
}
```

- Cree un enlace a su dashboard personalizado
- En `o11y/main.tf` agregue este fragmento de código después de `# TODO: Output the permalink to the custom dashboard`

```
output "my-team-custom-dashboard" {
  value = newrelic_one_dashboard_json.custom-dashboard.permalink
}
```

- Remember to save the file.

🏁 Paso 3: Finalizar
=======================



- Utilizando la pestaña Terminal, navegue al directorio `o11y` y ejecute el siguiente comando para previsualizar sus cambios:


```
terraform plan
```

- Una vez que esté satisfecho con los cambios, ejecute el siguiente comando para aplicar los cambios.

```
terraform apply
```

Para completar el desafío, presione **Check**
