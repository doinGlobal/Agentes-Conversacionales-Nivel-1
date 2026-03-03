<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Escenario 1</title>

  <!-- Fuente Poppins -->
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --verde: #99cc06;
      --gris-oscuro: #262626;
    }

    /* Reset */
    html, body {
      height: 100%;
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
      background: #000;
    }

    /* Iframe full screen */
    iframe {
      position: fixed;
      inset: 0;
      width: 100%;
      height: 100%;
      border: 0;
      display: block;
      background: #000;
    }

    /* Pop-Up Styles */
    .popup {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-color: rgba(0, 0, 0, 0.55);
      justify-content: center;
      align-items: center;
      z-index: 10000;
      padding: 16px;
      box-sizing: border-box;
    }

    .popup-content {
      background-color: #fff;
      padding: 20px;
      border-radius: 10px;
      width: 92vw;
      max-width: 560px;
      text-align: center;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.35);
      position: relative;
    }

    .popup-content h2 {
      margin: 0 0 8px;
      font-weight: 700;
      color: var(--verde);
    }

    .popup-content p {
      margin: 10px 0;
      line-height: 1.45;
      font-size: 15px;
      color: #222;
    }

    #Gif {
      width: 100%;
      max-width: 520px;
      height: auto;
      border-radius: 10px;
      margin: 12px auto 6px;
      display: block;
      animation: zoomIn 0.35s ease-in-out;
    }

    @keyframes zoomIn {
      from { transform: scale(0.95); opacity: 0; }
      to   { transform: scale(1); opacity: 1; }
    }

    .popup .continue-button {
      margin-top: 14px;
      padding: 12px 20px;
      background-color: var(--gris-oscuro);
      color: #fff;
      border: none;
      font-weight: 600;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.2s ease, transform 0.05s ease;
    }

    .popup .continue-button:hover { background-color: #111; }
    .popup .continue-button:active { transform: translateY(1px); }

    .popup .close {
      position: absolute;
      top: 10px;
      right: 12px;
      font-size: 24px;
      cursor: pointer;
      color: #333;
      line-height: 1;
      user-select: none;
    }

    /* Small screens */
    @media (max-width: 420px) {
      .popup-content { padding: 16px; }
      .popup-content p { font-size: 14px; }
    }
  </style>
</head>
<body>

  <!-- HeyGen LiveAvatar Embed -->
  <iframe
    src="https://embed.liveavatar.com/v1/a44b83a9-761d-402a-8827-6a082f0e446d"
    allow="microphone"
    title="LiveAvatar Embed"
    style="aspect-ratio: 16/9;"
  ></iframe>

  <!-- GIF Pop-Up -->
  <div id="popup" class="popup" role="dialog" aria-modal="true" aria-labelledby="popupTitle">
    <div class="popup-content">
      <span id="closePopup" class="close" aria-label="Cerrar">&times;</span>

      <h2 id="popupTitle"><b>Importante</b></h2>

      <p><b>Para interactuar con el avatar, tené en cuenta estas indicaciones:</b></p>

      <p><b>1) Configurá tu conversación:</b> hacé clic en <b>"Start new chat"</b> y elegí el idioma <b>"Spanish"</b>.</p>

      <img id="Gif" src="./assets/gif-popup.gif" alt="Ejemplo de configuración de idioma en HeyGen LiveAvatar">

      <p><b>2) Activá el micrófono en el navegador:</b> cuando te lo pida, elegí <b>"Permitir"</b>. Esto se hace una sola vez.</p>

      <button id="continueButton" class="continue-button">Continuar</button>
    </div>
  </div>

  <script>
    // Mostrar el pop-up al cargar la página.
    // (Tip) Si querés que aparezca solo una vez por sesión, cambiá localStorage por sessionStorage.
    window.addEventListener('load', () => {
      const key = 'heygen_popup_seen';
      const seen = localStorage.getItem(key);
      if (!seen) {
        document.getElementById('popup').style.display = 'flex';
      }
    });

    function closePopup() {
      document.getElementById('popup').style.display = 'none';
      localStorage.setItem('heygen_popup_seen', '1');
    }

    document.getElementById('closePopup').addEventListener('click', closePopup);
    document.getElementById('continueButton').addEventListener('click', closePopup);

    // Cerrar con ESC
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') closePopup();
    });
  </script>
</body>
</html>
