---
slug: terraform-workflow
id: 
type: challenge
title: Terraform workflow
teaser: Review terraform commands
notes:
- type: text
  contents: |-
    # Terraform Workflow

    En este desafío, se le asigna la tarea de:
    -   Agregar sus credenciales de New Relic a `o11y/terraform.tfvars`
    -   Inicializar Terraform utilizando `terraform init`
    -   Validar su configuración de Terraform utilizando `terraform validate`
    -   Previsualizar sus cambios utilizando `terraform plan`
    -   Aplicar sus cambios utilizando `terraform apply`
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
🧪 Paso 1: Preparar el archivo `o11y/terraform.tfvars` de Terraform
===================================================================

-   Usando la pestaña Editor, navegue a `o11y/terraform.tfvars` y agregue sus secretos.

-   Nota: `NEW_RELIC_API_KEY` es diferente de `NEW_RELIC_LICENSE_KEY`

-   Nota: `NEW_RELIC_API_KEY` debe comenzar con `NRAK-`

-   Actualice `ALERT_NOTIFICATION_EMAIL` para que apunte a su dirección de correo electrónico.

🧪 Paso 2: terraform init
=========================

-   En la pestaña Terminal, cambie el directorio a `o11y` y ejecute el siguiente comando:

    ```
    terraform init
    ```
🧪 Paso 3: terraform validate
=============================

-   En la pestaña Editor, abra `o11y/main.tf`
-   En `o11y/main.tf`, agregue este fragmento de código después de `# TODO: Output the names of the apps we are going to monitor`
    ```
    output "o11y-as-code-apps" {
        value = toset(var.APPS)
    }`
    ```
-   Recuerde guardar el archivo.

-   Usando la pestaña Terminal, cambie el directorio a `o11y` y valide los cambios ejecutando el siguiente comando:
    ```
    terraform validate
    ```
    
🧪 Paso 4: terraform plan
=========================

-   Usando la pestaña Terminal, obtenga una vista previa de los cambios utilizando el siguiente comando:

    ```
    terraform plan
    ```

🏁 Paso 5: terraform apply
==========================

-   Una vez que esté satisfecho con los cambios, ejecute el siguiente comando para aplicarlos.

    ```
    terraform apply
    ```

-   Para completar el desafío, presione Check
