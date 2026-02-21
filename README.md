# 🔐 Primeros Pasos Cifrando 

Aplicación interactiva desarrollada con **HTML, CSS y JavaScript puro** que permite cifrar y descifrar mensajes utilizando algoritmos clásicos de criptografía:

- Cifrado César
- Cifrado Atbash

#Control de Modo
function setMode(mode) {
  currentMode = mode;
  document.getElementById('btn-encrypt').className =
    'mode-btn' + (mode === 'encrypt' ? ' active' : '');
  document.getElementById('btn-decrypt').className =
    'mode-btn' + (mode === 'decrypt' ? ' active-red' : '');
}

Esta función:
actualiza el estado interno
cambia estilos visuales

#Selección de Algoritmo
function setCipher(cipher) {
  currentCipher = cipher;
  document.getElementById('btn-cesar').classList.toggle('active', cipher === 'cesar');
  document.getElementById('btn-atbash').classList.toggle('active', cipher === 'atbash');
  document.getElementById('shift-section').style.display =
    cipher === 'cesar' ? 'block' : 'none';
}

Lógica
Busca índice del carácter
Aplica desplazamiento
Usa módulo para circular
Si el carácter no está en el charset:
if (idx === -1) return char;
No se modifica.

# Algoritmo Atbash
function atbashCipher(text, charset) {
  const last = charset.length - 1;

  return text.split('').map(char => {
    const idx = charset.indexOf(char);
    if (idx === -1) return char;
    return charset[last - idx];
  }).join('');
}
Funciona como espejo:
primero ↔ último
segundo ↔ penúltimo
Es simétrico: cifrar = descifrar.

function process() {
Controla todo el sistema.

#Lectura de inputs
const inputText  = document.getElementById('input-text').value;
const charsetRaw = document.getElementById('charset-input').value;
const shift      = parseInt(document.getElementById('shift').value);

#Validaciones
if (!inputText.trim()) return alert('Escribe un mensaje');
if (!charsetRaw.trim()) return alert('Define el conjunto');
