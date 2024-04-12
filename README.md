# en_un_lugar_de_la_mancha


El link a este repositorio es: [github](https://github.com/GonzaloGmv/en_un_lugar_de_la_mancha)

Los colaboradores somos:
* Alexandre Muñoz
* Gonzalo Martínez
* Miguel González

# Resolución del problema

Para resolver el problema hemos usado un cifrado Book cipher, pero hemos que tenido que modificar las posiciones que nos habian dado ya que las que teniamos correspondian con las páginas del libro original y en el pdf hay páginas en blanco, fotos y además encabezados que hay que tener en cuenta.

# Código
```
import PyPDF2

def cargar_pdf(ruta_pdf):
    with open(ruta_pdf, 'rb') as file:
        pdf_reader = PyPDF2.PdfReader(file)
        texto_pdf = ''
        num_paginas = len(pdf_reader.pages)
        
        for pagina_num in range(num_paginas):
            texto_pagina = pdf_reader.pages[pagina_num].extract_text()
            texto_pdf += texto_pagina
            
    return texto_pdf

def descifrar_pdf(ruta_pdf, coordenadas):
    with open(ruta_pdf, 'rb') as file:
        pdf_reader = PyPDF2.PdfReader(file)
        palabras_descifradas = []  # Lista para almacenar las palabras descifradas
        
        for coord in coordenadas:
            pagina_num, indice_linea, indice_palabra = map(int, coord.split(':'))
            texto_pagina = pdf_reader.pages[pagina_num - 1].extract_text()
            lineas = texto_pagina.split('\n')
            try:
                palabra = lineas[indice_linea - 1].split()[indice_palabra - 1]
                palabras_descifradas.append(palabra)
            except IndexError:
                pass
        
    return '_'.join(palabras_descifradas)

# Ruta del PDF
ruta_pdf = 'quijote.pdf'

# Coordenadas de desencriptación
coordenadas = [
    '18:9:2',
    '33:14:1',
    '40:9:2',
    '40:27:7',
    '45:2:7',
    '163:20:10',
    '163:12:8',
    '164:12:5'
]

# Descifrar el PDF utilizando las coordenadas
texto_descifrado = descifrar_pdf(ruta_pdf, coordenadas)

# Imprimir el texto descifrado con las palabras separadas por guion bajo
print('flag{'+texto_descifrado+'}')


```
![flag](https://github.com/GonzaloGmv/en_un_lugar_de_la_mancha/assets/91721507/06d0b9ba-98a1-4663-9582-564f6bc093a0)
