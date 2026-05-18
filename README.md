import React, { useState } from 'react';
import { Sparkles, Rocket, Search, Trophy, ArrowRight, Star, RefreshCw, CheckCircle2, XCircle, Home, Brain, Binary, LayoutGrid, Ruler, Target, FerrisWheel } from 'lucide-react';

// Preguntas categorizadas
const allQuestions = [
  {
    id: 1,
    category: 'cero_uno',
    theme: "El Agujero Negro Espacial 🌌",
    icon: <Binary className="w-8 h-8 text-orange-500" />,
    question: "Si tienes 45 varitas mágicas y las multiplicas por 0, ¡el agujero negro se las lleva! ¿Cuál es el resultado de 45 x 0?",
    options: [
      { text: "45", isCorrect: false, feedback: "Recuerda que el cero actúa como un agujero negro." },
      { text: "0", isCorrect: true, feedback: "¡Exacto! Todo número multiplicado por cero siempre da cero." },
      { text: "1", isCorrect: false, feedback: "Ese sería el resultado si dividieras el número por sí mismo." },
      { text: "450", isCorrect: false, feedback: "Eso pasaría si multiplicaras por 10." }
    ]
  },
  {
    id: 2,
    category: 'cero_uno',
    theme: "El Espejo Mágico 🪞",
    icon: <Binary className="w-8 h-8 text-orange-500" />,
    question: "Tienes 128 dulces y los multiplicas por 1. El número se mira al espejo y... ¿Cuál es el producto de 128 x 1?",
    options: [
      { text: "0", isCorrect: false, feedback: "Esto pasaría si multiplicaras por el agujero negro (cero)." },
      { text: "128", isCorrect: true, feedback: "¡Súper! Al multiplicar cualquier número por 1, el resultado es el mismo número." },
      { text: "1", isCorrect: false, feedback: "El 1 es el espejo, ¡pero no el resultado!" },
      { text: "1281", isCorrect: false, feedback: "No hay que pegarle el 1 al final, sino multiplicar." }
    ]
  },
  {
    id: 3,
    category: 'trucos',
    theme: "Truco de Superhéroe 🚀",
    icon: <Brain className="w-8 h-8 text-blue-500" />,
    question: "Para usar la técnica del 'doble del doble' y calcular 7 x 4, ¿qué debes hacer primero?",
    options: [
      { text: "Sumar 7 + 4", isCorrect: false, feedback: "Estamos multiplicando, ¡no sumando!" },
      { text: "Calcular la mitad de 7", isCorrect: false, feedback: "Para el doble necesitamos multiplicar por 2, no dividir." },
      { text: "Multiplicar 7 x 2 x 4", isCorrect: false, feedback: "Eso sería multiplicar por 8, ¡demasiado grande!" },
      { text: "Calcular el doble de 7", isCorrect: true, feedback: "¡Correcto! Primero calculamos 7 x 2 = 14, y luego el doble de 14." }
    ]
  },
  {
    id: 4,
    category: 'trucos',
    theme: "Balanza Mágica ⚖️",
    icon: <Brain className="w-8 h-8 text-blue-500" />,
    question: "Si usas el truco 'mitad y doble' para hacer más fácil 14 x 5, ¿en qué se transforma la operación?",
    options: [
      { text: "7 x 10", isCorrect: true, feedback: "¡Excelente! Cortas el 14 a la mitad (7) y doblas el 5 (10). ¡7 x 10 es mucho más fácil!" },
      { text: "28 x 10", isCorrect: false, feedback: "Aquí doblaste ambos números." },
      { text: "7 x 5", isCorrect: false, feedback: "Dividiste el 14, pero olvidaste doblar el 5." },
      { text: "14 x 10", isCorrect: false, feedback: "Dejaste el 14 igual y solo doblaste el 5." }
    ]
  },
  {
    id: 5,
    category: 'distributiva',
    theme: "Rompecabezas Numérico 🧩",
    icon: <LayoutGrid className="w-8 h-8 text-purple-500" />,
    question: "Usando la 'propiedad distributiva' para desarmar números, ¿cómo se expresa 6 x 15?",
    options: [
      { text: "(6 + 10) x 5", isCorrect: false, feedback: "El 6 debe multiplicar a las piezas del 15, no sumarse." },
      { text: "6 x (10 + 5) = (6 x 10) + (6 x 5)", isCorrect: true, feedback: "¡Magia pura! Desarmaste el 15 en 10 + 5, y el 6 multiplicó a cada uno." },
      { text: "6 x 10 x 5", isCorrect: false, feedback: "Se combina multiplicación con suma, no puras multiplicaciones." },
      { text: "6 + (10 x 5)", isCorrect: false, feedback: "El 6 es un factor, no se debe sumar al final." }
    ]
  },
  {
    id: 6,
    category: 'estimacion',
    theme: "Aproximando como Detective 🕵️‍♀️",
    icon: <Target className="w-8 h-8 text-green-600" />,
    question: "Quieres comprar 6 jugos que cuestan $790 cada uno. Si redondeas $790 a la centena para estimar rápido, ¿qué valor usarías?",
    options: [
      { text: "$700", isCorrect: false, feedback: "$790 está mucho más cerca de la siguiente centena." },
      { text: "$800", isCorrect: true, feedback: "¡Gran deducción! $790 está a solo 10 pesos de $800." },
      { text: "$750", isCorrect: false, feedback: "Esa no es una centena exacta." },
      { text: "$900", isCorrect: false, feedback: "¡Te pasaste de largo!" }
    ]
  },
  {
    id: 7,
    category: 'algoritmo',
    theme: "Desafío Final del Campeón 🏆",
    icon: <Ruler className="w-8 h-8 text-red-500" />,
    question: "Si un paquete de lápices cuesta $280 y compras 6 paquetes, ¿cuánto pagas en total? (Pista: Haz 200x6 y 80x6 y suma)",
    options: [
      { text: "$1.480", isCorrect: false, feedback: "Revisa la suma: 1200 + 480 da un poco más." },
      { text: "$1.280", isCorrect: false, feedback: "Olvidaste sumar lo que te dio 80 x 6." },
      { text: "$1.680", isCorrect: true, feedback: "¡Eres brillante! 200x6=1200 y 80x6=480. Al sumarlos da 1.680." },
      { text: "$1.880", isCorrect: false, feedback: "La suma es un poquito menor." }
    ]
  }
];

// Opciones del Menú Principal
const menuItems = [
  { id: 'all', title: 'Rueda de la Fortuna', badge: 'Inicio', badgeColor: 'bg-green-500', icon: <FerrisWheel className="w-14 h-14 text-indigo-400" /> },
  { id: 'trucos', title: 'Trucos Mentales', badge: 'Básico', badgeColor: 'bg-blue-500', icon: <Brain className="w-14 h-14 text-pink-400" /> },
  { id: 'cero_uno', title: 'El 0 y el 1', badge: 'Importante', badgeColor: 'bg-orange-500', icon: <div className="w-14 h-14 bg-blue-500 rounded-xl text-white flex items-center justify-center font-black text-3xl shadow-inner animate-pulse-soft">0</div> },
  { id: 'distributiva', title: 'Propiedad Distributiva', badge: 'Intermedio', badgeColor: 'bg-purple-600', icon: <div className="w-14 h-14 bg-blue-400 rounded-xl text-white flex flex-col items-center justify-center font-black text-sm leading-none shadow-inner"><span>1 2</span><span>3 4</span></div> },
  { id: 'algoritmo', title: 'Multiplicación con Algoritmo', badge: 'Avanzado', badgeColor: 'bg-red-500', icon: <Ruler className="w-14 h-14 text-gray-400" /> },
  { id: 'estimacion', title: 'Estimación de Productos', badge: 'Estimación', badgeColor: 'bg-green-500', icon: <Target className="w-14 h-14 text-pink-500" /> },
];

// Componente Gatito Kawaii 2D Sólido
function KawaiiCat2D({ expression }) {
  // Configuración de colores del gatito
  const bodyColor = "#FFC83B";       // Amarillo/Naranja kawaii suave
  const shadowColor = "#E09B14";     // Bordes y detalles
  const cheekColor = "#FF9494";      // Color de las mejillas sonrosadas
  const eyeColor = "#2C3E50";        // Color de ojos oscuros

  return (
    <svg viewBox="0 0 100 100" className="w-20 h-20 md:w-32 md:h-32 drop-shadow-xl transition-all duration-300">
      {/* Oreja Izquierda */}
      <polygon 
        points="18,38 12,12 38,26" 
        fill={bodyColor} 
        stroke={shadowColor} 
        strokeWidth="3.5" 
        strokeLinejoin="round" 
      />
      <polygon points="21,34 16,18 33,26" fill={cheekColor} />

      {/* Oreja Derecha */}
      <polygon 
        points="82,38 88,12 62,26" 
        fill={bodyColor} 
        stroke={shadowColor} 
        strokeWidth="3.5" 
        strokeLinejoin="round" 
      />
      <polygon points="79,34 84,18 67,26" fill={cheekColor} />

      {/* Cabeza Redondita */}
      <rect 
        x="15" 
        y="23" 
        width="70" 
        height="62" 
        rx="31" 
        ry="27" 
        fill={bodyColor} 
        stroke={shadowColor} 
        strokeWidth="3.5" 
      />

      {/* Bigotes */}
      {/* Izquierda */}
      <line x1="6" y1="56" x2="19" y2="58" stroke={shadowColor} strokeWidth="3" strokeLinecap="round" />
      <line x1="4" y1="64" x2="17" y2="64" stroke={shadowColor} strokeWidth="3" strokeLinecap="round" />
      {/* Derecha */}
      <line x1="94" y1="56" x2="81" y2="58" stroke={shadowColor} strokeWidth="3" strokeLinecap="round" />
      <line x1="96" y1="64" x2="83" y2="64" stroke={shadowColor} strokeWidth="3" strokeLinecap="round" />

      {/* Mejillas Sonrosadas (Blush) */}
      <ellipse cx="28" cy="62" rx="7" ry="4.5" fill={cheekColor} opacity="0.8" />
      <ellipse cx="72" cy="62" rx="7" ry="4.5" fill={cheekColor} opacity="0.8" />

      {/* Expresiones Interactivas */}
      {expression === 'neutral' && (
        <>
          {/* Ojos curiosos y brillantes */}
          <circle cx="34" cy="48" r="6.5" fill={eyeColor} />
          <circle cx="32" cy="45" r="2.5" fill="#FFFFFF" />
          <circle cx="35.5" cy="50.5" r="1.2" fill="#FFFFFF" />

          <circle cx="66" cy="48" r="6.5" fill={eyeColor} />
          <circle cx="64" cy="45" r="2.5" fill="#FFFFFF" />
          <circle cx="67.5" cy="50.5" r="1.2" fill="#FFFFFF" />

          {/* Boquita Kawaii de Gato (w) */}
          <path 
            d="M 45 56 Q 48 59 50 56 Q 52 59 55 56" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="3.5" 
            strokeLinecap="round" 
          />
        </>
      )}

      {expression === 'success' && (
        <>
          {/* Ojos cerrados de felicidad feliz ^ _ ^ */}
          <path 
            d="M 26 50 Q 33 41 40 50" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="4.5" 
            strokeLinecap="round" 
          />
          <path 
            d="M 60 50 Q 67 41 74 50" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="4.5" 
            strokeLinecap="round" 
          />
          {/* Boca grande y alegre abierta */}
          <path 
            d="M 45 57 Q 50 66 55 57 Z" 
            fill="#FF5E7E" 
            stroke={eyeColor} 
            strokeWidth="3.5" 
            strokeLinejoin="round" 
          />
        </>
      )}

      {expression === 'error' && (
        <>
          {/* Ojos tristes decaídos */}
          <path 
            d="M 27 44 Q 34 52 41 44" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="4.5" 
            strokeLinecap="round" 
          />
          <path 
            d="M 59 44 Q 66 52 73 44" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="4.5" 
            strokeLinecap="round" 
          />
          {/* Boquita triste curvada hacia abajo */}
          <path 
            d="M 45 59 Q 50 54 55 59" 
            fill="none" 
            stroke={eyeColor} 
            strokeWidth="3.5" 
            strokeLinecap="round" 
          />
          {/* Lágrima Kawaii azul flotante */}
          <path 
            d="M 22 54 Q 22 66 26 66 Q 30 66 30 54 Z" 
            fill="#4D96FF" 
            className="animate-pulse-soft"
          />
        </>
      )}
    </svg>
  );
}

// Generador de sonidos
const playSound = (type) => {
  try {
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    const oscillator = audioCtx.createOscillator();
    const gainNode = audioCtx.createGain();

    oscillator.connect(gainNode);
    gainNode.connect(audioCtx.destination);

    if (type === 'success') {
      oscillator.type = 'sine';
      oscillator.frequency.setValueAtTime(523.25, audioCtx.currentTime); // C5
      oscillator.frequency.setValueAtTime(659.25, audioCtx.currentTime + 0.1); // E5
      oscillator.frequency.setValueAtTime(783.99, audioCtx.currentTime + 0.2); // G5
      gainNode.gain.setValueAtTime(0.1, audioCtx.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 0.4);
      oscillator.start();
      oscillator.stop(audioCtx.currentTime + 0.4);
    } else if (type === 'error') {
      oscillator.type = 'triangle';
      oscillator.frequency.setValueAtTime(300, audioCtx.currentTime);
      oscillator.frequency.exponentialRampToValueAtTime(100, audioCtx.currentTime + 0.3);
      gainNode.gain.setValueAtTime(0.1, audioCtx.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 0.3);
      oscillator.start();
      oscillator.stop(audioCtx.currentTime + 0.3);
    } else if (type === 'click') {
      oscillator.type = 'sine';
      oscillator.frequency.setValueAtTime(600, audioCtx.currentTime);
      gainNode.gain.setValueAtTime(0.05, audioCtx.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 0.1);
      oscillator.start();
      oscillator.stop(audioCtx.currentTime + 0.1);
    }
  } catch (e) {
    console.log("Audio no soportado");
  }
};

export default function App() {
  const [view, setView] = useState('menu'); // 'menu', 'quiz', 'end'
  const [activeQuestions, setActiveQuestions] = useState([]);
  const [currentQIndex, setCurrentQIndex] = useState(0);
  const [score, setScore] = useState(0);
  const [selectedOption, setSelectedOption] = useState(null);
  const [showFeedback, setShowFeedback] = useState(false);

  // Obtener la pregunta actual de forma segura
  const question = activeQuestions && activeQuestions.length > 0 ? activeQuestions[currentQIndex] : null;

  const startQuiz = (categoryId) => {
    playSound('click');
    const filtered = categoryId === 'all' 
      ? allQuestions 
      : allQuestions.filter(q => q.category === categoryId);
    
    setActiveQuestions(filtered);
    setCurrentQIndex(0);
    setScore(0);
    setSelectedOption(null);
    setShowFeedback(false);
    setView('quiz');
  };

  const handleOptionClick = (option) => {
    if (showFeedback) return;
    
    setSelectedOption(option);
    setShowFeedback(true);
    
    if (option.isCorrect) {
      playSound('success');
      setScore(score + 1);
    } else {
      playSound('error');
    }
  };

  const handleNext = () => {
    if (currentQIndex < activeQuestions.length - 1) {
      setCurrentQIndex(currentQIndex + 1);
      setSelectedOption(null);
      setShowFeedback(false);
    } else {
      setView('end');
      if (score === activeQuestions.length) {
          playSound('success');
          setTimeout(() => playSound('success'), 400);
      }
    }
  };

  const goHome = () => {
    playSound('click');
    setView('menu');
  };

  // Determinar la expresión actual del gatito
  let currentExpression = 'neutral';
  if (view === 'quiz' && showFeedback) {
    currentExpression = selectedOption?.isCorrect ? 'success' : 'error';
  } else if (view === 'end') {
    currentExpression = 'success';
  }

  // VISTA: MENÚ PRINCIPAL
  if (view === 'menu') {
    return (
      <div className="min-h-screen bg-gradient-to-br from-indigo-500 via-indigo-600 to-purple-600 flex flex-col items-center py-12 px-4 sm:px-8 font-sans relative overflow-hidden">
        
        {/* Cabecera Alegre y Animada con "Estudiando con el 4°A" */}
        <div className="z-10 text-center mb-10 mt-4 flex flex-col items-center">
          <div className="bg-yellow-400 text-purple-900 font-black px-8 py-3 rounded-full text-2xl sm:text-4xl shadow-lg border-4 border-white mb-5 animate-pulse-soft transform rotate-1 flex items-center space-x-2 select-none">
            <Sparkles className="w-8 h-8 text-indigo-950 animate-spin" style={{ animationDuration: '6s' }} />
            <span>🎉 ESTUDIANDO CON EL 4°A 🎒</span>
            <Sparkles className="w-8 h-8 text-indigo-950 animate-spin" style={{ animationDuration: '6s' }} />
          </div>
          <h1 className="text-xl sm:text-2xl font-semibold text-indigo-100 tracking-wide drop-shadow-md">
            Matemáticas 4° Básico · Unidad 1: Multiplicación
          </h1>
        </div>

        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6 max-w-5xl w-full z-10">
          {menuItems.map((item) => (
            <button
              key={item.id}
              onClick={() => startQuiz(item.id)}
              className="bg-white rounded-[2.5rem] p-8 flex flex-col items-center justify-between h-72 shadow-xl transform transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl group outline-none focus:ring-4 focus:ring-pink-300"
            >
              <div className="mt-4 transform transition-transform group-hover:scale-110 duration-300">
                {item.icon}
              </div>
              
              <h2 className="text-xl font-extrabold text-gray-800 text-center mt-4 mb-auto">
                {item.title}
              </h2>
              
              <div className={`${item.badgeColor} text-white font-bold text-sm px-6 py-1.5 rounded-full mt-4 shadow-md`}>
                {item.badge}
              </div>
            </button>
          ))}
        </div>

        {/* Gatito animando el menú flotando arriba a la derecha */}
        <div className="fixed top-8 right-6 md:top-12 md:right-12 z-50 animate-float pointer-events-none hidden sm:block">
          <KawaiiCat2D expression="neutral" />
        </div>

        {/* Burbujas de fondo */}
        <div className="fixed inset-0 pointer-events-none overflow-hidden z-0">
          <div className="absolute top-[10%] left-[5%] w-40 h-40 bg-white/10 rounded-full blur-2xl"></div>
          <div className="absolute bottom-[10%] right-[10%] w-64 h-64 bg-pink-400/20 rounded-full blur-3xl"></div>
        </div>
      </div>
    );
  }

  // VISTA: PANTALLA FINAL
  if (view === 'end') {
    return (
      <div className="min-h-screen bg-gradient-to-br from-indigo-400 via-purple-400 to-pink-400 flex items-center justify-center p-4">
        <div className="bg-white rounded-[3rem] shadow-2xl p-10 max-w-lg w-full text-center transform transition-all animate-bounce-short border-8 border-white/40">
          <div className="flex justify-center mb-6">
            <KawaiiCat2D expression="success" />
          </div>
          <h1 className="text-4xl font-extrabold text-purple-600 mb-4">¡Misión Completada!</h1>
          <p className="text-xl text-gray-700 mb-6 font-medium">
            Lograste <span className="font-black text-3xl text-pink-500">{score}</span> de {activeQuestions.length} estrellas.
          </p>
          
          {score === activeQuestions.length ? (
            <p className="text-xl text-green-500 font-bold mb-8">¡Eres un Maestro de las Matemáticas! 🌟</p>
          ) : score > activeQuestions.length / 2 ? (
            <p className="text-xl text-blue-500 font-bold mb-8">¡Súper buen trabajo! Sigue practicando. 🚀</p>
          ) : (
            <p className="text-xl text-orange-500 font-bold mb-8">¡No te rindas! ¡Tú puedes lograrlo! 💪</p>
          )}

          <div className="flex flex-col sm:flex-row gap-4 justify-center">
            <button 
              onClick={() => startQuiz(activeQuestions[0]?.category || 'all')}
              className="flex-1 bg-gradient-to-r from-pink-500 to-purple-500 hover:from-pink-600 hover:to-purple-600 text-white font-bold py-4 px-6 rounded-full shadow-lg transform transition hover:scale-105 flex items-center justify-center space-x-2"
            >
              <RefreshCw className="w-6 h-6" />
              <span>Reintentar</span>
            </button>
            <button 
              onClick={goHome}
              className="flex-1 bg-white border-4 border-indigo-100 hover:border-indigo-300 text-indigo-600 font-bold py-4 px-6 rounded-full shadow-lg transform transition hover:scale-105 flex items-center justify-center space-x-2"
            >
              <Home className="w-6 h-6" />
              <span>Menú</span>
            </button>
          </div>
        </div>
      </div>
    );
  }

  // VISTA: QUIZ
  return (
    <div className="min-h-screen bg-gradient-to-br from-cyan-300 via-blue-400 to-purple-500 flex flex-col items-center justify-center p-4 sm:p-8 font-sans relative overflow-hidden">
      
      {/* Botón Volver (Arriba Izquierda) */}
      <button 
        onClick={goHome}
        className="absolute top-6 left-6 z-20 bg-white/20 hover:bg-white/40 text-white p-3 rounded-full backdrop-blur-md transition-all duration-300"
      >
        <Home className="w-7 h-7" />
      </button>

      {/* Título Principal */}
      <div className="mb-6 mt-12 md:mt-0 text-center animate-fade-in z-10">
        <h1 className="text-3xl sm:text-5xl font-extrabold text-white drop-shadow-lg tracking-wide">
          Estudiando con el 4°A
        </h1>
      </div>

      <div className="bg-white/95 backdrop-blur-sm rounded-[3rem] shadow-[0_20px_50px_rgba(8,_112,_184,_0.4)] overflow-hidden max-w-2xl w-full flex flex-col border-4 border-white/50 relative z-10">
        
        {/* Header / Progress */}
        <div className="bg-indigo-50/80 p-6 sm:px-10 border-b border-indigo-100 flex items-center justify-between rounded-t-[2.7rem]">
          <div className="flex items-center space-x-4">
            <div className="bg-white p-3 rounded-full shadow-md">
              {question?.icon}
            </div>
            <div>
              <p className="text-sm font-bold text-indigo-400 uppercase tracking-widest">
                Misión {currentQIndex + 1} de {activeQuestions.length}
              </p>
              <h2 className="text-xl sm:text-2xl font-extrabold text-indigo-700">{question?.theme}</h2>
            </div>
          </div>
          <div className="hidden sm:flex space-x-2">
            {activeQuestions.map((_, idx) => (
              <div 
                key={idx} 
                className={`w-3 h-3 rounded-full transition-all duration-300 ${idx <= currentQIndex ? 'bg-pink-500 scale-110 shadow-[0_0_8px_rgba(236,72,153,0.8)]' : 'bg-indigo-200'}`}
              />
            ))}
          </div>
        </div>

        {/* Question Area */}
        <div className="p-6 sm:p-10 flex-grow">
          <h3 className="text-2xl sm:text-3xl font-extrabold text-gray-800 mb-8 leading-relaxed">
            {question?.question}
          </h3>

          <div className="grid grid-cols-1 sm:grid-cols-2 gap-5 mb-8">
            {question?.options.map((option, idx) => {
              let btnClass = "bg-white border-2 border-gray-200 hover:border-indigo-400 hover:bg-indigo-50 hover:-translate-y-1 hover:shadow-lg text-gray-700";
              
              if (showFeedback) {
                if (option.isCorrect) {
                  btnClass = "bg-green-100 border-[3px] border-green-500 text-green-800 font-bold scale-105 shadow-xl";
                } else if (selectedOption === option) {
                  btnClass = "bg-red-100 border-[3px] border-red-400 text-red-800 opacity-90 scale-95";
                } else {
                  btnClass = "bg-gray-50 border-2 border-gray-200 text-gray-400 opacity-50";
                }
              }

              return (
                <button
                  key={idx}
                  onClick={() => handleOptionClick(option)}
                  disabled={showFeedback}
                  className={`p-5 sm:p-7 text-xl font-medium rounded-[2rem] transition-all duration-300 transform outline-none focus:outline-none ${btnClass}`}
                >
                  {option.text}
                </button>
              );
            })}
          </div>

          {/* Feedback Area */}
          {showFeedback && (
            <div className={`p-6 rounded-[2rem] mb-2 animate-fade-in shadow-inner ${selectedOption?.isCorrect ? 'bg-green-100 text-green-900 border border-green-300' : 'bg-orange-100 text-orange-900 border border-orange-300'}`}>
              <div className="flex items-start space-x-4">
                <div className="mt-1">
                  {selectedOption?.isCorrect ? <CheckCircle2 className="w-10 h-10 text-green-600" /> : <XCircle className="w-10 h-10 text-orange-600" />}
                </div>
                <div>
                  <h4 className="text-xl font-extrabold mb-2">
                    {selectedOption?.isCorrect ? '¡Magnífico!' : '¡Casi, detective!'}
                  </h4>
                  <p className="text-lg font-medium">
                    {selectedOption?.isCorrect ? selectedOption.feedback : question?.options.find(o => o.isCorrect).feedback}
                  </p>
                </div>
              </div>
            </div>
          )}
        </div>

        {/* Footer */}
        <div className="bg-indigo-50/50 p-6 sm:px-10 border-t border-indigo-100 flex items-center justify-between rounded-b-[2.7rem]">
          <div className="flex items-center space-x-2 text-pink-500 font-extrabold text-xl">
            <Star className="w-7 h-7 fill-current drop-shadow-sm" />
            <span>Puntos: {score}</span>
          </div>
          
          <button
            onClick={handleNext}
            disabled={!showFeedback}
            className={`flex items-center space-x-2 py-4 px-10 rounded-full font-bold text-xl transition-all duration-300 ${showFeedback ? 'bg-indigo-600 hover:bg-indigo-500 text-white shadow-xl transform hover:scale-105' : 'bg-gray-200 text-gray-400 cursor-not-allowed'}`}
          >
            <span>{currentQIndex === activeQuestions.length - 1 ? 'Terminar' : 'Siguiente'}</span>
            <ArrowRight className="w-6 h-6" />
          </button>
        </div>

      </div>

      {/* Gatito Kawaii Flotante (Vector SVG Sólido, Gigante y Flotando) */}
      <div className="fixed top-8 right-6 md:top-12 md:right-12 z-50 animate-float pointer-events-none">
        <KawaiiCat2D expression={currentExpression} />
      </div>

      {/* Fondo con burbujas decorativas */}
      <div className="fixed inset-0 pointer-events-none overflow-hidden z-0">
        <div className="absolute top-[10%] left-[10%] w-32 h-32 bg-white/20 rounded-full blur-xl"></div>
        <div className="absolute bottom-[20%] right-[15%] w-48 h-48 bg-pink-400/20 rounded-full blur-2xl"></div>
        <div className="absolute top-[50%] right-[5%] w-24 h-24 bg-purple-300/30 rounded-full blur-lg"></div>
      </div>

      <style dangerouslySetInnerHTML={{__html: `
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(15px); }
          to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
          animation: fadeIn 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
        }
        @keyframes bounceShort {
          0%, 100% { transform: translateY(0); }
          50% { transform: translateY(-20px); }
        }
        .animate-bounce-short {
          animation: bounceShort 0.8s ease-in-out;
        }
        @keyframes float {
          0% { transform: translateY(0px) rotate(0deg); }
          50% { transform: translateY(-15px) rotate(3deg); }
          100% { transform: translateY(0px) rotate(0deg); }
        }
        .animate-float {
          animation: float 4s ease-in-out infinite;
        }
        @keyframes pulseSoft {
          0%, 100% { opacity: 1; transform: scale(1); }
          50% { opacity: 0.8; transform: scale(1.05); }
        }
        .animate-pulse-soft {
          animation: pulseSoft 2s ease-in-out infinite;
        }
      `}} />
    </div>
  );
}
