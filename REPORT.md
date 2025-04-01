
# Desafio TechFlow

> **Objetivo**: Comprender paso a paso cómo implementar un pipeline de integración continua usando Git, Node.js, Jest y Jenkins para el proyecto TechFlow.

---

## 🌱 1. Estructura del Proyecto

Tu proyecto debe tener una estructura ordenada como esta:

```
desafio-techflow/
├── tests
   ├── app.test.js     # Pruebas unitarias con Jest
├── app.js             # Código principal de la aplicación
├── db.json            # Base de datos simulada 
├── .gitignore            # Gitignore
├── package.json       # Dependencias y scripts de Node.js
└── Jenkinsfile        # Define el pipeline de CI para Jenkins
```

---

## ⚙️ 2. Configuración del Proyecto Node.js

### `package.json`

Este archivo define las dependencias y scripts del proyecto. Asegúrate de incluir:

```json
{
  "name": "ci_pipeline_project",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "test": "jest --silent=false",
    "dev": "nodemon app.js",
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "nodemon": "^3.1.9"
  },
  "devDependencies": {
    "jest": "^29.4.1",
    "supertest": "^6.3.3"
  },
  "description": "Desafio del módulo 8 clase 8 del curso de DesafioLatam Backend JavaScript",
  "directories": {
    "test": "tests"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/NicoDizel/desafio-techflow.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/NicoDizel/desafio-techflow/issues"
  },
  "homepage": "https://github.com/NicoDizel/desafio-techflow#readme"
}
```

### Instalación

```bash
npm install
```

---

## 🧪 3. Código fuente y pruebas

### `app.js`

```js
// app.js - Endpoints de TechFlow. Devuelven los usuarios contenidos en el JSON.

app.get('/', (req, res) => {
    res.status(200).send("Welcome to the TechFlow API");
});

app.get('/users', (req, res) => {
    res.status(200).json(data.users);
});

app.get('/users/:id', (req, res) => {
    const user = data.users.find(u => u.id === parseInt(req.params.id, 10));
    if (user) {
        res.status(200).json(user);
    } else {
        res.status(404).json({ error: 'User not found' });
    }
});
```

### `app.test.js`

```js
// app.test.js - Pruebas unitarias con Jest para probar los endpoints de TechFlow


const request = require('supertest');
const app = require('../app.js');

describe('API Tests', () => {
  it('should return a 200 status code', async () => {
    const res = await request(app).get('/');
    expect(res.statusCode).toEqual(200);
  });

  it('should return a list of users', async () => {
    const res = await request(app).get('/users');
    expect(res.statusCode).toEqual(200);
    expect(res.body).toHaveLength(2);
  });

  it('should return a single user', async () => {
    const res = await request(app).get('/users/1');
    expect(res.statusCode).toEqual(200);
    expect(res.body.name).toEqual('Alice');
  });
});
```

---

## 🧪 4. Jenkinsfile

Este archivo define las etapas de integración continua.

```groovy
pipeline{
  agent any 

  stages{

    stage('Instalar dependencias'){
      steps{
        script {
          try {
            //Instalando dependencias
            echo 'Instalando dependencias...'
            sh 'npm install'
          }
          catch (Exception e) { 
            error('❌ Error en la etapa de instalación de dependencias.')
          }
        }
      }
    }

    stage('Pruebas'){
      steps{
        script {
          //Ejecutando pruebas
          echo 'Ejecutando pruebas...'
          sh 'npm test -- --coverage'
        }
      }
    }

    stage('Iniciando el servidor'){
      steps{
        script {
          try {
            //Iniciando servidor
            echo 'Iniciando el servidor...'
            sh 'npm run start'
          }
          catch (Exception e) { 
            error('❌ Error en la etapa de inicialización de servidor.')
          }
        }
      }
    }

  }
}
```

---

## 📁 5. Reporte de cobertura

Jest genera un reporte HTML. Esto lo puedes verificar en el output del terminal en Jenkins.
---

## 🧪 6. Jenkins: Configuración del Job

1. Crear un nuevo pipeline en Jenkins.
2. Fuente del repositorio: `https://github.com/NicoDizel/desafio-techflow.git/`
3. Jenkins buscará el `Jenkinsfile` y ejecutará las etapas automáticamente.

---

