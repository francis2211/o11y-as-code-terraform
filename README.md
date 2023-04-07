[![New Relic Experimental header](https://github.com/newrelic/opensource-website/raw/master/src/images/categories/Experimental.png)](https://opensource.newrelic.com/oss-category/#new-relic-experimental)

Taller: Observabilidad como código con Terraform
================================================

Esta aplicación demuestra cómo incorporar Terraform y New Relic juntos utilizando Observabilidad como código.

Configurar Terraform y gestionar tus secretos
---------------------------------------------

### Configurar cuentas

-   [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
-   [New Relic](https://newrelic.com/signup)

#### Confirmar la instalación de Terraform

bashCopy code

`which terraform`

#### Instalar Terraform

bashCopy code

`brew tap hashicorp/tap
brew install hashicorp/tap/terraform`

#### Obtener credenciales

-   <https://one.newrelic.com/launcher/api-keys-ui.api-keys-launcher>

#### Clonar el repositorio y ejecutar la aplicación

goCopy code

`git clone
make
make up`

#### Configurar tus secretos

bashCopy code

`make source`

### Ejecutar Terraform

bashCopy code

`cd o11y
terraform apply
terraform down`

LICENCIA
--------

Esto está licenciado con la licencia Apache 2.0 [licencia](https://chat.openai.com/LICENSE).
