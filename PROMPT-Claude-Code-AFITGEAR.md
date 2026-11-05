# Proyecto: AFITGEAR Gestión — sistema de gestión integral

Sos mi desarrollador. Quiero que construyas una web app de gestión completa para mi negocio. No soy programador: explicame cada paso que yo tenga que hacer (crear cuentas, pegar claves, etc.) en lenguaje simple y de a uno por vez.

**Antes de escribir código:** leé todos los archivos de esta carpeta, armá un plan por fases (modelo de datos + pantallas) y mostrámelo para que lo apruebe. Después avanzá fase por fase y al final de cada una mostrame qué quedó funcionando y verificá que todo ande (probalo vos en el navegador).

---

## 1. El negocio

- **Marca:** AFITGEAR — Artículos deportivos (equipamiento de entrenamiento funcional, fitness, yoga, coordinación).
- **Usuario:** solo yo (Facu). Uso principal desde el **celular**, también desde la compu. Los datos tienen que estar sincronizados entre ambos.
- **Canales de venta:** redes sociales (Instagram), Facebook Marketplace, WhatsApp. Estoy armando una tienda en Tiendanube (todavía inactiva).
- **Modalidad:** trabajo **por encargo** (preparación: 1 semana). Tengo muy poco stock físico.
- **Entregas:** retiro sin costo en la estación de tren o en la plaza de Monte Grande (coordinando día y horario), envío a domicilio en auto (más rápido) o por correo (más económico), con costo según ubicación.
- **Pagos:** efectivo o transferencia.
- **Contacto:** WhatsApp 11 3046-0671 · Instagram @afit_gear · afit.gear25@gmail.com

## 2. Archivos de esta carpeta (fuente de datos)

- `AFITGEAR · Costos y precios.html` → mi sitio actual de costos. Dentro del `<script>` está la constante `SEED` con **proveedores, 17 categorías (en orden) y 90 productos** (costo, proveedor, categoría, multiplicadores de los 3 precios, precio fijo opcional, precio de Mercado Libre opcional, nota). **Importá todo esto.** También mirá qué funciones tiene (edición, actualización masiva de costos %, catálogo PDF, copiar para WhatsApp, CSV, respaldo): el sistema nuevo tiene que tener todo eso y mejor.
- `AFITGEAR · Mensajes.html` → mi sitio de mensajes rápidos (~60 mensajes agrupados en Atención, Precios, Entregas, Catálogo, Ampliar pedido, Sin stock, Cierre). **Importá todos los mensajes** (excepciones abajo).
- `AFIT PROYEC LOGO.png` → logo oficial.
- Fotos de productos (.jpeg, .png, .heic).

## 3. Reglas de negocio (importantes)

### Precios por cantidad — se calculan POR PRODUCTO
Cada producto tiene 3 precios:
1. **Unitario:** llevando 1 unidad de ese producto.
2. **2 a 9 unidades** del mismo producto: baja el precio de cada unidad.
3. **10 o más unidades** del mismo producto: baja más todavía.

La escala depende de la cantidad **de ese mismo producto**, no del total del pedido. Ejemplo: 1 shampoo + 1 crema + 1 acondicionador → los tres a precio unitario. 12 del mismo producto + 1 de otro → los 12 a precio "10 o más" y el otro a unitario.
En cada pedido tiene que poder sobrescribir a mano el precio de una línea (precio especial), sin cambiar la regla general.

### Cálculo de precios
- Precio = costo × multiplicador (uno por cada escala). Ej: ×2,0 / ×1,8 / ×1,5.
- Cada escala puede tener además un **precio fijo** opcional que reemplaza al multiplicador.
- Si cambio un costo, los precios se recalculan solos (salvo los fijos).
- Cada proveedor tiene un **recargo de envío (%)** sobre el costo (Gold Fitness: 10% — su envío es $17.000 por pedido; Fer: 0%, retiro y pago después). Por defecto el recargo **no se suma al precio**, solo se descuenta de la ganancia (opción en Ajustes para sumarlo, como en mi sitio actual).
- **Margen** = (precio − costo con envío) / precio. Margen mínimo aceptable configurable (hoy 15%). Mostrar margen y ganancia en $ al lado de cada precio con colores: verde OK, amarillo bajo el mínimo, rojo sin ganancia o pérdida. Hay productos (cajones de fenólico grandes en precio 10+) que quedan con margen bajo: está bien, que se marquen en amarillo.
- Las mancuernas se venden **por par** (colores rosa y negro). Que se pueda indicar en la descripción del producto y salga en el catálogo.

### Proveedores
- Cada producto pertenece a un solo proveedor (no se repiten productos entre proveedores).
- Proveedores: **Gold Fitness y Boxeo**, **Fer**, **Iniciativa Deportiva** (creado pero **sin productos todavía**; los voy a cargar yo después desde la app).
- Guardar **historial de costos** de cada producto (fecha + costo anterior + costo nuevo), para ver aumentos.

## 4. Decisiones ya tomadas sobre los datos

- **NO importar los productos de fútbol** que aparecen solo en el sitio de mensajes (Pelota profesional azul N5, Pelota profesional roja N5, Cronómetro deportivo, Botella caramañola Gatorade, Bolso pelotero). Ya no los vendo. Eliminá también los mensajes que los mencionan (por ejemplo "Pack fútbol / entrenador") o sacales esas menciones.
- El **Kit de 20 kg (discos lisos) con costo $18.000 es correcto**, no lo cambies.
- Las **listas de catálogo por categoría** del sitio de mensajes (los mensajes "Lista: …" y "Mancuernas (respuesta rápida)") **no se copian como texto fijo**: tienen que generarse automáticamente desde los precios actuales de la base de datos.

## 5. Fotos de productos

- Asociá cada foto con su producto por nombre (ojo: hay errores de tipeo, ej. "Mancerunas", "Pelpoota", "slalon", "Bnada", "equilibro").
- Convertí las **.heic/.HEIC** a un formato web y **comprimí/redimensioná** todas (webp o jpg, ~1200px máx.) para que la app cargue rápido. **No borres ni modifiques los archivos originales.**
- Si hay varias fotos del mismo producto, usá la mejor como principal y guardá las otras como galería.
- Las fotos grupales (`Mancuernas.jpeg`, `Pesas rusas.jpeg`, `Fitness .jpeg`, `Coordinacion y salto.jpeg`, `Barras y tobilleras.jpeg`, `Discos con agarre y kits agarre.jpeg`, `Discos lisos y kits lisos.jpeg`) usalas como **portada de su categoría**.
- **NO incluyas** las fotos de productos de Iniciativa Deportiva (todavía no los vendo): arco de fútbol, miniarco, bochas de hockey, pelotas de handball/vóley/básquet, pizarra táctica, inflador, protector cervical, medicinal balls de goma y de pique, bolso pelotero, y similares.
- Las fotos con nombres genéricos (`IMG_1096.PNG`, códigos largos tipo `29786010-….JPG.jpeg`, `monaco quality.jpeg`) miralas y si podés identificar el producto, asocialas; si no, dejalas sin asignar.
- Al terminar, dame una **lista de fotos sin asignar** y de **productos sin foto**, y que desde la app yo pueda subir o cambiar la foto de cualquier producto.

## 6. Módulos que tiene que tener

Todo tiene que ser **editable desde la app** (crear, editar, duplicar, pausar/archivar, eliminar). Nada de pantallas "quietas".

1. **Inicio / Panel:** ventas y ganancia real del mes, pedidos pendientes por estado, saldos por cobrar, productos más vendidos, alertas (márgenes bajos, pedidos atrasados).
2. **Productos:** listado con buscador y filtros (categoría, proveedor, margen bajo, activos/pausados), foto, costo, costo con envío, los 3 precios con margen. Ficha con vista previa en vivo del margen al editar. Duplicar producto. Pausar sin borrar. Reordenar productos dentro de la categoría (orden del catálogo). **Edición masiva:** subir/bajar costos o precios un % por proveedor, categoría o selección.
3. **Categorías:** crear, renombrar, reordenar, eliminar (solo si está vacía), foto de portada.
4. **Proveedores:** datos de contacto, recargo de envío (con la calculadora envío ÷ pedido típico), notas, mínimo de compra, forma de pago, demora de entrega, productos de cada uno.
5. **Pedidos (el corazón del sistema, porque vendo por encargo):**
   - Cliente, canal de venta (Instagram, Marketplace, WhatsApp, Tiendanube, otro), productos y cantidades con **escala de precio automática por producto**, precio especial manual opcional, descuento, costo y tipo de entrega (retiro estación/plaza Monte Grande, auto, correo), medio de pago.
   - **Estados:** Consulta/Presupuesto → Seña recibida → Pedido al proveedor → Recibido → Listo para entregar → Entregado → Cobrado (y Cancelado).
   - Registrar **seña y pagos parciales**, ver saldo pendiente.
   - Generar **presupuesto en PDF con mi marca** y **texto para WhatsApp** listo para copiar.
   - Sugerencia automática: "si llevás X más llegás al precio de 2 a 9 / 10 o más".
   - Fecha prometida de entrega (por defecto +7 días) y aviso si se atrasa.
6. **Lista de compra a proveedores:** a partir de los pedidos confirmados que todavía no pedí, armar automáticamente la lista **agrupada por proveedor** (producto + cantidad total + costo total), copiable para WhatsApp, y marcar como "pedido al proveedor".
7. **Clientes:** nombre, teléfono, zona, tipo (particular / profe / gimnasio / escuela / mayorista), notas, historial de pedidos, total comprado y saldo que me deben (cuenta corriente).
8. **Mensajes rápidos:** todos los mensajes importados, por grupo, con buscador, **tocar = copiar**. Crear/editar/borrar/reordenar mensajes y grupos. Campos variables ([nombre], [total], [cantidad], [producto], [localidad], etc.) que se completen solos cuando abro el mensaje desde un pedido o cliente. Las listas de precios por categoría se generan en vivo desde la base.
9. **Catálogo:**
   - **PDF con el logo y los colores de la marca**, con o sin fotos, eligiendo qué precios mostrar (unitario / 2-9 / 10+), por categoría o completo, con título personalizado (ej. nombre del cliente) y pie con condiciones (encargo 1 semana, entregas en Monte Grande, envíos con costo, efectivo o transferencia).
   - **Link público de catálogo** (solo lectura, sin costos ni márgenes, solo productos activos) para mandar por WhatsApp/redes.
   - Copiar catálogo como texto para WhatsApp y exportar CSV/Excel.
10. **Gastos y ganancias:** gastos (envíos, packaging, comisiones, publicidad, otros), ganancia real por pedido y por mes (venta − costo − envío proveedor − gastos), ganancia por categoría, proveedor y canal.
11. **Stock (simple):** cantidad en mano opcional por producto para lo poco que tengo físico; que se descuente al entregar un pedido.
12. **Ajustes:** margen mínimo, recargo de envío al precio sí/no, datos del negocio, **datos de transferencia** (tomalos del mensaje "Datos de transferencia" del sitio de mensajes; guardalos en Ajustes, no hardcodeados), texto del pie del catálogo, **respaldo** (descargar/restaurar JSON) y **exportar todo a Excel**.

## 7. Diseño y experiencia

- **Marca:** usar el logo `AFIT PROYEC LOGO.png`. Colores del logo: azul **#0D57A3** (principal) y celeste **#A9CBF7** (secundario), blanco. Tipografía bold, deportiva y moderna (ej. Montserrat o similar). Que se vea profesional y dinámico.
- **Mobile-first**, rápida, botones grandes, navegación inferior en celular. También cómoda en compu.
- **Instalable** en el celular como app (PWA, ícono con el logo).
- Modo claro y oscuro.
- Todo en **español de Argentina**, montos en pesos con formato `$ 12.345`.
- Confirmación antes de borrar cualquier cosa.

## 8. Tecnología

- **Next.js (App Router) + TypeScript + Tailwind**, base de datos **Supabase** (Postgres + Auth + Storage para las fotos), deploy en **Vercel**. Usá los planes gratuitos.
- **Login** (solo mi usuario). Las tablas protegidas con Row Level Security. La única parte pública es el link del catálogo (sin costos).
- Script de **importación** reproducible de productos, proveedores, categorías, mensajes y fotos.
- Guiame paso a paso para crear las cuentas de Supabase y Vercel y configurar las claves (nunca subas claves al repositorio).
- Pensá el modelo de datos para que más adelante se pueda **sincronizar con Tiendanube** (productos, precios, stock) y agregar **facturación ARCA**. No los hagas ahora, solo dejá la estructura preparada.

## 9. Fases sugeridas

1. Plan + modelo de datos (esperar mi aprobación).
2. Proyecto base, login, diseño de marca, importación de datos y fotos, Productos / Categorías / Proveedores con edición completa y edición masiva.
3. Catálogo PDF + link público + texto WhatsApp.
4. Pedidos, clientes, lista de compra a proveedores.
5. Mensajes rápidos.
6. Gastos, ganancias y panel de inicio. Stock simple.
7. PWA, deploy a Vercel, prueba completa desde el celular, y una guía corta de uso para mí.

Al final de cada fase: verificá que funcione, contame en simple qué quedó hecho y qué tengo que probar yo.
