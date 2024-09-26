# Lo que cuenta el cliente

Mire Firibicundio, lo que necesitamos es un sistema para manejar nuestras ventas. 

Tenemos varias tiendas, cada una con su dirección y nombre. En estas tiendas guardamos los artículos que vendemos.

Cuando hacemos una venta, necesitamos registrar varias cosas. Primero, qué artículos se vendieron y en qué cantidad - eso le llamamos líneas de venta. Luego, necesitamos saber la fecha y hora de la venta.

También es importante registrar cómo se pagó la venta. Ya sabes, la cantidad que se pagó y todo eso.

Ah, y cada venta se captura en un registro que se guarda en la tienda donde se hizo la venta. Es como tener un historial de todas las ventas por tienda.

Queremos poder ver qué se vendió, cuándo, dónde, cómo se pagó y tener un registro de todo.

|Paso|Ejemplo|
|-|:-:|
|1. Listar las clases conceptuales candidatas.|Línea de venta, artículo, venta, tienda, registro, pago
|2. Representarlas en el modelo de dominio de partida.|![](/imagenes/modelosUML/mdd001.svg)
|3. Añadir las asociaciones necesarias para registrar las relaciones.|![](/imagenes/modelosUML/mdd002.svg)
|4. Añadir los atributos que satisfagan los requisitos de información.|![](/imagenes/modelosUML/mdd004.svg)
|5. Iterar...|![](/imagenes/modelosUML/mdd005.svg)