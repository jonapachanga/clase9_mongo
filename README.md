# CoderHouse Clase 8  - SQL


La base de datos y las colecciones estan subidas al Cloud de MongoDB

## String Connections

  Tiene permiso de lectura y escritura:
  `mongodb+srv://admin:XGIGcsR29l611Ge3@cluster0.w3kxf.mongodb.net/ecommerce`

  Tiene permiso de lectura:
  `mongodb+srv://pepe:asd456@cluster0.w3kxf.mongodb.net/ecommerce`



## Ejercicios

### 1-2) Inserto 10 registros en la coleccion de Mensajes y Productos
````
db.messages.insertMany([
  {
    "user": "jeseiza@gmail.com",
    "date": "31/01/2021 12:26:00 pm",
    "message": "Hola!"
  },
  {
    "user": "jeseiza@gmail.com",
    "message": "Hay alguien",
    "date": "12/02/2022 05:27:16 pm"
  },
  {
    "user": "flor@gmail.com",
    "message": "Hola si",
    "date": "12/02/2022 05:27:38 pm"
  },
  {
    "user": "flor@gmail.com",
    "message": "Ahi agregue auriculares",
    "date": "12/02/2022 05:30:12 pm"
  },
  {
    "user": "jeseiza@gmail.com",
    "message": "genial",
    "date": "12/02/2022 05:30:21 pm"
  },
  {
    "user": "flor@gmail.com",
    "message": "Elimine el logitech 915",
    "date": "13/02/2022 02:30:21 pm"
  },
  {
    "user": "jeseiza@gmail.com",
    "message": "bien",
    "date": "13/02/2022 02:35:21 pm"
   },
   {
    "user": "jeseiza@gmail.com",
    "message": "falta agregar los monitores que llegaron hoy",
    "date": "13/02/2022 04:35:21 pm"
  },
  {
    "user": "jeseiza@gmail.com",
    "message": "ya lo hago",
    "date": "13/02/2022 05:35:21 pm"
  },
  {
    "user": "jeseiza@gmail.com",
    "message": "Hasta mañana",
    "date": "13/02/2022 06:05:21 pm"
  }
])
````

````
db.products.insertMany([
    {
        "title": "IPhone 13",
        "price": 120,
        "thumbnail": "/cellphone21x21.png"
    },
    {
        "title": "Xiaomi Box",
        "price": 580,
        "thumbnail": "/xiaomi_box.png"
    },
    {
        "title": "Chromecast",
        "price": 900,
        "thumbnail": "/chromecast.png"
    },
    {
        "title": "Laptop",
        "price": 1280,
        "thumbnail": "/laptop.png"
    },
    {
        "title": "Monitor",
        "price": 2300,
        "thumbnail": "/monitor.png"
    },
    {
        "title": "Auriculares",
        "price": 2860,
        "thumbnail": "/auriculares.png"
    },
    {
        "title": "Termo Coleman",
        "price": 3350,
        "thumbnail": "/coleman21x21.png"
    },
    {
        "title": "Vaso Termico Wagner 480ml",
        "price": 4320,
        "thumbnail": "/wagner.png"
    },
    {
        "title": "monitor",
        "price": 4990,
        "thumbnail": "monitor21x22"
    },
    {
        "title": "Teclado mecanico Logitech",
        "price": 385,
        "thumbnail": "/logi915.png"
    }
])
````

### 3) Listo todos los documentos de Mensajes y Productos

````
db.messages.find()

db.products.find()
````

### 4) Cuento la cantidad de documentos en la coleccion de Mensajes

````
db.messages.count()

db.products.count()
````

### 5) CRUD sobre la coleccion de productos:

#### A. Insertar un producto a la collecion

````
db.products.insertOne({
    "title": "Xiaomi Redmi Note 10",
    "price": 5800,
    "thumbnail": "/redmi10.png"
})
````

#### B. Realizar una consulta por nombre de producto especifico:

#### I. Listar todos los productos con precio menor a 1000

````
db.products.find({price: {$lt: 1000}})
````

#### II. Listar todos los productos con precio entre a 1000 a 3000 pesos

````
db.products.find({
    $and: [
        {price: {$gt: 1000}},
        {price: {$lt: 3000}},
    ]
})
````

#### III. Listar todos los productos con precio mayor 3000 pesos

````
db.products.find({price: {$gt: 3000}})
````

#### IV. Consulta que solo trae el nombre del tercer producto mas barato.

````
db.products.find({},{title:1, _id:0}).sort({price:1}).skip(2).limit(1)
````

### C. Agregar el campo stock con el valor inicial 100 a todos los productos.

````
db.products.update({},{$set : {stock: 100}},{upsert: false, multi: true})
````

### D. Cambia el stock a cero de los productos con precios mayores a 4000

````
db.products.updateMany(
    { price: { $gt: 4000 } },
    { $set: { stock: 0 } }
)
````

### E. Borra los productos com precio menor a 1000

````  
db.products.deleteMany({price:{$lt: 1000}})
````

### 6) Crea el usuario 'pepe' clave:'asd456' que solo pueda leer la base de datos ecommerce

Este no es necesario correrlo ya que el usuario esta creado y solo tiene permiso de lectura para esa db en concreto

````
db.createUser({
    user: "pepe",
    pwd: "asd456",
    roles: [
      { role: "read", db: "ecommerce" }
    ]
})
````