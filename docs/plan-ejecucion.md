# Plan de ejecución — App de Mandado (P7 + P21)

> Estado: plan listo como biblioteca, no para correr con prisa.
> Decisión del 13 nov 2026: Dulce dijo NO a correr el hackatón BuildHybridAI del 30 nov 2026 con esta app. No quiere que la apuren con tan poco tiempo; cualquier imprevisto en casa le comería las mañanas y ya le pasó antes con un proyecto que fue postergando. Los bloques de calendario del hackatón (16, 18, 19, 23-27 y 30 nov) fueron borrados ese mismo día. Este plan queda guardado para cuando aparezca un hackatón u oportunidad que encaje; entonces solo es ponerse a construir.

## 1. Objetivo
- Que una persona no se pase de su presupuesto de quincena cuando hace el mandado.
- Al final, la persona puede: hacer su lista antes de ir a la tienda, ir registrando lo que compra por kilo, por pieza o por presentación, ver cuánto lleva gastado contra su presupuesto, y cerrar la cuenta sabiendo cuánto gastó y cuánto se ahorró con las ofertas.

## 2. Para quién
- Lo usa primero: una persona que hace el mandado de su casa, como Dulce, en el celular, en la tienda.
- Lo paga o lo compra después: tiendas grandes como Soriana o HEB, que quieren darles la app a sus clientas o integrar la función en su web.
- ¿Por qué le sirve a la tienda? La tienda ya tiene el dato del ticket, pero no tiene el dato de intención: cuánto pensaba gastar la persona, si gastó más o menos, y si compró todo lo que anotó o compró de más.
- Dónde se usa: en el celular, en la tienda. Tienda principal: HEB.

## 3. MVP — lo mínimo que se construye primero
1. Antes de ir a la tienda: abrir la app y anotar qué falta comprar, por secciones. Poner el presupuesto de la quincena (por ejemplo, lo que el esposo dice que es para mandado).
2. En la tienda, por secciones:
   - Frutas y verduras por kilo: la app pregunta precio y kilos o gramos, y suma.
   - Huevo por presentación: pregunta precio y presentación (6, 12, 18 o 30 huevos).
   - Abarrotes por pieza: pregunta precio y pieza.
   - Carnes frías / carnes en charola por kilo: precio y kilos o gramos. La foto es solo una ayuda para leer el precio, no es obligatoria.
3. Ofertas: marcar 2x1, 3x2 o combos, marcar qué se lleva gratis y cuánto costaba eso gratis, para saber cuánto se ahorró de verdad.
4. Cierre de cuenta: total gastado contra presupuesto. Si te estás pasando, la app avisa y pregunta si quieres quitar productos para ver qué puedes dejar.
5. Al salir de la caja: foto del ticket, solo guardada, para el ajuste final y el ahorro.

## 4. Qué NO lleva el MVP
- Login ni cuentas: un solo usuario, los datos se guardan en su propio teléfono.
- Red familiar ni sincronización entre varios celulares: eso va después del hackatón / MVP.
- Catálogo de productos: se escribe el precio a mano en la tienda.
- Leer el ticket con la cámara (OCR): la foto solo se guarda, no se lee. Leerla es un proyecto entero.
- App nativa para Play Store o App Store, ni pagos: es web instalable (PWA) y gratis.

## 5. Fases en orden, con horas estimadas
| Fase | Qué se hace | Horas |
|---|---|---|
| 0. Registro | Crear cuenta en Devpost, registrarse en el hackatón que encaje, crear proyecto Firebase (plan Spark, gratis, sin tarjeta) y repositorio público vacío en GitHub | 1 h |
| 1. Alcance en 1 página | Escribir un `PRD.md`: para quién, el único trabajo que hace la app (no pasarse del presupuesto de quincena), pantallas (lista, en tienda, cierre) y la lista de lo que NO lleva | 1 h |
| 2. App a copiar | Elegir en el celular una app de lista de compras que le guste, hacer capturas de sus 3 pantallas principales y decirle a Claude: "clona este diseño, cambia colores y textos a Mandado, no copies su código" | 1 h |
| 3. Base: PWA web simple | Una sola app web para celular (HTML/CSS/JS sin paso de compilación, instalable como PWA), que guarde en el teléfono (localStorage). Publicarla en Firebase Hosting. No empezar con React Native ni con login | 3-4 h |
| 4. Núcleo calculadora | Lista previa por secciones; presupuesto de quincena; en tienda: frutas/verduras por kilo (precio × kilos/gramos), huevo por presentación (6/12/18/30), abarrotes por pieza, carnes por kilo; subtotal por producto, total, total vs. presupuesto, aviso "te estás pasando, ¿qué quitas?". Probar con una lista real de HEB | 9-10 h |
| 5. Ofertas | Modificadores 2x1, 3x2 y combo: marcar qué se lleva gratis, precio del gratis y cuánto se ahorró de verdad. Cierre de cuenta: total gastado vs. presupuesto y qué quitar para bajar | 3-4 h |
| 6. La IA híbrida (mínima, obligatoria solo si el hackatón la pide) | Una sola función: "¿Qué quito para no pasarme?" — con la lista y el presupuesto, la IA sugiere 2-3 cambios (quitar algo o cambiarlo por algo más barato). Usar Firebase AI Logic en modo `PREFER_ON_DEVICE`, con respaldo a Gemini en la nube si el teléfono no tiene Gemini Nano, y mostrar en pantalla si respondió "en el dispositivo" o "en la nube" | 4-5 h |
| 7. Pruebas reales | Probarla en una compra real o simulada completa, en el celular, con datos reales de HEB. Arreglar solo lo que impida terminar la compra; anotar el resto en una lista de "después" | 4 h |
| 8. Entrega | Video demo de 2-3 min grabado en el celular (lista → en tienda → alerta de presupuesto → sugerencia de la IA → cierre), README con qué hace, cómo se instala y cómo se usó la IA, y envío en Devpost. Enviar en la mañana del día de cierre, no en la última hora | 3-4 h |

- Total de horas estimadas: ~30-34 horas.
- Horas por semana disponibles: 20 horas, de lunes a viernes de 8:00 a 12:00.
- Fecha límite real: ninguna por ahora. La del 30 nov 2026 quedó descartada por decisión de Dulce (ver nota al inicio).

## 6. Requisitos técnicos
- Se construye con Claude, copiando el diseño de una app que le guste en el celular. Si Claude lo hace solo, sale feo; si copia, copia bonito (así se hizo Hilván con Canva).
- Web para celular (PWA), HTML/CSS/JS simple, sin compilación. Datos guardados en el teléfono (localStorage).
- Cuentas que hacen falta: Devpost (para el hackatón), GitHub (repositorio público), Firebase (plan Spark gratis, Hosting + AI Logic).
- Sin login en el MVP. Sin cámara obligatoria: la foto del ticket solo se guarda.
- Permisos especiales: ninguno en el MVP.

## 7. Repos de GitHub útiles
Revisados el 13 nov 2026.

| Repo | Qué aporta | Licencia | Cómo se usa |
|---|---|---|---|
| danieltugok/supermkt-list — https://github.com/danieltugok/supermkt-list | El más parecido a lo que hay que construir: PWA para celular, HTML/CSS/JS sin compilación, lista por categorías, lista compartida en tiempo real, login con Google y Firebase (plan Spark gratis), instalable en el teléfono. Aporta la arquitectura completa a imitar y el modelo de datos por producto | Sin LICENSE visible en el repo | Solo referencia de diseño y estructura. No reutilizar su código sin permiso |
| Shopping List Calculator (F-Droid) — https://staging.f-droid.org/en/packages/io.github.buildsbyben.shoppinglistcalc/ | App Android que es casi el núcleo de Mandado: lista, total acumulado, presupuesto y cuánto queda, cálculo por peso y por varias piezas, listas guardadas reutilizables, sin cuenta y sin anuncios. Aporta la lógica de cálculo por kilo y el panel de presupuesto | MIT, verificada en F-Droid | Copiar la lógica, no usarla como base web (es Android nativo). El código fuente está enlazado desde la página de F-Droid |
| grocy/grocy — https://github.com/grocy/grocy | Gestión de despensa y compras para el hogar (PHP + SQLite, PWA, API REST, escaneo de código de barras). Aporta el modelo de datos (producto, cantidad, unidad, lista de compras, stock) y qué pantallas tiene una app madura de este tipo | MIT, verificada | Solo referencia. No usar como base: es un sistema enorme, en PHP, imposible de adaptar en 2 semanas |
| TomBursch/kitchenowl — https://github.com/TomBursch/kitchenowl | Lista de compras y recetas para el hogar, con sincronización en tiempo real entre familiares, gastos compartidos, Flutter + Flask. Aporta cómo se ven las listas compartidas en familia (la red familiar de Mandado, fase posterior) | AGPL-3.0 | Solo referencia, no base. AGPL obliga a compartir el código si se publica el servicio modificado. Además es demasiado grande para 2 semanas |
| Mo3bassia/product-list-with-cart-react-app — https://github.com/Mo3bassia/product-list-with-cart-react-app | Lista de productos con carrito en React, con totales calculados en tiempo real al agregar o quitar productos. Aporta el patrón más simple de "lista + carrito + total en vivo", útil si Claude decide hacerlo en React en vez de HTML simple | Licencia no verificada en la página consultada | Referencia de patrón, no código a reutilizar sin revisar su LICENSE |

Recomendación de ruta: arquitectura de supermkt-list (PWA + HTML/JS simple + Firebase) como la más rápida para una principiante con Claude; lógica de presupuesto y peso, de Shopping List Calculator; modelo de datos, de grocy.

## 8. Qué hackatones u oportunidades le encajan
| Oportunidad | Qué pide | Qué fecha cierra | Qué le falta a este proyecto para entrar |
|---|---|---|---|
| BuildHybridAI 2026, Devpost, Google/Firebase, $30,000 USD | App web o móvil que funcione, con inferencia híbrida con Firebase AI Logic — Gemini Nano en el dispositivo cuando se pueda y Gemini en la nube como respaldo —, repositorio público y video demo. Es 100% en línea | Lunes 30 nov 2026 | La función de IA híbrida de la fase 6. Una calculadora sola, sin IA, no cumple el tema. Decisión de Dulce: NO correrlo en esa fecha, por poco tiempo. Queda como ejemplo de lo que piden este tipo de hackatones |
| (Por llenar) | | | |

- No se anotan fechas de hackatones futuros inventadas. Cuando salga uno nuevo, se revisa su correo de Devpost y se agrega aquí con su fecha real y su fuente.
- Contactos para venderlo / pedir opinión cuando el MVP esté listo: la novia de su hermano (project manager en Soriana, Monterrey), un hermano en Top Human (empresa de recursos humanos que también hace software, para tiendas como HEB y Soriana), y otro hermano ingeniero en software por su cuenta, en el Estado de México. Dulce quiere presentárselo a los tres juntos para que le den opciones de venta y de pitch. Lo que más quiere de ellos: retroalimentación de cómo venderlo, o que uno diga "yo te lo vendo / yo te lo desarrollo / te consigo quien lo haga".

## 9. Riesgos
- Que la apuren con poco tiempo: cualquier imprevisto en casa le come las mañanas. Por eso este plan no tiene fecha límite puesta; se construye cuando haya una oportunidad con tiempo suficiente.
- Que Gemini Nano no funcione en todos los teléfonos: solo está en algunos Android y en Chrome 139+ en computadora. Por eso la fase 6 debe tener respaldo en la nube y mostrar de dónde vino la respuesta; si se diseña "solo en dispositivo", fallará en la demo del jurado.
- Que la idea crezca: login, red familiar, catálogo y leer el ticket con cámara son el proyecto completo, no el MVP. Si se añaden, el plazo se rompe.
- Que se copie código sin licencia: en Devpost el repositorio es público y la licencia se ve. Solo referencia donde no hay licencia, y nada de AGPL como base.
- Si falta tiempo: lo que se puede recortar sin perder el hackatón es la fase 5 (ofertas, dejar solo 2x1). Lo que NO se puede recortar es la fase 6 (IA híbrida), si el hackatón la pide.
- No dejar el envío para la noche del cierre: el video y el README siempre toman más de lo previsto.

## 10. Criterios de listo para construir
- [x] Se sabe para quién es y qué hace en una frase.
- [x] El MVP cabe en la sección 3, sin añadir nada.
- [x] Están escritas las fases, con horas, y el total (~30-34 h) cabe en 20 h por semana en 2 semanas.
- [x] Se sabe con qué se construye (Claude + PWA + Firebase) y qué cuentas hacen falta.
- [ ] Se tiene la app o diseño a copiar, con capturas. — Pendiente: elegirla en el celular cuando se vaya a construir.
- [x] Se sabe qué pide un hackatón de este tipo (IA híbrida) y qué fase lo cubre (fase 6).
- [x] Están anotados los repos, con licencia y cómo se usan.

## 11. Qué falta por decidir
- Precio de venta a tiendas (Soriana, HEB): no definido.
- Qué app de lista de compras copiar como diseño: pendiente de elegir en el celular, con capturas de sus 3 pantallas principales.
- Qué hackatón concreto se va a correr: ninguno por ahora; estar al pendiente de los correos de Devpost.
- Si el MVP se presenta primero a los tres contactos (novia de su hermano, hermano de Top Human, hermano ingeniero) antes o después de un hackatón: pendiente.
