---
slug: lab-tags
id: obg6yuxxcyvq
type: challenge
title: 'Lab: Tags'
teaser: Etiquetar tus aplicaciones
notes:
- type: text
  contents: |-
    # Laboratorio: Etiquetando tus aplicaciones

    En este desafío, se te asigna la tarea de:
    - Obtener tus recursos de aplicación desde New Relic
    - Etiquetar tus aplicaciones con pares clave-valor equipo y entorno.
    - Revisar tus etiquetas en New Relic.
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
🧪 Paso 1: Agregar etiquetas a tus aplicaciones
=======================

- Obtén los metadatos de la aplicación de New Relic.
- En `o11y/main.tf` agrega este código después de `# TODO: Obtener las aplicaciones de New Relic.`

```
data "newrelic_entity" "APPS" {
  count = length(var.APPS)
  name  = var.APPS[count.index]
  type = "APPLICATION"
  domain = "APM"
}
```

- Salida de los metadatos de la aplicación.
- En `o11y/main.tf` agrega este código después de `# TODO: Mostrar los GUID de las aplicaciones que vamos a supervisar.`

```
output "o11y_apps" {
  value = data.newrelic_entity.APPS[*].guid
}
```

- Recuerda guardar el archivo.
- Usando la pestaña Terminal, visualiza los cambios utilizando el siguiente comando:

```
terraform plan
```

- Una vez que estés satisfecho con los cambios, ejecuta el siguiente comando para aplicar los cambios.

```
terraform apply
```

🧪 Paso 2: Agregar etiquetas a tus aplicaciones
=======================

- Usando los metadatos recuperados en el paso anterior, ahora tenemos acceso al guid que necesita `newrelic_entity_tags.`
- Revisa la variable de entorno `TF_VAR_TAGS` en `o11y/terraform.tfvars`
- Usa variables de entorno para etiquetar tus aplicaciones dinámicamente
- En o11y/main.tf agrega este código después de `# TODO: Etiquetar cada aplicación con los valores de equipo y entorno.`

```
resource "newrelic_entity_tags" "APPS" {
  count = length(var.APPS)
  guid  = data.newrelic_entity.APPS[count.index].guid

  dynamic "tag" {
    for_each = var.TAGS
    content {
      key    = tag.key
      values = [tag.value]
    }
  }
}
```

- Recuerda guardar el archivo.

🏁 Paso 3: Finalizar
=======================

- Usando la pestaña Terminal, visualiza los cambios utilizando el siguiente comando:

```
terraform plan
```

- Una vez que estés satisfecho con los cambios, ejecuta el siguiente comando para aplicar los cambios.

```
terraform apply
```

- Para completar el desafío, presiona **Check**
