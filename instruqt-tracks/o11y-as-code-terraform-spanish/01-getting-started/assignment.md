---
slug: getting-started
id: jrfv24uxeyzj
type: challenge
title: Getting Started
teaser: Comenzando con Terraform
notes:
- type: text
  contents: |-
    # Empezando con Observability as Code

    En este desafío, se te pide que
    - Te registres en una cuenta gratuita de New Relic
    - Configures tus aplicaciones con la clave de licencia de NEW_RELIC_LICENSE_KEY
    - Inicies tus aplicaciones para generar telemetría
    - Revises los registros para asegurarte de que todo está funcionando
tabs:
- title: Terminal
  type: terminal
  hostname: docker-vm
  workdir: /newrelic
- title: Editor
  type: code
  hostname: docker-vm
  path: /newrelic
difficulty: basic
timelimit: 600
---

🧪 Paso 1: Configura tus aplicaciones
=======================

- En el directorio de trabajo raíz, ejecuta el comando make.

```
make
```

- Se generarán archivos .env para tus aplicaciones.

🧪 SPaso 2: Agrega tus claves de licencia de New Relic
=======================

- Usa la pestaña del Editor para actualizar los archivos apps/*/.env y agregar tu clave de licencia de NEW_RELIC_LICENSE_KEY a cada aplicación.

```
- apps/web-api/.env
- apps/login-service/.env
- apps/cloud-infra/.env
```

Archivo .env:

```
NEW_RELIC_LICENSE_KEY=AABBCC
```

Nota: NRIA_LICENSE_KEY toma el mismo valor que NEW_RELIC_LICENSE_KEY


🏁 Paso 3: Termina
=========

- Verifica que todo está funcionando.

```
make up
```

- Visualiza los registros de las aplicaciones.

```
make logs
```

- Detrás de escena, se están ejecutando pruebas de humo para simular carga en tus aplicaciones. En unos minutos, estos datos aparecerán en la interfaz de usuario de New Relic.

Para completar el desafío, presiona Comprobar.
