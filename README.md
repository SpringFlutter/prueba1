# Prueba 1

Extraccion de los datos

## Tabla de contenido

- [Prueba 1](#project-title)
  - [Tabla de contenido](#tabla-de-contenido)
  - [Requerimientos](#requerimientos)
  - [Fuente de datos](#fuente-de-datos)
  - [Codigo](#codigo)
  - [Uso](#uso)
  - [License](#license)
  - [Acknowledgments](#acknowledgments)

### Requerimientos

Las librerias necesarias se encuentran en el archivo requirements.txt. Ademas, se necesita tener una cuenta creada en mongo atlas con una base de datos para establecer la conexion.

### Fuente de datos
La fuente de datos a utilizar sera la proporcionada por API Gob.Ec, la cual contiene datos que se generan en las instituciones públicas del ecuador.
Para mayor informacion y sus metodos de uso visitar en el siguiente enlace: https://www.gob.ec/api

## Codigo

Parte 1 : en este bloque de codigo realizamos un solicitud GET para obtener los datos de las instituciones finacieras
```python
    url = 'https://www.gob.ec/api/v1/instituciones'
    headers = {'User-agent': 'Chrome/58.0.3029.110'}

    # Realizar una solicitud GET
    response = requests.get(url=url, headers=headers)

    # Verificar si la solicitud fue exitosa (código de respuesta 200)
    if response.status_code == 200:
        # Convertir la respuesta a formato JSON
        data = response.json()

        primer_resultado = data[0]

        for resultado in data:
            # Iterar a través de las claves (campos) en el objeto
            for campo, valor in primer_resultado.items():
                # Imprimir el nombre del campo y su valor
                print(f"{campo}: {valor}")

    else:
        print(f'Error al hacer la solicitud. Código de respuesta: {response.status_code}')
```
Resultado 1: imprime en json un arreglo de datos de las instituciones. Por ejemplo, este es el resultado del primer elemento que corresponde a la Institucion ACESS.
```json
{
    "institucion_id": "131",
    "institucion": "Agencia de Aseguramiento de la Calidad de los Servicios de Salud y Medicina Prepagada",
    "siglas": "ACESS",
    "logo": "https://www.gob.ec//sites/default/files/2020-01/logo%20acess-08.jpg",
    "url": "https://www.gob.ec/acess",
    "website": "http://www.acess.gob.ec/",
    "tipo": "Ejecutiva",
    "descripcion": "Vigilar y controlar la calidad de los servicios que brindan los prestadores de salud y las compañías que financien servicios de atención integral en salud prepagada y de las de seguros que oferten cobertura de seguros de asistencia médica, velando por la seguridad de los pacientes y usuarios a través de la regulación y aseguramiento de la calidad y bajo los enfoques de derechos de género, interculturalidad, generacional y bioético.",
    "sector": "Social",
    "modificado": "2022-09-15T08:41:06-0500",
    "publicado": "Si"
}
```
Parte 2: en este bloque almacenamos los datos obtenidos en una base datos mongodb en la nube
```python
    # Cadena de conexion a la base de datos en la nube
    connection_string = "mongodb+srv://projectspring85:prueba123@cluster0.xqrsb1a.mongodb.net/?retryWrites=true&w=majority"

    # Se abre una conexion a la base de datos dbDatos en la coleccion docInstitucion
    client = pymongo.MongoClient(connection_string)
    db = client["dbDatos"]
    collection = db["docInstitucion"]

    # Se insertan los datos
    result = collection.insert_many(data)

    # Se imprime los ID de documentos insertados
    print("Documentos insertados IDs:", result.inserted_ids)

    # Se cierra la conexion
    client.close()
```
Resultado 2: Imprime los ids de los documentos insertados en la base. Por ejemplo:
```json
Documentos insertados IDs: [ObjectId('65174839920f46e0b537e27d'), ObjectId('65174839920f46e0b537e27e'), ... , ObjectId('65174839920f46e0b537e27f')]
```
## Uso
Instalar las librerias necesarias
```python
pip install -r requirements.txt
```
Correr el codigo

```python
python3 prueba.py
```
Ademas se puede ver el ejercicio completo con resultados en el archivo prueba.ipynb
