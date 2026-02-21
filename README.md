# cicd_tf_ejercicio1
Ejercicio1
Crear un pipeline, utilizando GitHub Actions que me permita desplegar recursos mediante comandos de Terraform dentro del cloud provider Azure.

Recursos:

resource group
virtual networks
storage accounts
.

Solución:

Crear un repositorio en GitHub con el nombre "cicd_tf_ejercicio1" y descargarlo en la maquina local, ejecutando el siguiente comando:
git clone https://github.com/VillaviH/cicd_tf_ejercicio1.git
Debemos conectar GitHub con Azure Cloud para el Pipeline pueda crear nuestra infraestructura, para lo cual debemos ejecutar los siguientes comandos de azure, teniendo en cuenta que el resultado es un yaml y debemos pasarlo como variables de entorno en GitHub.
az account show --query id
az ad sp create-for-rbac --name "github-actions-terraform" --role contributor --scopes /subscriptions/YOUR_SUBSCRIPTION_ID --sdk-auth
En el repositorio de GitHub debemos crear un "repositorio de secretos" llamado "AZURE_CREDENTIALS" con los datos yaml que se obtuvieron del paso anterior, para esto ir a Settings->New repository secret
Una vez realizado los pasos anteriores, debemos descargar los siguientes archivos a la carpeta creada anteriormente.
Con la carpeta y archivos listos debemos enviar un cambio en el repositorio, podríamos modificar el archivo README y ejecutar los siguientes comandos para actualizar el repositorio.
git add .
git commit -m "Add Terraform infrastructure and CI/CD pipeline 1"
git push origin main
Con esta actualización se ejecuta el Pipeline llamado "Terraform Azure Infrastructure" y luego de un momento debemos revisar el portal de azure y veremos algo así:
.

Al final debemos destruir todo los recursos creados y así evitar se genere costos innecesarios, para esto debemos ejecutar el Pipeline llamado "Terraform Destroy Infrastructure", pero debemos ingresar en el label la palabra DESTROY.