# Nadai ERC 3535 en Starknet (Semi Fungibles Tokens)

Buenas Amigos, ha llegado 2023 y como no, podemos empezar con alguna ideas de desarrollo hacia L3, recordamos que ya el L2022 ya ha pasado, es año del L32023 XD. Pero antes de extendernos sobre ideas más locas y detalles mas técnicos, iremos de distintas soluciones hasta llegar a esas ideas un poco mas innovadoras y complejas.

## ¿Qué son los SFTs y ERC 3525?

Los ERC-3525 Semi-Fungible Token `SFT`, es un token estándar independiente de activos de uso general que impulsa la representación digital de última generación de propiedad, valor, derechos, estado e identidad. 

Este estándar introduce un <ID, SLOT, VALUE> modelo escalar triple que representa la estructura semifungible de un token. También introduce nuevos modelos de transferencia, así como modelos de aprobación que reflejan la naturaleza semifungible de los tokens.

El token contiene una propiedad de ID equivalente a EIP-721 para identificarse como una entidad universalmente única, de modo que los tokens se puedan transferir entre direcciones y se aprueben para operar de manera compatible con EIP-721.

El significado de la propiedad `value` es muy similar al de la propiedad `saldo` de un token EIP-20. Cada token tiene un atributo de `slot`, lo que garantiza que el valor de dos tokens con la misma ranura se trate como fungible, lo que agrega fungibilidad a la propiedad de valor de los tokens.

Reescribe la generación y el comercio de activos digitales, creando eficiencias y mejorando la integridad del mercado. Con él, los activos tradicionalmente ilíquidos, como bonos, acciones futuras, ABS, bienes raíces y energía renovable, pueden volverse divisibles, representados en la cadena y comercializados libremente en un mercado abierto.

El ERC-721 es un estándar para tokens no fungibles `NFT`, lo que significa que cada uno de ellos es único y tiene su propio valor. Por otro lado, el ERC-3525 es una extensión del ERC-721 que agrega una capa adicional de lógica a la funcionalidad básica de tokens no fungibles.

Un ejemplo de uso del ERC-721 podría ser un juego en el que cada token representa un objeto único en el juego, como una espada mágica o un tesoro. Los jugadores podrían comprar y vender estos tokens entre ellos, y el valor de cada token dependería de su rareza y de su utilidad en el juego.

En cambio, si se utiliza el ERC-3525, se podrían agregar características adicionales a cada token, como la posibilidad de dividir o fusionar tokens para crear nuevos tokens con características únicas. Por ejemplo, si en el juego anterior se utilizara el ERC-3525, podríamos fusionar dos espadas mágicas para crear una espada mágica aún más poderosa.

En resumen, la principal diferencia entre el ERC-721 y el ERC-3525 es que el segundo agrega una capa adicional de lógica y funcionalidad a los tokens no fungibles, lo que permite a los desarrolladores crear tokens más complejos y personalizados.

Algunos links sobre ERC3525

* [EIP 3525](https://eips.ethereum.org/EIPS/eip-3525)
* [SFTlabs](https://sftlabs.io/)

### SFTs en Starknet

Después de hacer varios `deploy` de algunos contratos y ver el potencial que podrian traer decidí analizar un poco más sobre ello, todo fue debido a  

Ahora que sabemos un poco más sobre los `SFTs` podemos ver un caso de uso en una de las soluciones de ETH en la `L2 de Starknet`, primero hablaremos un poco de como han migrado estos contratos a `Cairo` en el ecosistema de `Starknet`. Has sido el caso de `Carbonable`, que según sus documentos oficales abrieron la implementación de EIP-3525. La implementación se basa en la versión [Solidity ERC 3525](https://github.com/solv-finance/erc-3525/tree/main/contracts) de [Solv-protocol](https://twitter.com/SolvProtocol), cuyo equipo fue coautor del EIP, y estan tomando medidas para estandarizar la implementación de StarkNet.

Recomendamos encarecidamente si quiere saber más sobre estos `SFTs` leer el siguiente artículo.

* [Carbonable Semi Fungible Tokens](https://carbonable.medium.com/semi-fungible-tokens-sfts-are-now-available-on-starknet-2e108594216f)


## Nadai SFTs en Starknet

Aquí realize algunas pruebas al respecto, sobre todo para distinguir entre dos versiones para su uso de idea final, puede revisar y crear sus propios `SFTs` clonando la guia de [Nadai ERC3525 Starknet] y haciendo los deploy. Aquí no nos extenderemos mucho para ver hasta donde llega el documetno xd....

Entre estos contratos tenemos 3 opciones, aunque hemos decidido analizar dos contratos. El [ERC3525MintableBurnable](/src/carbonable/erc3525/presets/ERC3525MintableBurnable.cairo) y el [ERC3525SlotEnumerableMintableBurnable](/src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo) para marcar las principales diferencias y así ver como pueden mejorar en la tecnología y en no saturar la red con lógicas implementaciones en soluciones innecesarias. 

El segundo contrato es prácticamente igual al primero, con la única diferencia de que incluye la librería `ERC3525SlotEnumerable` (que permite la implementación de una extensión de la funcionalidad de un token ERC721 llamada `enumerable slot`). La funcionalidad `enumerable slot` permite enumerar todos los tokens ERC721 existentes en el contrato y obtener información sobre un token específico por su índice en la lista.

Un ejemplo de cómo este contrato podría ser útil podría ser el siguiente:

## Tienda Online Anime Parte 1

Imagina que tienes una tienda de juguetes y quieres vender figuras de anime. Supongamos que quieres dividir tus figuras en diferentes categorías, como `Dragon Ball Z` y `Naruto`. Además, quieres poder contar cuántas figuras hay en cada categoría. En este caso, el contrato `ERC3525SlotEnumerableMintableBurnable` sería el adecuado. Puedes usar las funciones [slotByIndex](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L156) y [tokenSupplyInSlot](src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L163) para acceder a las figuras en cada categoría y [tokenInSlotByIndex]src/carbonable/erc3525/presets/ERC3525SlotEnumerableMintableBurnable.cairo#L171) para contar cuántas figuras hay en cada categoría.

Cada juguete sería un token único y no fungible, y cada token se asignaría a un slot específico basado en el anime al que pertenece. Por ejemplo, todos los juguetes de Dragon Ball Z estarían en el slot 0, todos los de Naruto estarían en el slot 1, y así sucesivamente.

Pero ahora iremos mucho más haya, ya que lo queremos plasmar es como estos Token nos podrían ayudar más que en otra L2 u en L1 o en una solución centralizada.

## Tienda Online Anime Parte 2

Para llevar a cabo nuestra tienda de juguetes de anime de manera eficiente y segura, podemos utilizar la plataforma StarkNet en las capas 2 y 3. En la capa 2, utilizaremos contratos ERC3525 SlotEnumerable para llevar un registro de nuestros juguetes de anime, como Dragon Ball y Naruto, y ofrecer descuentos y recompensas a nuestros clientes más leales. Estos contratos ERC3525 SlotEnumerable nos permiten enumerar nuestros juguetes de manera más sencilla y rápida que si utilizáramos contratos ERC721, lo que nos ayudará a escalar y procesar transacciones de manera más eficiente gracias a la utilización de zk-rollup.  

**Transaciones** En la capa 2, utilizaremos contratos ERC3525 SlotEnumerable para llevar un registro de nuestros juguetes de anime, como Dragon Ball y Naruto, y ofrecer descuentos y recompensas a nuestros clientes más leales. Estos contratos ERC3525 SlotEnumerable nos permiten enumerar nuestros juguetes de manera más sencilla y rápida que si utilizáramos contratos ERC721, lo que nos ayudará a escalar y procesar transacciones de manera más eficiente gracias a la utilización de zk-rollup.

Pero imagina ahora que esta idea se va haciendo realidad, que de verdad nos decidimos a realizarla, tenderemos que tener en cuenta transacciones, datos de usuarios, datos de empresas, mmmm demasiado no??? L3 y ZKPs al rescate. 

**Privacidad L3** En el caso de querer llevar a cabo una gestión interna privada de tu tienda, puedes utilizar tecnologías de privacidad en capa 3, como son Zero-Knowledge Proofs `ZKPs`. Los ZKPs te permiten probar la veracidad de una afirmación sin revelar información adicional.

Por ejemplo, si quieres comprobar que un cliente ha realizado más de 10 compras sin revelar cuántas compras ha realizado exactamente, puedes utilizar un ZKP para verificar que ha realizado más de 10 compras sin revelar la cantidad exacta. De esta manera, puedes utilizar la privacidad en tu gestión interna sin revelar información innecesaria a terceros.

Por otro lado, en la capa 3, podemos utilizar zk-Starks para garantizar la privacidad de ciertos datos sensibles, como los montos totales gastados por cada cliente, nóminas de empleados... Esto nos permitiría ofrecer a nuestros clientes la opción de optar por ciertos descuentos y recompensas sin revelar su información personal a terceros, `ni a nuestro propios empleados`. Además, al utilizar `zk-Starks` en lugar de `zk-SNARKs`, podemos estar preparados para el futuro y la posible llegada de la computación cuántica, ya que zk-Starks son resistentes a ataques cuánticos.

**Seguridad** Además de heredar la seguridad de la L1 de ETH en lo que son transacciones, saldos... podemos dejar un espacio extra para AA.

**Account Abstraction** Account abstraction aplicada a la Tienda, mejoraría la seguridad en el inicio de sesión en la cuenta de nuestra tienda de juguetes en línea. Esto nos permitiría utilizar contraseñas más seguras y protegidas gracias a la utilización de criptografía avanzada. Además, al utilizar account abstraction, podríamos garantizar que solo el propietario de la cuenta pueda acceder a ella y realizar transacciones, evitando posibles intentos de hackeo o fraudes.


 ## Tienda Online Parte 3 

Como Resumen final de lo que podríamos tener en StarkNet, sería una plataforma descentralizada basada en tecnología de capa 2 y 3 que ofrece escalabilidad y privacidad a través de la utilización de contratos inteligentes y criptografía de prueba de conocimiento 0. En este documento, hemos explorarado un hipotético uso de cómo se puede utilizar StarkNet en la creación de una tienda en línea de juguetes de Anime, y cómo sus características únicas pueden mejorar la experiencia de compra de nuestros clientes, podríamos tener una tienda de juguetes en línea que utilice la tecnología de StarkNet en las capas 2 y 3. 

Para llevar a cabo nuestro objetivo, utilizaremos contratos ERC3525 SlotEnumerable en la capa 2 de StarkNet. Los contratos ERC3525 SlotEnumerable son similares a los contratos ERC721 y ERC1155, que también son utilizados en la creación de juguetes no fungibles. Sin embargo, existen algunas diferencias clave entre estos contratos.

Mientras que los contratos ERC721 y ERC1155 permiten la creación de un juguete único y no fungible, los contratos ERC3525 SlotEnumerable permiten la creación de un conjunto de juguetes no fungibles que se pueden enumerar y recorrer de manera secuencial. Esto puede ser útil en nuestra tienda de juguetes de anime, ya que podríamos utilizar los contratos ERC3525 SlotEnumerable para llevar un registro de nuestros juguetes de Dragon Ball y Naruto y ofrecer descuentos y recompensas a nuestros clientes más leales. Además, implementaríamos Account Abstraction para mejorar la seguridad y simplificar el proceso de inicio de sesión de nuestros clientes.

En la capa 3, podríamos utilizar zk-Starks y ZKPs para garantizar la privacidad de ciertos datos sensibles, como los montos totales gastados por cada cliente o la información de los empleados de la tienda. Esto nos permitiría ofrecer a nuestros clientes la opción de optar por ciertos descuentos y recompensas sin revelar su información personal a terceros, así como proteger la privacidad de nuestros empleados.

Al utilizar StarkNet en las capas 2 y 3, podemos aprovechar las ventajas de la escalabilidad, la simplicidad y la privacidad que ofrece esta plataforma. Con los contratos ERC3525 SlotEnumerable en la capa 2 y las pruebas de validez Starks en la capa 3, podemos ofrecer a nuestros clientes una experiencia de compra óptima y segura en nuestra tienda en línea de juguetes de anime. Además, al implementar Account Abstraction en la capa 2, podemos mejorar la seguridad y simplicidad del proceso de inicio de sesión de nuestros clientes.





## Pruebas Developer

Si quieren hacer el deploy de estos contratos repasar cualquiera de las [Nadai Guía Stark Min]() para tener los conceptos básicos y minimos para poder avanzar. Una vez decidido que tipo de contrato vamos ahcer el `deploy` deberemos declarar su `Class Hash` en nuestro caso pasaremos los ajuste realizados tanto para un código MintBurnable como para SlotEnumerableMintBurnable. Primero tendremos que hacer el compile.

```
protostar build
```

![Graph]



### MintableBurnable

protostar -p testnet declare ./build/ERC3525MintableBurnable.json --max-fee auto

Declare

https://testnet.starkscan.co/tx/0x4db6928c73b64b76874c309ce40547dec8c99d81ca3afab0af7f380b5e563ae

Deploy

https://testnet.starkscan.co/tx/0x4db6928c73b64b76874c309ce40547dec8c99d81ca3afab0af7f380b5e563ae

Contract ERC 3525 Min-Butn = 0x059ad1b4990c51d5cc7082b752302c43392ec6fd831b69d256d1107937f14328

* Mint ID = 1 Slot = 1 Valor 25

https://testnet.starkscan.co/tx/0x26836c2339ff4ccc5a70c315d2d9b61cb4cbeacd6c13df16309b32a590310b3

* Mint ID = 2 Slot = 1 Valor 10

https://testnet.starkscan.co/tx/0xe6110df595214776c894269fc267674781864cdecb53d1f6f29f32887e6ffe

* Mint ID = 3 Slot = 2 Valor 500000000000

https://testnet.starkscan.co/tx/0x3703aa31eaa429fbdba8905955a9d6dd27cb18e44c4e1901e76b15ce6b2fcc

* Mint ID = 4 Slot = 2 Valor 120

https://testnet.starkscan.co/tx/0x406d7a7e73f68c807dc628511fe284de79799149f02bfa6a5098aadf237685f



User Wallet:
╔══════╦══════════╦═══════════════╗
║ SLOT ║ TOKEN_ID ║     VALUE     ║
╠══════╬══════════╬═══════════════╣
║ 1    ║        1 ║            25 ║
║ 1    ║        2 ║            10 ║
║ 2    ║        3 ║  500000000000 ║
║ 2    ║        4 ║           120 ║
╚══════╩══════════╩═══════════════╝

Total Slot 1 = 35
Total Slot 2 = 500000000120 
-----------

## SlotEnumerableMintableBurnable

protostar -p testnet declare ./build/ERC3525MintableBurnable.json --max-fee auto

Declare

https://testnet.starkscan.co/class/0x0058a8813fe98f05aa3a1883da43e41bd9faa490646e57e9579505c2a6eca9c

Deploy

https://testnet.starkscan.co/tx/0x5d8656217f7697009a519eb9aa02767a695b1d4b1755de1ec93ca885b222e15

Contract ERC 3525 SlotEnum-Mint-Burn = 0x0779c7fc964520c6bb70d3be54b69ec2c6b020e1243282e37296179d39508ff3

* Mint ID = 1 Slot = 1 Valor 25

https://testnet.starkscan.co/tx/0x626fa54c2f577ebbba5bd0dc7b3ebc2c547667151b6494013d317c3118d419a

* Mint ID = 2 Slot = 1 Valor 10

https://testnet.starkscan.co/tx/0x3812b8f96bcb792612bac5a69c743c791b158dc9a4ff054bd0bfad39396be19

* Mint ID = 3 Slot = 2 Valor 500000000000

https://testnet.starkscan.co/tx/0x18d811c6167951a8ba29c4128ee58cb5c7c4b2a900db466875de096f94195ed

* Mint ID = 4 Slot = 2 Valor 120

https://testnet.starkscan.co/tx/0x1976e79e3fca6a660c1bc79e2d1be7e6b312bc7dc241cd626b830d2242ab198




User Wallet:
╔══════╦══════════╦═══════════════╗
║ SLOT ║ TOKEN_ID ║     VALUE     ║
╠══════╬══════════╬═══════════════╣
║ 1    ║        1 ║            25 ║
║ 1    ║        2 ║            10 ║
║ 2    ║        3 ║  500000000000 ║
║ 2    ║        4 ║           120 ║
╚══════╩══════════╩═══════════════╝

Total Slot 1 = 35
Total Slot 2 = 500000000120 

