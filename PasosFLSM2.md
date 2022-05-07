
-----------------------------------------
## **INDICE** 📚
-----------------------------------------
1. [**Pasos a seguir**](#cls)
   1. [**Calcular el número de bits de subred necesarios**](#cl1)
   2. [**Obtener las subredes**](#cl2)
   3. [**Calcular los parámetros de cada subred**](#cl3)
2. [**Resultado**](#result)

<div id = "topo">

# Cómo subdividir una red utilizando la técnica FLSM
_FLSM del Inglés **Fixed Length Subnet Mask** o **Máscara de Subred de Longitud Fariable** es la forma tradicional de subdividir una red, consiste en "tomar prestados" unos bits en la parte de host para generar nuevas subredes._

Entonces, para este caso de ejemplo vamos a subdividir la red 10.4.0.0 /16 para subdividirla en 16384 subreedes.

<div id="cls">

### Pasos a seguir 📋

<div id="cl1">

## 1. Calcular el número de bits de subred necesarios
- Ya que nuestra dirección ip tiene el prefijo /16 esto significa que 16 bits representan la parte de red y 16 bits la parte de host. Se puede visualizar de la siguiente forma:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/1.png">
    </p>
</div>

- Para determinar el número de bits que hay que tomar de la parte de host para obtener 16384 subredes se utiliza la expresión:
```
2² ≥ 16384
```

Donde **n** es el número de bits necesarios. Para obtener **n** se puede utilizar la tabla siguiente:

| Valor de n | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| ------ | -- | -- | -- | -- | -- | --  | -- | -- |
| N° subredes |  1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 |

Esta tabla se puede prolongar todo lo que se quiera calculando potencias de 2. En nuestro caso

```
2¹⁴ = 16384 ≥ 16384 ⇒ n = 14
```

Por lo que hay que tomar **14 bits** en la parte del host como se muestra:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/2.png">
    </p>
</div>

Esto significa que las subredes tendrán el prefijo /30. Convirtiendo a decimal cada uno de los octetos se obtiene la nueva máscara de subred, que será la misma para todas las subredes, de ahí se obtiene el prefijo _Máscara fija._
```
255.255.255.252
```
<div id="cl2">

## 2. Obtener las subredes
- Para obtener la dirección de red de cada subred basta con cambiar los bits de subred calculados en el paso anterior. En nuestro caso hay **16384** posibles combinaciones desde 00000000000000 hasta 11111111111111 cada una de las combinaciones es una dirección de red diferente. Esto se aplica de la siguiente forma :
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/3.png">
    </p>
</div>

_**NOTA:** Si no se siente cómodo con los números, también puede obtener las direcciones de red a travéz del llamado **salto de red** que es la diferencia entre dos direcciones de red consecutivas. El salto de red se calcula como la diferencia entre **256** y el valor del **último octeto no nulo** de la misma máscara. En este caso sería_
```
S = 256 - 252 = 4
```

Entonces para obtener las direcciones de red solo tiene que ir sumando a la dirección de red original el valor del respectivo salto.
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/4.png">
    </p>
</div>

<div id="cl3">

## 3. Calcular los parámetros de cada subred

El número de host por subred se calcula de la siguiente forma:
```
H = 2ⁿ - 2
```

En este caso **n** es el número de bits de la parte de host (bits azules en los pasos anteriores). El -2 de la fórmula se debe a que la primera dirección corresponde a la dirección de red y la última corresponde a la dirección de broadcast, por lo que no se las puede asignar a ningún host. Teniendo esto en cuenta, el número de hosts por cada una de nuestras subredes es
```
H = 2² - 2 = 2
```

Para calcular el resto de parámetros tomaremos como referencia la primera subred ya que el proceso es el mismo para el resto de subredes.

Las direcciones de host se obtienen combinando los bits de host desde **01** hasta **10**. De esta forma obtenemos las del **primero y el último host**
```
10.4.00000000.00000001 ⇒ 10.4.0.1 
10.4.00000000.00000010 ⇒ 10.4.0.2
```

La dirección de **broadcast** se obtiene haciendo 1 todos los bits de la parte del host
```
10.4.00000000.00000011 ⇒ 10.4.0.3
```

_**NOTA:** Si lo desea puede realizar los calculos sin utilizar números binaios de la manera siguiente_

1. La dirección del primer host se obtiene **sumando 1 a la dirección de red.**
```
10.4.0+10 ⇒ 10.4.0.1
```

2. La dirección del último host se obtiene **sumando a la dirección de red el número de hosts por subred.**
```
10.4.0+20 ⇒ 10.4.0.2
```

2. La dirección de broadcast se obtiene **Sumando 1 a la dirección del último host**

```
10.4.2+10 ⇒ 10.4.0.3
```

<div id="result">

## Tras calcular los parámetros de todas las subredes, el resultado final queda como se muestra en la siguiente tabla
![Tabla de resultados](/pictures/Tabla.png "This is a sample image.")

Si desea probar la calculadora FLSM puede hacerlo dando click [aqui](https://arcadio.gq/calculadora-subredes-flsm.html).