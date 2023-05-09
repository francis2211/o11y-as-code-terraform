---
slug: getting-started
id: 
type: challenge
title: Empezando
teaser: Empezando con Terraform
notes:
- type: text
  contents: |-
    # Empezando con Observabilidad como Código

    En este desafío, se le encarga:
    - registrarse para obtener una cuenta gratuita de New Relic.
    - configurar sus aplicaciones con la NEW_RELIC_LICENSE_KEY.
    - iniciar sus aplicaciones para generar telemetría.
    - verificar los registros para asegurarse de que todo está funcionando.
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

🧪 Paso 1: Configurar las aplicaciones
======================================

-   En el directorio principal del espacio de trabajo, ejecute el comando `make`.

    ```
    `make`
    ```

-   Esto generará archivos `.env` para sus aplicaciones.

🧪 Paso 2: Agregar las claves de licencia de New Relic
======================================================

-   Usando la pestaña del Editor, actualice los archivos `apps/*/.env` para agregar su `NEW_RELIC_LICENSE_KEY` a cada aplicación.

    ```
    - apps/web-api/.env
    - apps/login-service/.env
    - apps/cloud-infra/.env`
    ```
Archivo .env:

makefileCopy code
    ```
    NEW_RELIC_LICENSE_KEY=AABBCC
    ```
Nota: `NRIA_LICENSE_KEY` toma el mismo valor que `NEW_RELIC_LICENSE_KEY`. (Ingest Key)

🏁 Paso 3: Finalizar
====================

-   Verifique que todo esté funcionando.

    ```
    make up
    ```

-   Vea los registros de las aplicaciones.
    ```
    make logs
    ```

-   En segundo plano, se están ejecutando pruebas de carga para simular la carga en sus aplicaciones. En unos minutos, estos datos aparecerán en la interfaz de usuario de New Relic.

Para completar el desafío, presione Comprobar.
