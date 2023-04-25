---
slug: lab-synthetic-checks
id: peyqosomoipv
type: challenge
title: 'Lab: Synthetic Checks'
teaser: Creando monitores sintéticos
notes:
- type: text
  contents: |-
    # Crear Monitores Sintéticos

    En este desafío, se le solicita que:
    - Monitoree un conjunto de URLs en busca de certificados SSL no válidos
    - Monitoree un conjunto de URLs en busca de enlaces rotos
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
🧪  Paso 1: Verificar certificados SSL válidos
=======================

- Use `newrelic_synthetics_cert_check_monitor` para verificar certificados SSL inválidos.
- En `o11y/main.tf` agrega este fragmento de código después de `# TODO: Crear un monitor de sintéticos para verificar certificados SSL válidos`

```
resource "newrelic_synthetics_cert_check_monitor" "cert-check-monitor" {
  count                  = length(var.SYNTHETIC_CHECK_SSL_URLS)
  name                   = "cert-check-monitor-${var.SYNTHETIC_CHECK_SSL_URLS[count.index]}"
  domain                 = "${var.SYNTHETIC_CHECK_SSL_URLS[count.index]}"
  # Public minion location
  # https://docs.newrelic.com/docs/synthetics/synthetic-monitoring/administration/synthetic-public-minion-ips/#location
  locations_public       = ["AWS_SA_EAST_1", "AWS_US_EAST_1"]
  certificate_expiration = "10"
  period                 = "EVERY_6_HOURS"
  status                 = "ENABLED"

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
- Revisa la variable `TF_VAR_SYNTHETIC_CHECK_SSL` en `o11y/terraform.tfvars`

🧪 Paso 2: Verificar enlaces rotos
=======================

- Use `newrelic_synthetics_broken_links_monitor` para verificar enlaces rotos.
- En `o11y/main.tf` agrega este fragmento de código después de `# TODO: Crear un monitor de sintéticos para verificar enlaces rotos`

```
resource "newrelic_synthetics_broken_links_monitor" "monitor" {
  count                  = length(var.SYNTHETIC_CHECK_SSL_URLS)
  name                   = "broken-links-monitor-${var.SYNTHETIC_CHECK_SSL_URLS[count.index]}"

  uri              = "${var.SYNTHETIC_CHECK_SSL_URLS[count.index]}"
  # Public minion location
  # https://docs.newrelic.com/docs/synthetics/synthetic-monitoring/administration/synthetic-public-minion-ips/#location
  locations_public       = ["AWS_SA_EAST_1", "AWS_US_EAST_1"]
  period                 = "EVERY_6_HOURS"
  status                 = "ENABLED"
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
- Revisa la variable `TF_VAR_SYNTHETIC_CHECK_SSL` en `o11y/terraform.tfvars`

🏁 Paso 3: Finalizar
=======================



- Revisa los cambios que se realizarán usando el siguiente comando:

```
terraform plan
```

- Una vez que estés satisfecho con los cambios, ejecuta el siguiente comando para aplicar los cambios.

```
terraform apply
```

Para completar el desafío, presiona  **Check**
