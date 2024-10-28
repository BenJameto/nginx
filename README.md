# Despliegue de NGINX

1. Para el despliegue primero clona el repositorio con el siguiente comando:

```
git clone BenJameto/nginx
```

2. Accede a la interfaz de Jenkins

3. Selecciona nueva tarea (New Job)

4. Pale un nombre que haga referencia a lo que estas por hacer **Ejemplo:** *Deploy-test-nginx* y selecciona **pipeline**

5. En la seccion **pipeline** > **Definition** selecciona *Pipeline Script*

6. Copia el siguiente pipeline y guarda los cambios.

7. Dale click a **Construir ahora**

```
pipeline {
    agent any

    stages {
        stage('Clonar el repositorio') {
            steps {
                // Clonar el repositorio desde GitHub para obtener el archivo nginx-deployment.yaml
                git url: 'https://github.com/BenJameto/nginx.git', branch: 'main'
            }
        }

        stage('Desplegar en Kubernetes') {
            steps {
                script {
                    // Aplicar el archivo nginx-deployment.yaml en Kubernetes
                    sh 'kubectl apply -f nginx-deployment.yaml'
                }
            }
        }
    }

    post {
        success {
            echo 'Despliegue completado exitosamente.'
        }
        failure {
            echo 'El despliegue ha fallado.'
        }
    }
}
```
8. Copia la url de jenkins y cambiala por 192.168.x.x:30007, veras welcome to nginx