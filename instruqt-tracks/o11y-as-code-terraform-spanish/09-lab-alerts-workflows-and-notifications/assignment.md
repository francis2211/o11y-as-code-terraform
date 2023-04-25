---
slug: lab-alerts-workflows-and-notifications
id: hozaf1qzkbhd
type: challenge
title: 'Lab: Alerts, Workflows and Notifications'
teaser: Configura alertas y notificaciones antes de que los problemas se conviertan
  en un problema mayor.
notes:
- type: text
  contents: |-
    # Creando Alertas, Flujos de Trabajo y Notificaciones

    En este desafío, se te asigna:
    - Crear políticas de alerta para cada aplicación
    - Cada aplicación monitoreará la latencia y las tasas de error
    - Configurar un destino y canal de correo electrónico
    - Agregar un flujo de trabajo para enviar notificaciones cuando se alcancen ciertos umbrales.
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
timelimit: 1800
---
🧪 Paso 1: Crear políticas de alerta
=======================

- Usa `newrelic_alert_policy` para crear políticas de alerta
- En `o11y/main.tf`, agrega este fragmento de código después de `# TODO: Create an alert policy for the apps`

```
resource "newrelic_alert_policy" "alert_policies" {
  name = "${var.APPS[count.index]} alert policy (TF)"
  count = length(var.APPS)
  incident_preference = "PER_CONDITION"
}
```

- Recuerda guardar el archivo.

🧪 Paso 2: Crear condiciones de alerta
=======================

- Usa `newrelic_nrql_alert_condition` para crear condiciones de alerta que observen la latencia.
1. En `o11y/main.tf`, agrega este fragmento de código después de `# TODO: Create an alert condition observing latency of the apps`

```
resource "newrelic_nrql_alert_condition" "Latency" {
  count              = length(var.APPS)
  policy_id          = newrelic_alert_policy.alert_policies[count.index].id
  name               = "${var.APPS[count.index]}-latency-baseline (TF)"
  account_id         = var.NEW_RELIC_ACCOUNT_ID
  type               = var.ALERT_LATENCY.type
  description        = var.ALERT_LATENCY.description
  enabled            = var.ALERT_LATENCY.enabled
  aggregation_method = var.ALERT_LATENCY.aggregation_method
  aggregation_delay  = var.ALERT_LATENCY.aggregation_delay
  baseline_direction = var.ALERT_LATENCY.baseline_direction
  slide_by           = var.ALERT_LATENCY.slide_by

  nrql {
    query = replace(var.ALERT_LATENCY.query, "__APP_NAME__", var.APPS[count.index])
  }

  critical {
    operator              = var.ALERT_LATENCY.critical_operator
    threshold             = var.ALERT_LATENCY.critical_threshold
    threshold_duration    = var.ALERT_LATENCY.critical_threshold_duration
    threshold_occurrences = var.ALERT_LATENCY.critical_threshold_occurrences
  }

  warning {
    operator              = var.ALERT_LATENCY.warning_operator
    threshold             = var.ALERT_LATENCY.warning_threshold
    threshold_duration    = var.ALERT_LATENCY.warning_threshold_duration
    threshold_occurrences = var.ALERT_LATENCY.warning_threshold_occurrences
  }
}
```

- Usa `newrelic_nrql_alert_condition` para crear condiciones de alerta que observen las tasas de error.
2. En `o11y/main.tf`, agrega este fragmento de código después de `# TODO: Create an alert condition observing error rates of the apps`

```
resource "newrelic_nrql_alert_condition" "ErrorRate" {
  count              = length(var.APPS)
  policy_id          = newrelic_alert_policy.alert_policies[count.index].id
  name               = "${var.APPS[count.index]}-error-rate-baseline (TF)"
  account_id         = var.NEW_RELIC_ACCOUNT_ID
  type               = var.ALERT_ERROR_RATE.type
  description        = var.ALERT_ERROR_RATE.description
  enabled            = var.ALERT_ERROR_RATE.enabled
  aggregation_method = var.ALERT_ERROR_RATE.aggregation_method
  aggregation_delay  = var.ALERT_ERROR_RATE.aggregation_delay
  baseline_direction = var.ALERT_ERROR_RATE.baseline_direction
  slide_by           = var.ALERT_ERROR_RATE.slide_by

  nrql {
    query = replace(var.ALERT_ERROR_RATE.query, "__APP_NAME__", var.APPS[count.index])
  }

  critical {
    operator              = var.ALERT_ERROR_RATE.critical_operator
    threshold             = var.ALERT_ERROR_RATE.critical_threshold
    threshold_duration    = var.ALERT_ERROR_RATE.critical_threshold_duration
    threshold_occurrences = var.ALERT_ERROR_RATE.critical_threshold_occurrences
  }

  warning {
    operator              = var.ALERT_ERROR_RATE.warning_operator
    threshold             = var.ALERT_ERROR_RATE.warning_threshold
    threshold_duration    = var.ALERT_ERROR_RATE.warning_threshold_duration
    threshold_occurrences = var.ALERT_ERROR_RATE.warning_threshold_occurrences
  }
}
```

- Usa `newrelic_nrql_alert_condition` para crear condiciones de alerta observando los patrones de tráfico.
- En `o11y/main.tf`, agrega este fragmento de código después de `# TODO: Crear una condición de alerta observando el tráfico de las aplicaciones.`

```
resource "newrelic_nrql_alert_condition" "Traffic" {
  count              = length(var.APPS)
  policy_id          = newrelic_alert_policy.alert_policies[count.index].id
  name               = "${var.APPS[count.index]}-traffic-baseline (TF)"
  account_id         = var.NEW_RELIC_ACCOUNT_ID
  type               = var.ALERT_TRAFFIC.type
  description        = var.ALERT_TRAFFIC.description
  enabled            = var.ALERT_TRAFFIC.enabled
  aggregation_method = var.ALERT_TRAFFIC.aggregation_method
  aggregation_delay  = var.ALERT_TRAFFIC.aggregation_delay
  baseline_direction = var.ALERT_TRAFFIC.baseline_direction
  slide_by           = var.ALERT_TRAFFIC.slide_by

  nrql {
    query = replace(var.ALERT_TRAFFIC.query, "__APP_NAME__", var.APPS[count.index])
  }

  critical {
    operator              = var.ALERT_TRAFFIC.critical_operator
    threshold             = var.ALERT_TRAFFIC.critical_threshold
    threshold_duration    = var.ALERT_TRAFFIC.critical_threshold_duration
    threshold_occurrences = var.ALERT_TRAFFIC.critical_threshold_occurrences
  }

  warning {
    operator              = var.ALERT_TRAFFIC.warning_operator
    threshold             = var.ALERT_TRAFFIC.warning_threshold
    threshold_duration    = var.ALERT_TRAFFIC.warning_threshold_duration
    threshold_occurrences = var.ALERT_TRAFFIC.warning_threshold_occurrences
  }
}
```

- Usa `newrelic_nrql_alert_condition` para crear condiciones de alerta que observen la saturación.
3. En `o11y/main.tf` agrega este fragmento de código después de `# TODO: Crear una condición de alerta que observe la saturación de las aplicaciones.`

```
resource "newrelic_nrql_alert_condition" "Saturation" {
  count              = length(var.APPS)
  policy_id          = newrelic_alert_policy.alert_policies[count.index].id
  name               = "${var.APPS[count.index]}-saturation-baseline (TF)"
  account_id         = var.NEW_RELIC_ACCOUNT_ID
  type               = var.ALERT_SATURATION.type
  description        = var.ALERT_SATURATION.description
  enabled            = var.ALERT_SATURATION.enabled
  aggregation_method = var.ALERT_SATURATION.aggregation_method
  aggregation_delay  = var.ALERT_SATURATION.aggregation_delay
  baseline_direction = var.ALERT_SATURATION.baseline_direction
  slide_by           = var.ALERT_SATURATION.slide_by

  nrql {
    query = replace(var.ALERT_SATURATION.query, "__APP_NAME__", var.APPS[count.index])
  }

  critical {
    operator              = var.ALERT_SATURATION.critical_operator
    threshold             = var.ALERT_SATURATION.critical_threshold
    threshold_duration    = var.ALERT_SATURATION.critical_threshold_duration
    threshold_occurrences = var.ALERT_SATURATION.critical_threshold_occurrences
  }

  warning {
    operator              = var.ALERT_SATURATION.warning_operator
    threshold             = var.ALERT_SATURATION.warning_threshold
    threshold_duration    = var.ALERT_SATURATION.warning_threshold_duration
    threshold_occurrences = var.ALERT_SATURATION.warning_threshold_occurrences
  }
}
```

- Remember to save the file.

🧪 Paso 2: Configurar Workflows
=======================

- Utilice `newrelic_workflow` para crear un nuevo flujo de trabajo
- En `o11y/main.tf` agregue este fragmento de código después de `# TODO: Crear un flujo de trabajo para cada aplicación`

```
resource "newrelic_workflow" "Workflow" {
  for_each           = toset(var.APPS)
  name                  = "Workflow ${each.key} (TF)"
  account_id            = var.NEW_RELIC_ACCOUNT_ID
  muting_rules_handling = "NOTIFY_ALL_ISSUES"

  issues_filter {
    name = "Filter-name"
    type = "FILTER"
    predicate {
      attribute = "accumulations.policyName"
      operator  = "CONTAINS"
      values    = ["O11yAsCode-${each.key}"]
    }
  }
  destination {
    channel_id = newrelic_notification_channel.alert_notification_email.id
  }
}
```

- Remember to save the file.

🧪 Paso 2: Crear Notificaciones
=======================

- Utilice newrelic_notification_destination para crear un destino de notificación
- En `o11y/main.tf`, agregue este fragmento de código después de `# TODO: Crear un destino de notificación por correo electrónico utilizando la variable de correo electrónico`

```
resource "newrelic_notification_destination" "alert_email_destination" {
  name = "email"
  type = "EMAIL"

  property {
    key   = "email"
    value = var.ALERT_NOTIFICATION_EMAIL
  }
}
```

- Usa `newrelic_notification_channel` para crear un canal de notificación
- En `o11y/main.tf`, agrega este fragmento de código después de `# TODO: Crear una destino de notificación de correo electrónico utilizando la variable de correo electrónico.`

```
resource "newrelic_notification_channel" "alert_notification_email" {
  account_id     = var.NEW_RELIC_ACCOUNT_ID
  name           = "email"
  type           = "EMAIL"
  destination_id = newrelic_notification_destination.alert_email_destination.id
  product        = "IINT"

  property {
    key   = "subject"
    value = "name: {{ alert_notification_email }}"
  }
}
```

- Recuerde guardar el archivo.

🏁 Paso 3: Finalizar
=======================


- Utilizando la pestaña Terminal, previsualice los cambios utilizando el siguiente comando:

```
terraform plan
```

- Una vez satisfecho con los cambios, ejecute el siguiente comando para aplicar los cambios.

```
terraform apply
```

- Para completar el desafío, presione **Check**
