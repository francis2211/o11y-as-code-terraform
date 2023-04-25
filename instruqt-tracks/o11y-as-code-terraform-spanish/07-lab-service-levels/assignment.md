---
slug: lab-service-levels
id: ybxqr81ifw0t
type: challenge
title: 'Lab: Service Levels'
teaser: Creando SLIs y SLOs para sus aplicaciones
notes:
- type: text
  contents: |-
    # Creación de SLIs y SLOs para tus aplicaciones

    En este desafío, se te asigna la tarea de:

    - Crear un Indicador de Nivel de Servicio (SLI) para la latencia de tus aplicaciones.
    - Crear un Indicador de Nivel de Servicio (SLI) para las tasas de error de tus aplicaciones.
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
🧪 Paso 1: Crear un SLI para latencia
=======================

- Cree un indicador de nivel de servicio para cada aplicación utilizando `newrelic_service_level`
- En `o11y/main.tf`, agregue este fragmento de código después de `# TODO: Create a Serivce Level Indicator for the latency of your applications`

```
resource "newrelic_service_level" "latency" {
  count = length(var.APPS)
  guid = data.newrelic_entity.APPS[count.index].guid
  name = "Latency for ${var.APPS[count.index]}"
  description = "Proportion of requests that are served faster than a threshold."

  events {
    account_id = var.NEW_RELIC_ACCOUNT_ID
    valid_events {
      from = "Transaction"
      where = "appName = '${var.APPS[count.index]}' AND (transactionType='Web')"
    }
    good_events {
      from = "Transaction"
      where = "appName = '${var.APPS[count.index]}' AND (transactionType= 'Web') AND duration < 0.1"
    }
  }

  objective {
    target = 99.00
    time_window {
      rolling {
        count = 7
        unit = "DAY"
      }
    }
  }
}
```

- Recuerde guardar el archivo.

🧪 Paso 2: Crear un SLI para la tasa de error
=======================

- Cree un indicador de nivel de servicio para cada aplicación utilizando `newrelic_service_level`
- En `o11y/main.tf`, agregue este fragmento de código después de `# TODO: Create a Serivce Level Indicator for the error rates of your applications`

```
resource "newrelic_service_level" "error-rate" {
  count = length(var.APPS)
  guid = data.newrelic_entity.APPS[count.index].guid
  name = "Error Rate for ${var.APPS[count.index]}"
  description = "Proportion of requests that are returning errors above an acceptable threshold."

  events {
    account_id = var.NEW_RELIC_ACCOUNT_ID
    valid_events {
      from = "Transaction"
      where = "appName = '${var.APPS[count.index]}' AND (transactionType='Web')"
    }
    bad_events {
      from = "Transaction"
      where = "appName = '${var.APPS[count.index]}' AND (transactionType= 'Web') AND error.expected IS FALSE"
    }
  }

  objective {
    target = 99.00
    time_window {
      rolling {
        count = 7
        unit = "DAY"
      }
    }
  }
}
```

- Recuerde guardar el archivo.

🏁 Paso 3: Finalizar
=======================



- Usando la pestaña Terminal, previsualice los cambios usando el siguiente comando:

```
terraform plan
```

- Una vez que esté satisfecho con los cambios, ejecute el siguiente comando para aplicarlos:

```
terraform apply
```

- Para completar el desafío, presione **Check**

