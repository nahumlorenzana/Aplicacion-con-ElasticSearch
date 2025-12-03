# Aplicación-con-ElasticSearch
Después de la importación a Elasticsearch es momento de hacer una pequeña aplicación para comprobar que todo funcione
[AplicacionWeb.zip](https://github.com/user-attachments/files/23912004/AplicacionWeb.zip)
# Sentencias CRUD

## Create (Insertar documentos)

**1.Crear un documento con ID específico**

Descripción: Crea un documento nuevo en el índice productos con ID = 1.

PUT/productos/_doc/1
```json
{
  "nombre": "Café Latte",
  "precio": 50
}
```
**2.Crea un documento sin especificar ID**

Descripción: Elasticsearch genera automáticamente un ID.

POST/productos/_doc

```json
{
  "nombre": "Té Verde",
  "precio": 40
}
```
**3.Crea un indice nuevo**

Descripción: Crea un índice vacío llamado clientes.
```json

PUT /clientes

```
**4.Crear documento y actualizar si ya existe (upsert)**

Descripción: Si el documento existe, lo actualiza; si no, lo crea.

POST /inventario/_update/10
```json
{
  "doc": { "stock": 20 },
  "doc_as_upsert": true
}
```
**5.Crear varios documentos al mismo tiempo (bulk)**

Descripción: Inserta varios documentos en una sola operación.

POST /productos/_bulk
```json
{"index":{}}
{"nombre":"Café Americano","precio":35}
{"index":{}}
{"nombre":"Capuchino","precio":45}
```
## READ – Consultar documentos

**1.Leer un documento por ID**

Devuelve el documento con ID = 1.
```json
GET /productos/_doc/1
```
**2. Mostrar todos los documentos**

Descripción: Retorna todos los documentos del índice productos.

```json
GET /productos/_search
```
**3.Busqueda por coincidencia**

Descripción: Busca documentos que contengan la palabra café.

GET /productos/_search

```json
{
  "query": {
    "match": { "nombre": "café" }
  }
}
```
**4.Filtrar por rango**

Descripción: Muestra productos con precio mayor o igual a 40.

GET /productos/_search
```json
{
  "query": {
    "range": {
      "precio": { "gte": 40 }
    }
  }
}
```
**5.Obtener los primeros 5 resultados**

Descripción: Limita la consulta a solo 5 documentos
```json
GET /productos/_search?size=5
```
# UPDATE – Actualizar documentos

**1. Actualizar un campo específico**

Descripción: Cambia solo el campo precio del documento 1.

POST /productos/_update/1
```json
{
  "doc": { "precio": 55 }
}
```
**2. Actualizar varios campos**

Descripción: Modifica varios campos a la vez.

POST /productos/_update/1
```json
{
  "doc": {
    "nombre": "Café Latte Grande",
    "precio": 60
  }
}
```
**3. Incrementar un valor numérico**

Descripción: Suma 5 al precio actual.

POST /productos/_update/1
```json
{
  "script": "ctx._source.precio += 5"
}
```
**4. Añadir un campo nuevo**

Descripción: Agrega un nuevo campo categoria

POST /productos/_update/1
```json
{
  "doc": { "categoria": "Bebidas" }
}
```
**5. Reemplazar un documento completo**

Descripción: Sustituye todo el documento por uno nuevo

PUT /productos/_doc/1
```json
{
  "nombre": "Café Mocha",
  "precio": 70
}
```
# DELETE – Eliminar documentos

**1. Eliminar un documento por ID**

Descripción: Borra el documento con ID = 1.
```json
DELETE /productos/_doc/1
```
**2.Eliminar un indice completo**

Descripción: Elimina el índice productos y todo su contenido.
```json
DELETE /productos
```

**3.Eliminar documentos por consulta**

Descripción: Borra todos los documentos que contengan café.

POST /productos/_delete_by_query
```json
{
  "query": {
    "match": { "nombre": "café" }
  }
}
```
**4.Eliminar documentos con precio bajo**

Descripción: Elimina los que tengan precio menor a 40.

POST /productos/_delete_by_query
```json
{
  "query": {
    "range": {
      "precio": { "lt": 40 }
    }
  }
}
```

**5. Eliminar usando Bulk**

Descripción: Borra varios documentos en una sola operación.

POST /productos/_bulk
```json
{"delete":{"_id":2}}
{"delete":{"_id":3}}
```
# Operaciones realizadas

## Create

**Las sentencias Create realizadas en la aplicación Web fueron:**

1. **Crear documento con ID específico**
2. **Crear varios documentos al mismo tiempo**

## Read

**Las sentencias Read realizadas fueron:**
1. **Leer un documento por ID**
2. **Mostrar todos los documentos**
3. **Búsqueda por coincidencia**
4. **Filtrar por rango**

# Update

**Las sentencias Update realizadas fueron:**

1. **Actualizar un campo específico**
2. **Incrementar un valor númerico**
3. **Añadir un campo nuevo**
4. **Reemplazar un documento completo**

# Delete

**Las sentencias Delete realizadas fueron**

1. **Eliminar un documento por ID**
2. **Elimiar documentos por rango**

# Lenguaje y herramientas utilizadas

Para poder realizar esta aplicación Web se utilizo como principal herramienta el VS Code para comodidad, obviamente utilizando distintas extensiones.

**VS Code:** Utilizado para comodidad y poder tener ambos códigos en un solo lugar.  
**Python:** El lenguaje utilizado para poder correr nuestro código, en este se realizaron todas las sentencias y lo escogimos gracias a su facilidad para trabajar.  
**HTML:** Utilizado para la creación de la pagina Web donde un usuario puede interactuar con el dataset.  
**PostMan:** Utilizado para ver los datos del dataset.  
