# 🧠 Formulario con Node.js y MySQL – Clase Práctica

### 📚 CECyTE 47 – Grupo Segundo A  
**Alumno:** Jorge Villanueva López

---

## 📋 Objetivo de esta práctica

Crear un formulario web con HTML que envíe datos a un servidor hecho en Node.js, el cual guardará los datos en una base de datos MySQL.

---

## 🔧 Requisitos previos

Antes de comenzar, necesitas tener instalado:

- [Node.js](https://nodejs.org/)
- [MySQL](https://www.mysql.com/)
- Un editor de código como [Visual Studio Code](https://code.visualstudio.com/)
- Conocimientos básicos de JavaScript, SQL, HTML Y CSS

---

## 🛠️ Tecnologías usadas

- Node.js (JavaScript del lado del servidor)
- Express.js (framework para el servidor)
- MySQL (base de datos relacional)
- HTML (para el formulario / CSS estilos)

---

## 📦 Instalación y configuración

1. **Clona o descarga el proyecto**

```bash
git clone https://github.com/tuusuario/tu-proyecto.git
cd tu-proyecto
```

2. **Instala las dependencias**

```bash
npm install
```

3. **Crea la base de datos en MySQL**

```sql
CREATE DATABASE formulario_db;

USE formulario_db;

CREATE TABLE usuarios (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100),
  correo VARCHAR(100)
);
```

4. **Configura la conexión a la base de datos**

En el archivo `db.js`:

```javascript
const mysql = require('mysql');
const connection = mysql.createConnection({
  host: 'localhost',
  user: 'tu_usuario',
  password: 'tu_contraseña',
  database: 'formulario_db'
});

module.exports = connection;
```

---

## 📄 Estructura del proyecto

```
/
├── views/            # HTML del formulario
│   └── index.html
├── db.js             # Conexión a MySQL
├── app.js            # Código principal de Express
├── package.json      # Lista de dependencias
└── README.md         # Este documento
```

---

## 🧪 ¿Cómo funciona?

1. El usuario llena el formulario y presiona “Enviar”.
2. El navegador envía los datos al servidor mediante POST.
3. Node.js recibe los datos y los guarda en la base de datos.
4. El servidor responde confirmando que todo fue correcto.

---

## 🧾 Código importante

**Formulario HTML (`views/index.html`):**

```html
<form action="/guardar" method="POST">
  <input type="text" name="nombre" placeholder="Nombre" required>
  <input type="email" name="correo" placeholder="Correo" required>
  <button type="submit">Enviar</button>
</form>
```

**Servidor en Node.js (`app.js`):**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const db = require('./db');

const app = express();
app.use(bodyParser.urlencoded({ extended: true }));

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/views/index.html');
});

app.post('/guardar', (req, res) => {
  const { nombre, correo } = req.body;
  db.query('INSERT INTO usuarios (nombre, correo) VALUES (?, ?)', [nombre, correo], (err) => {
    if (err) throw err;
    res.send('Datos guardados correctamente');
  });
});

app.listen(3000, () => {
  console.log('Servidor corriendo en http://localhost:3000');
});
```

---

## 🤓 Consejos para mis compañeros

- Asegúrate de que tu servidor MySQL esté funcionando.
- Usa `console.log()` para depurar si algo no funciona.
- Lee bien los errores: suelen indicar qué parte del código falló.

---

## 🎓 ¿Qué vas a aprender?

- Cómo enviar datos desde un formulario HTML a un backend.
- Cómo Node.js puede recibir y procesar esos datos.
- Cómo guardar información en una base de datos MySQL desde JavaScript.

---

## 👨‍🏫 Autor

**Jorge Villanueva López**  
Grupo Segundo A  
Escuela: CECyTE 47  
GitHub: [Lopz532](https://github.com/Lopz532)

---