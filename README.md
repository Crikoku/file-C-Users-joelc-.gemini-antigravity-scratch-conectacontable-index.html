<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ConectaContable - Tu contabilidad, simple y al día</title>
    <!-- SEO Meta Tags -->
    <meta name="description" content="Asesoría contable, tributaria y laboral premium para PYMEs y emprendedores en Chile. Declaración mensual F29, Operación Renta F22 y remuneraciones con Previred.">
    <meta name="keywords" content="contabilidad pyme chile, contador las condes, declaracion f29, operacion renta f22, previred sueldos, conectacontable">
    <meta name="author" content="ConectaContable">

    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Alpine.js (Menú, Scroll, Contador, Carrusel, Acordeón, Calculadora) -->
    <script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/collapse@3.x.x/dist/cdn.min.js"></script>
    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        navy: {
                            DEFAULT: '#1B2A4A',
                            dark: '#0F182A',
                            light: '#283B60'
                        },
                        tealCustom: {
                            DEFAULT: '#00B89C',
                            hover: '#00A38A',
                            glow: '#00B89C33'
                        },
                        goldCustom: {
                            DEFAULT: '#C9A84C',
                            glow: '#C9A84C33'
                        },
                        charcoal: {
                            DEFAULT: '#334155',
                            light: '#475569',
                            dark: '#1E293B'
                        },
                        surface: {
                            DEFAULT: '#F8F9FA',
                            card: '#FFFFFF'
                        }
                    },
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'Inter', 'sans-serif'],
                    },
                    animation: {
                        'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'float': 'float 6s ease-in-out infinite',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-10px)' },
                        }
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Outfit:wght@300;400;500;600;700;900&display=swap');
        
        h1, h2, h3, .font-display {
            font-family: 'Outfit', sans-serif;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #1B2A4A;
        }
        ::-webkit-scrollbar-thumb {
            background: #283B60;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #00B89C;
        }

        /* Range Slider Custom Styling */
        input[type="range"] {
            -webkit-appearance: none;
            appearance: none;
            background: transparent;
            cursor: pointer;
        }
        input[type="range"]::-webkit-slider-runnable-track {
            background: #E2E8F0;
            height: 8px;
            border-radius: 4px;
        }
        input[type="range"]::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            margin-top: -6px;
            background-color: #00B89C;
            height: 20px;
            width: 20px;
            border-radius: 50%;
            box-shadow: 0 0 8px rgba(0, 184, 156, 0.4);
            transition: transform 0.1s ease;
        }
        input[type="range"]::-webkit-slider-thumb:hover {
            transform: scale(1.2);
        }
    </style>
</head>
<body class="bg-surface text-charcoal antialiased selection:bg-tealCustom selection:text-white" 
      x-data="{ 
          mobileMenu: false, 
          scrolled: false,
          calcFacturas: 15,
          calcTrabajadores: 2,
          calcSociedad: 'spa',
          calcMensaje: '',
          calculaPrecio() {
              let base = 15000;
              if (this.calcFacturas <= 5) base = 15000;
              else if (this.calcFacturas <= 20) base = 25000;
              else if (this.calcFacturas <= 50) base = 48000;
              else if (this.calcFacturas <= 100) base = 85000;
              else base = 120000;

              let sueldos = this.calcTrabajadores * 5000;
              let tipoExtra = (this.calcSociedad === 'natural') ? 0 : 10000;

              return base + sueldos + tipoExtra;
          },
          copiarACotizacion() {
              let sociedadNombre = 'SpA o Limitada';
              if (this.calcSociedad === 'eirl') sociedadNombre = 'EIRL';
              if (this.calcSociedad === 'natural') sociedadNombre = 'Persona Natural con Giro';

              this.calcMensaje = `Hola ConectaContable! Me gustaría cotizar el plan estimado para mi empresa (${sociedadNombre}) con aprox. ${this.calcFacturas} facturas mensuales y ${this.calcTrabajadores} trabajadores. Quedo atento a su contacto.`;
              
              document.getElementById('contacto-mensaje').value = this.calcMensaje;
              document.getElementById('contacto').scrollIntoView({ behavior: 'smooth' });
              
              // Highlight the contact form inputs
              const formContainer = document.getElementById('form-container');
              formContainer.classList.add('ring-2', 'ring-tealCustom');
              setTimeout(() => formContainer.classList.remove('ring-2', 'ring-tealCustom'), 2000);
          }
      }" 
      @scroll.window="scrolled = (window.scrollY > 50)">

    <!-- --- STICKY NAV --- -->
    <nav class="fixed top-0 left-0 right-0 z-50 transition-all duration-500" 
         :class="scrolled ? 'bg-navy/95 backdrop-blur-lg border-b border-white/10 py-3.5 shadow-xl' : 'bg-navy py-5'">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex justify-between items-center relative z-10">
            <!-- Logo -->
            <a href="#hero" class="flex items-center space-x-3 group">
                <div class="w-10 h-10 rounded-xl bg-[#00B89C] flex items-center justify-center font-black text-white text-xl shadow-lg shadow-tealCustom/20 group-hover:scale-105 transition-transform duration-300">C</div>
                <span class="font-extrabold text-2xl text-white tracking-tight">Conecta<span class="text-tealCustom">Contable</span></span>
            </a>

            <!-- Desktop Nav Links -->
            <div class="hidden md:flex items-center space-x-8">
                <a href="#servicios" class="text-slate-300 hover:text-tealCustom transition-colors duration-300 text-sm font-semibold tracking-wide uppercase">Servicios</a>
                <a href="#calculadora" class="text-slate-300 hover:text-tealCustom transition-colors duration-300 text-sm font-semibold tracking-wide uppercase">Cotizador</a>
                <a href="#planes" class="text-slate-300 hover:text-tealCustom transition-colors duration-300 text-sm font-semibold tracking-wide uppercase">Planes</a>
                <a href="#nosotros" class="text-slate-300 hover:text-tealCustom transition-colors duration-300 text-sm font-semibold tracking-wide uppercase">Nosotros</a>
                <a href="#contacto" class="px-6 py-2.5 rounded-xl text-sm font-bold text-white bg-tealCustom hover:bg-tealCustom/90 transition-all duration-300 shadow-lg shadow-tealCustom/20 hover:shadow-tealCustom/40 hover:-translate-y-0.5">
                    Contáctanos
                </a>
            </div>

            <!-- Hamburger Mobile Menu -->
            <div class="md:hidden">
                <button @click="mobileMenu = true" class="text-slate-300 hover:text-tealCustom transition-colors duration-300 p-2 focus:outline-none" aria-label="Abrir Menú">
                    <i data-lucide="menu" class="w-7 h-7"></i>
                </button>
            </div>
        </div>
    </nav>

    <!-- Mobile Slide-over Menu -->
    <div x-show="mobileMenu" 
         class="fixed inset-0 z-50 overflow-hidden md:hidden" 
         x-transition:enter="transition ease-out duration-300"
         x-transition:enter-start="opacity-0"
         x-transition:enter-end="opacity-100"
         x-transition:leave="transition ease-in duration-200"
         x-transition:leave-start="opacity-100"
         x-transition:leave-end="opacity-0"
         x-cloak>
        <!-- Overlay -->
        <div class="absolute inset-0 bg-navy/80 backdrop-blur-md" @click="mobileMenu = false"></div>
        
        <!-- Sidebar Content -->
        <div class="absolute inset-y-0 right-0 pl-10 max-w-full flex">
            <div class="w-screen max-w-xs bg-navy border-l border-white/10 p-6 flex flex-col justify-between shadow-2xl relative"
                 x-show="mobileMenu"
                 x-transition:enter="transform transition ease-out duration-300"
                 x-transition:enter-start="translate-x-full"
                 x-transition:enter-end="translate-x-0"
                 x-transition:leave="transform transition ease-in duration-200"
                 x-transition:leave-start="translate-x-0"
                 x-transition:leave-end="translate-x-full">
                
                <div>
                    <!-- Close btn -->
                    <div class="flex justify-between items-center mb-10">
                        <span class="font-extrabold text-xl text-white tracking-tight">Conecta<span class="text-tealCustom">Contable</span></span>
                        <button @click="mobileMenu = false" class="text-slate-300 hover:text-tealCustom focus:outline-none p-2" aria-label="Cerrar Menú">
                            <i data-lucide="x" class="w-6 h-6"></i>
                        </button>
                    </div>

                    <!-- Links -->
                    <div class="space-y-4">
                        <a href="#servicios" @click="mobileMenu = false" class="block py-3 px-4 rounded-xl text-lg font-medium text-slate-300 hover:text-tealCustom hover:bg-white/5 transition-all">Servicios</a>
                        <a href="#calculadora" @click="mobileMenu = false" class="block py-3 px-4 rounded-xl text-lg font-medium text-slate-300 hover:text-tealCustom hover:bg-white/5 transition-all">Cotizador</a>
                        <a href="#planes" @click="mobileMenu = false" class="block py-3 px-4 rounded-xl text-lg font-medium text-slate-300 hover:text-tealCustom hover:bg-white/5 transition-all">Planes</a>
                        <a href="#nosotros" @click="mobileMenu = false" class="block py-3 px-4 rounded-xl text-lg font-medium text-slate-300 hover:text-tealCustom hover:bg-white/5 transition-all">Nosotros</a>
                    </div>
                </div>

                <div class="mt-auto pt-6">
                    <a href="#contacto" @click="mobileMenu = false" class="block w-full text-center bg-tealCustom hover:bg-tealCustom/90 text-white font-bold py-4 rounded-xl shadow-lg transition-all">
                        Contáctanos
                    </a>
                </div>
            </div>
        </div>
    </div>

    <!-- --- 1. HERO SECTION (Azul Marino Profundo Background) --- -->
    <section id="hero" class="relative bg-navy pt-36 pb-24 md:pt-48 md:pb-40 overflow-hidden z-10 border-b border-white/5">
        <!-- Technical Dot Background Pattern -->
        <div class="absolute inset-0 opacity-15 pointer-events-none">
            <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
                <defs>
                    <pattern id="dotGrid" width="30" height="30" patternUnits="userSpaceOnUse">
                        <circle cx="15" cy="15" r="1.2" fill="white" />
                    </pattern>
                </defs>
                <rect width="100%" height="100%" fill="url(#dotGrid)" />
            </svg>
        </div>

        <!-- Glowing Ambient Backdrops inside Hero -->
        <div class="absolute top-1/4 left-1/3 w-[500px] h-[250px] bg-tealCustom/10 rounded-full blur-[90px] pointer-events-none"></div>
        <div class="absolute bottom-10 right-1/4 w-[400px] h-[200px] bg-goldCustom/5 rounded-full blur-[80px] pointer-events-none"></div>

        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-16 items-center">
                
                <!-- Left text column -->
                <div class="lg:col-span-7 text-left space-y-8">
                    <!-- Trust Badge with Oro Cálido -->
                    <div class="inline-flex items-center space-x-2.5 bg-white/5 border border-goldCustom/40 px-5 py-2 rounded-full shadow-lg">
                        <i data-lucide="award" class="w-4 h-4 text-goldCustom"></i>
                        <span class="text-xs md:text-sm font-semibold text-gray-200 tracking-wide">
                            Contadores Auditores Certificados · SII · Previred
                        </span>
                    </div>

                    <!-- Main Headline -->
                    <h1 class="text-4xl md:text-6.5xl font-black tracking-tight leading-[1.1] text-white">
                        Tu contabilidad, <br>
                        <span class="text-tealCustom bg-gradient-to-r from-tealCustom via-emerald-300 to-[#10B981] bg-clip-text text-transparent drop-shadow-sm">simple y al día</span>
                    </h1>

                    <!-- Subheadline -->
                    <p class="text-lg md:text-xl text-slate-300 max-w-xl font-light leading-relaxed">
                        Olvídate del estrés financiero. Nos encargamos de tus impuestos, libros contables y liquidaciones de sueldo para que tú te enfoques en liderar tu negocio.
                    </p>

                    <!-- CTAs -->
                    <div class="flex flex-col sm:flex-row items-center gap-4.5 pt-4">
                        <a href="#calculadora" class="w-full sm:w-auto text-center px-8 py-4 rounded-xl text-base font-bold bg-tealCustom hover:bg-tealCustom-hover text-white hover:shadow-tealCustom/30 shadow-lg shadow-tealCustom/15 hover:-translate-y-0.5 transition-all duration-300">
                            Calcular Tarifa Mensual
                        </a>
                        <a href="#servicios" class="w-full sm:w-auto text-center px-8 py-4 rounded-xl text-base font-bold border border-white/20 hover:border-white/40 text-white hover:bg-white/5 transition-all duration-300">
                            Ver Servicios
                        </a>
                    </div>

                    <!-- Client Logos / Social proof -->
                    <div class="pt-8 border-t border-white/10 space-y-4">
                        <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Cumplimiento y sincronización con:</p>
                        <div class="flex flex-wrap gap-8 items-center opacity-75 grayscale hover:grayscale-0 hover:opacity-100 transition-all">
                            <span class="text-sm font-bold tracking-widest text-slate-300 flex items-center gap-1.5"><i data-lucide="building" class="w-4 h-4 text-tealCustom"></i> SII (Impuestos Internos)</span>
                            <span class="text-sm font-bold tracking-widest text-slate-300 flex items-center gap-1.5"><i data-lucide="briefcase" class="w-4 h-4 text-tealCustom"></i> PREVIRED (Previsión)</span>
                            <span class="text-sm font-bold tracking-widest text-slate-300 flex items-center gap-1.5"><i data-lucide="scale" class="w-4 h-4 text-tealCustom"></i> DT (Dirección del Trabajo)</span>
                        </div>
                    </div>
                </div>

                <!-- Right dashboard mockup column (Navy Light dashboard) -->
                <div class="lg:col-span-5 relative mt-8 lg:mt-0">
                    <div class="absolute inset-0 bg-tealCustom/15 rounded-3xl filter blur-3xl pointer-events-none transform scale-90 -z-10 animate-pulse-slow"></div>
                    
                    <!-- CSS Mockup Panel inside dark Navy Hero -->
                    <div class="relative bg-navy-light/60 border border-white/10 backdrop-blur-2xl rounded-3xl p-6 shadow-2xl overflow-hidden group hover:border-white/20 transition-all duration-500 animate-float">
                        <div class="absolute -top-12 -right-12 w-28 h-28 bg-tealCustom/25 rounded-full blur-xl pointer-events-none"></div>

                        <!-- Header mockup -->
                        <div class="flex justify-between items-center pb-5 mb-5 border-b border-white/10">
                            <div class="flex items-center space-x-2.5">
                                <div class="w-3.5 h-3.5 rounded-full bg-red-500/80"></div>
                                <div class="w-3.5 h-3.5 rounded-full bg-yellow-500/80"></div>
                                <div class="w-3.5 h-3.5 rounded-full bg-green-500/80"></div>
                            </div>
                            <span class="text-xs font-semibold text-tealCustom bg-tealCustom/10 px-3 py-1 rounded-full border border-tealCustom/25">Sincronizado SII</span>
                        </div>

                        <!-- Mini stats block -->
                        <div class="grid grid-cols-2 gap-4 mb-6">
                            <div class="bg-navy/70 border border-white/5 rounded-2xl p-4">
                                <span class="text-[10px] uppercase font-bold text-slate-400 tracking-wider">Ventas Netas (Mes)</span>
                                <p class="text-lg font-extrabold text-white mt-1">$14.280.000</p>
                                <span class="text-[9px] text-emerald-400 flex items-center mt-1"><i data-lucide="trending-up" class="w-3 h-3 mr-0.5"></i> +12.4% vs anterior</span>
                            </div>
                            <div class="bg-navy/70 border border-white/5 rounded-2xl p-4">
                                <span class="text-[10px] uppercase font-bold text-slate-400 tracking-wider">Estimación IVA F29</span>
                                <p class="text-lg font-extrabold text-tealCustom mt-1">$2.713.200</p>
                                <span class="text-[9px] text-slate-400 flex items-center mt-1"><i data-lucide="calendar" class="w-3 h-3 mr-0.5"></i> Plazo: 20 de Junio</span>
                            </div>
                        </div>

                        <!-- Remuneraciones payroll preview -->
                        <div class="bg-navy/70 border border-white/5 rounded-2xl p-4 mb-6">
                            <div class="flex justify-between items-center mb-3">
                                <span class="text-xs font-bold text-white flex items-center gap-1.5"><i data-lucide="users" class="w-3.5 h-3.5 text-tealCustom"></i> Liquidaciones de Sueldo</span>
                                <span class="text-[10px] bg-slate-800 text-slate-300 font-semibold px-2 py-0.5 rounded">Previred OK</span>
                            </div>
                            <div class="space-y-2">
                                <div class="flex justify-between items-center text-xs bg-navy-light/40 p-2 rounded border border-white/5">
                                    <span class="text-slate-300 font-medium">Carlos R. (Ventas)</span>
                                    <span class="text-tealCustom font-bold">$780.000 Líquido</span>
                                </div>
                                <div class="flex justify-between items-center text-xs bg-navy-light/40 p-2 rounded border border-white/5">
                                    <span class="text-slate-300 font-medium">Andrea M. (Operaciones)</span>
                                    <span class="text-tealCustom font-bold">$920.000 Líquido</span>
                                </div>
                            </div>
                        </div>

                        <!-- Progress Bar / Facturación -->
                        <div class="space-y-2">
                            <div class="flex justify-between text-xs font-semibold text-slate-400">
                                <span>Facturas de Compra/Venta</span>
                                <span class="text-tealCustom">24 emitidas esta semana</span>
                            </div>
                            <div class="w-full h-2 bg-navy rounded-full overflow-hidden">
                                <div class="h-full bg-gradient-to-r from-tealCustom to-emerald-400 rounded-full" style="width: 72%;"></div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </section>

    <!-- --- 2. SERVICES SECTION (Blanco de Superficie y Gris Carbón) --- -->
    <section id="servicios" class="py-24 md:py-32 relative bg-surface border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            
            <div class="text-center max-w-3xl mx-auto mb-20">
                <div class="inline-flex items-center space-x-2 bg-tealCustom/10 border border-tealCustom/25 px-4 py-1.5 rounded-full mb-4.5">
                    <span class="text-xs font-bold text-tealCustom uppercase tracking-widest">¿Qué hacemos por ti?</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight">Servicios que impulsan tu negocio</h2>
                <p class="text-charcoal-light mt-4.5 text-base md:text-lg font-light leading-relaxed">
                    Cubrimos todas las necesidades de administración, impuestos y cumplimiento legal para que tu negocio funcione sin interrupciones.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- Card 1 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="bar-chart-3" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Contabilidad & Finanzas</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Registro y conciliación bancaria sistemática, balances generales y estados de resultados para tomar las mejores decisiones financieras.</p>
                </div>
                <!-- Card 2 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="file-text" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Tributación & IVA</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Cálculo, revisión y presentación mensual de F29 (Créditos, Débitos, Retenciones de Boletas y PPM) ante el SII sin errores.</p>
                </div>
                <!-- Card 3 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="users" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Recursos Humanos</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Cálculo de liquidaciones de sueldo, emisión de contratos y finiquitos, declaración y pago de imposiciones mensuales mediante Previred.</p>
                </div>
                <!-- Card 4 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="shield-check" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Auditoría Externa</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Evaluación de procesos internos, control de riesgos, conciliación bancaria exhaustiva y regularización de balances ante fiscalizaciones.</p>
                </div>
                <!-- Card 5 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="calculator" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Declaración de Renta</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Operación Renta anual (F22) sin sorpresas, declaraciones juradas (DDJJ) y optimización estratégica de impuestos corporativos y de socios.</p>
                </div>
                <!-- Card 6 -->
                <div class="relative bg-white border border-slate-200 p-8.5 rounded-3xl shadow-sm flex flex-col items-start transition-all duration-300 hover:-translate-y-2 hover:border-tealCustom hover:shadow-xl group">
                    <div class="p-4 rounded-2xl bg-slate-50 text-tealCustom mb-6 group-hover:bg-tealCustom group-hover:text-white transition-all duration-300 border border-slate-100">
                        <i data-lucide="book-open" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-xl font-bold text-navy mb-3.5">Libros Electrónicos</h3>
                    <p class="text-charcoal text-sm leading-relaxed font-light">Mantén tus registros de Compra y Venta sincronizados de forma diaria y automática con la plataforma del SII, evitando multas.</p>
                </div>
            </div>
        </div>
    </section>

    <!-- --- 3. DYNAMIC CALCULATOR SECTION --- -->
    <section id="calculadora" class="py-24 md:py-32 bg-slate-50 relative overflow-hidden border-b border-slate-200">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            
            <div class="text-center max-w-3xl mx-auto mb-16">
                <div class="inline-flex items-center space-x-2 bg-tealCustom/10 border border-tealCustom/25 px-4 py-1.5 rounded-full mb-4">
                    <i data-lucide="sparkles" class="w-4 h-4 text-tealCustom"></i>
                    <span class="text-xs font-bold text-tealCustom uppercase tracking-widest">Estima en línea</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight">Simula tu Tarifa de Manera Simple</h2>
                <p class="text-charcoal-light mt-4.5 text-base md:text-lg font-light leading-relaxed">
                    Selecciona las variables de tu negocio y obtén un valor mensual referencial al instante. ¡Transparente y directo!
                </p>
            </div>

            <!-- Main calculator card (Clean Surface White Layout) -->
            <div class="bg-white border border-slate-200 rounded-3xl p-8 md:p-12 shadow-xl">
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-center">
                    
                    <!-- Sliders & Inputs -->
                    <div class="lg:col-span-7 space-y-8">
                        <!-- SOCIEDAD SELECTION -->
                        <div>
                            <label class="block text-sm font-semibold text-charcoal uppercase tracking-wider mb-4">1. Tipo de Constitución o Estructura</label>
                            <div class="grid grid-cols-3 gap-3">
                                <button @click="calcSociedad = 'spa'" 
                                        :class="calcSociedad === 'spa' ? 'bg-tealCustom text-white font-bold border-tealCustom' : 'bg-slate-50 border-slate-200 hover:border-slate-300 text-charcoal'"
                                        class="py-3.5 px-4 rounded-xl border text-sm transition-all focus:outline-none select-none">
                                    SpA / SRL
                                </button>
                                <button @click="calcSociedad = 'eirl'" 
                                        :class="calcSociedad === 'eirl' ? 'bg-tealCustom text-white font-bold border-tealCustom' : 'bg-slate-50 border-slate-200 hover:border-slate-300 text-charcoal'"
                                        class="py-3.5 px-4 rounded-xl border text-sm transition-all focus:outline-none select-none">
                                    EIRL
                                </button>
                                <button @click="calcSociedad = 'natural'" 
                                        :class="calcSociedad === 'natural' ? 'bg-tealCustom text-white font-bold border-tealCustom' : 'bg-slate-50 border-slate-200 hover:border-slate-300 text-charcoal'"
                                        class="py-3.5 px-4 rounded-xl border text-sm transition-all focus:outline-none select-none font-semibold">
                                    P. Natural <span class="hidden sm:inline">con Giro</span>
                                </button>
                            </div>
                        </div>

                        <!-- INVOICES SLIDER -->
                        <div class="space-y-4">
                            <div class="flex justify-between items-center">
                                <label class="text-sm font-semibold text-charcoal uppercase tracking-wider">2. Facturas de Compra/Venta al mes</label>
                                <span class="text-tealCustom text-lg font-black bg-tealCustom/10 px-3 py-1 rounded-lg border border-tealCustom/20" x-text="calcFacturas"></span>
                            </div>
                            <div class="relative flex items-center">
                                <input type="range" min="0" max="120" step="5" x-model="calcFacturas" class="w-full">
                            </div>
                            <div class="flex justify-between text-xs text-slate-400">
                                <span>0 (Inicio)</span>
                                <span>20 (Plan Básico)</span>
                                <span>50 (Plan Estándar)</span>
                                <span>100+ (Plan Completo)</span>
                            </div>
                        </div>

                        <!-- EMPLOYEES SLIDER -->
                        <div class="space-y-4">
                            <div class="flex justify-between items-center">
                                <label class="text-sm font-semibold text-charcoal uppercase tracking-wider">3. Trabajadores contratados (Liquidaciones)</label>
                                <span class="text-tealCustom text-lg font-black bg-tealCustom/10 px-3 py-1 rounded-lg border border-tealCustom/20" x-text="calcTrabajadores"></span>
                            </div>
                            <div class="relative flex items-center">
                                <input type="range" min="0" max="15" step="1" x-model="calcTrabajadores" class="w-full">
                            </div>
                            <div class="flex justify-between text-xs text-slate-400">
                                <span>Sin trabajadores</span>
                                <span>2 trabajadores</span>
                                <span>5 trabajadores</span>
                                <span>15+ contratados</span>
                            </div>
                        </div>
                    </div>

                    <!-- Calculated Fee Panel (Deep Navy Panel for Elegant Contrast) -->
                    <div class="lg:col-span-5 bg-navy border border-white/5 rounded-3xl p-7 text-center relative overflow-hidden shadow-2xl">
                        <!-- Warm Gold Corner Line Accent -->
                        <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-tealCustom via-goldCustom to-tealCustom"></div>
                        
                        <span class="text-xs font-bold text-slate-300 uppercase tracking-widest block mb-1.5">Tu estimación mensual es</span>
                        
                        <div class="my-4 flex justify-center items-baseline text-white">
                            <span class="text-5xl md:text-6xl font-black text-tealCustom tracking-tight">$<span x-text="calculaPrecio().toLocaleString('es-CL')"></span></span>
                            <span class="text-slate-300 text-sm font-medium ml-2">+ IVA / mes</span>
                        </div>

                        <hr class="border-white/10 my-5">

                        <!-- Checklist components included -->
                        <ul class="text-left space-y-3 mb-6 text-sm text-slate-200">
                            <li class="flex items-center"><i data-lucide="check" class="w-4.5 h-4.5 text-tealCustom mr-2.5"></i> Declaración F29 Mensual</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4.5 h-4.5 text-tealCustom mr-2.5"></i> Libros Contables al día en SII</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4.5 h-4.5 text-tealCustom mr-2.5"></i> Declaración Renta F22 Anual</li>
                            <li class="flex items-center" x-show="calcTrabajadores > 0"><i data-lucide="check" class="w-4.5 h-4.5 text-tealCustom mr-2.5"></i> Previred y remuneraciones</li>
                        </ul>

                        <!-- CTA button -->
                        <button @click="copiarACotizacion()" 
                                class="w-full py-4 px-6 rounded-xl font-bold bg-tealCustom hover:bg-tealCustom/90 text-white shadow-lg shadow-tealCustom/20 hover:-translate-y-0.5 transition-all duration-300">
                            Cotizar esta Configuración
                        </button>
                        
                        <span class="text-[11px] text-slate-400 mt-3 block">Las tarifas indicadas son referenciales y se formalizan según el perfil.</span>
                    </div>

                </div>
            </div>

        </div>
    </section>

    <!-- --- 4. PRICING PLANS SECTION --- -->
    <section id="planes" class="py-24 md:py-32 bg-surface border-b border-slate-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            
            <div class="text-center max-w-3xl mx-auto mb-20">
                <div class="inline-flex items-center space-x-2 bg-tealCustom/10 border border-tealCustom/25 px-4 py-1.5 rounded-full mb-4">
                    <span class="text-xs font-bold text-tealCustom uppercase tracking-widest">Nuestros Planes Estándar</span>
                </div>
                <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight">Planes mensuales a tu medida</h2>
                <p class="text-charcoal-light mt-4.5 text-base md:text-lg font-light leading-relaxed">
                    Precios transparentes, sin letras chicas ni contratos forzosos. Soluciones predefinidas para tu pyme.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 items-stretch">
                <!-- Plan 1 -->
                <div class="bg-white border border-slate-200 rounded-3xl flex flex-col justify-between p-8 relative overflow-hidden transition-all duration-300 hover:border-slate-300 hover:-translate-y-1 shadow-sm">
                    <div class="space-y-6">
                        <div>
                            <h3 class="text-xl font-bold text-navy mb-1.5">Plan Básico</h3>
                            <p class="text-xs text-slate-500">Para quienes inician o emiten pocas facturas al mes.</p>
                        </div>
                        <p class="text-sm font-semibold text-tealCustom bg-tealCustom/10 inline-block px-3 py-1 rounded-md">Hasta 20 facturas mensuales</p>
                        <div class="flex items-baseline">
                            <span class="text-4xl font-extrabold text-navy tracking-tight">$15.000</span>
                            <span class="text-slate-500 text-sm font-medium ml-2">+ IVA / mes</span>
                        </div>
                        <hr class="border-slate-100" />
                        <ul class="space-y-4 text-sm text-charcoal">
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración mensual de F29 (SII)</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Libros contables electrónicos</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Soporte vía email</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración de Renta anual</li>
                        </ul>
                    </div>
                    <div class="pt-8">
                        <a href="#contacto" @click="calcFacturas = 15; calcTrabajadores = 0; calcSociedad = 'spa';" 
                           class="block text-center w-full py-3.5 px-4 rounded-xl text-sm font-bold bg-slate-50 hover:bg-slate-150 text-navy border border-slate-200 transition-all">
                            Cotizar ahora
                        </a>
                    </div>
                </div>

                <!-- Plan 2 (Popular Highlighted with Teal & Gold) -->
                <div class="bg-white border-2 border-tealCustom rounded-3xl flex flex-col justify-between p-8 relative overflow-hidden transition-all duration-300 lg:scale-105 z-10 shadow-2xl ring-4 ring-tealCustom/10">
                    <div class="absolute top-0 right-0 bg-tealCustom text-white text-[10px] font-black uppercase tracking-wider px-4 py-1.5 rounded-bl-2xl shadow-sm">Más popular</div>
                    <div class="space-y-6">
                        <div>
                            <h3 class="text-xl font-bold text-navy mb-1.5">Plan Estándar</h3>
                            <p class="text-xs text-slate-500">El equilibrio ideal para pymes en desarrollo con personal.</p>
                        </div>
                        <p class="text-sm font-semibold text-tealCustom bg-tealCustom/10 inline-block px-3 py-1 rounded-md">Hasta 40 facturas mensuales</p>
                        <div class="flex items-baseline">
                            <span class="text-4xl font-extrabold text-navy tracking-tight">$30.000</span>
                            <span class="text-slate-500 text-sm font-medium ml-2">+ IVA / mes</span>
                        </div>
                        <hr class="border-slate-100" />
                        <ul class="space-y-4 text-sm text-charcoal">
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración mensual de F29 (SII)</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Libros contables electrónicos</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Soporte prioritario WhatsApp</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración de Renta anual</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>1 Liquidación de sueldo incluida</li>
                        </ul>
                    </div>
                    <div class="pt-8">
                        <a href="#contacto" @click="calcFacturas = 35; calcTrabajadores = 1; calcSociedad = 'spa';" 
                           class="block text-center w-full py-4 px-4 rounded-xl text-sm font-bold bg-tealCustom hover:bg-tealCustom/90 text-white shadow-lg shadow-tealCustom/25 transition-all">
                            Cotizar ahora
                        </a>
                    </div>
                </div>

                <!-- Plan 3 -->
                <div class="bg-white border border-slate-200 rounded-3xl flex flex-col justify-between p-8 relative overflow-hidden transition-all duration-300 hover:border-slate-300 hover:-translate-y-1 shadow-sm">
                    <div class="space-y-6">
                        <div>
                            <h3 class="text-xl font-bold text-navy mb-1.5">Plan PYME</h3>
                            <p class="text-xs text-slate-500">Para empresas consolidadas con mayor flujo operacional.</p>
                        </div>
                        <p class="text-sm font-semibold text-tealCustom bg-tealCustom/10 inline-block px-3 py-1 rounded-md">Hasta 80 facturas mensuales</p>
                        <div class="flex items-baseline">
                            <span class="text-4xl font-extrabold text-navy tracking-tight">$50.000</span>
                            <span class="text-slate-500 text-sm font-medium ml-2">+ IVA / mes</span>
                        </div>
                        <hr class="border-slate-100" />
                        <ul class="space-y-4 text-sm text-charcoal">
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración mensual de F29 (SII)</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Libros contables electrónicos</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Asesoría mensual estratégica</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Declaración de Renta anual</li>
                            <li class="flex items-center"><i data-lucide="check" class="w-4 h-4 text-tealCustom mr-3"></i>Hasta 3 liquidaciones de sueldo</li>
                        </ul>
                    </div>
                    <div class="pt-8">
                        <a href="#contacto" @click="calcFacturas = 75; calcTrabajadores = 3; calcSociedad = 'spa';" 
                           class="block text-center w-full py-3.5 px-4 rounded-xl text-sm font-bold bg-slate-50 hover:bg-slate-150 text-navy border border-slate-200 transition-all">
                            Cotizar ahora
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- --- 5. STATS COUNTER SECTION (Navy Background) --- -->
    <section id="nosotros" class="py-24 bg-navy text-white relative overflow-hidden" 
             x-data="{ 
                triggered: false,
                counters: [
                    { current: 0, target: 200, label: 'Clientes atendidos', prefix: '+' },
                    { current: 0, target: 10, label: 'Años de experiencia', prefix: '+' },
                    { current: 0, target: 5000, label: 'Declaraciones realizadas', prefix: '+' },
                    { current: 0, target: 3, label: 'Contadores certificados', prefix: '' }
                ],
                startCounters() {
                    if (this.triggered) return;
                    this.triggered = true;
                    this.counters.forEach(c => {
                        let start = 0;
                        let end = c.target;
                        let duration = 2000;
                        let startTime = null;
                        
                        const animate = (timestamp) => {
                            if (!startTime) startTime = timestamp;
                            let progress = timestamp - startTime;
                            let currentVal = Math.min(Math.floor((progress / duration) * (end - start) + start), end);
                            c.current = currentVal.toLocaleString('es-CL');
                            if (progress < duration) {
                                window.requestAnimationFrame(animate);
                            }
                        };
                        window.requestAnimationFrame(animate);
                    });
                }
             }"
             @scroll.window="if (window.scrollY + window.innerHeight > $el.offsetTop + 100) startCounters()">
        
        <!-- Grid pattern overlay -->
        <div class="absolute inset-0 opacity-10 pointer-events-none">
            <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
                <rect width="100%" height="100%" fill="none" />
                <path d="M 40 0 L 0 40 M 0 0 L 40 40" fill="none" stroke="white" strokeWidth="0.5"/>
            </svg>
        </div>

        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
            <div class="grid grid-cols-2 lg:grid-cols-4 gap-12 text-center">
                <template x-for="stat in counters">
                    <div class="flex flex-col items-center p-6 bg-white/5 border border-white/10 rounded-3xl backdrop-blur-md">
                        <div class="text-4xl md:text-5xl font-black text-tealCustom tracking-tight mb-2.5">
                            <span x-text="stat.prefix"></span><span x-text="stat.current || 0"></span>
                        </div>
                        <div class="text-xs md:text-sm font-semibold text-slate-300 max-w-[160px] uppercase tracking-wider leading-relaxed" x-text="stat.label"></div>
                    </div>
                </template>
            </div>
        </div>
    </section>

    <!-- --- 6. TESTIMONIALS SECTION --- -->
    <section class="py-24 md:py-32 relative overflow-hidden bg-surface border-b border-slate-200">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10"
             x-data="{ 
                activeSlide: 0,
                testimonials: [
                    { name: 'Francisca Valdés', role: 'Fundadora de DecoCasa SpA', text: 'ConectaContable ordenó toda nuestra facturación. El proceso de IVA mensual y las remuneraciones pasaron de ser una tortura a algo automático. ¡100% recomendados!', img: 'https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?q=80&w=200&auto=format&fit=crop' },
                    { name: 'Sebastián Lagos', role: 'CEO de AndesTech Solutions Ltd.', text: 'El equipo no solo declara nuestros impuestos a tiempo, sino que nos asesora en la Operación Renta anual con una visión estratégica clave para nuestro flujo de caja.', img: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?q=80&w=200&auto=format&fit=crop' },
                    { name: 'María Inés Rivas', role: 'Gerente General de Emporio Gourmet', text: 'Cambiarme a ConectaContable ha sido la mejor decisión para mi cafetería. Su calculadora de tarifas es transparente y el soporte vía WhatsApp nos resuelve todo al instante.', img: 'https://images.unsplash.com/photo-1580489944761-15a19d654956?q=80&w=200&auto=format&fit=crop' }
                ],
                next() { this.activeSlide = (this.activeSlide + 1) % this.testimonials.length },
                prev() { this.activeSlide = (this.activeSlide - 1 + this.testimonials.length) % this.testimonials.length }
             }">
             
            <div class="text-center max-w-3xl mx-auto mb-16">
                <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight font-display">Pymes que confían en nosotros</h2>
                <div class="w-16 h-1 bg-tealCustom mx-auto mt-4 rounded-full"></div>
            </div>

            <!-- Testimonial Slider Wrapper (White card surface) -->
            <div class="relative bg-white border border-slate-200 p-8 md:p-14 rounded-3xl shadow-lg">
                <!-- Slides Container -->
                <div class="min-h-[220px] flex items-center">
                    <template x-for="(test, index) in testimonials" :key="index">
                        <div x-show="activeSlide === index" 
                             x-transition:enter="transition ease-out duration-500"
                             x-transition:enter-start="opacity-0 transform translate-x-12"
                             x-transition:enter-end="opacity-100 transform translate-x-0"
                             class="space-y-6 md:space-y-0 md:flex md:items-center md:space-x-10">
                            
                            <!-- Profile picture border layout with custom gradients -->
                            <div class="flex-shrink-0 flex justify-center">
                                <div class="w-24 h-24 rounded-full p-1.5 bg-gradient-to-tr from-tealCustom to-goldCustom shadow-md">
                                    <img :src="test.img" :alt="test.name" class="w-full h-full object-cover rounded-full border-2 border-white">
                                </div>
                            </div>
                            
                            <!-- Content -->
                            <div class="flex-grow space-y-4 text-center md:text-left">
                                <i data-lucide="quote" class="w-8 h-8 text-tealCustom/20 mx-auto md:mx-0"></i>
                                <p class="text-base md:text-xl text-charcoal font-light italic leading-relaxed" x-text="'&ldquo;' + test.text + '&rdquo;'"></p>
                                <div>
                                    <h4 class="text-lg font-bold text-navy" x-text="test.name"></h4>
                                    <p class="text-xs font-semibold text-tealCustom uppercase tracking-wider mt-0.5" x-text="test.role"></p>
                                </div>
                            </div>
                        </div>
                    </template>
                </div>

                <!-- Navigation Controls -->
                <div class="flex justify-between items-center mt-10 border-t border-slate-100 pt-6">
                    <div class="flex space-x-2">
                        <template x-for="(dot, dIndex) in testimonials">
                            <button @click="activeSlide = dIndex" 
                                    class="w-2.5 h-2.5 rounded-full transition-all duration-300"
                                    :class="activeSlide === dIndex ? 'bg-tealCustom w-6' : 'bg-slate-200 hover:bg-slate-350'"></button>
                        </template>
                    </div>
                    <div class="flex space-x-3">
                        <button @click="prev()" class="p-2.5 rounded-xl border border-slate-200 hover:border-tealCustom text-slate-400 hover:text-tealCustom bg-slate-50 transition-all">
                            <i data-lucide="chevron-left" class="w-5 h-5"></i>
                        </button>
                        <button @click="next()" class="p-2.5 rounded-xl border border-slate-200 hover:border-tealCustom text-slate-400 hover:text-tealCustom bg-slate-50 transition-all">
                            <i data-lucide="chevron-right" class="w-5 h-5"></i>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- --- 7. FAQ ACCORDION SECTION --- -->
    <section class="py-24 md:py-32 relative bg-slate-50 border-b border-slate-200">
        <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10" x-data="{ activeFaq: null }">
            
            <div class="text-center max-w-3xl mx-auto mb-16">
                <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight font-display">Preguntas Frecuentes</h2>
                <p class="text-charcoal-light mt-4.5 text-base md:text-lg font-light">Todas las dudas contables de tu negocio resueltas de forma clara.</p>
            </div>

            <div class="space-y-4.5">
                <!-- FAQ Item 1 -->
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden transition-all duration-300" :class="activeFaq === 1 ? 'border-tealCustom shadow-md' : ''">
                    <button @click="activeFaq = (activeFaq === 1 ? null : 1)" class="w-full flex justify-between items-center p-6 text-left focus:outline-none">
                        <span class="font-bold text-navy text-base md:text-lg">¿Qué trámites incluye la contabilidad mensual?</span>
                        <i data-lucide="chevron-down" class="w-5 h-5 text-slate-400 transition-transform duration-300" :class="activeFaq === 1 ? 'rotate-180 text-tealCustom' : ''"></i>
                    </button>
                    <div x-show="activeFaq === 1" x-collapse x-cloak>
                        <div class="px-6 pb-6 pt-1 text-charcoal text-sm md:text-base leading-relaxed font-light border-t border-slate-100">
                            Incluye el procesamiento mensual de tu Registro de Compras y Ventas (RCV), conciliación de tus cuentas bancarias corporativas, declaración de tu Formulario F29 de IVA, cálculo de retención de boletas de honorarios y generación de balances generales.
                        </div>
                    </div>
                </div>

                <!-- FAQ Item 2 -->
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden transition-all duration-300" :class="activeFaq === 2 ? 'border-tealCustom shadow-md' : ''">
                    <button @click="activeFaq = (activeFaq === 2 ? null : 2)" class="w-full flex justify-between items-center p-6 text-left focus:outline-none">
                        <span class="font-bold text-navy text-base md:text-lg">¿Cómo se gestiona el cálculo de trabajadores y Previred?</span>
                        <i data-lucide="chevron-down" class="w-5 h-5 text-slate-400 transition-transform duration-300" :class="activeFaq === 2 ? 'rotate-180 text-tealCustom' : ''"></i>
                    </button>
                    <div x-show="activeFaq === 2" x-collapse x-cloak>
                        <div class="px-6 pb-6 pt-1 text-charcoal text-sm md:text-base leading-relaxed font-light border-t border-slate-100">
                            Nos envías las novedades del mes (inasistencias, comisiones, licencias médicas) y nosotros calculamos la liquidación de sueldo líquida y bruta. Luego, cargamos el archivo de forma automática en la plataforma Previred para que tú solo tengas que autorizar el pago con tu banco.
                        </div>
                    </div>
                </div>

                <!-- FAQ Item 3 -->
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden transition-all duration-300" :class="activeFaq === 3 ? 'border-tealCustom shadow-md' : ''">
                    <button @click="activeFaq = (activeFaq === 3 ? null : 3)" class="w-full flex justify-between items-center p-6 text-left focus:outline-none">
                        <span class="font-bold text-navy text-base md:text-lg">¿La Operación Renta (F22) se cobra por separado?</span>
                        <i data-lucide="chevron-down" class="w-5 h-5 text-slate-400 transition-transform duration-300" :class="activeFaq === 3 ? 'rotate-180 text-tealCustom' : ''"></i>
                    </button>
                    <div x-show="activeFaq === 3" x-collapse x-cloak>
                        <div class="px-6 pb-6 pt-1 text-charcoal text-sm md:text-base leading-relaxed font-light border-t border-slate-100">
                            En el **Plan Estándar** y **PYME** la Operación Renta básica anual está incorporada sin cobros adicionales siempre que el cliente lleve más de 8 meses continuos de servicio con nosotros. En el Plan Básico o casos especiales, se realiza una cotización preferencial.
                        </div>
                    </div>
                </div>

                <!-- FAQ Item 4 -->
                <div class="bg-white border border-slate-200 rounded-2xl overflow-hidden transition-all duration-300" :class="activeFaq === 4 ? 'border-tealCustom shadow-md' : ''">
                    <button @click="activeFaq = (activeFaq === 4 ? null : 4)" class="w-full flex justify-between items-center p-6 text-left focus:outline-none">
                        <span class="font-bold text-navy text-base md:text-lg">¿Tengo contrato de permanencia o exclusión?</span>
                        <i data-lucide="chevron-down" class="w-5 h-5 text-slate-400 transition-transform duration-300" :class="activeFaq === 4 ? 'rotate-180 text-tealCustom' : ''"></i>
                    </button>
                    <div x-show="activeFaq === 4" x-collapse x-cloak>
                        <div class="px-6 pb-6 pt-1 text-charcoal text-sm md:text-base leading-relaxed font-light border-t border-slate-100">
                            No exigimos contratos forzosos. Creemos en la libertad y calidad del servicio. Si deseas dar de baja la asesoría, solo nos debes avisar con 30 días de anticipación para realizar el cierre ordenado de tu carpeta tributaria y entregarte tu clave del SII limpia.
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- --- 8. CONTACT SECTION --- -->
    <section id="contacto" class="py-24 md:py-32 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10">
        
        <div class="text-center max-w-3xl mx-auto mb-20">
            <div class="inline-flex items-center space-x-2 bg-tealCustom/10 border border-tealCustom/25 px-4 py-1.5 rounded-full mb-4">
                <span class="text-xs font-bold text-tealCustom uppercase tracking-widest">Hablemos hoy</span>
            </div>
            <h2 class="text-3xl md:text-5xl font-black text-navy tracking-tight">Hablemos de tu negocio</h2>
            <p class="text-charcoal-light mt-4.5 text-base md:text-lg font-light leading-relaxed">
                Déjanos tus datos y un asesor te contactará a la brevedad.
            </p>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-12 items-stretch">
            <!-- Form Card (White Surface Card) -->
            <div id="form-container" class="lg:col-span-7 bg-white border border-slate-200 p-8 md:p-12 rounded-3xl shadow-xl transition-all duration-500">
                <form onsubmit="event.preventDefault(); alert('¡Mensaje enviado con éxito! Nos contactaremos contigo a la brevedad.');" class="space-y-6">
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-xs font-bold uppercase tracking-wider text-charcoal-light">Nombre completo</label>
                            <input type="text" class="w-full px-4.5 py-3.5 rounded-xl border border-slate-200 bg-slate-50 focus:outline-none focus:ring-2 focus:ring-tealCustom/25 focus:border-tealCustom text-charcoal text-sm transition-all" placeholder="Juan Pérez" required />
                        </div>
                        <div class="space-y-2">
                            <label class="block text-xs font-bold uppercase tracking-wider text-charcoal-light">Correo electrónico</label>
                            <input type="email" class="w-full px-4.5 py-3.5 rounded-xl border border-slate-200 bg-slate-50 focus:outline-none focus:ring-2 focus:ring-tealCustom/25 focus:border-tealCustom text-charcoal text-sm transition-all" placeholder="juan@empresa.cl" required />
                        </div>
                    </div>
                    
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                        <div class="space-y-2">
                            <label class="block text-xs font-bold uppercase tracking-wider text-charcoal-light">Teléfono de contacto</label>
                            <input type="tel" class="w-full px-4.5 py-3.5 rounded-xl border border-slate-200 bg-slate-50 focus:outline-none focus:ring-2 focus:ring-tealCustom/25 focus:border-tealCustom text-charcoal text-sm transition-all" placeholder="+56 9 1234 5678" required />
                        </div>
                        <div class="space-y-2">
                            <label class="block text-xs font-bold uppercase tracking-wider text-charcoal-light">RUT Empresa (Opcional)</label>
                            <input type="text" class="w-full px-4.5 py-3.5 rounded-xl border border-slate-200 bg-slate-50 focus:outline-none focus:ring-2 focus:ring-tealCustom/25 focus:border-tealCustom text-charcoal text-sm transition-all" placeholder="76.123.456-K" />
                        </div>
                    </div>

                    <div class="space-y-2">
                        <label class="block text-xs font-bold uppercase tracking-wider text-charcoal-light">Mensaje o requerimiento</label>
                        <textarea id="contacto-mensaje" rows="4" class="w-full px-4.5 py-3.5 rounded-xl border border-slate-200 bg-slate-50 focus:outline-none focus:ring-2 focus:ring-tealCustom/25 focus:border-tealCustom text-charcoal text-sm transition-all resize-none" placeholder="Cuéntanos brevemente sobre tu pyme..." required></textarea>
                    </div>

                    <button type="submit" class="w-full bg-tealCustom hover:bg-tealCustom/90 text-white font-bold py-4.5 rounded-xl text-base shadow-lg shadow-tealCustom/15 hover:shadow-tealCustom/30 hover:-translate-y-0.5 transition-all duration-200">
                        Enviar mensaje
                    </button>
                </form>
            </div>

            <!-- Contact Information Side Card -->
            <div class="lg:col-span-5 flex flex-col justify-between space-y-6">
                <div class="bg-white border border-slate-200 p-6.5 rounded-2xl flex items-start space-x-4.5 shadow-sm">
                    <div class="p-3.5 bg-slate-50 rounded-xl text-tealCustom border border-slate-100"><i data-lucide="phone" class="w-5.5 h-5.5"></i></div>
                    <div>
                        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">Llámanos</h4>
                        <p class="text-base text-navy font-semibold">+56 2 2345 6789</p>
                    </div>
                </div>

                <div class="bg-white border border-slate-200 p-6.5 rounded-2xl flex items-start space-x-4.5 shadow-sm">
                    <div class="p-3.5 bg-slate-50 rounded-xl text-tealCustom border border-slate-100"><i data-lucide="mail" class="w-5.5 h-5.5"></i></div>
                    <div>
                        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">Escríbenos</h4>
                        <p class="text-base text-navy font-semibold">contacto@conectacontable.cl</p>
                    </div>
                </div>

                <div class="bg-white border border-slate-200 p-6.5 rounded-2xl flex items-start space-x-4.5 shadow-sm">
                    <div class="p-3.5 bg-slate-50 rounded-xl text-tealCustom border border-slate-100"><i data-lucide="map-pin" class="w-5.5 h-5.5"></i></div>
                    <div>
                        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-widest mb-1">Oficina Central</h4>
                        <p class="text-sm text-charcoal leading-relaxed font-semibold">Av. Andrés Bello 2711, Las Condes, Santiago, Chile.</p>
                    </div>
                </div>

                <!-- Styled Dark Map Visual (Elegant Navy streets styling!) -->
                <div class="w-full h-56 bg-navy border border-white/10 rounded-3xl overflow-hidden shadow-xl relative group">
                    <div class="absolute inset-0 bg-[#16223B] flex items-center justify-center pointer-events-none opacity-85 transition-all duration-500 group-hover:scale-105">
                        <svg class="w-full h-full stroke-white/10 stroke-[0.5]" viewBox="0 0 400 200">
                            <!-- Streets grid -->
                            <line x1="0" y1="50" x2="400" y2="50" />
                            <line x1="0" y1="120" x2="400" y2="120" />
                            <line x1="100" y1="0" x2="100" y2="200" />
                            <line x1="280" y1="0" x2="280" y2="200" />
                            <line x1="0" y1="20" x2="400" y2="190" stroke-width="0.3" />
                            <!-- costanera center marker -->
                            <rect x="250" y="70" width="40" height="40" rx="4" fill="none" class="stroke-tealCustom/25 stroke-[1]" />
                            <circle cx="270" cy="90" r="3.5" fill="#C9A84C" />
                            <circle cx="270" cy="90" r="10" fill="none" class="stroke-goldCustom/30 stroke-[1] animate-ping" />
                        </svg>
                    </div>
                    <div class="absolute bottom-4 left-4 bg-navy/95 border border-white/10 text-white text-xs font-semibold px-3 py-1.5 rounded-lg shadow-md flex items-center gap-1.5">
                        <i data-lucide="map-pin" class="w-3.5 h-3.5 text-goldCustom"></i> Santiago, Chile
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- --- FOOTER (Azul Marino Profundo Background) --- -->
    <footer class="bg-navy border-t border-white/10 py-12 text-center text-xs text-slate-400 relative z-10">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 space-y-6">
            <div class="flex justify-center space-x-6">
                <a href="#servicios" class="text-slate-300 hover:text-tealCustom transition-colors">Servicios</a>
                <a href="#calculadora" class="text-slate-300 hover:text-tealCustom transition-colors">Cotizador</a>
                <a href="#planes" class="text-slate-300 hover:text-tealCustom transition-colors">Planes</a>
                <a href="#contacto" class="text-slate-300 hover:text-tealCustom transition-colors">Contacto</a>
            </div>
            <p class="leading-relaxed">&copy; 2026 ConectaContable. Todos los derechos reservados. Diseñado para PYMEs en Chile.</p>
        </div>
    </footer>

    <script>
        // Init Lucide Icons
        lucide.createIcons();
    </script>
</body>
</html>
