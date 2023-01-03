# ¿Qué son los SFTs (Semi Fungibles Tokens)? 
## Los ERC-3525 están en Starknet.

Buenas Amigos, ha llegado 2023 y como no podía ser menos debemos empezar con algunas ideas de desarrollo hacia L3. ¿Porqué en L3? ¿Es necesario? La mayoría de las respuestas serán NO, no debemos de sobrecargar las red principal de ETH y seguridad con proyectos, protocolos o capas innecesarias desde ningun punto de vista. Ya que desde mi humilde opinión, podemos crear modelos de nogocios inservibles, envueltos en fomo y con otras expectativas que no tendrán su logro, esto puede ser debido a que aunque la tecnología subyacente sea exitosa, su proyecto no debe necesarimente tener que incorporarla, ni servirle, recordad siempre los grandes casos de `BTC`, por ejemplo, Satoshi creo `BTC` como moneda para un medio de pagos entre personas libre, sin terceros ni autoridades intermediarias, pero al final el mal uso de la tecnolgía ha llevado a muchos declives de proyectos por estas malas causas, pero no ha sido culpa de `BTC` X...

Pero bueno, ya que vamos hablar sobre nuevas ideas, recordamos que el **`L2022`** ya ha pasado, es año del **`L32023`**, memes a parte XD, antes de extendernos sobre ideas más locas y detalles más técnicos, iremos entrando en contexto con distintas soluciones, como los `SFTs`, hasta llegar a esas ideas un poco mas innovadoras y complejas, como posibles soluciones en una `Layer 3`.

## ¿Qué son los SFTs y ERC 3525?

El ERC-3525 Semi-Fungible Token `SFT`, es un token estándar independiente de activos de uso general que impulsa la representación digital de última generación de propiedad, valor, derechos, estado e identidad. 

Este estándar introduce un **`ID, SLOT, VALUE`** modelo escalar triple que representa la estructura semifungible de un token. También introduce nuevos modelos de transferencia, así como modelos de aprobación que reflejan la naturaleza semifungible de los tokens. El token contiene una propiedad de ID equivalente a EIP-721 para identificarse como una entidad universalmente única, de modo que los tokens se puedan transferir entre direcciones y se aprueben para operar de manera compatible con EIP-721.

El significado de la propiedad `value` es muy similar al de la propiedad `saldo` de un token EIP-20. Cada token tiene un atributo de `slot`, lo que garantiza que el valor de dos tokens con la misma ranura se trate como fungible, lo que agrega fungibilidad a la propiedad de valor de los tokens.

Según [SFTlabs](https://sftlabs.io/), un laboratorio que proporciona a las empresas criptográficas/Web3 y a los protocolos del mañana la gama completa de recursos, financiamiento y soporte para lanzar activos digitales disruptivos de Web3 con tecnología del estándar de token semifungible ERC-3525, comenta lo siguiente:

> Reescribe la generación y el comercio de activos digitales, creando eficiencias y mejorando la integridad del mercado. Con él, los activos tradicionalmente ilíquidos, como bonos, acciones futuras, ABS, bienes raíces y energía renovable, pueden volverse divisibles, representados en la cadena y comercializados libremente en un mercado abierto.

> Una de las diferencias posibles en una caso de uso con ERC-721, podría ser un juego en el que cada token representa un objeto único en el juego, como una espada mágica o un tesoro. Los jugadores podrían comprar y vender estos tokens entre ellos, y el valor de cada token dependería de su rareza y de su utilidad en el juego.

> En cambio, si se utiliza el ERC-3525, se podrían agregar características adicionales a cada token, como la posibilidad de dividir o fusionar tokens para crear nuevos tokens con características únicas. Por ejemplo, si en el juego anterior se utilizara el ERC-3525, podríamos fusionar dos espadas mágicas para crear una espada mágica aún más poderosa.

En resumen, la principal diferencia entre el ERC-721 y el ERC-3525 es que el segundo agrega una capa adicional de lógica y funcionalidad a los tokens no fungibles, lo que permite a los desarrolladores crear tokens más complejos y personalizados.

Algunos links sobre ERC3525:

* [EIP 3525](https://eips.ethereum.org/EIPS/eip-3525)
* [SFTlabs](https://sftlabs.io/)

---

### SFTs en Starknet

Después de hacer varios `deploy` de algunos contratos de este tipo y ver el potencial que podrian traer, decidí analizar un poco más su lógica y aprender un poco más sobre ello, vemos como siguen llegando todo tipo de código a `Cairo` e impulsando aún más las soluciones de L2.

Ahora que sabemos un poco más sobre los `SFTs` podemos ver un caso de uso en `L2 de Starknet`. Primero hablaremos un poco de como han migrado estos contratos a `Cairo` en el ecosistema de `Starknet`. Ha sido el caso de `Carbonable`, que según sus documentos oficales abrieron la implementación de EIP-3525 en Starknet. La implementación se basa en la versión [Solidity ERC 3525](https://github.com/solv-finance/erc-3525/tree/main/contracts) de [Solv-protocol](https://twitter.com/SolvProtocol), cuyo equipo fue coautor del EIP, y estan tomando medidas para estandarizar la implementación de StarkNet.

**Recomendamos encarecidamente si quiere saber más sobre estos `SFTs` y grandes casos de uso como en DEFI, leer el siguiente artículo.**

* [Carbonable Semi Fungible Tokens](https://carbonable.medium.com/semi-fungible-tokens-sfts-are-now-available-on-starknet-2e108594216f)

---
## Nadai SFTs en Starknet

Aquí tuve que realizar algunas pruebas al respecto, sobre todo para distinguir entre dos versiones de contrato para su uso en una idea final, (que poco a poco iremos descubriendo). Podrá revisar y crear sus propios `SFTs` clonando la guia de [Nadai ERC3525 Starknet](https://github.com/Nadai2010/Nadai-ERC3525-Starknet) o en la [Repo Oficial Carbonable](https://github.com/Carbonable/carbonable-contracts) y haciendo los deploy de los contratos que usted decida. 

**[`Al final del documento dejaremos una mini sección para developer`](https://github.com/Nadai2010/Nadai-ERC3525-Starknet#pruebas-developer)**

Entre estos contratos tenemos 3 opciones, aunque hemos decidido analizar dos contratos. El [ERC3525MintableBurnable](/src/carbonable/erc3525/presets/ERC3525MintableBurnable.cairo) y el [ERC3525SlotEnumerableMintableBurnable](/src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo) para marcar las principales diferencias y así ver como pueden mejorar en la tecnología y en no saturar la L1 con lógicas e implementaciones en soluciones innecesarias. 

El segundo contrato es prácticamente igual al primero, con la única diferencia de que incluye la librería `ERC3525SlotEnumerable` (que permite la implementación de una extensión de la funcionalidad de un token ERC721 llamada `enumerable slot`). La funcionalidad `enumerable slot` permite enumerar todos los tokens ERC721 existentes en el contrato y obtener información sobre un token específico por su índice en la lista.

Un ejemplo de cómo este contrato podría ser útil podría ser el siguiente:

### Tienda Online Anime Parte 1

Imagina que tienes una tienda de juguetes y quieres vender figuras de anime. Supongamos que quieres dividir tus figuras en diferentes categorías, como `Dragon Ball Z` y `Naruto`. Además, quieres poder contar cuántas figuras hay en cada categoría. En este caso, el contrato `ERC3525SlotEnumerableMintableBurnable` sería el adecuado. Puedes usar las funciones [slotByIndex](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L156) y [tokenSupplyInSlot](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L163) para acceder a las figuras en cada categoría y [tokenInSlotByIndex]src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L171) para contar cuántas figuras hay en cada categoría.

Cada juguete sería un token único y no fungible, y cada token se asignaría a un slot específico basado en el anime al que pertenece. Por ejemplo, todos los juguetes de Dragon Ball Z estarían en el slot 0, todos los de Naruto estarían en el slot 1, y así sucesivamente. 

Pero ahora iremos mucho más haya, podríamos crear colecciones gigantes, pedidos inmensos o inclusive una parte en mercado libre, pero lo quiero plasmar es una idea de como los `SFTs` nos podrían ayudar más en una solución L2 como `Starknet` que en una L1 o en una solución centralizada. 


---
### Tienda Online Anime Parte 2

Para llevar a cabo nuestra tienda de juguetes de anime de manera eficiente y segura, podemos utilizar la plataforma StarkNet en las capas 2 y 3. **Pero imagina ahora que esta idea se va haciendo realidad, que de verdad nos decidimos a crear nuestra tienda virtual, tenderemos que tener en cuenta transacciones, datos de usuarios, datos de empresas, Mmmm empieza a complicarse no??? L3 y ZKPs al rescate.** 

* **Transaciones** En la capa 2, utilizaremos contratos `ERC3525 SlotEnumerable` para llevar un registro de nuestros juguetes de anime, como `Dragon Ball Z` y `Naruto`, y ofrecer descuentos y recompensas a nuestros clientes más leales. Estos contratos ERC3525 SlotEnumerable nos permiten enumerar nuestros juguetes de manera más sencilla y rápida que si utilizáramos contratos ERC721, lo que nos ayudará a escalar y procesar transacciones de manera más eficiente gracias a la utilización de `zk-rollup`.  

* **Privacidad L3** En el caso de querer llevar a cabo una gestión interna privada de tu tienda, puedes utilizar tecnologías de privacidad en capa 3, como son Zero-Knowledge Proofs `ZKPs`. Los ZKPs te permiten probar la veracidad de una afirmación sin revelar información adicional.

Por ejemplo, si quieres comprobar que un cliente ha realizado más de 10 compras sin revelar cuántas compras ha realizado exactamente, puedes utilizar un ZKP para verificar que ha realizado más de 10 compras sin revelar la cantidad exacta. De esta manera, puedes utilizar la privacidad en tu gestión interna sin revelar información innecesaria a terceros.

Por otro lado, en la capa 3, podemos utilizar zk-Starks para garantizar la privacidad de ciertos datos sensibles, como los montos totales gastados por cada cliente, nóminas de empleados... Esto nos permitiría ofrecer a nuestros clientes la opción de optar por ciertos descuentos y recompensas sin revelar su información personal a terceros, `ni a nuestro propios empleados`. Además, al utilizar `zk-Starks` en lugar de `zk-Snarks`, podemos estar preparados para el futuro y la posible llegada de la computación cuántica, ya que zk-Starks son resistentes a ataques cuánticos.

* **Seguridad** Además de heredar la seguridad de la L1 de ETH en lo que son transacciones, saldos y todo lo que tengamos ejecutado en L2... podemos dejar un espacio extra para AA.

* **Account Abstraction** aplicada a la Tienda, mejoraría la seguridad en el inicio de sesión en la cuenta de nuestra tienda de juguetes en línea. Esto nos permitiría utilizar contraseñas más seguras y protegidas gracias a la utilización de criptografía avanzada. Además, al utilizar account abstraction, podríamos garantizar que solo el propietario de la cuenta pueda acceder a ella y realizar transacciones, evitando posibles intentos de hackeo o fraudes.


## Resumen Final del Montaje de Tienda.

Como Resumen final de lo que podríamos tener en StarkNet, sería una plataforma descentralizada basada en tecnología de capa 2 y 3 que ofrece escalabilidad y privacidad a través de la utilización de contratos inteligentes y criptografía de prueba de conocimiento 0. En este documento, hemos explorarado un hipotético uso de cómo se puede utilizar StarkNet en la creación de una tienda en línea de juguetes de Anime, y cómo sus características únicas pueden mejorar la experiencia de compra de nuestros clientes, podríamos tener una tienda de juguetes en línea que utilice la tecnología de StarkNet en las capas 2 y 3. 

Para llevar a cabo nuestro objetivo, utilizaremos contratos ERC3525 SlotEnumerable en la capa 2 de StarkNet. Los contratos ERC3525 SlotEnumerable son similares a los contratos ERC721 y ERC1155, que también son utilizados en la creación de juguetes no fungibles. Sin embargo, existen algunas diferencias clave entre estos contratos.

Mientras que los contratos ERC721 y ERC1155 permiten la creación de un juguete único y no fungible, los contratos ERC3525 SlotEnumerable permiten la creación de un conjunto de juguetes no fungibles que se pueden enumerar y recorrer de manera secuencial. Esto puede ser útil en nuestra tienda de juguetes de anime, ya que podríamos utilizar los contratos ERC3525 SlotEnumerable para llevar un registro de nuestros juguetes de Dragon Ball Z y Naruto y ofrecer descuentos y recompensas a nuestros clientes más leales. Además, implementaríamos Account Abstraction para mejorar la seguridad y simplificar el proceso de inicio de sesión de nuestros clientes.

En la capa 3, podríamos utilizar zk-Starks y ZKPs para garantizar la privacidad de ciertos datos sensibles, como los montos totales gastados por cada cliente o la información de los empleados de la tienda. Esto nos permitiría ofrecer a nuestros clientes la opción de optar por ciertos descuentos y recompensas sin revelar su información personal a terceros, así como proteger la privacidad de nuestros empleados.

Al utilizar StarkNet en las capas 2 y 3, podemos aprovechar las ventajas de la escalabilidad, la simplicidad y la privacidad que ofrece esta plataforma. Con los contratos ERC3525 SlotEnumerable en la capa 2 y las pruebas de validez Starks en la capa 3, podemos ofrecer a nuestros clientes una experiencia de compra óptima y segura en nuestra tienda en línea de juguetes de anime. Además, al implementar Account Abstraction en la capa 2, podemos mejorar la seguridad y simplicidad del proceso de inicio de sesión de nuestros clientes.

Mmmm Nuestra tienda virtual podría ampliarse a vender `FUNKO` de todos los tipos con contratos ajustados, haciendo pragmatica nuestra idea y empresa en un futuro.

---

## Pruebas Developer

Si quieren hacer el deploy de estos contratos puede repasar cualquiera de las [Nadai Guía Stark Min](https://github.com/Nadai2010/Nadai-Min-Starknet), aunque para esta mejor fijarnos en [Nadai Guía Min ERC 721](https://github.com/Nadai2010/Nadai-Min-Starknet/blob/master/src/min_erc721/README.md)si tiene alguna duda, aunque debe de tener los conceptos básicos y mínimos en `Protostar` y `Starknet` para poder avanzar. 

Una vez decidido que tipo de contrato vamos a necesitar para el `deploy`, deberemos hacer el `build` para compilar su contrato y poder declarar su `Class Hash`. En nuestro caso pasaremos los ajuste realizados tanto para un código [ERC3525MintableBurnable.cairo](/src/carbonable/erc3525/presets/ERC3525MintableBurnable.cairo) como para [ERC3525SlotEnumerableMintBurnable.cairo](/src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo). Primero tendremos que hacer el compile desde nuestro proyecto. 

Primero clonaremos esta repo, e instaleremos si no las tenemos las librerias de [Contract OppenZepelin](https://github.com/OpenZeppelin/cairo-contracts).

```bash
gh repo clone Nadai2010/Nadai-ERC3525-Starknet
```

Y luego si no tenemos las librerias puede clonar o instalar las librerias oficiales haciendo en su terminal.


```bash

gh repo clone OpenZeppelin/cairo-contracts
```

Ahora ya podemos hacer el compile, que nos dará el `Class Hash` de todos nuestros contratos, ya que lo tenemos definido así en el [protostar.toml](/protostar.toml)

```
protostar build
```

![Graph](/im%C3%A1genes/build.png)


---

### Compile de MintableBurnable y SlotEnumerableMintableBurnable.

Dejaremos los comandos y herramientas utilizadas para hacer el deploy, en ambos casos ha sido igual y solo hemos cambiado el nombre del `Simbolo` que  ha sido distinto entre ambos `deploy` cuando lo convettimos a `felt` con la herramienta [Stark Utils](https://www.stark-utils.xyz/converter). El constructor nos pide 3 argumentos que son (Nombre, Simbolo, Decimales), que usaremos en esta guía usando el Universal Deploy Contract de Starknet [UDC](https://testnet.starkscan.co/contract/0x041a78e741e5af2fec34b695679bc6891742439f7afb8484ecd7766661ad02bf#write-contract), pero primero declararemos nuestro contrato usando el siguiente comando.

```bash
protostar -p testnet declare ./build/ERC3525MintableBurnable.json --max-fee auto
```

![Graph](/im%C3%A1genes/delcaremint.png)

* [Declare Cass Hash](https://testnet.starkscan.co/tx/0x4db6928c73b64b76874c309ce40547dec8c99d81ca3afab0af7f380b5e563ae)


```bash
protostar -p testnet declare ./build/ERC3525SlotEnumerableMintableBurnable.json --max-fee auto
```
* [Declare Cass Hash](https://testnet.starkscan.co/class/0x0058a8813fe98f05aa3a1883da43e41bd9faa490646e57e9579505c2a6eca9c)

---

### Deploy de MintableBurnable y SlotEnumerableMintableBurnable.

Aquí podra escoger que contrato se adapta mejor a sus necesidades para poder hacer el deploy. en este caso les dejaremos los resultados de ambos deploy para poder por último ver las diferencia entres ambos. Usaremos el [UDC](https://testnet.starkscan.co/contract/0x041a78e741e5af2fec34b695679bc6891742439f7afb8484ecd7766661ad02bf#write-contract) oficial para nuestro esfuerzos mínimos, en el que tendremos que pasar `Class Hash` y los argumentos del contructor `Nombre, Simbolo, Decimales` que describimos arriba.

![Graph](/im%C3%A1genes/deploymint.png)

* [Hash Deploy MintBurn](https://testnet.starkscan.co/tx/0x4db6928c73b64b76874c309ce40547dec8c99d81ca3afab0af7f380b5e563ae)
* [Contract ERC 3525 MintBurn](https://testnet.starkscan.co/contract/0x059ad1b4990c51d5cc7082b752302c43392ec6fd831b69d256d1107937f14328)

![Graph](/im%C3%A1genes/deployslot.png)

* [Hash Deploy SlotEnumerableMintBurn](https://testnet.starkscan.co/tx/0x5d8656217f7697009a519eb9aa02767a695b1d4b1755de1ec93ca885b222e15)
* [Contract ERC 3525 SlotEnumerableMintBurn](https://testnet.starkscan.co/contract/0x0779c7fc964520c6bb70d3be54b69ec2c6b020e1243282e37296179d39508ff3)


Ahora procederemos a crear dos ejemplos iguales para los 2 contratos. Crearemos 4 mint de SFT, 2 en el `Slot 1` y 2 en el `Slot 2`, en ambos ejemplos con mismos valores y luego comprobaremos las principales diferencias, supomgamos que fuera el ejemplo de la juguetería para explicar los ejemplos. 

* [slotByIndex](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L156) es una función que se utiliza para acceder a uno de los slots del contrato ERC3525 SlotEnumerable. Cada slot representa una categoría por ejemplo de juguetes, y al utilizar esta función podemos obtener información sobre la categoría específica a la que estamos accediendo.
* [tokenSupplyInSlot](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L163) es una función que nos permite conocer la cantidad de juguetes de una categoría específica. Al proporcionarle el índice del slot al que queremos acceder, podemos obtener el número total de juguetes en esa categoría.
* [tokenInSlotByIndex](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L171) es una función que nos permite acceder a un juguete específico dentro de una categoría. Al proporcionarle el índice del slot y el índice del juguete dentro de ese slot, podemos obtener información sobre el juguete en cuestión.


Así que procedi a crear los `SFT` con estos ajustes:

**`MintBurnable`**
* [Mint ID 1](https://testnet.starkscan.co/tx/0x26836c2339ff4ccc5a70c315d2d9b61cb4cbeacd6c13df16309b32a590310b3) = Slot  1, Valor 25
* [Mint ID 2](https://testnet.starkscan.co/tx/0xe6110df595214776c894269fc267674781864cdecb53d1f6f29f32887e6ffe) = Slot 1, Valor 10
* [Mint ID 3](https://testnet.starkscan.co/tx/0x3703aa31eaa429fbdba8905955a9d6dd27cb18e44c4e1901e76b15ce6b2fcc) = Slot 2, Valor 500000000000
* [Mint ID 4](https://testnet.starkscan.co/tx/0x406d7a7e73f68c807dc628511fe284de79799149f02bfa6a5098aadf237685f) = Slot 2, Valor 120

![Graph](/im%C3%A1genes/mint1.png) ![Graph](/im%C3%A1genes/mint2.png) 
![Graph](/im%C3%A1genes/mint3.png) ![Graph](/im%C3%A1genes/mint4.png)


**`SlotEnumerableMintBurnable`**
* [Mint ID 1](https://testnet.starkscan.co/tx/0x626fa54c2f577ebbba5bd0dc7b3ebc2c547667151b6494013d317c3118d419a) = Slot  1, Valor 25
* [Mint ID 2](https://testnet.starkscan.co/tx/0x3812b8f96bcb792612bac5a69c743c791b158dc9a4ff054bd0bfad39396be19) = Slot 1, Valor 10
* [Mint ID 3](https://testnet.starkscan.co/tx/0x18d811c6167951a8ba29c4128ee58cb5c7c4b2a900db466875de096f94195ed) = Slot 2, Valor 500000000000
* [Mint ID 4](https://testnet.starkscan.co/tx/0x1976e79e3fca6a660c1bc79e2d1be7e6b312bc7dc241cd626b830d2242ab198) = Slot 2, Valor 120



User Wallet:
```bash
╔══════╦══════════╦═══════════════╗
║ SLOT ║ TOKEN_ID ║     VALUE     ║
╠══════╬══════════╬═══════════════╣
║ 1    ║        1 ║            25 ║
║ 1    ║        2 ║            10 ║
║ 2    ║        3 ║  500000000000 ║
║ 2    ║        4 ║           120 ║
╚══════╩══════════╩═══════════════╝
```

Total Slot 1 = 35
Total Slot 2 = 500000000120 

![Graph](/im%C3%A1genes/value1.png)
![Graph](/im%C3%A1genes/value2.png)

-----------


