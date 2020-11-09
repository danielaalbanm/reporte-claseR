# reporte-claseR---
title: "Mi primer reporte en R"
author: "Daniela Albán"
date: "6/11/2020"
output: html_document
---

# Este es un título

## Este es un subtitulo

### Mientras más numerales el tamaño de letra es mas  pequeño

Observación: Debe existir un espacio entre el signo # y el texto

Aquí puedo redactar el cuerpo del reporte, o del documento que quiero hacer 


Se elabora el presente informe de fin de gestión, de conformodidad con la normativa en el _Instituto Nacional de Estadística y Censos_, las Directrices emitidas de la *Controlaría General*


_Este es un texto cursiva_

*Tambien es Cursiva=Itálica*


**Este texto es Negrita**


_ Si ponemos espacio, lee como texto _

Las listas se escriben de la siguiente manera:
- Item 1
- Item 2

  + Item 1
  + Item 2
  
Listas enumeradas

1. Item 1
2. Item 2

imagen: ![](https://www.cronista.com/__export/1581291594418/sites/diarioelcronista/img/2020/02/09/dolar_kathy_crop1578583045001_crop1580331066305_crop1581291593852.jpg_258117318.jpg)



Hipervinculo:[Daniela]( https://www.instagram.com/daniela_alban/ )

Para introducir ecuaciones se pone el signo de dolar

$x_1 = x_2^3 - x_2^{t+1}$

$ingreso = \beta_1 \; salario + \beta_2\; edad$

- $x_1$
- $x_2$



editor de latex en linea: pagina en donde estan todos los comandos (https://latex.codecogs.com/eqneditor/editor.php)

(https://www.codecogs.com/latex/eqneditor.php?lang=es-es)

se pone en insrt: codigo r
```{r}
#  echo=F sirve para no ver el codigo 
# Todo lo que escriba en esta área es código de R
a=c(1:5, 10:20)
media =mean(a)

```
La edad promedio de las personas que cumplen los requisitos para ser aprobados en un préstamo es 
`r media`




