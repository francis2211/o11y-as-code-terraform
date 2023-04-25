---
slug: terraform-workflow
id: 99fhykcobr5j
type: challenge
title: Terraform workflow
teaser: Revisar los comandos de Terraform
notes:
- type: text
  contents: |-
    # Terraform Workflow

    En este desafío, se te pide que
    - Agregues tus credenciales de New Relic a o11y/terraform.tfvars
    - Inicialices Terraform usando terraform init
    - Valides tu configuración de Terraform usando terraform validate
    - Previsualices tus cambios usando terraform plan
    - Aplices tus cambios usando terraform apply
tabs:
- title: Editor
  type: code
  hostname: docker-vm
  path: /newrelic/o11y
- title: Terminal
  type: terminal
  hostname: docker-vm
  workdir: /newrelic
difficulty: basic
timelimit: 600
---
🧪 Paso 1: Preparando tu archivo o11y/terraform.tfvars de Terraform
=======================

- Usando la pestaña del Editor, navega a o11y/terraform.tfvars y coloca tus secretos.
- Nota: NEW_RELIC_API_KEY es diferente de NEW_RELIC_LICENSE_KEY
- Nota: NEW_RELIC_API_KEY debe comenzar con NRAK-
- Actualiza ALERT_NOTIFICATION_EMAIL para que apunte a tu dirección de correo electrónico.

🧪 Step 2: terraform init
=======================

- En la pestaña del Terminal, cambia el directorio a o11y y luego ejecuta el siguiente comando:

```
terraform init
```

🧪 Step 3: terraform validate
=======================

- En la pestaña del Editor, abre o11y/main.tf
- En `o11y/main.tf` agrega este fragmento de código después de `# TODO: Output the names of the apps we are going to monitor`

```
output "o11y-as-code-apps" {
  value = toset(var.APPS)
}
```

- Recuerda guardar el archivo.
- Usando la pestaña del Terminal, cambia el directorio a `o11y` y valida los cambios ejecutando el siguiente comando:

```
terraform validate
```

🧪 Step 3: terraform plan
=======================

- Usando la pestaña del Terminal, previsualiza los cambios ejecutando el siguiente comando:

```
terraform plan
```

🏁 Step 4: terraform apply
=======================

- Una vez que estés satisfecho con los cambios, ejecuta el siguiente comando para aplicar los cambios.

```
terraform apply
```

- Para completar el desafío, presiona **Check**
