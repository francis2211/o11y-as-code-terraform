---
slug: lab-refresh
id: cgt0dnt5rexj
type: challenge
title: 'Lab: Refresh'
teaser: Revertir cambios manuales con terraform refresh
notes:
- type: text
  contents: |-
    # Lab: Revertir cambios manuales

    En este desafío, se te asignará la tarea de

    - Modificar manualmente recursos en la interfaz de usuario de New Relic
    - Actualizar el estado con `terraform refresh`
    - Revertir cambios manuales con `terraform apply`
tabs:
- title: Terminal
  type: terminal
  hostname: docker-vm
  workdir: /newrelic/o11y
- title: Editor
  type: code
  hostname: docker-vm
  path: /newrelic/o11y
difficulty: basic
timelimit: 600
---
🧪  Paso 1: Modificar un recurso existente
=======================

- Dirígete al panel de control de New Relic importado creado en el desafío anterior y elimina algunos elementos.

🧪 Paso 2: terraform refresh
=========

- En la pestaña del terminal, en `cd o11y`, ejecuta `terraform refresh` para actualizar el estado de tus recursos.

```
terraform refresh
```

🏁 Step 3: terraform apply
=========

- (Opcional) En la pestaña del Terminal, carga tus variables de entorno navegando hasta el directorio `o11y` y ejecutando el siguiente comando:

```
source .env
```

- Para corregir cualquier cambio manual en tus recursos, ejecuta `terraform apply` y confirma los cambios.


```
terraform apply
```

Para completar el desafío, presiona  **Check**

