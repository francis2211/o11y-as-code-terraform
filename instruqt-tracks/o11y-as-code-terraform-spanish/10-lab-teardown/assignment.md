---
slug: lab-teardown
id: uqiymgroagmd
type: challenge
title: 'Lab: Teardown'
teaser: Elimina todos tus recursos.
notes:
- type: text
  contents: |-
    # Terraform Destroy

    En este desafío, se le asigna la tarea de
    - limpiar su entorno ejecutando `terraform destroy`.
tabs:
- title: Terminal
  type: terminal
  hostname: docker-vm
  workdir: /newrelic/o11y
difficulty: basic
timelimit: 600
---
🏁 Ejecutar Pulumi Down
=========

- En la pestaña del terminal, `cd o11y`, ejecuta `terraform destroy` y confirma para destruir todos tus recursos en New Relic.
- Esto restablecerá tu entorno mientras mantiene el código para reproducirlo nuevamente si es necesario.

```
terraform destroy
```

- Para completar el desafío, presiona **Check**
