# Prueba 1

Extraccion de los datos

## Tabla de contenido

- [Prueba 1](#project-title)
  - [Tabla de contenido](#tabla-de-contenido)
  - [Requerimientos](#requerimientos)
  - [Fuente de datos](#fuente-de-datos)
  - [Codigo](#codigo)
  - [Contributing](#contributing)
  - [License](#license)
  - [Acknowledgments](#acknowledgments)

### Requerimientos

List any prerequisites or dependencies that need to be installed before running the code.

### Fuente de datos

Provide step-by-step instructions on how to install and set up your project. Include any configuration files or environment variables that need to be set.

## Codigo
En este bloque de codigo realizamos un solicitud GET para obtener los datos de las instituciones finacieras
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
## Contributing

Explain how others can contribute to your project, such as guidelines for submitting pull requests and reporting issues. Include information on your preferred code style and any coding standards to follow.

## License

Specify the license under which your code is distributed. If you're unsure, you can include a link to the [Choose a License](https://choosealicense.com/) website to help users choose an appropriate license.

## Acknowledgments

Give credit to any individuals, libraries, or resources that were helpful or inspirational during the development of your project.

---

Feel free to customize this template to fit your specific project. Once you've created your README file, save it as `README.md` in your GitHub repository, and it will automatically be displayed on your repository's main page.
