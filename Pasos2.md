
Subdividir la dirección IP 192.168.44.0 /24 cuya dirección de red es 192.168.44.0 /24, para subdividirla en 4 subredes.


<div id="cl1">

## 1. Calcular el número de bits de subred necesarios
- Nuestra dirección ip tiene el prefijo /24, esto siginifica que 24 bits representan la parte de red y 8 bits a la parte de host, esto se representa de la forma:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/21.png">
    </p>
</div>

- Para determinar el número de bits que hay que tomar de la parte de host para obtener 4 subredes se utiliza la expresión:
```
2² ≥ 4
```

Donde **n** es el número de bits necesarios. Para obtener **n** se puede utilizar la tabla siguiente:

| Valor de n | 0 | 1 | **2** | 3 | 4 | 5 | 6 | 7 |
| ------ | -- | -- | -- | -- | -- | --  | -- | -- |
| N° subredes |  1 | 2 | **4** | 8 | 16 | 32 | 64 | 128 |

Esta tabla se puede prolongar todo lo que se quiera calculando potencias de 2. En nuestro caso

```
2² = 4 ≥ 4 ⇒ n = 2
```

Por lo que hay que tomar **2 bits** en la parte del host como se muestra:

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/22.png">
    </p>
</div>

Esto significa que las subredes tendrán el prefijo /26. Convirtiendo a decimal cada uno de los octetos se obtiene la nueva máscara de subred, que será la misma para todas las subredes, de ahí se obtiene el prefijo _Máscara fija._
```
255.255.255.192
```
<div id="cl2">

## 2. Obtener las subredes
- Para obtener la dirección de red de cada subred basta con cambiar los bits de subred calculados en el paso anterior. En nuestro caso hay **4** posibles combinaciones desde **_00_** hasta **_11_** cada una de las combinaciones es una dirección de red diferente. Esto se aplica de la siguiente forma :

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/23.png">
    </p>
</div>

_**NOTA:** Si no se siente cómodo con los números, también puede obtener las direcciones de red a travéz del llamado **salto de red** que es la diferencia entre dos direcciones de red consecutivas. El salto de red se calcula como la diferencia entre **256** y el valor del **último octeto no nulo** de la misma máscara. En este caso sería_
```
S = 256 - 192 = 64
```

Entonces para obtener las direcciones de red solo tiene que ir sumando a la dirección de red original el valor del respectivo salto.
<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/24.png">
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
H = 2⁶ - 2 = 2
```

Para calcular el resto de parámetros tomaremos como referencia la primera subred ya que el proceso es el mismo para el resto de subredes.

Las direcciones de host se obtienen combinando los bits de host desde **000001** hasta **111110**. De esta forma obtenemos las del **primero y el último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/25.png">
    </p>
</div>

La dirección de **broadcast** se obtiene haciendo 1 todos los bits de la parte del host

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/26.png">
    </p>
</div>

_**NOTA:** Si lo desea puede realizar los calculos sin utilizar números binaios de la manera siguiente_

1. La dirección del primer host se obtiene **sumando 1 a la dirección de red.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/27.png">
    </p>
</div>

2. La dirección del último host se obtiene **sumando a la dirección de red el número de hosts por subred.**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/28.png">
    </p>
</div>

2. La dirección de broadcast se obtiene **Sumando 1 a la dirección del último host**

<div>
    <p align ="center">
        <img width="500" src="https://github.com/Josue-Zea/pruebas/blob/master/pictures/29.png">
    </p>
</div>
<div id="result">

## Tras calcular los parámetros de todas las subredes, el resultado final queda como se muestra en la siguiente tabla
![Tabla de resultados](/pictures/Tabla2.png "This is a sample image.")

Si desea probar la calculadora FLSM puede hacerlo dando click [aqui](https://arcadio.gq/calculadora-subredes-flsm.html).