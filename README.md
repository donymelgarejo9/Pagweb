<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Tienda de Zapatillas</title>
    <!-- Agrega la biblioteca de generación de códigos QR -->
    <script src="https://cdn.rawgit.com/kazuhikoarase/qrcode-generator/gh-pages/js/qrcode.js"></script>
</head>
<body>
    <h1>Bienvenido a la Tienda de Zapatillas</h1>

    <!-- Inventario de productos -->
    <div class="producto">
        <h2>Zapatilla 1</h2>
        <label for="precio1">Precio: $</label>
        <input type="number" id="precio1" value="50.00" onchange="calcularTotal()">
        <input type="checkbox" id="seleccion1" onclick="calcularTotal()">
    </div>

    <div class="producto">
        <h2>Zapatilla 2</h2>
        <label for="precio2">Precio: $</label>
        <input type="number" id="precio2" value="60.00" onchange="calcularTotal()">
        <input type="checkbox" id="seleccion2" onclick="calcularTotal()">
    </div>

    <!-- Carrito de Compra -->
    <h2>Carrito de Compra</h2>
    <ul id="carrito">
        <!-- Elementos seleccionados aparecerán aquí -->
    </ul>
    <p>Total: $<span id="total">0.00</span></p>

    <!-- Botón para pagar -->
    <button id="botonPagar" onclick="generarCodigoQR()">Pagar</button>

    <!-- Contenedor para el código QR -->
    <div id="codigoQR"></div>

    <!-- Script para calcular el total y generar un código QR con información -->
    <script>
        let codigoSeguimiento = '';
        let productosSeleccionados = [];

        function calcularTotal() {
            let total = 0;
            productosSeleccionados = [];

            if (document.getElementById('seleccion1').checked) {
                total += parseFloat(document.getElementById('precio1').value);
                productosSeleccionados.push('Zapatilla 1');
            }

            if (document.getElementById('seleccion2').checked) {
                total += parseFloat(document.getElementById('precio2').value);
                productosSeleccionados.push('Zapatilla 2');
            }

            document.getElementById('total').textContent = total.toFixed(2);
        }

        function generarCodigoQR() {
            const infoCompra = {
                total: parseFloat(document.getElementById('total').textContent),
                productosSeleccionados: productosSeleccionados
            };

            const infoCompraJSON = JSON.stringify(infoCompra);

            // Genera el código QR con la información de compra
            const qrcode = new QRCode(document.getElementById("codigoQR"), {
                text: infoCompraJSON,
                width: 128,
                height: 128
            });

            // Puedes mostrar el código de seguimiento (opcional)
            codigoSeguimiento = generarCodigoSeguimiento();
            console.log("Código de seguimiento: " + codigoSeguimiento);
        }

        function generarCodigoSeguimiento() {
            // Aquí puedes generar un código de seguimiento único (por ejemplo, un UUID)
            // Puedes utilizar bibliotecas como 'uuid' o generar tu propio esquema de códigos únicos.
            return "CódigoÚnico123"; // Reemplaza esto con tu lógica de generación de códigos únicos.
        }
    </script>
</body>
</html>
