import React, { useState, useEffect } from 'react';
import { ShoppingCart, User, Menu, X, Phone, Mail, MapPin } from 'lucide-react';

const PRODUCTS = [
  { id: 1, name: "Tapitas de dulce", price: 500, emoji: "🍯", category: "dulces" },
  { id: 2, name: "Confites Gallito", price: 300, emoji: "🍬", category: "confites" },
  { id: 3, name: "Cajetas de leche", price: 600, emoji: "🍫", category: "chocolates" },
  { id: 4, name: "Cocadas", price: 450, emoji: "🥥", category: "dulces" },
  { id: 5, name: "Tapa de dulce con maní", price: 700, emoji: "🥜", category: "especialidades" },
  { id: 6, name: "Melcochas", price: 400, emoji: "🍭", category: "confites" },
  { id: 7, name: "Turrón criollo", price: 800, emoji: "🧁", category: "especialidades" },
  { id: 8, name: "Dulce de camote", price: 550, emoji: "🍠", category: "dulces" },
  { id: 9, name: "Dulce de banano", price: 500, emoji: "🍌", category: "dulces" },
  { id: 10, name: "Jalea de guayaba", price: 900, emoji: "🍈", category: "dulces" },
  { id: 11, name: "Dulce de leche tradicional", price: 1200, emoji: "🥛", category: "especialidades" },
  { id: 12, name: "Empanaditas de chiverre", price: 350, emoji: "🌰", category: "dulces" },
  { id: 13, name: "Periquitos", price: 250, emoji: "🍪", category: "confites" },
  { id: 14, name: "Cajeta de coco con dulce de tapa", price: 750, emoji: "🍮", category: "especialidades" },
  { id: 15, name: "Maní garapiñado", price: 600, emoji: "🥜", category: "confites" },
  { id: 16, name: "Dulce de tapa con jengibre", price: 850, emoji: "🍯", category: "especialidades" },
  { id: 17, name: "Tabletas de cacao", price: 1500, emoji: "🍫", category: "chocolates" },
  { id: 18, name: "Dulce de tamarindo", price: 400, emoji: "🧃", category: "dulces" },
  { id: 19, name: "Confites de limón", price: 200, emoji: "🍋", category: "confites" },
  { id: 20, name: "Confites de manzana roja", price: 250, emoji: "🍎", category: "confites" },
  { id: 21, name: "Dulce de mango verde", price: 650, emoji: "🥭", category: "dulces" },
  { id: 22, name: "Dulce de papaya", price: 550, emoji: "🍈", category: "dulces" },
  { id: 23, name: "Dulce de piña", price: 600, emoji: "🍍", category: "dulces" },
  { id: 24, name: "Cajeta envinada", price: 1800, emoji: "🍫", category: "especialidades" },
  { id: 25, name: "Cocadas negras", price: 500, emoji: "🥥", category: "dulces" },
  { id: 26, name: "Rompope artesanal", price: 2500, emoji: "🧁", category: "especialidades" },
  { id: 27, name: "Bolitas de cacao con azúcar", price: 800, emoji: "🍫", category: "chocolates" },
  { id: 28, name: "Dulce de leche cortado", price: 1100, emoji: "🍮", category: "dulces" },
  { id: 29, name: "Banano pasado con miel", price: 700, emoji: "🍌", category: "dulces" },
  { id: 30, name: "Mielcita Gallito", price: 300, emoji: "🍯", category: "confites" },
  { id: 31, name: "Chicles Gallito", price: 200, emoji: "🍬", category: "confites" },
  { id: 32, name: "Dulce de coco rallado", price: 600, emoji: "🥥", category: "dulces" },
  { id: 33, name: "Dulce de guayabita", price: 450, emoji: "🍈", category: "dulces" },
  { id: 34, name: "Caramelos de feria", price: 350, emoji: "🍭", category: "confites" },
  { id: 35, name: "Cajeta de pinito", price: 7000, emoji: "🧁", category: "especialidades" }
];

export default function LataSuWebsite() {
  const [currentView, setCurrentView] = useState('home');
  const [cart, setCart] = useState([]);
  const [menuOpen, setMenuOpen] = useState(false);
  const [user, setUser] = useState(null);
  const [selectedCategory, setSelectedCategory] = useState('all');
  const [showWelcome, setShowWelcome] = useState(true);
  
  const [authMode, setAuthMode] = useState('login');
  const [formData, setFormData] = useState({
    email: '',
    password: '',
    name: '',
    document: '',
    address: '',
    phone: ''
  });

  const [paymentMethod, setPaymentMethod] = useState('');
  const [cardInfo, setCardInfo] = useState({ number: '', cvv: '', expiry: '' });
  const [shippingAddress, setShippingAddress] = useState('');

  useEffect(() => {
    const timer = setTimeout(() => setShowWelcome(false), 3000);
    return () => clearTimeout(timer);
  }, []);

  const addToCart = (product) => {
    const existing = cart.find(item => item.id === product.id);
    if (existing) {
      setCart(cart.map(item => 
        item.id === product.id ? { ...item, quantity: item.quantity + 1 } : item
      ));
    } else {
      setCart([...cart, { ...product, quantity: 1 }]);
    }
  };

  const removeFromCart = (productId) => {
    setCart(cart.filter(item => item.id !== productId));
  };

  const updateQuantity = (productId, newQuantity) => {
    if (newQuantity === 0) {
      removeFromCart(productId);
    } else {
      setCart(cart.map(item => 
        item.id === productId ? { ...item, quantity: newQuantity } : item
      ));
    }
  };

  const getTotal = () => {
    return cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
  };

  const handleLogin = (e) => {
    e.preventDefault();
    setUser({ email: formData.email, name: formData.name || formData.email });
    setCurrentView('home');
  };

  const handleRegister = (e) => {
    e.preventDefault();
    setUser({ email: formData.email, name: formData.name });
    setCurrentView('home');
  };

  const handleCheckout = () => {
    if (!paymentMethod) {
      alert('Por favor seleccione un método de pago');
      return;
    }
    if (paymentMethod === 'tarjeta' && (!cardInfo.number || !cardInfo.cvv || !cardInfo.expiry)) {
      alert('Por favor complete la información de la tarjeta');
      return;
    }
    if (!shippingAddress) {
      alert('Por favor confirme la dirección de envío');
      return;
    }
    
    alert(`¡Compra exitosa! Total: ₡${getTotal().toLocaleString()}\nDirección de envío: ${shippingAddress}\nMétodo de pago: ${paymentMethod === 'fisico' ? 'Efectivo' : 'Tarjeta'}`);
    setCart([]);
    setCurrentView('home');
    setPaymentMethod('');
    setCardInfo({ number: '', cvv: '', expiry: '' });
    setShippingAddress('');
  };

  const filteredProducts = selectedCategory === 'all' 
    ? PRODUCTS 
    : PRODUCTS.filter(p => p.category === selectedCategory);

  if (showWelcome) {
    return (
      <div className="min-h-screen bg-gray-900 flex items-center justify-center">
        <div className="text-center animate-pulse">
          <h1 className="text-7xl font-bold text-white mb-8">¡BIENVENIDO!</h1>
          <h2 className="text-5xl font-bold mb-6">
            A <span className="text-red-600">LA</span>
            <span className="text-white">TA</span>
            <span className="text-blue-500">SU</span>
          </h2>
          <p className="text-xl text-gray-300 mb-8">TU TIENDA TRADICIONAL COSTARRICENSE A TU ALCANCE</p>
          <div className="text-6xl">🦥</div>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-50">
      <nav className="bg-black text-white sticky top-0 z-50 shadow-lg">
        <div className="max-w-7xl mx-auto px-4">
          <div className="flex justify-between items-center h-16">
            <div className="flex items-center">
              <h1 className="text-3xl font-bold cursor-pointer" onClick={() => setCurrentView('home')}>
                <span className="text-red-600">LA</span>
                <span className="text-white">TA</span>
                <span className="text-blue-500">SU</span>
              </h1>
            </div>

            <div className="hidden md:flex space-x-8">
              <button onClick={() => setCurrentView('home')} className="hover:text-red-500 transition">INICIO</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('chocolates'); }} className="hover:text-red-500 transition">CHOCOLATES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('confites'); }} className="hover:text-red-500 transition">CONFITES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('dulces'); }} className="hover:text-red-500 transition">DULCES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('especialidades'); }} className="hover:text-red-500 transition">ESPECIALIDADES</button>
            </div>

            <div className="flex items-center space-x-4">
              {user ? (
                <span className="text-sm">Hola, {user.name}</span>
              ) : (
                <button onClick={() => setCurrentView('auth')} className="border border-white px-4 py-2 rounded hover:bg-white hover:text-black transition">
                  <User size={20} />
                </button>
              )}
              <button onClick={() => setCurrentView('cart')} className="relative">
                <ShoppingCart size={24} />
                {cart.length > 0 && (
                  <span className="absolute -top-2 -right-2 bg-red-600 text-white rounded-full w-6 h-6 flex items-center justify-center text-xs">
                    {cart.length}
                  </span>
                )}
              </button>
              <button className="md:hidden" onClick={() => setMenuOpen(!menuOpen)}>
                {menuOpen ? <X size={24} /> : <Menu size={24} />}
              </button>
            </div>
          </div>

          {menuOpen && (
            <div className="md:hidden pb-4">
              <button onClick={() => { setCurrentView('home'); setMenuOpen(false); }} className="block w-full text-left py-2 hover:text-red-500">INICIO</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('chocolates'); setMenuOpen(false); }} className="block w-full text-left py-2 hover:text-red-500">CHOCOLATES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('confites'); setMenuOpen(false); }} className="block w-full text-left py-2 hover:text-red-500">CONFITES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('dulces'); setMenuOpen(false); }} className="block w-full text-left py-2 hover:text-red-500">DULCES</button>
              <button onClick={() => { setCurrentView('products'); setSelectedCategory('especialidades'); setMenuOpen(false); }} className="block w-full text-left py-2 hover:text-red-500">ESPECIALIDADES</button>
            </div>
          )}
        </div>
      </nav>

      <div className="max-w-7xl mx-auto px-4 py-8">
        {currentView === 'home' && (
          <div>
            <div className="bg-gradient-to-r from-red-600 via-black to-blue-600 text-white text-center py-20 rounded-lg mb-12">
              <h1 className="text-5xl font-bold mb-4">Dulces Tradicionales Costarricenses</h1>
              <p className="text-xl">El sabor de Costa Rica en cada bocado 🇨🇷</p>
            </div>

            <div className="mb-8">
              <h2 className="text-3xl font-bold mb-6 text-center">Nuestras Categorías</h2>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                {['chocolates', 'confites', 'dulces', 'especialidades'].map(cat => (
                  <button
                    key={cat}
                    onClick={() => { setCurrentView('products'); setSelectedCategory(cat); }}
                    className="bg-white p-6 rounded-lg shadow-lg hover:shadow-xl transition transform hover:-translate-y-1"
                  >
                    <h3 className="text-xl font-bold capitalize text-center">{cat}</h3>
                  </button>
                ))}
              </div>
            </div>

            <div className="text-center mt-12">
              <button 
                onClick={() => { setCurrentView('products'); setSelectedCategory('all'); }}
                className="bg-red-600 text-white px-8 py-4 rounded-lg text-xl font-bold hover:bg-red-700 transition"
              >
                Ver Todos Los Productos
              </button>
            </div>
          </div>
        )}

        {currentView === 'products' && (
          <div>
            <h2 className="text-4xl font-bold mb-8 text-center">
              {selectedCategory === 'all' ? 'Todos Los Productos' : selectedCategory.charAt(0).toUpperCase() + selectedCategory.slice(1)}
            </h2>
            
            <div className="mb-6 flex flex-wrap justify-center gap-2">
              <button onClick={() => setSelectedCategory('all')} className={`px-4 py-2 rounded ${selectedCategory === 'all' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}>Todos</button>
              <button onClick={() => setSelectedCategory('chocolates')} className={`px-4 py-2 rounded ${selectedCategory === 'chocolates' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}>Chocolates</button>
              <button onClick={() => setSelectedCategory('confites')} className={`px-4 py-2 rounded ${selectedCategory === 'confites' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}>Confites</button>
              <button onClick={() => setSelectedCategory('dulces')} className={`px-4 py-2 rounded ${selectedCategory === 'dulces' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}>Dulces</button>
              <button onClick={() => setSelectedCategory('especialidades')} className={`px-4 py-2 rounded ${selectedCategory === 'especialidades' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}>Especialidades</button>
            </div>

            <div className="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
              {filteredProducts.map(product => (
                <div key={product.id} className="bg-white rounded-lg shadow-lg overflow-hidden hover:shadow-xl transition transform hover:-translate-y-1">
                  <div className="text-center py-8 text-6xl bg-gradient-to-br from-yellow-100 to-orange-100">
                    {product.emoji}
                  </div>
                  <div className="p-4">
                    <h3 className="font-bold text-lg mb-2">{product.name}</h3>
                    <p className="text-2xl font-bold text-red-600 mb-3">₡{product.price.toLocaleString()}</p>
                    <button
                      onClick={() => addToCart(product)}
                      className="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700 transition"
                    >
                      Agregar al Carrito
                    </button>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}

        {currentView === 'auth' && (
          <div className="max-w-md mx-auto bg-white p-8 rounded-lg shadow-lg">
            <div className="flex mb-6">
              <button
                onClick={() => setAuthMode('login')}
                className={`flex-1 py-2 ${authMode === 'login' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}
              >
                Iniciar Sesión
              </button>
              <button
                onClick={() => setAuthMode('register')}
                className={`flex-1 py-2 ${authMode === 'register' ? 'bg-red-600 text-white' : 'bg-gray-200'}`}
              >
                Registrarse
              </button>
            </div>

            {authMode === 'login' ? (
              <div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Email</label>
                  <input
                    type="email"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.email}
                    onChange={(e) => setFormData({...formData, email: e.target.value})}
                  />
                </div>
                <div className="mb-6">
                  <label className="block mb-2 font-bold">Contraseña</label>
                  <input
                    type="password"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.password}
                    onChange={(e) => setFormData({...formData, password: e.target.value})}
                  />
                </div>
                <button onClick={handleLogin} className="w-full bg-red-600 text-white py-3 rounded font-bold hover:bg-red-700">
                  Iniciar Sesión
                </button>
              </div>
            ) : (
              <div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Nombre Completo</label>
                  <input
                    type="text"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.name}
                    onChange={(e) => setFormData({...formData, name: e.target.value})}
                  />
                </div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Documento de Identidad</label>
                  <input
                    type="text"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.document}
                    onChange={(e) => setFormData({...formData, document: e.target.value})}
                  />
                </div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Email</label>
                  <input
                    type="email"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.email}
                    onChange={(e) => setFormData({...formData, email: e.target.value})}
                  />
                </div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Contraseña</label>
                  <input
                    type="password"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.password}
                    onChange={(e) => setFormData({...formData, password: e.target.value})}
                  />
                </div>
                <div className="mb-4">
                  <label className="block mb-2 font-bold">Dirección</label>
                  <input
                    type="text"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.address}
                    onChange={(e) => setFormData({...formData, address: e.target.value})}
                  />
                </div>
                <div className="mb-6">
                  <label className="block mb-2 font-bold">Teléfono</label>
                  <input
                    type="tel"
                    required
                    className="w-full border p-2 rounded"
                    value={formData.phone}
                    onChange={(e) => setFormData({...formData, phone: e.target.value})}
                  />
                </div>
                <button onClick={handleRegister} className="w-full bg-red-600 text-white py-3 rounded font-bold hover:bg-red-700">
                  Registrarse
                </button>
              </div>
            )}
          </div>
        )}

        {currentView === 'cart' && (
          <div>
            <h2 className="text-4xl font-bold mb-8">Carrito de Compras</h2>
            {cart.length === 0 ? (
              <div className="text-center py-12">
                <p className="text-2xl text-gray-500 mb-4">Tu carrito está vacío</p>
                <button
                  onClick={() => setCurrentView('products')}
                  className="bg-red-600 text-white px-6 py-3 rounded-lg hover:bg-red-700"
                >
                  Ir a Comprar
                </button>
              </div>
            ) : (
              <div className="grid md:grid-cols-3 gap-8">
                <div className="md:col-span-2">
                  {cart.map(item => (
                    <div key={item.id} className="bg-white p-4 rounded-lg shadow mb-4 flex items-center">
                      <div className="text-4xl mr-4">{item.emoji}</div>
                      <div className="flex-1">
                        <h3 className="font-bold text-lg">{item.name}</h3>
                        <p className="text-red-600 font-bold">₡{item.price.toLocaleString()}</p>
                      </div>
                      <div className="flex items-center space-x-2">
                        <button
                          onClick={() => updateQuantity(item.id, item.quantity - 1)}
                          className="bg-gray-200 px-3 py-1 rounded"
                        >
                          -
                        </button>
                        <span className="font-bold">{item.quantity}</span>
                        <button
                          onClick={() => updateQuantity(item.id, item.quantity + 1)}
                          className="bg-gray-200 px-3 py-1 rounded"
                        >
                          +
                        </button>
                        <button
                          onClick={() => removeFromCart(item.id)}
                          className="bg-red-600 text-white px-3 py-1 rounded ml-2"
                        >
                          Eliminar
                        </button>
                      </div>
                    </div>
                  ))}
                </div>

                <div className="bg-white p-6 rounded-lg shadow h-fit">
                  <h3 className="text-2xl font-bold mb-4">Resumen</h3>
                  <div className="border-t pt-4 mb-4">
                    <div className="flex justify-between text-xl font-bold">
                      <span>Total:</span>
                      <span className="text-red-600">₡{getTotal().toLocaleString()}</span>
                    </div>
                  </div>

                  <div className="mb-4">
                    <label className="block mb-2 font-bold">Método de Pago</label>
                    <select
                      className="w-full border p-2 rounded"
                      value={paymentMethod}
                      onChange={(e) => setPaymentMethod(e.target.value)}
                    >
                      <option value="">Seleccionar</option>
                      <option value="fisico">Efectivo</option>
                      <option value="tarjeta">Tarjeta</option>
                    </select>
                  </div>

                  {paymentMethod === 'tarjeta' && (
                    <div className="mb-4 space-y-2">
                      <input
                        type="text"
                        placeholder="Número de tarjeta"
                        className="w-full border p-2 rounded"
                        value={cardInfo.number}
                        onChange={(e) => setCardInfo({...cardInfo, number: e.target.value})}
                      />
                      <div className="flex space-x-2">
                        <input
                          type="text"
                          placeholder="MM/AA"
                          className="w-1/2 border p-2 rounded"
                          value={cardInfo.expiry}
                          onChange={(e) => setCardInfo({...cardInfo, expiry: e.target.value})}
                        />
                        <input
                          type="text"
                          placeholder="CVV"
                          className="w-1/2 border p-2 rounded"
                          value={cardInfo.cvv}
                          onChange={(e) => setCardInfo({...cardInfo, cvv: e.target.value})}
                        />
                      </div>
                    </div>
                  )}

                  <div className="mb-4">
                    <label className="block mb-2 font-bold">Dirección de Envío</label>
                    <textarea
                      className="w-full border p-2 rounded"
                      rows="3"
                      value={shippingAddress}
                      onChange={(e) => setShippingAddress(e.target.value)}
                      placeholder="Ingrese su dirección completa"
                    />
                  </div>

                  <button
                    onClick={handleCheckout}
                    className="w-full bg-red-600 text-white py-3 rounded-lg font-bold hover:bg-red-700"
                  >
                    Finalizar Compra
                  </button>
                </div>
              </div>
            )}
          </div>
        )}
      </div>

      <footer className="bg-black text-white mt-16 py-8">
        <div className="max-w-7xl mx-auto px-4">
          <div className="grid md:grid-cols-3 gap-8">
            <div>
              <h3 className="text-2xl font-bold mb-4">
                <span className="text-red-600">LA</span>
                <span className="text-white">TA</span>
                <span className="text-blue-500">SU</span>
              </h3>
              <p className="text-gray-400">Tu tienda tradicional costarricense</p>
            </div>
            <div>
              <h4 className="font-bold mb-4">Contacto</h4>
              <div className="space-y-2">
                <div className="flex items-center">
                  <Phone size={18} className="mr-2" />
                  <span>+506 6249 5992</span>
                </div>
                <div className="flex items-center">
                  <Mail size={18} className="mr-2" />
                  <span>info@latasu.com</span>
                </div>
                <div className="flex items-center">
                  <MapPin size={18} className="mr-2" />
                  <span>Costa Rica</span>
                </div>
              </div>
            </div>
            <div>
              <h4 className="font-bold mb-4">Síguenos</h4>
              <p className="text-gray-400">Dulces tradicionales con amor costarricense 🇨🇷</p>
            </div>
          </div>
          <div className="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
            <p>&copy; 2025 LATASU. Todos los derechos reservados.</p>
          </div>
        </div>
      </footer>

    <a
  href="https://wa.me/50662495992"
  target="_blank"
  rel="noopener noreferrer"
  className="fixed bottom-6 right-6 bg-green-500 text-white p-4 rounded-full shadow-lg hover:bg-green-600 transition z-50"
>
  <svg className="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
    <path d="M20.52 3.48A11.94 11.94 0 0012 0C5.37 0 0 5.37 0 12a11.93 11.93 0 001.64 6.02L0 24l6.24-1.63A11.95 11.95 0 0012 24c6.63 0 12-5.37 12-12 0-3.19-1.24-6.19-3.48-8.52zM12 22c-1.87 0-3.67-.5-5.26-1.45l-.38-.22-3.7.97.99-3.6-.25-.39A9.94 9.94 0 012 12C2 6.48 6.48 2 12 2s10 4.48 10 10-4.48 10-10 10zm5.2-7.62c-.28-.14-1.65-.81-1.91-.9-.26-.09-.45-.14-.64.14-.19.28-.75.91-.91 1.09-.17.18-.33.2-.61.07-.28-.14-1.17-.43-2.23-1.36a8.23 8.23 0 01-1.52-1.86c-.16-.27-.02-.42.12-.56.12-.12.27-.3.4-.45.13-.15.17-.26.26-.43.09-.17.04-.32-.02-.45-.07-.14-.64-1.55-.88-2.12-.23-.55-.47-.47-.64-.48h-.55c-.17 0-.45.06-.68.32-.23.25-.89.87-.89 2.13s.91 2.47 1.04 2.64c.13.17 1.79 2.74 4.34 3.84 2.55 1.09 2.55.73 3.01.68.46-.05 1.48-.6 1.7-1.17.21-.56.21-1.03.15-1.13-.06-.1-.23-.16-.5-.3z"/>
  </svg>
</a>
    </div>
  );
}

