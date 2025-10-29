<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Latasu - Tienda Tradicional Costarricense</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            background-color: #000000;
            color: white;
            overflow-x: hidden;
        }

        /* Header/Navbar */
        header {
            background-color: #000000;
            padding: 20px 0;
            position: fixed;
            top: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: 0 4px 15px rgba(255,0,0,0.3);
            border-bottom: 3px solid #ff0000;
        }

        .navbar {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 40px;
            flex-wrap: wrap;
            gap: 20px;
        }

        .logo {
            font-size: 42px;
            font-weight: bold;
            letter-spacing: 4px;
            font-family: 'Georgia', serif;
            text-transform: uppercase;
            cursor: pointer;
        }

        .logo .la { color: #ff0000; }
        .logo .ta { color: #ffffff; }
        .logo .su { color: #2196F3; }

        .nav-center {
            display: flex;
            gap: 25px;
            list-style: none;
            align-items: center;
        }

        .nav-center a {
            color: #ffffff;
            text-decoration: none;
            font-size: 16px;
            font-weight: 600;
            transition: all 0.3s;
            padding: 8px 15px;
            border-radius: 8px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .nav-center a:hover {
            background: rgba(255,255,255,0.1);
            transform: translateY(-2px);
        }

        .nav-actions {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .btn-login {
            background: transparent;
            color: white;
            border: 2px solid #2196F3;
            padding: 8px 20px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            transition: all 0.3s;
            text-transform: uppercase;
            font-family: 'Georgia', serif;
        }

        .btn-login:hover {
            background: #2196F3;
            transform: scale(1.05);
        }

        .carrito-btn {
            position: relative;
            background: transparent;
            border: none;
            font-size: 28px;
            cursor: pointer;
            transition: all 0.3s;
            color: white;
        }

        .carrito-btn:hover {
            transform: scale(1.1);
        }

        .carrito-badge {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #ff0000;
            color: white;
            border-radius: 50%;
            width: 22px;
            height: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
            font-family: Arial;
        }

        .usuario-info {
            display: none;
            align-items: center;
            gap: 12px;
            color: white;
            font-size: 14px;
        }

        .usuario-info.active {
            display: flex;
        }

        .btn-logout {
            background: #ff0000;
            color: white;
            border: none;
            padding: 6px 15px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: bold;
            font-size: 12px;
            transition: all 0.3s;
            text-transform: uppercase;
        }

        .btn-logout:hover {
            background: #cc0000;
            transform: scale(1.05);
        }

        /* Bandera decorativa */
        .bandera-decorativa {
            position: fixed;
            top: 0;
            right: 0;
            width: 400px;
            height: 250px;
            background: linear-gradient(135deg, 
                #2196F3 0%, 
                #2196F3 25%, 
                #ffffff 25%, 
                #ffffff 50%, 
                #ff0000 50%, 
                #ff0000 100%);
            clip-path: polygon(100% 0, 0 0, 100% 100%);
            opacity: 0.3;
            z-index: 0;
            pointer-events: none;
        }

        .bandera-decorativa-izq {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 400px;
            height: 250px;
            background: linear-gradient(135deg, 
                #ff0000 0%, 
                #ff0000 25%, 
                #ffffff 25%, 
                #ffffff 50%, 
                #2196F3 50%, 
                #2196F3 100%);
            clip-path: polygon(0 100%, 0 0, 100% 100%);
            opacity: 0.3;
            z-index: 0;
            pointer-events: none;
        }

        /* Sección */
        section {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 120px 40px 80px 40px;
            position: relative;
        }

        /* Bienvenida */
        #bienvenida {
            background: linear-gradient(135deg, #000000 0%, #1a1a1a 50%, #000000 100%);
            text-align: center;
        }

        #bienvenida h1 {
            font-size: 88px;
            margin-bottom: 40px;
            letter-spacing: 4px;
            color: #ffffff;
            text-transform: uppercase;
        }

        #bienvenida h2 {
            font-size: 58px;
            margin-bottom: 30px;
            letter-spacing: 3px;
        }

        #bienvenida h2 .la { color: #ff0000; }
        #bienvenida h2 .ta { color: #ffffff; }
        #bienvenida h2 .su { color: #2196F3; }

        .subtitulo {
            font-size: 26px;
            color: #cccccc;
            margin-bottom: 60px;
            max-width: 800px;
            line-height: 1.6;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .perezoso-ascii {
            font-size: 120px;
            filter: drop-shadow(0 0 20px rgba(255,255,255,0.3));
            margin: 40px 0;
        }

        /* Sección de Categorías */
        .seccion-categoria {
            background: #000000;
            padding: 100px 40px;
        }

        .categoria-header {
            text-align: center;
            margin-bottom: 80px;
        }

        .categoria-header h2 {
            font-size: 72px;
            margin-bottom: 20px;
            letter-spacing: 5px;
            text-transform: uppercase;
            position: relative;
            display: inline-block;
        }

        .categoria-header h2::after {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 0;
            width: 100%;
            height: 4px;
            background: currentColor;
        }

        /* Grid de productos */
        .productos-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 50px;
            max-width: 1400px;
            margin: 0 auto;
        }

        .producto-card {
            background: transparent;
            border: 3px solid white;
            border-radius: 20px;
            padding: 40px;
            position: relative;
            transition: all 0.4s;
            text-align: center;
        }

        .producto-icono {
            font-size: 80px;
            margin-bottom: 25px;
            filter: drop-shadow(0 4px 10px rgba(255,255,255,0.3));
        }

        .producto-nombre {
            font-size: 32px;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .producto-descripcion {
            font-size: 18px;
            color: #cccccc;
            margin-bottom: 30px;
            line-height: 1.6;
        }

        .producto-precio {
            font-size: 36px;
            font-weight: bold;
            margin-bottom: 30px;
        }

        .btn-comprar {
            width: 100%;
            padding: 18px;
            font-size: 20px;
            font-weight: bold;
            border: 3px solid white;
            background: transparent;
            color: white;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 2px;
            font-family: 'Georgia', serif;
        }

        /* Colores por categoría */
        #chocolates {
            background: linear-gradient(180deg, #000000 0%, #0a1929 100%);
        }

        #chocolates .categoria-header h2 { color: #2196F3; }
        #chocolates .producto-card { border-color: #2196F3; }
        #chocolates .producto-card:hover {
            background: rgba(33, 150, 243, 0.1);
            transform: translateY(-10px);
        }
        #chocolates .producto-precio { color: #2196F3; }
        #chocolates .btn-comprar:hover {
            background: #2196F3;
            border-color: #2196F3;
        }

        #cajetas {
            background: linear-gradient(180deg, #0a1929 0%, #1a0000 100%);
        }
        #cajetas .categoria-header h2 { color: #ff0000; }
        #cajetas .producto-card { border-color: #ff0000; }
        #cajetas .producto-card:hover {
            background: rgba(255, 0, 0, 0.1);
            transform: translateY(-10px);
        }
        #cajetas .producto-precio { color: #ff0000; }
        #cajetas .btn-comprar:hover {
            background: #ff0000;
            border-color: #ff0000;
        }

        #surtidos {
            background: linear-gradient(180deg, #1a0000 0%, #0a0a0a 100%);
        }
        #surtidos .categoria-header h2 { color: #ffffff; }
        #surtidos .producto-card:hover {
            background: rgba(255, 255, 255, 0.05);
            transform: translateY(-10px);
        }
        #surtidos .producto-precio { color: #ffffff; }
        #surtidos .btn-comprar:hover {
            background: #ffffff;
            color: #000000;
        }

        #caseros {
            background: linear-gradient(180deg, #0a0a0a 0%, #000000 100%);
        }
        #caseros .categoria-header h2 { color: #2196F3; }
        #caseros .producto-card { border-color: #2196F3; }
        #caseros .producto-card:hover {
            background: rgba(33, 150, 243, 0.1);
            transform: translateY(-10px);
        }
        #caseros .producto-precio { color: #2196F3; }
        #caseros .btn-comprar:hover {
            background: #2196F3;
            border-color: #2196F3;
        }

        /* Modal Base */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.95);
            z-index: 3000;
            justify-content: center;
            align-items: center;
            overflow-y: auto;
            padding: 20px;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: linear-gradient(135deg, #1a1a1a 0%, #000000 100%);
            padding: 40px;
            border-radius: 20px;
            max-width: 550px;
            width: 100%;
            border: 4px solid white;
            box-shadow: 0 0 40px rgba(255,255,255,0.3);
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-content h3 {
            font-size: 32px;
            margin-bottom: 25px;
            color: #ffffff;
            letter-spacing: 2px;
            text-transform: uppercase;
            text-align: center;
        }

        .form-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
        }

        .tab-btn {
            flex: 1;
            padding: 12px;
            background: transparent;
            border: 2px solid #2196F3;
            color: white;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.3s;
            text-transform: uppercase;
            font-family: 'Georgia', serif;
        }

        .tab-btn.active {
            background: #2196F3;
        }

        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 14px;
            color: #ffffff;
            font-weight: bold;
            text-transform: uppercase;
        }

        .form-group input {
            width: 100%;
            padding: 12px;
            font-size: 15px;
            border: 2px solid #2196F3;
            background: rgba(255,255,255,0.1);
            color: white;
            border-radius: 8px;
            font-family: 'Georgia', serif;
        }

        .form-group input:focus {
            outline: none;
            border-color: #ff0000;
            background: rgba(255,255,255,0.15);
        }

        .modal-botones {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 25px;
        }

        .btn-modal {
            padding: 14px 35px;
            font-size: 16px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
            text-transform: uppercase;
            font-family: 'Georgia', serif;
        }

        .btn-primary {
            background-color: #4CAF50;
            color: white;
        }

        .btn-primary:hover {
            background-color: #45a049;
            transform: scale(1.05);
        }

        .btn-secondary {
            background-color: transparent;
            color: white;
            border: 3px solid #ff0000;
        }

        .btn-secondary:hover {
            background-color: #ff0000;
        }

        /* Carrito Panel */
        .carrito-panel {
            position: fixed;
            right: -450px;
            top: 0;
            width: 450px;
            height: 100vh;
            background: linear-gradient(135deg, #1a1a1a 0%, #000000 100%);
            border-left: 4px solid #2196F3;
            z-index: 2000;
            transition: right 0.4s;
            overflow-y: auto;
            padding: 25px;
        }

        .carrito-panel.active {
            right: 0;
        }

        .carrito-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 3px solid #2196F3;
        }

        .carrito-header h3 {
            font-size: 28px;
            color: #2196F3;
            text-transform: uppercase;
        }

        .btn-close-carrito {
            background: transparent;
            border: none;
            font-size: 30px;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-close-carrito:hover {
            color: #ff0000;
        }

        .carrito-item {
            background: rgba(255,255,255,0.05);
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 12px;
            border: 2px solid rgba(255,255,255,0.1);
        }

        .carrito-item-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }

        .carrito-item-nombre {
            font-size: 18px;
            font-weight: bold;
            color: #2196F3;
        }

        .carrito-item-precio {
            font-size: 20px;
            font-weight: bold;
            color: #ff0000;
        }

        .carrito-item-acciones {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .btn-cantidad {
            background: #2196F3;
            border: none;
            color: white;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            font-size: 18px;
            cursor: pointer;
        }

        .cantidad-numero {
            font-size: 18px;
            font-weight: bold;
            min-width: 30px;
            text-align: center;
        }

        .btn-eliminar {
            background: #ff0000;
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 12px;
            margin-left: auto;
        }

        .carrito-total {
            padding: 20px;
            background: rgba(33, 150, 243, 0.1);
            border-radius: 12px;
            margin: 20px 0;
            border: 3px solid #2196F3;
            text-align: center;
        }

        .carrito-total-label {
            font-size: 20px;
            font-weight: bold;
            text-transform: uppercase;
        }

        .carrito-total-precio {
            font-size: 36px;
            font-weight: bold;
            color: #4CAF50;
            margin-top: 8px;
        }

        .btn-checkout {
            width: 100%;
            padding: 16px;
            background: #4CAF50;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            font-family: 'Georgia', serif;
        }

        .btn-checkout:hover {
            background: #45a049;
        }

        .carrito-vacio {
            text-align: center;
            padding: 50px 20px;
            color: #666;
        }

        .carrito-vacio-icon {
            font-size: 60px;
            margin-bottom: 15px;
        }

        /* Página Gracias */
        .gracias-page {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100vh;
            background: linear-gradient(135deg, #000000 0%, #1a1a1a 50%, #000000 100%);
            z-index: 4000;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .gracias-page.active {
            display: flex;
        }

        .gracias-icono {
            font-size: 120px;
        }

        .gracias-titulo {
            font-size: 60px;
            margin: 25px 0;
            color: #4CAF50;
            text-transform: uppercase;
            letter-spacing: 4px;
        }

        .gracias-subtitulo {
            font-size: 32px;
            color: #ffffff;
            margin-bottom: 15px;
        }

        .gracias-mensaje {
            font-size: 20px;
            color: #cccccc;
            max-width: 600px;
            margin: 0 auto 40px;
            line-height: 1.6;
        }

        .btn-volver-inicio {
            padding: 18px 45px;
            background: #2196F3;
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 20px;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            font-family: 'Georgia', serif;
        }

        .btn-volver-inicio:hover {
            background: #1976D2;
        }

        /* Footer */
        footer {
            background: #000000;
            text-align: center;
            padding: 50px 20px;
            border-top: 3px solid #ff0000;
        }

        footer p {
            font-size: 18px;
            color: #cccccc;
        }

        /* Responsive */
        @media (max-width: 968px) {
            .logo { font-size: 32px; }
            .nav-center { display: none; }
            #bienvenida h1 { font-size: 48px; }
            #bienvenida h2 { font-size: 36px; }
            .categoria-header h2 { font-size: 42px; }
            .productos-grid { grid-template-columns: 1fr; }
            .carrito-panel { width: 100%; right: -100%; }
        }
    </style>
</head>
<body>
    <div class="bandera-decorativa"></div>
    <div class="bandera-decorativa-izq"></div>

    <header>
        <nav class="navbar">
            <div class="logo" onclick="scrollToTop()">
                <span class="la">LA</span><span class="ta">TA</span><span class="su">SU</span>
            </div>
            <ul class="nav-center">
                <li><a href="#chocolates">Chocolates</a></li>
                <li><a href="#cajetas">Cajetas</a></li>
                <li><a href="#surtidos">Surtidos</a></li>
                <li><a href="#caseros">Caseros</a></li>
            </ul>
            <div class="nav-actions">
                <div class="usuario-info" id="usuarioInfo">
                    <span id="usuarioNombre"></span>
                    <button class="btn-logout" onclick="cerrarSesion()">Salir</button>
                </div>
                <button class="btn-login" id="btnLogin" onclick="abrirModalLogin()">Distribuidores</button>
                <button class="carrito-btn" onclick="toggleCarrito()">
                    🛒
                    <span class="carrito-badge" id="carritoBadge">0</span>
                </button>
            </div>
        </nav>
    </header>

    <section id="bienvenida">
        <h1>¡BIENVENIDO!</h1>
        <h2>A <span class="la">LA</span><span class="ta">TA</span><span class="su">SU</span></h2>
        <p class="subtitulo">Tu tienda tradicional costarricense a tu alcance</p>
        <div class="perezoso-ascii">🦥</div>
    </section>

    <section id="chocolates" class="seccion-categoria">
        <div class="categoria-header">
            <h2>CHOCOLATES</h2>
        </div>
        <div class="productos-grid">
            <div class="producto-card">
                <div class="producto-icono">🍫</div>
                <div class="producto-nombre">Negro</div>
                <p class="producto-descripcion">Chocolate negro de la más alta calidad</p>
                <p class="producto-precio">₡3,500</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Chocolate Negro', 3500, '🍫')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">🎨</div>
                <div class="producto-nombre">Artesanal</div>
                <p class="producto-descripcion">Elaborado con ingredientes locales</p>
                <p class="producto-precio">₡4,200</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Chocolate Artesanal', 4200, '🎨')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">⭐</div>
                <div class="producto-nombre">Chocolates Sibo</div>
                <p class="producto-descripcion">Variedad premium de chocolates</p>
                <p class="producto-precio">₡5,000</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Chocolates Sibo', 5000, '⭐')">Agregar al Carrito</button>
            </div>
        </div>
    </section>

    <section id="cajetas" class="seccion-categoria">
        <div class="categoria-header">
            <h2>CAJETAS</h2>
        </div>
        <div class="productos-grid">
            <div class="producto-card">
                <div class="producto-icono">🥥</div>
                <div class="producto-nombre">Cajetas de Coco</div>
                <p class="producto-descripcion">Dulces tradicionales con coco fresco</p>
                <p class="producto-precio">₡2,200</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Cajetas de Coco', 2200, '🥥')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">🍮</div>
                <div class="producto-nombre">Cajetas de Dulce de Leche</div>
                <p class="producto-descripcion">Con auténtico dulce de leche</p>
                <p class="producto-precio">₡2,500</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Cajetas de Dulce de Leche', 2500, '🍮')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">🥛</div>
                <div class="producto-nombre">Cajetas de Leche</div>
                <p class="producto-descripcion">Clásicas cajetas al estilo tico</p>
                <p class="producto-precio">₡1,800</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Cajetas de Leche', 1800, '🥛')">Agregar al Carrito</button>
            </div>
        </div>
    </section>

    <section id="surtidos" class="seccion-categoria">
        <div class="categoria-header">
            <h2>SURTIDOS</h2>
        </div>
        <div class="productos-grid">
            <div class="producto-card">
                <div class="producto-icono">🍬</div>
                <div class="producto-nombre">Melcocha</div>
                <p class="producto-descripcion">Dulce tradicional con melaza de caña</p>
                <p class="producto-precio">₡1,500</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Melcocha', 1500, '🍬')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">🥚</div>
                <div class="producto-nombre">Huevitos de Chocolate</div>
                <p class="producto-descripcion">Delicias de chocolate rellenas</p>
                <p class="producto-precio">₡3,200</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Huevitos de Chocolate', 3200, '🥚')">Agregar al Carrito</button>
            </div>
            <div class="producto-card">
                <div class="producto-icono">🍯</div>
                <div class="producto-nombre">Turrones</div>
                <p class="producto-descripcion">Turrones artesanales con miel</p>
                <p class="producto-precio">₡4,500</p>
                <button class="btn-comprar" onclick="agregarAlCarrito('Turrones', 4500, '🍯')">Agregar al Carrito</button>
            </div>
        </div>
    </section>

    <section id="caseros" class="seccion-categoria">
        <div class="categoria-header">
            <h2
