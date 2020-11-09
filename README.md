---
title: "Reporte"
author: "Daniela Albán"
date: "7/11/2020"
output:   
  prettydoc::html_pretty:
    theme: cayman
    highlight: github
    toc: TRUE
   
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


.....

# Librerias que se utilizaron
```{r}
library(readxl)
library("dplyr")
library(ggplot2)
```

# Lectura de archivos xlsx

```{r}
base<- read_excel("C:/Users/danie/Documents/Clases R/Clase 8/Base de datos trabajo.xlsx",sheet = "BASE", col_names = TRUE, na=c(""))
```
# Analisís de las variables
## Transformación de variables tipo Character a factor
```{r}
str(base)
base$TIENE_CREDITO=as.factor(base$TIENE_CREDITO)
base$ESTADO_CIVIL=as.factor(base$ESTADO_CIVIL)
base$GENERO_C=as.factor(base$GENERO_C)
base$CALIFICACION=as.factor(base$CALIFICACION)
base$TIPO_VIVIENDA=as.factor(base$TIPO_VIVIENDA)
str(base)
```



## Creación de funciones 
- Se crea una función que nos permitira modificar por un valor arbitrario "a" los valores pérdidos  NA tanto a la base completa como a variables dadas (vectores). 

```{r}
reemplazar_na <- function(vector, a) {
  vector[is.na(vector)]<-a
}
```

- Para modificar el valor arbitrario inicial por un nuevo valor "b", se crea la siguiente función:
```{r}
reemplazar_a=function(vector, a, b){
  vector[i=a]<-b
}
```


# EJERCICIOS
Los siguientes resultados se obtuvieron utilizando la libreria dplyr 


- Número de individuos por cada provincia
```{r}
ind_prov<- base %>%group_by(PROVINCIA) %>%
           summarise(numero_individuos=length(PROVINCIA))

```

```{r, echo=FALSE}
knitr::kable(ind_prov)

```

- Número de hombres y mujeres por cada provincia
```{r}
ind_prov_gen<- base %>%group_by(PROVINCIA, GENERO_C) %>%
  summarise(numero_individuos=length(PROVINCIA))

```
```{r, echo=FALSE}
knitr::kable(ind_prov_gen)

```


- Utilizando el argumento "subset" se obtiene: El número máximo de hijos en las personas de 35 a 45 años que si tienen crédito es 
```{r}
h<- subset(base,TIENE_CREDITO=="SI" & EDAD >= 35 & EDAD <= 45, select= NUM_HIJOS)
num_max=max(h,na.rm = T)


```
El resultado es: 
`r num_max`

- Número de personas que no tienen calificación
```{r}
no_calif <- base%>%
  filter(is.na(CALIFICACION))
nc=count(no_calif)
```

```{r, echo=FALSE}
plot(base$CALIFICACION, main="CALIFICACION", xlab="Calificación", ylab="Frecuencia", col=palette("Pastel 2"))
```

 El resultado es: 
`r nc` 

- Para saber el tipo de clientes (hombres o mujeres) que dominan en la base de datos, se utilizó el siguiente código:
```{r}

d=base%>%
  group_by(GENERO_C)%>%
 count(GENERO_C)
dom=max(d$n)

```

```{r, echo=FALSE}
knitr::kable(d)
plot(base$GENERO_C, main="GENERO", xlab="Género", ylab="Frecuencia", col=c("tan1","yellow"))
```


- Calificación con mayor frecuencia
```{r}
calificacion=base%>%
  group_by(CALIFICACION)%>%
  count(CALIFICACION)
max_calif=max(calificacion$n)
```
```{r, echo=FALSE}
knitr::kable(calificacion)
plot(base$CALIFICACION, main="CALIFICACION", xlab="Calificación", ylab="Frecuencia", col=palette("Pastel 2"))
```

- Estado civil con mayor frecuencua
```{r}

ec=base%>%
  group_by(ESTADO_CIVIL)%>%
  count(ESTADO_CIVIL)

mec=max(ec$n)



```

```{r, echo=FALSE}
knitr::kable(ec)

plot(base$ESTADO_CIVIL, main="ESTADO CIVIL", xlab="Estado civil", ylab="Frecuencia",col=palette("Set 2"))
```

Saldo a financiar mínimo de las personas entre 30 y 40 años de edad que tenga crédito
```{r}
e <-base%>%filter(TIENE_CREDITO=="SI" & EDAD >= 30 & EDAD <= 40)%>%
  select(SALDO_FINANCIAR)

mine=min(e,na.rm = T)
```
 El resultado es: 
`r mine`

Personas que tienen tarjeta de crédito
```{r}
c_tarjeta_cred <-base%>%filter(TIENE_CREDITO=="SI") %>%count(TIENE_CREDITO)
```
 El resultado es: 
```{r, echo=FALSE}
knitr::kable(c_tarjeta_cred)

```


Del total de personas que tienen tarjeta de crédito, se utiliza el siguiente código para saber cuántos son hombres y cuántas son mujeres
```{r}

gen_credito=base%>%
  group_by(GENERO_C)%>%
  filter(TIENE_CREDITO=="SI")%>%
  count(GENERO_C)
```
```{r, echo=FALSE}
knitr::kable(gen_credito)

plot(base$TIENE_CREDITO, main="TIENE CREDITO", xlab="Tiene Crédito", ylab="Frecuencia", col=c("black","palevioletred1"))


```

Tipo de vivienda predomina en las provincias de Pichincha, Guayas y Azuay
```{r}
w <-base%>%group_by(TIPO_VIVIENDA)%>%
  filter(PROVINCIA=="PICHINCHA" | PROVINCIA=="GUAYAS" | PROVINCIA=="AZUAY")%>%
  count()
```
```{r, echo=FALSE}
knitr::kable(gen_credito)
wv=max(w$n)
```
 El resultado es: 
`r wv`


Edad media de los individuos que tienen un saldo a financiar mayor a 2000
```{r}

r <-base%>%filter(SALDO_FINANCIAR > 2000)%>%
  summarise(media=mean(EDAD))
```
 El resultado es: 
`r r`



Numero de personas que no tienen vencimiento en bancos
```{r}
nvb <-base%>%filter(VENCIMIENTOS_EN_BANCOS=="")%>%
  count(VENCIMIENTOS_EN_BANCOS)
```


Gráfico variable tipo de vivienda
```{r, echo=FALSE}

plot(base$TIPO_VIVIENDA, main="TIPO DE VIVIENDA", xlab="Tipo de vivienda", ylab="Frecuencia", col=palette("Pastel 1"))






