# mybiblegamehub-demo
<!doctype html>
<html lang="es" style="height: 100%; margin: 0; padding: 0;">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MyBibleGameHub-Iglesia Activa</title>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    body {
      box-sizing: border-box;
    }
    
    @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600;700&display=swap');
    
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    html, body {
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;
    }
    
    body {
      overflow: hidden;
      -webkit-overflow-scrolling: touch;
      font-family: 'Montserrat', system-ui, -apple-system, sans-serif;
    }

    :root {
      --bg-900: #031427;
      --bg-800: #062238;
      --bg-700: #0B3D91;
      --bg-600: #1565C0;
      --bg-500: #42A5F5;
      --text-on-dark: rgba(255,255,255,0.95);
    }

    body, #root, .app-container {
      background: linear-gradient(180deg, var(--bg-900), var(--bg-800));
      color: var(--text-on-dark);
    }

    /* Unified controls and surfaces for a clean, consistent look */
    .btn-base,
    .generate-btn,
    .start-game-btn,
    .next-verse-btn,
    .menu-button,
    .dropdown-toggle,
    .control-btn.primary,
    .bingo-menu-btn {
      background: linear-gradient(135deg, var(--bg-600) 0%, var(--bg-700) 100%);
      color: var(--text-on-dark);
      border: 1px solid rgba(21,101,192,0.18);
      border-radius: 0.75rem;
      padding: 0.9rem 1.25rem;
      font-weight: 700;
      box-shadow: 0 8px 22px rgba(3,20,39,0.45);
      transition: all 0.22s cubic-bezier(0.4,0,0.2,1);
    }

    .btn-base:hover,
    .generate-btn:hover,
    .start-game-btn:hover,
    .next-verse-btn:hover,
    .dropdown-toggle:hover,
    .control-btn.primary:hover,
    .bingo-menu-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 12px 30px rgba(3,20,39,0.55);
    }

    .action-btn,
    .control-btn,
    .back-to-menu-btn {
      background: rgba(3,20,39,0.18);
      border: 1px solid rgba(21,101,192,0.12);
      color: var(--text-on-dark);
      border-radius: 0.75rem;
      padding: 0.85rem 1rem;
      font-weight: 600;
      transition: all 0.18s;
    }

    .card-header {
      background: linear-gradient(135deg, var(--bg-500) 0%, var(--bg-600) 100%);
      padding: 1.5rem 1rem;
      text-align: center;
      border-bottom: 3px solid rgba(21,101,192,0.35);
    }

    .card-footer {
      background: linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
      border-radius: 0.75rem;
      border: 1px solid rgba(21,101,192,0.08);
      padding: 0.9rem;
    }
    
    #root {
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;
      position: relative;
    }
    
    .app-container {
      height: 100%;
      width: 100%;
      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }
    
    .no-select {
      user-select: none;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
    }
    
    .app-container,
    [tabindex],
    button {
      -webkit-tap-highlight-color: transparent;
    }
    
    /* Page System */
    .page {
      display: none;
      flex: 1;
      overflow-y: auto;
      overflow-x: hidden;
      -webkit-overflow-scrolling: touch;
    }
    
    .page.active {
      display: flex;
      flex-direction: column;
    }
    
    /* Home Screen Styles */
    .nav-bar {
      width: 100%;
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
      backdrop-filter: blur(10px);
      background: rgba(3,20,39,0.55);
      border-bottom: 3px solid rgba(21,101,192,0.45);
      flex-shrink: 0;
    }
    
    .nav-content {
      max-width: 1400px;
      margin: 0 auto;
      padding: 1rem 2rem;
      display: flex;
      flex-direction: column;
      gap: 1rem;
      position: relative;
    }
    
    .nav-left-section {
      display: flex;
      align-items: center;
      gap: 1.25rem;
      justify-content: flex-start;
    }
    
    .nav-right-section {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      justify-content: flex-start;
      flex-wrap: wrap;
    }
    
    .logo-section {
      display: flex;
      align-items: center;
      gap: 1.25rem;
      cursor: pointer;
    }
    
    .logo-svg {
      width: 45px;
      height: 45px;
      flex-shrink: 0;
      filter: drop-shadow(0 4px 8px rgba(33, 150, 243, 0.3));
      transition: transform 0.3s ease;
    }
    
    .logo-svg:hover {
      transform: scale(1.05) rotate(2deg);
    }
    
    .site-title {
      font-weight: 800;
      color: white;
      line-height: 1.2;
      font-size: 1.5rem;
      letter-spacing: -0.5px;
      text-shadow: 0 2px 8px rgba(33, 150, 243, 0.4);
    }
    
    .tagline {
      font-size: 0.8rem;
      color: white;
      opacity: 0.85;
      letter-spacing: 0.3px;
      font-weight: 500;
    }
    
    .menu-button {
      padding: 0.75rem 1.5rem;
      border-radius: 0.5rem;
      font-weight: 600;
      border: none;
      cursor: pointer;
      transition: all 0.3s;
      white-space: nowrap;
    }
    
    .menu-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15);
    }
    
    .dropdown-toggle {
      padding: 0.6rem 0.9rem;
      border-radius: 0.75rem;
      font-weight: 700;
      font-size: 0.8rem;
      border: none;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      white-space: nowrap;
      display: inline-flex;
      align-items: center;
      gap: 0.35rem;
      background: linear-gradient(135deg, rgba(33, 150, 243, 0.15) 0%, rgba(33, 150, 243, 0.08) 100%);
      color: white;
      box-shadow: 0 4px 12px rgba(33, 150, 243, 0.2);
      border: 1px solid rgba(33, 150, 243, 0.3);
      min-width: fit-content;
    }
    
    .dropdown-toggle:hover {
      background: linear-gradient(135deg, rgba(33, 150, 243, 0.25) 0%, rgba(33, 150, 243, 0.15) 100%);
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(33, 150, 243, 0.3);
    }
    
    .dropdown-toggle span:first-child {
      font-size: 1.1rem;
    }
    
    .hero-section {
      width: 100%;
      padding: 0.5rem 2rem;
      background: linear-gradient(135deg, var(--bg-700) 0%, var(--bg-800) 100%);
    }
    
    .hero-content {
      max-width: 1200px;
      margin: 0 auto;
      text-align: center;
    }
    
    .welcome-title {
      font-weight: 800;
      margin-bottom: 0.75rem;
      color: white;
      line-height: 1.1;
      letter-spacing: -1px;
      text-shadow: 0 4px 20px rgba(33, 150, 243, 0.3);
      background: linear-gradient(135deg, #ffffff 0%, #e3f2fd 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      font-size: 3.5rem;
    }
    
    .welcome-text {
      font-size: 1.35rem;
      color: white;
      opacity: 0.9;
      margin-bottom: 1.25rem;
      line-height: 1.5;
      font-weight: 500;
      letter-spacing: 0.3px;
      max-width: 800px;
      margin-left: auto;
      margin-right: auto;
    }
    
    /* Main Content Grid */
    .main-content-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 1.5rem;
      margin: 0.75rem 0 1.5rem 0;
      max-width: 1200px;
      margin-left: auto;
      margin-right: auto;
    }
    
    /* Verse Display Styles */
    .verse-container {
      background: linear-gradient(135deg, rgba(255,255,255,0.03) 0%, rgba(255,255,255,0.01) 100%);
      border-radius: 1.5rem;
      padding: 1.5rem;
      box-shadow: 0 12px 48px rgba(3,20,39,0.28), 0 0 0 1px rgba(21,101,192,0.08);
      border: 3px solid rgba(21,101,192,0.12);
      position: relative;
      overflow: hidden;
    }
    
    .verse-container::before {
      content: '✨';
      position: absolute;
      top: -20px;
      right: -20px;
      font-size: 6rem;
      opacity: 0.05;
      pointer-events: none;
    }
    
    .verse-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1rem;
      flex-wrap: wrap;
      gap: 1rem;
    }
    
    .verse-header h3 {
      color: #1565c0;
      font-weight: 800;
      font-size: 1.2rem;
      margin: 0;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      letter-spacing: -0.3px;
    }
    
    .next-verse-btn {
      background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
      border: none;
      color: #ffffff;
      padding: 0.7rem 1.5rem;
      border-radius: 0.75rem;
      cursor: pointer;
      font-size: 0.95rem;
      font-weight: 700;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      display: flex;
      align-items: center;
      gap: 0.5rem;
      box-shadow: 0 4px 12px rgba(33, 150, 243, 0.35);
      letter-spacing: 0.3px;
    }
    
    .next-verse-btn:hover {
      background: linear-gradient(135deg, #1976d2 0%, #1565c0 100%);
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(33, 150, 243, 0.45);
    }
    
    .next-verse-btn:active {
      transform: translateY(-1px);
    }
    
    .verse-display {
      background: #ffffff;
      border-radius: 1rem;
      padding: 1.5rem 2rem;
      margin-bottom: 1rem;
      min-height: 120px;
      border: 2px solid #e3f2fd;
      box-shadow: inset 0 2px 8px rgba(33, 150, 243, 0.08);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      animation: fadeIn 0.6s ease;
      position: relative;
    }
    
    @keyframes fadeIn {
      from {
        opacity: 0;
        transform: translateY(15px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
    
    .verse-text {
      color: #0d1b2a;
      font-size: 1.5rem;
      line-height: 1.8;
      margin-bottom: 1.25rem;
      font-weight: 500;
      font-style: italic;
      position: relative;
      max-width: 100%;
      letter-spacing: 0.3px;
      font-family: 'Georgia', 'Palatino', 'Times New Roman', serif;
    }
    
    .verse-text::before {
      content: '"';
      font-size: 4rem;
      color: #2196f3;
      opacity: 0.15;
      position: absolute;
      left: -2rem;
      top: -1rem;
      font-family: Georgia, serif;
    }
    
    .verse-reference {
      color: #1565c0;
      font-size: 1.2rem;
      font-weight: 800;
      margin: 0;
      padding-top: 1rem;
      border-top: 2px solid #e3f2fd;
      letter-spacing: 0.3px;
      font-family: 'Montserrat', sans-serif;
    }
    
    .toast {
      position: fixed;
      bottom: 2.5rem;
      left: 50%;
      transform: translateX(-50%);
      background: linear-gradient(135deg, var(--bg-600) 0%, var(--bg-700) 100%);
      color: white;
      padding: 1.25rem 2.5rem;
      border-radius: 1rem;
      box-shadow: 0 8px 32px rgba(3,20,39,0.6);
      z-index: 1000;
      animation: slideUp 0.4s cubic-bezier(0.4, 0, 0.2, 1);
      font-weight: 600;
      font-size: 1rem;
      letter-spacing: 0.3px;
      border: 2px solid rgba(255, 255, 255, 0.06);
      backdrop-filter: blur(10px);
    }

    @keyframes slideUp {
      from {
        opacity: 0;
        transform: translate(-50%, 30px) scale(0.9);
      }
      to {
        opacity: 1;
        transform: translate(-50%, 0) scale(1);
      }
    }
    
    /* Tool Page Styles */
    .tool-page-container {
      flex: 1;
      padding: 2rem;
      overflow-y: auto;
      width: 100%;
    }
    
    .tool-page-content {
      width: 100%;
      margin: 0 auto;
    }
    
    .tool-page-header {
      text-align: center;
      margin-bottom: 1rem;
    }
    
    .tool-page-title {
      font-size: 3rem;
      font-weight: 800;
      color: white;
      margin-bottom: 1rem;
      text-shadow: 0 4px 20px rgba(33, 150, 243, 0.3);
    }
    
    .tool-page-description {
      font-size: 1.2rem;
      color: white;
      opacity: 0.9;
    }
    
    .placeholder-content {
      background: linear-gradient(135deg, rgba(3,20,39,0.6) 0%, rgba(6,34,56,0.6) 100%);
      border-radius: 1rem;
      padding: 3rem;
      text-align: center;
      border: 2px solid rgba(21,101,192,0.2);
    }
    
    .placeholder-icon {
      font-size: 5rem;
      margin-bottom: 1rem;
    }
    
    .placeholder-text {
      font-size: 1.5rem;
      color: white;
      opacity: 0.8;
    }

    /* Bingo Styles */
    .bingo-menu {
      max-width: 900px;
      margin: 0 auto;
    }

    .bingo-menu-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-top: 2rem;
    }

    .bingo-menu-btn {
      background: linear-gradient(135deg, rgba(33, 150, 243, 0.15) 0%, rgba(33, 150, 243, 0.05) 100%);
      border: 2px solid rgba(33, 150, 243, 0.3);
      border-radius: 1.5rem;
      padding: 3rem 2rem;
      cursor: pointer;
      transition: all 0.3s;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      text-align: center;
    }

    .bingo-menu-btn:hover {
      background: linear-gradient(135deg, rgba(33, 150, 243, 0.25) 0%, rgba(33, 150, 243, 0.15) 100%);
      transform: translateY(-5px);
      box-shadow: 0 10px 30px rgba(33, 150, 243, 0.3);
    }

    .menu-btn-icon {
      font-size: 4rem;
    }

    .menu-btn-title {
      font-size: 1.8rem;
      font-weight: 700;
      color: white;
    }

    .menu-btn-desc {
      font-size: 1rem;
      color: rgba(255, 255, 255, 0.8);
    }

    .bingo-section {
      animation: fadeIn 0.4s ease;
      width: 100%;
    }

    .back-to-menu-btn {
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      color: white;
      padding: 0.75rem 1.5rem;
      border-radius: 0.75rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      margin-bottom: 2rem;
      font-size: 1rem;
    }

    .back-to-menu-btn:hover {
      background: rgba(33, 150, 243, 0.3);
      transform: translateX(-5px);
    }

    .bingo-creator, .bingo-game {
      width: 100%;
      margin: 0 auto;
    }

    .section-title {
      font-size: 1.8rem;
      font-weight: 700;
      color: white;
      margin: 1rem 0 1rem 0;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }

    .config-grid {
      display: grid;
      gap: 1.5rem;
      background: rgba(26, 47, 74, 0.5);
      padding: 2rem;
      border-radius: 1rem;
      border: 2px solid rgba(33, 150, 243, 0.2);
    }

    .config-item label {
      display: block;
      color: white;
      font-weight: 600;
      margin-bottom: 0.5rem;
      font-size: 1rem;
    }

    .bingo-select, .bingo-input {
      width: 100%;
      padding: 0.75rem;
      border-radius: 0.5rem;
      border: 2px solid rgba(33, 150, 243, 0.3);
      background: rgba(13, 27, 42, 0.8);
      color: white;
      font-size: 1rem;
      font-weight: 600;
    }

    .bingo-select:focus, .bingo-input:focus {
      outline: none;
      border-color: #2196f3;
    }

    .content-tabs {
      display: flex;
      gap: 1rem;
      margin: 1.5rem 0 1rem 0;
    }

    .content-tab {
      flex: 1;
      padding: 1rem;
      background: rgba(26, 47, 74, 0.5);
      border: 2px solid rgba(33, 150, 243, 0.2);
      border-radius: 0.75rem;
      color: white;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      font-size: 1rem;
    }

    .content-tab.active {
      background: rgba(33, 150, 243, 0.3);
      border-color: #2196f3;
    }

    .content-tab:hover {
      background: rgba(33, 150, 243, 0.2);
    }

    .content-panel {
      display: none;
    }

    .content-panel.active {
      display: block;
    }

    .bingo-textarea {
      width: 100%;
      padding: 1rem;
      border-radius: 0.75rem;
      border: 2px solid rgba(33, 150, 243, 0.3);
      background: rgba(13, 27, 42, 0.8);
      color: white;
      font-size: 1rem;
      font-family: 'Courier New', monospace;
      resize: vertical;
      margin-top: 0.5rem;
    }

    .bingo-textarea:focus {
      outline: none;
      border-color: #2196f3;
    }

    .helper-text {
      color: rgba(255, 255, 255, 0.7);
      font-size: 0.9rem;
      margin-top: 0.5rem;
    }

    .helper-text span {
      color: #2196f3;
      font-weight: 700;
    }

    .generate-btn, .start-game-btn {
      width: 100%;
      padding: 1.25rem;
      background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
      border: none;
      border-radius: 1rem;
      color: white;
      font-size: 1.3rem;
      font-weight: 700;
      cursor: pointer;
      margin-top: 2rem;
      transition: all 0.3s;
      box-shadow: 0 4px 15px rgba(33, 150, 243, 0.4);
    }

    .generate-btn:hover, .start-game-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 20px rgba(33, 150, 243, 0.5);
    }

    .cards-actions {
      display: flex;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .action-btn {
      flex: 1;
      padding: 1rem;
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      border-radius: 0.75rem;
      color: white;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      font-size: 1rem;
    }

    .action-btn:hover {
      background: rgba(33, 150, 243, 0.3);
      transform: translateY(-2px);
    }

    .cards-grid {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 1rem;
      margin-top: 2rem;
      width: 100%;
    }

    .bingo-card {
      background: white;
      border-radius: 1rem;
      padding: 0;
      box-shadow: 0 8px 30px rgba(0, 0, 0, 0.2);
      border: 3px solid #2196f3;
      overflow: hidden;
      display: flex;
      flex-direction: column;
      width: 100%;
      aspect-ratio: 8.5 / 11;
      margin: 0 auto;
    }

    .card-header {
      background: linear-gradient(135deg, #64b5f6 0%, #42a5f5 100%);
      padding: 2rem 1.5rem;
      text-align: center;
      border-bottom: 3px solid #2196f3;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    }

    .card-title {
      font-size: 2rem;
      font-weight: 900;
      color: white;
      margin: 0 0 0.5rem 0;
      letter-spacing: 3px;
      text-transform: uppercase;
      text-shadow: 0 3px 8px rgba(0, 0, 0, 0.3), 0 0 20px rgba(255, 255, 255, 0.3);
      position: relative;
      display: inline-block;
    }

    .card-title::before {
      content: '✨';
      position: absolute;
      left: -30px;
      font-size: 1.5rem;
    }

    .card-title::after {
      content: '✨';
      position: absolute;
      right: -30px;
      font-size: 1.5rem;
    }

    .card-subtitle {
      font-size: 1rem;
      color: white;
      font-weight: 600;
      margin: 0;
      opacity: 0.95;
    }

    .card-number {
      font-size: 1rem;
      color: white;
      margin-top: 0.5rem;
      opacity: 0.95;
      font-weight: 700;
      letter-spacing: 1px;
    }

    .card-name-section {
      background: white;
      padding: 1rem 1.5rem;
      border-bottom: 2px dashed #2196f3;
      display: flex;
      align-items: center;
      gap: 0.75rem;
    }

    .card-name-label {
      font-size: 0.95rem;
      font-weight: 700;
      color: #1565c0;
      white-space: nowrap;
    }

    .card-name-line {
      flex: 1;
      border-bottom: 2px solid #90caf9;
      min-height: 1.5rem;
    }

    .bingo-grid {
      display: grid;
      gap: 0.5rem;
      margin: 1rem 1.5rem 1.5rem 1.5rem;
      flex: 1;
    }

    .bingo-cell {
      min-height: 55px;
      background: #f5f5f5;
      border: 2px solid #2196f3;
      border-radius: 0.5rem;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 0.5rem;
      font-size: clamp(0.55rem, 1.3vw, 0.8rem);
      font-weight: 600;
      color: #333;
      text-align: center;
      overflow-wrap: break-word;
      word-break: break-word;
      line-height: 1.2;
      hyphens: auto;
    }

    .bingo-cell.free {
      background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
      color: white;
      font-size: 1.1rem;
      font-weight: 800;
    }

    .bingo-cell img {
      max-width: 100%;
      max-height: 100%;
      object-fit: contain;
    }

    .card-footer {
      margin: 0 1.5rem 1.5rem 1.5rem;
      padding: 1rem;
      background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
      border-radius: 0.75rem;
      border: 2px solid #2196f3;
      box-shadow: 0 2px 8px rgba(33, 150, 243, 0.2);
    }

    .card-verse {
      font-size: 0.85rem;
      color: #1565c0;
      font-style: italic;
      font-weight: 600;
      text-align: center;
      line-height: 1.4;
    }

    .game-setup {
      background: rgba(26, 47, 74, 0.5);
      padding: 2rem;
      border-radius: 1rem;
      border: 2px solid rgba(33, 150, 243, 0.2);
    }

    .game-setup label {
      display: block;
      color: white;
      font-weight: 600;
      margin-bottom: 0.75rem;
      font-size: 1.1rem;
    }

    .game-controls {
      display: flex;
      gap: 1rem;
      margin: 2rem 0;
    }

    .control-btn {
      flex: 1;
      padding: 1.25rem;
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      border-radius: 1rem;
      color: white;
      font-size: 1.2rem;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s;
    }

    .control-btn.primary {
      background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
      border-color: #2196f3;
    }

    .control-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 20px rgba(33, 150, 243, 0.4);
    }

    .control-btn:disabled {
      opacity: 0.5;
      cursor: not-allowed;
      transform: none;
    }

    .roulette-container {
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.8) 0%, rgba(13, 27, 42, 0.8) 100%);
      border-radius: 1.5rem;
      padding: 3rem;
      border: 3px solid rgba(33, 150, 243, 0.4);
      margin: 2rem 0;
    }

    .current-item {
      text-align: center;
    }

    .item-label {
      font-size: 1.2rem;
      color: rgba(255, 255, 255, 0.7);
      margin-bottom: 1rem;
      font-weight: 600;
    }

    .item-content {
      font-size: 3rem;
      font-weight: 800;
      color: white;
      background: linear-gradient(135deg, #2196f3 0%, #64b5f6 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      min-height: 4rem;
      display: flex;
      align-items: center;
      justify-content: center;
      animation: pulse 0.5s ease;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); }
    }

    .game-stats {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1rem;
      margin: 2rem 0;
    }

    .stat-item {
      background: rgba(26, 47, 74, 0.5);
      padding: 1.5rem;
      border-radius: 1rem;
      border: 2px solid rgba(33, 150, 243, 0.3);
      text-align: center;
    }

    .stat-label {
      display: block;
      color: rgba(255, 255, 255, 0.7);
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
    }

    .stat-value {
      display: block;
      font-size: 2.5rem;
      font-weight: 800;
      color: #2196f3;
    }

    .history-section {
      margin-top: 3rem;
    }

    .history-title {
      font-size: 1.5rem;
      font-weight: 700;
      color: white;
      margin-bottom: 1rem;
    }

    .history-list {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
      gap: 1rem;
    }

    .history-item {
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      border-radius: 0.75rem;
      padding: 1rem;
      text-align: center;
      color: white;
      font-weight: 600;
      font-size: 1rem;
    }

    /* Scoreboard Styles */
    .scoreboard-wrapper {
      margin-top: 2rem;
    }

    .scoreboard-grid-fixed {
      display: grid;
      gap: 1.5rem;
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.5) 0%, rgba(13, 27, 42, 0.5) 100%);
      padding: 2rem;
      border-radius: 1.5rem;
      border: 3px solid rgba(33, 150, 243, 0.3);
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
      overflow: visible;
    }
    
    .scoreboard-grid-fixed[data-teams="1"],
    .scoreboard-grid-fixed[data-teams="2"],
    .scoreboard-grid-fixed[data-teams="3"],
    .scoreboard-grid-fixed[data-teams="4"],
    .scoreboard-grid-fixed[data-teams="5"] {
      grid-template-columns: repeat(var(--cols), 1fr);
    }
    
    .scoreboard-grid-fixed[data-teams="6"],
    .scoreboard-grid-fixed[data-teams="7"],
    .scoreboard-grid-fixed[data-teams="8"],
    .scoreboard-grid-fixed[data-teams="9"],
    .scoreboard-grid-fixed[data-teams="10"] {
      grid-template-columns: repeat(5, 1fr);
    }
    
    .scoreboard-grid-fixed[data-teams="11"],
    .scoreboard-grid-fixed[data-teams="12"],
    .scoreboard-grid-fixed[data-teams="13"],
    .scoreboard-grid-fixed[data-teams="14"],
    .scoreboard-grid-fixed[data-teams="15"] {
      grid-template-columns: repeat(5, 1fr);
    }

    .scoreboard-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
      margin: 0;
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.5) 0%, rgba(13, 27, 42, 0.5) 100%);
      padding: 2rem;
      border-radius: 1.5rem;
      border: 3px solid rgba(33, 150, 243, 0.3);
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
    }

    .team-card {
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.8) 0%, rgba(13, 27, 42, 0.8) 100%);
      border-radius: 1.5rem;
      padding: 1.5rem;
      border: 3px solid rgba(33, 150, 243, 0.4);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1rem;
      transition: all 0.3s;
      min-width: 0;
      position: relative;
      overflow: visible;
    }

    .team-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 30px rgba(33, 150, 243, 0.3);
    }

    .trophy-badge {
      position: absolute;
      top: -15px;
      right: -15px;
      width: 70px;
      height: 70px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2.5rem;
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.4);
      z-index: 10;
      animation: trophyFloat 2s ease-in-out infinite;
      border: 4px solid;
    }

    .trophy-badge.gold {
      background: linear-gradient(135deg, #ffd700 0%, #ffed4e 50%, #ffd700 100%);
      border-color: #ffed4e;
      box-shadow: 0 8px 25px rgba(255, 215, 0, 0.6), 0 0 30px rgba(255, 215, 0, 0.4);
    }

    .trophy-badge.silver {
      background: linear-gradient(135deg, #c0c0c0 0%, #e8e8e8 50%, #c0c0c0 100%);
      border-color: #e8e8e8;
      box-shadow: 0 8px 25px rgba(192, 192, 192, 0.6), 0 0 30px rgba(192, 192, 192, 0.4);
    }

    .trophy-badge.bronze {
      background: linear-gradient(135deg, #cd7f32 0%, #e6a157 50%, #cd7f32 100%);
      border-color: #e6a157;
      box-shadow: 0 8px 25px rgba(205, 127, 50, 0.6), 0 0 30px rgba(205, 127, 50, 0.4);
    }

    @keyframes trophyFloat {
      0%, 100% {
        transform: translateY(0px) rotate(0deg);
      }
      25% {
        transform: translateY(-5px) rotate(5deg);
      }
      50% {
        transform: translateY(0px) rotate(0deg);
      }
      75% {
        transform: translateY(-5px) rotate(-5deg);
      }
    }

    .team-name {
      font-size: 1.2rem;
      font-weight: 800;
      color: white;
      text-align: center;
      word-break: break-word;
    }

    .team-score {
      font-size: 3rem;
      font-weight: 900;
      color: #2196f3;
      text-shadow: 0 4px 20px rgba(33, 150, 243, 0.5);
      animation: pulse 0.3s ease;
    }

    .team-controls {
      display: flex;
      gap: 0.75rem;
      width: 100%;
    }

    .score-btn {
      flex: 1;
      padding: 0.5rem 0.75rem;
      font-size: 0.9rem;
      font-weight: 700;
      border: none;
      border-radius: 0.5rem;
      cursor: pointer;
      transition: all 0.3s;
      color: white;
    }

    .score-btn.add {
      background: linear-gradient(135deg, #4caf50 0%, #388e3c 100%);
    }

    .score-btn.subtract {
      background: linear-gradient(135deg, #f44336 0%, #c62828 100%);
    }

    .score-btn:hover {
      transform: scale(1.05);
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
    }

    .score-btn:active {
      transform: scale(0.98);
    }

    /* Timer Styles */
    .timer-control-section {
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.5) 0%, rgba(13, 27, 42, 0.5) 100%);
      border-radius: 0.75rem;
      padding: 0.5rem 1rem;
      border: 2px solid rgba(33, 150, 243, 0.3);
      margin-bottom: 1rem;
      max-width: 700px;
      margin-left: auto;
      margin-right: auto;
    }

    .timer-config {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }

    .timer-inputs {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(110px, 1fr));
      gap: 0.4rem;
    }

    .timer-input-group {
      display: flex;
      flex-direction: column;
      gap: 0.2rem;
    }

    .timer-input-group label {
      color: white;
      font-weight: 600;
      font-size: 0.75rem;
    }

    .timer-display-compact {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: 1rem;
      padding: 1rem 0;
    }

    .timer-time-compact {
      font-size: 3.5rem;
      font-weight: 900;
      color: #2196f3;
      text-shadow: 0 2px 15px rgba(33, 150, 243, 0.6);
      font-family: 'Courier New', monospace;
      letter-spacing: 0.05em;
      margin: 0;
      text-align: center;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .timer-time-compact.warning {
      color: #ff9800;
      animation: pulse 1s ease infinite;
    }

    .timer-time-compact.danger {
      color: #f44336;
      animation: pulse 0.5s ease infinite;
    }

    .timer-controls-compact {
      display: flex;
      gap: 0.4rem;
      flex-wrap: wrap;
      justify-content: center;
      width: 100%;
    }

    .timer-btn {
      padding: 0.4rem 0.7rem;
      border: none;
      border-radius: 0.4rem;
      font-weight: 700;
      font-size: 0.75rem;
      cursor: pointer;
      transition: all 0.3s;
      color: white;
      white-space: nowrap;
    }

    .timer-btn.start {
      background: linear-gradient(135deg, #4caf50 0%, #388e3c 100%);
    }

    .timer-btn.pause {
      background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);
    }

    .timer-btn.reset {
      background: linear-gradient(135deg, #f44336 0%, #c62828 100%);
    }

    .timer-btn.edit {
      background: linear-gradient(135deg, #2196f3 0%, #1976d2 100%);
    }

    .timer-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
    }

    .timer-btn:active {
      transform: translateY(-1px);
    }

    .timer-display {
      background: linear-gradient(135deg, rgba(26, 47, 74, 0.8) 0%, rgba(13, 27, 42, 0.8) 100%);
      border-radius: 2rem;
      padding: 4rem 2rem;
      border: 4px solid rgba(33, 150, 243, 0.4);
      text-align: center;
      margin: 2rem 0;
    }

    .timer-time {
      font-size: 8rem;
      font-weight: 900;
      color: #2196f3;
      text-shadow: 0 4px 30px rgba(33, 150, 243, 0.6);
      font-family: 'Courier New', monospace;
      letter-spacing: 0.1em;
    }

    .timer-label {
      font-size: 1.5rem;
      color: rgba(255, 255, 255, 0.7);
      margin-top: 1rem;
      font-weight: 600;
    }

    /* NEW MARCADOR FEATURES STYLES */
    .preset-select {
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      color: white;
      padding: 0.75rem;
      border-radius: 0.5rem;
      font-weight: 600;
      cursor: pointer;
      font-size: 1rem;
    }

    .preset-select:focus {
      outline: none;
      border-color: #2196f3;
    }

    .rounds-indicator {
      background: rgba(33, 150, 243, 0.2);
      border: 2px solid rgba(33, 150, 243, 0.4);
      border-radius: 1rem;
      padding: 1rem;
      text-align: center;
      margin-bottom: 1rem;
    }

    .rounds-text {
      color: white;
      font-size: 1.2rem;
      font-weight: 700;
    }

    .round-number {
      color: #2196f3;
      font-size: 2rem;
      font-weight: 900;
    }

    .target-indicator {
      background: rgba(255, 193, 7, 0.2);
      border: 2px solid rgba(255, 193, 7, 0.4);
      border-radius: 1rem;
      padding: 0.75rem;
      text-align: center;
      margin-bottom: 1rem;
    }

    .target-text {
      color: #ffc107;
      font-size: 1rem;
      font-weight: 700;
    }

    .fullscreen-btn {
      background: linear-gradient(135deg, #9c27b0 0%, #7b1fa2 100%);
      border: none;
      color: white;
      padding: 0.75rem 1.5rem;
      border-radius: 0.75rem;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.3s;
      font-size: 1rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      justify-content: center;
    }

    .fullscreen-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 6px 20px rgba(156, 39, 176, 0.4);
    }

    .bonus-btn {
      background: linear-gradient(135deg, #ff9800 0%, #f57c00 100%);
    }

    .bonus-btn:hover {
      background: linear-gradient(135deg, #f57c00 0%, #ef6c00 100%);
    }

    .penalty-btn {
      background: linear-gradient(135deg, #795548 0%, #5d4037 100%);
    }

    .penalty-btn:hover {
      background: linear-gradient(135deg, #5d4037 0%, #4e342e 100%);
    }

    .progress-bar {
      width: 100%;
      height: 8px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 4px;
      overflow: hidden;
      margin-top: 0.5rem;
    }

    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #4caf50 0%, #8bc34a 100%);
      transition: width 0.3s ease;
      border-radius: 4px;
    }

    .stats-panel {
      background: rgba(26, 47, 74, 0.5);
      border: 2px solid rgba(33, 150, 243, 0.3);
      border-radius: 1rem;
      padding: 1.5rem;
      margin-top: 2rem;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1rem;
      margin-top: 1rem;
    }

    .stat-card {
      background: rgba(13, 27, 42, 0.5);
      padding: 1rem;
      border-radius: 0.75rem;
      border: 1px solid rgba(33, 150, 243, 0.2);
      text-align: center;
    }

    .stat-card-label {
      color: rgba(255, 255, 255, 0.7);
      font-size: 0.9rem;
      margin-bottom: 0.5rem;
    }

    .stat-card-value {
      color: #2196f3;
      font-size: 1.8rem;
      font-weight: 800;
    }

    .history-modal {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: linear-gradient(135deg, #1e3a5f 0%, #0d1b2a 100%);
      padding: 2rem;
      border-radius: 1.5rem;
      box-shadow: 0 10px 40px rgba(0, 0, 0, 0.5);
      z-index: 10000;
      border: 3px solid rgba(33, 150, 243, 0.4);
      max-width: 90%;
      max-height: 80%;
      overflow-y: auto;
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 1.5rem;
    }

    .modal-title {
      color: white;
      font-size: 1.8rem;
      font-weight: 800;
    }

    .modal-close {
      background: rgba(244, 67, 54, 0.2);
      border: 2px solid rgba(244, 67, 54, 0.4);
      color: white;
      padding: 0.5rem 1rem;
      border-radius: 0.5rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
    }

    .modal-close:hover {
      background: rgba(244, 67, 54, 0.3);
    }

    .round-history-item {
      background: rgba(26, 47, 74, 0.5);
      border: 2px solid rgba(33, 150, 243, 0.3);
      border-radius: 1rem;
      padding: 1.5rem;
      margin-bottom: 1rem;
    }

    .round-history-header {
      color: #2196f3;
      font-size: 1.3rem;
      font-weight: 700;
      margin-bottom: 1rem;
    }

    .round-scores {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      gap: 0.75rem;
    }

    .round-score-item {
      background: rgba(13, 27, 42, 0.5);
      padding: 0.75rem;
      border-radius: 0.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .round-team-name {
      color: white;
      font-weight: 600;
    }

    .round-team-score {
      color: #2196f3;
      font-size: 1.5rem;
      font-weight: 800;
    }

    .winner-badge {
      background: linear-gradient(135deg, #ffc107 0%, #ff9800 100%);
      color: #000;
      padding: 0.25rem 0.75rem;
      border-radius: 1rem;
      font-size: 0.75rem;
      font-weight: 700;
      margin-left: 0.5rem;
    }

    @media print {
      body * {
        visibility: hidden;
      }
      .cards-grid, .cards-grid * {
        visibility: visible;
      }
      .cards-grid {
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
      }
      .bingo-card {
        page-break-inside: avoid;
        break-inside: avoid;
      }
    }
    
    /* Footer Styles */
    .info-footer {
      width: 100%;
      background: linear-gradient(135deg, #1a2f4a 0%, #0d1b2a 100%);
      padding: 1.5rem 1.5rem 1rem 1.5rem;
      border-top: 3px solid rgba(33, 150, 243, 0.3);
      flex-shrink: 0;
    }
    
    .footer-content {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 1.5rem;
      margin-bottom: 1rem;
    }
    
    .footer-section {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }
    
    .footer-title {
      color: #2196f3;
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: 0.5rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .footer-text {
      color: #e3f2fd;
      font-size: 0.9rem;
      line-height: 1.7;
      opacity: 0.9;
    }
    
    .footer-links {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }
    
    .footer-links li {
      color: #e3f2fd;
      font-size: 0.9rem;
      opacity: 0.85;
      cursor: pointer;
      transition: all 0.3s;
      padding: 0.5rem;
      border-radius: 0.5rem;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .footer-links li:hover {
      opacity: 1;
      background: rgba(33, 150, 243, 0.15);
      transform: translateX(5px);
    }
    
    .link-icon {
      font-size: 1rem;
    }
    
    .contact-info {
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }
    
    .contact-item {
      color: #e3f2fd;
      font-size: 0.9rem;
      opacity: 0.9;
      display: flex;
      align-items: center;
      gap: 0.5rem;
    }
    
    .contact-icon {
      font-size: 1.1rem;
    }
    
    .footer-cta-btn {
      background: #2196f3;
      color: white;
      border: none;
      padding: 0.85rem 1.5rem;
      border-radius: 0.5rem;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      transition: all 0.3s;
      margin-top: 0.5rem;
      box-shadow: 0 4px 12px rgba(33, 150, 243, 0.3);
    }
    
    .footer-cta-btn:hover {
      background: #1976d2;
      transform: translateY(-3px);
      box-shadow: 0 6px 16px rgba(33, 150, 243, 0.4);
    }
    
    .footer-bottom {
      max-width: 1200px;
      margin: 0 auto;
      padding-top: 1rem;
      border-top: 1px solid rgba(33, 150, 243, 0.2);
      text-align: center;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }
    
    .copyright {
      color: #e3f2fd;
      font-size: 0.85rem;
      opacity: 0.7;
    }
    
    .footer-verse {
      color: #2196f3;
      font-size: 0.9rem;
      font-style: italic;
      font-weight: 500;
    }
    
    @media (max-width: 768px) {
      .nav-content {
        flex-direction: column;
        align-items: center;
        padding: 0.5rem 1rem;
      }
      
      .nav-buttons {
        margin-top: 0.75rem;
      }
      
      .logo-section {
        gap: 0.5rem;
      }
      
      .logo-svg {
        width: 30px;
        height: 30px;
      }
      
      .site-title {
        font-size: 1rem;
      }
      
      .tagline {
        font-size: 0.7rem;
      }
      
      .dropdown-toggle {
        padding: 0.5rem 1rem;
        font-size: 0.85rem;
      }
      
      .welcome-title {
        font-size: 2rem;
      }
      
      .welcome-text {
        font-size: 1rem;
      }
      
      .verse-container {
        padding: 1rem;
      }
      
      .verse-header {
        flex-direction: column;
        align-items: stretch;
        gap: 0.5rem;
      }
      
      .verse-header h3 {
        font-size: 1rem;
      }
      
      .next-verse-btn {
        width: 100%;
        justify-content: center;
        padding: 0.5rem;
        font-size: 0.85rem;
      }
      
      .verse-display {
        padding: 1rem 1.25rem;
        min-height: 100px;
      }
      
      .verse-text {
        font-size: 1.15rem;
        line-height: 1.6;
      }
      
      .verse-text::before {
        font-size: 2.5rem;
        left: -1rem;
        top: -0.5rem;
      }
      
      .verse-reference {
        font-size: 1rem;
      }
      
      .tool-page-title {
        font-size: 2rem;
      }
      
      .tool-page-container {
        padding: 1rem;
      }
      
      .footer-content {
        grid-template-columns: 1fr;
        gap: 2rem;
      }
      
      .footer-cta-btn {
        width: 100%;
      }
      
      .info-footer {
        padding: 2rem 1rem 1.5rem 1rem;
      }

      .cards-grid {
        grid-template-columns: 1fr;
      }

      .bingo-menu-grid {
        grid-template-columns: 1fr;
      }

      .game-controls {
        flex-direction: column;
      }

      .scoreboard-grid-fixed {
        grid-template-columns: 1fr;
        max-height: 500px;
      }

      .timer-time {
        font-size: 4rem;
      }

      .timer-time-compact {
        font-size: 4rem;
      }

      .team-name {
        font-size: 1.2rem;
      }

      .team-score {
        font-size: 3rem;
      }

      .stats-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
  <style>
    /* Theme overrides to ensure consistent, clean main screen */
    .generate-btn,
    .start-game-btn,
    .next-verse-btn,
    .menu-button,
    .dropdown-toggle,
    .control-btn.primary,
    .bingo-menu-btn {
      background: linear-gradient(135deg, var(--bg-600) 0%, var(--bg-700) 100%) !important;
      color: var(--text-on-dark) !important;
      border: 1px solid rgba(21,101,192,0.18) !important;
      box-shadow: 0 8px 22px rgba(3,20,39,0.45) !important;
    }

    .action-btn,
    .control-btn,
    .back-to-menu-btn {
      background: rgba(3,20,39,0.18) !important;
      border: 1px solid rgba(21,101,192,0.12) !important;
      color: var(--text-on-dark) !important;
    }

    .card-header {
      background: linear-gradient(135deg, var(--bg-500) 0%, var(--bg-600) 100%) !important;
      border-bottom: 3px solid rgba(21,101,192,0.35) !important;
    }

    .card-footer {
      background: linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)) !important;
      border: 1px solid rgba(21,101,192,0.08) !important;
    }
    /* Fallback overrides to catch inline styles and legacy blue rgba/hex usages */
    *[style*="#2196f3"] {
      background: var(--bg-500) !important;
      border-color: var(--bg-500) !important;
      color: var(--text-on-dark) !important;
    }

    *[style*="#1976d2"] {
      background: var(--bg-600) !important;
      border-color: var(--bg-600) !important;
      color: var(--text-on-dark) !important;
    }

    *[style*="rgba(33, 150, 243"] {
      /* replace old blue rgba with our bg-600 tone */
      background: linear-gradient(135deg, var(--bg-600) 0%, var(--bg-700) 100%) !important;
      border-color: rgba(21,101,192,0.28) !important;
      box-shadow: 0 8px 22px rgba(3,20,39,0.45) !important;
      color: var(--text-on-dark) !important;
    }

    /* SVG color fixes for inline fills/strokes */
    svg [fill="#2196f3"], svg [stroke="#2196f3"] {
      fill: var(--bg-500) !important;
      stroke: var(--bg-500) !important;
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <div id="root">
   <div class="app-container"><!-- SHARED NAVIGATION BAR -->
    <nav class="nav-bar">
     <div class="nav-content">
      <div class="nav-left-section">
       <div class="logo-section" onclick="navigateTo('/')">
        <svg class="logo-svg" id="logo" viewbox="0 0 50 50" xmlns="http://www.w3.org/2000/svg"><rect width="50" height="50" rx="8" fill="currentColor" /> <path d="M10 18 L10 38 L24 35 L24 15 Z" fill="white" opacity="0.9" /> <path d="M40 18 L40 38 L26 35 L26 15 Z" fill="white" opacity="0.9" /> <path d="M24 15 L26 15 L26 35 L24 35 Z" fill="white" /> <circle cx="17" cy="25" r="2" fill="#2196f3" /> <circle cx="33" cy="25" r="2" fill="#2196f3" /> <circle cx="25" cy="20" r="2" fill="#2196f3" /> <line x1="17" y1="25" x2="25" y2="20" stroke="#2196f3" stroke-width="1.5" /> <line x1="33" y1="25" x2="25" y2="20" stroke="#2196f3" stroke-width="1.5" />
        </svg>
        <div>
         <h1 class="site-title" id="site-title">MyBibleGameHub-Iglesia Activa</h1>
         <p class="tagline" id="tagline">Tu comunidad de fe conectada</p>
        </div>
       </div>
      </div>
      <div class="nav-right-section"><button class="dropdown-toggle" id="home-btn" onclick="navigateTo('/')"> <span>🏠</span> <span>Inicio</span> </button> <button class="dropdown-toggle" id="bingo-quick-btn" onclick="navigateTo('/bingo')"> <span>🎯</span> <span>Bingo</span> </button> <button class="dropdown-toggle" id="marcador-quick-btn" onclick="navigateTo('/marcador')"> <span>📊</span> <span>Marcador</span> </button> <button class="dropdown-toggle" id="trivia-quick-btn" onclick="navigateTo('/trivia')"> <span>🎲</span> <span>Trivia</span> </button> <button class="dropdown-toggle" id="ruleta-quick-btn" onclick="navigateTo('/ruleta')"> <span>🎡</span> <span>Ruleta</span> </button> <button class="dropdown-toggle" id="equipos-quick-btn" onclick="navigateTo('/equipos')"> <span>🃏</span> <span>Equipos</span> </button> <button class="dropdown-toggle" id="timer-quick-btn" onclick="navigateTo('/timer')"> <span>⏱️</span> <span>Timer</span> </button> <button class="dropdown-toggle" id="sorteo-quick-btn" onclick="navigateTo('/sorteo')"> <span>🎁</span> <span>Sorteo</span> </button> <button class="dropdown-toggle" id="asistencia-quick-btn" onclick="navigateTo('/asistencia')"> <span>✅</span> <span>Asistencia</span> </button>
      </div>
     </div>
    </nav><!-- HOME PAGE -->
    <div id="page-home" class="page active">
     <main class="hero-section">
      <div class="hero-content">
       <h2 class="welcome-title" id="welcome-title">Herramientas para tu Iglesia</h2>
       <p class="welcome-text" id="welcome-text">Recursos interactivos para reuniones, eventos y actividades que fortalecen tu comunidad</p><!-- Main Content Grid -->
       <div class="main-content-grid"><!-- Daily Verse Section -->
        <div class="verse-container">
         <div class="verse-header">
          <h3>✨ Versículo del Día</h3><button class="next-verse-btn" id="next-verse-btn">Siguiente 🔄</button>
         </div>
         <div class="verse-display">
          <p class="verse-text" id="verse-text"></p>
          <p class="verse-reference" id="verse-reference"></p>
         </div>
        </div>
       </div>
      </div>
     </main>
     <footer class="info-footer">
      <div class="footer-content">
       <div class="footer-section">
        <h4 class="footer-title">📋 Acerca de Nosotros</h4>
        <p class="footer-text">MyBibleGameHub es una plataforma de herramientas interactivas diseñada para líderes y equipos de iglesias. Facilitamos reuniones dinámicas, eventos juveniles, retiros y actividades grupales con recursos digitales listos para usar.</p>
       </div>
       <div class="footer-section">
        <h4 class="footer-title">🚀 Herramientas Populares</h4>
        <ul class="footer-links">
         <li><span class="link-icon">🎲</span> Trivia Bíblica Interactiva</li>
         <li><span class="link-icon">📊</span> Marcador de Equipos</li>
         <li><span class="link-icon">⏱️</span> Cronómetros y Timers</li>
         <li><span class="link-icon">🎯</span> Generadores Aleatorios</li>
        </ul>
       </div>
       <div class="footer-section">
        <h4 class="footer-title">❓ Preguntas Frecuentes</h4>
        <ul class="footer-links">
         <li><span class="link-icon">🔹</span> ¿Cómo usar el marcador?</li>
         <li><span class="link-icon">🔹</span> ¿Crear trivia personalizada?</li>
         <li><span class="link-icon">🔹</span> ¿Proyectar en pantalla grande?</li>
         <li><span class="link-icon">🔹</span> Soporte técnico</li>
        </ul>
       </div>
       <div class="footer-section">
        <h4 class="footer-title">💬 Ayuda &amp; Contacto</h4>
        <div class="contact-info">
        <p class="contact-item"><span class="contact-icon">📧</span> info@mybiblegamehub.com</p>
         <p class="contact-item"><span class="contact-icon">💬</span> Chat en vivo disponible</p>
         <p class="contact-item"><span class="contact-icon">🕐</span> Lunes a Viernes 9AM - 6PM</p>
        </div><button class="footer-cta-btn">Necesito Ayuda</button>
       </div>
      </div>
      <div class="footer-bottom">
      <p class="copyright">© 2024 MyBibleGameHub - Iglesia Activa. Todos los derechos reservados.</p>
       <p class="footer-verse">"Toda la Escritura es inspirada por Dios" - 2 Timoteo 3:16</p>
      </div>
     </footer>
    </div><!-- MARCADOR PAGE -->
    <div id="page-marcador" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">📊 Marcador de Equipos</h1>
        <p class="tool-page-description">Sistema de puntuación para competencias y juegos grupales</p>
       </div><!-- Main Menu -->
       <div id="marcador-menu" class="bingo-menu">
        <div class="bingo-menu-grid"><button class="bingo-menu-btn" id="btn-new-game"> <span class="menu-btn-icon">🎮</span> <span class="menu-btn-title">Nueva Partida</span> <span class="menu-btn-desc">Configura equipos y comienza a jugar</span> </button>
        </div>
       </div><!-- Game Setup Section -->
       <div id="game-setup-section" class="bingo-section" style="display: none;">
        <div class="bingo-creator">
         <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;"><button class="back-to-menu-btn" id="back-from-setup" style="margin: 0; padding: 0.5rem 1rem; font-size: 0.85rem;">← Volver</button>
          <h2 class="section-title" style="margin: 0;">⚙️ Configurar Equipos</h2>
         </div>
         <div class="config-grid"><!-- Preset Selection -->
          <div class="config-item"><label for="game-preset">🎮 Preset de Juego:</label> <select id="game-preset" class="preset-select"> <option value="custom">Personalizado</option> <option value="trivia">Trivia Bíblica (10/20/30 pts)</option> <option value="versos">Carreras de Versículos (2 min/ronda)</option> <option value="memorization">Memorización (5 min, 100 pts)</option> </select>
          </div>
          <div class="config-item"><label for="num-teams">Número de Equipos:</label> <select id="num-teams" class="bingo-select"> <option value="2" selected>2 Equipos</option> <option value="3">3 Equipos</option> <option value="4">4 Equipos</option> <option value="5">5 Equipos</option> <option value="6">6 Equipos</option> <option value="7">7 Equipos</option> <option value="8">8 Equipos</option> <option value="9">9 Equipos</option> <option value="10">10 Equipos</option> <option value="11">11 Equipos</option> <option value="12">12 Equipos</option> <option value="13">13 Equipos</option> <option value="14">14 Equipos</option> <option value="15">15 Equipos</option> </select>
          </div><!-- Rounds Configuration -->
          <div class="config-item"><label for="total-rounds">🔄 Número de Rondas:</label> <select id="total-rounds" class="bingo-select"> <option value="1" selected>1 Ronda</option> <option value="3">Mejor de 3</option> <option value="5">Mejor de 5</option> <option value="7">Mejor de 7</option> </select>
          </div><!-- Target Score -->
          <div class="config-item"><label for="target-score">🏁 Puntaje Objetivo (opcional):</label> <input type="number" id="target-score" class="bingo-input" placeholder="Ej: 100" min="0">
           <p class="helper-text">Dejar en blanco para juego sin límite</p>
          </div>
         </div>
         <h2 class="section-title">📝 Nombres de los Equipos</h2>
         <div id="team-names-container" class="config-grid"></div><button class="generate-btn" id="start-marcador-btn">🚀 Iniciar Partida</button>
        </div>
       </div><!-- Active Game Section -->
       <div id="active-game-section" class="bingo-section" style="display: none; flex: 1; overflow: hidden;">
        <div class="bingo-game" style="height: 100%; display: flex; flex-direction: column;">
         <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 0.5rem; flex-shrink: 0;"><button class="back-to-menu-btn" id="back-from-game" style="margin: 0; padding: 0.5rem 1rem; font-size: 0.85rem;">← Finalizar</button>
          <h2 class="section-title" style="margin: 0;">🎮 Partida en Curso</h2><button class="fullscreen-btn" id="fullscreen-btn" style="margin-left: auto;"> <span>🖥️</span> <span>Pantalla Completa</span> </button>
         </div><!-- Rounds Indicator -->
         <div id="rounds-indicator" class="rounds-indicator" style="display: none;"><span class="rounds-text">Ronda <span class="round-number" id="current-round-display">1</span> de <span id="total-rounds-display">1</span></span>
         </div><!-- Target Score Indicator -->
         <div id="target-indicator" class="target-indicator" style="display: none;"><span class="target-text">🏁 Objetivo: <span id="target-score-display">100</span> puntos</span>
         </div><!-- Timer Section -->
         <div class="timer-control-section" style="flex-shrink: 0;">
          <div class="timer-config" id="timer-config">
           <div class="timer-inputs">
            <div class="timer-input-group"><label for="timer-mode">Modo:</label> <select id="timer-mode" class="bingo-select"> <option value="countdown">⏱️ Cuenta Regresiva</option> <option value="stopwatch">⏲️ Cronómetro</option> </select>
            </div>
            <div class="timer-input-group"><label for="timer-minutes">Minutos:</label> <input type="number" id="timer-minutes" class="bingo-input" value="5" min="0" max="59">
            </div>
            <div class="timer-input-group"><label for="timer-seconds">Segundos:</label> <input type="number" id="timer-seconds" class="bingo-input" value="0" min="0" max="59">
            </div>
           </div><button class="control-btn primary" id="set-timer-btn">⚙️ Configurar Timer</button>
          </div>
          <div class="timer-display-compact" id="timer-display-compact" style="display: none;">
           <div class="timer-time-compact" id="timer-time-display">
            05:00
           </div>
           <div class="timer-controls-compact"><button class="timer-btn start" id="timer-start-btn">▶️ Iniciar</button> <button class="timer-btn pause" id="timer-pause-btn" style="display: none;">⏸️ Pausar</button> <button class="timer-btn reset" id="timer-reset-btn">🔄 Reiniciar</button> <button class="timer-btn edit" id="timer-edit-btn">⚙️ Cambiar</button>
           </div>
          </div>
         </div><!-- Scoreboard Container -->
         <div class="scoreboard-wrapper" style="flex-shrink: 0; margin-top: 1rem;">
          <div id="scoreboard-container" class="scoreboard-grid-fixed"></div>
         </div>
         <div class="game-controls" style="margin-top: 1rem; flex-shrink: 0;"><button class="control-btn" id="reset-scores-btn">🔄 Reiniciar Puntajes</button> <button class="control-btn" id="next-round-btn" style="display: none;">⏭️ Siguiente Ronda</button> <button class="control-btn" id="view-stats-btn">📊 Ver Estadísticas</button> <button class="control-btn primary" id="end-game-btn">🏆 Finalizar Partida</button>
         </div>
        </div>
       </div>
      </div>
     </div>
    </div><!-- BINGO BIBLICO PAGE -->
    <div id="page-bingo" class="page">
     <div class="tool-page-container" style="padding-top: 1rem;">
      <div class="tool-page-content">
       <div class="tool-page-header" style="margin-bottom: 1.5rem;">
        <h1 class="tool-page-title" style="margin-bottom: 0.5rem;">🎯 Bingo Bíblico</h1>
        <p class="tool-page-description">Crea cartones personalizados y juega bingo interactivo</p>
       </div><!-- Main Menu -->
       <div id="bingo-menu" class="bingo-menu">
        <div class="bingo-menu-grid"><button class="bingo-menu-btn" id="btn-create-bingo"> <span class="menu-btn-icon">📋</span> <span class="menu-btn-title">Crear Cartones</span> <span class="menu-btn-desc">Diseña y genera cartones personalizados</span> </button> <button class="bingo-menu-btn" id="btn-play-bingo"> <span class="menu-btn-icon">🎲</span> <span class="menu-btn-title">Jugar Bingo</span> <span class="menu-btn-desc">Sortea elementos con ruleta interactiva</span> </button>
        </div>
       </div><!-- Create Bingo Section -->
       <div id="create-bingo-section" class="bingo-section" style="display: none;">
        <div class="bingo-creator">
         <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;"><button class="back-to-menu-btn" id="back-from-create" style="margin: 0; padding: 0.5rem 1rem; font-size: 0.85rem;">← Volver</button>
          <h2 class="section-title" style="margin: 0;">⚙️ Configuración del Cartón</h2>
         </div>
         <div class="config-grid">
          <div class="config-item"><label for="grid-size">Tamaño del Cartón:</label> <select id="grid-size" class="bingo-select"> <option value="3">3x3 (9 casillas)</option> <option value="4">4x4 (16 casillas)</option> <option value="5" selected>5x5 (25 casillas)</option> <option value="6">6x6 (36 casillas)</option> </select>
          </div>
          <div class="config-item"><label for="free-center"> <input type="checkbox" id="free-center" checked> Casilla central GRATIS (solo impar) </label>
          </div>
          <div class="config-item"><label for="num-cards">Cantidad de Cartones:</label> <input type="number" id="num-cards" class="bingo-input" value="4" min="1" max="50">
          </div>
         </div>
         <h2 class="section-title">📝 Contenido de las Casillas</h2>
         <div class="content-tabs"><button class="content-tab active" data-tab="text">Textos</button> <button class="content-tab" data-tab="images">Imágenes</button>
         </div>
         <div id="text-content" class="content-panel active"><label for="text-input">Ingresa los textos (uno por línea):</label> <textarea id="text-input" class="bingo-textarea" rows="10" placeholder="Ejemplo:
Génesis
Éxodo
Levítico
Números
Deuteronomio
..."></textarea>
          <p class="helper-text">Textos ingresados: <span id="text-count">0</span></p>
         </div>
         <div id="image-content" class="content-panel"><label for="image-input">Ingresa las URLs de imágenes (una por línea):</label> <textarea id="image-input" class="bingo-textarea" rows="10" placeholder="https://ejemplo.com/imagen1.jpg
https://ejemplo.com/imagen2.jpg
https://ejemplo.com/imagen3.jpg"></textarea>
          <p class="helper-text">Imágenes ingresadas: <span id="image-count">0</span></p>
         </div><button class="generate-btn" id="generate-cards-btn">🎨 Generar Cartones</button> <!-- Cards Display -->
         <div id="cards-container" style="display: none;">
          <h2 class="section-title">🎯 Cartones Generados</h2>
          <div class="cards-actions"><button class="action-btn" id="print-cards-btn">🖨️ Imprimir Todos</button> <button class="action-btn" id="new-cards-btn">🔄 Generar Nuevos</button>
          </div>
          <div id="cards-grid" class="cards-grid"></div>
         </div>
        </div>
       </div><!-- Play Bingo Section -->
       <div id="play-bingo-section" class="bingo-section" style="display: none;">
        <div class="bingo-game">
         <div style="display: flex; align-items: center; gap: 1rem; margin-bottom: 1rem;"><button class="back-to-menu-btn" id="back-from-play" style="margin: 0; padding: 0.5rem 1rem; font-size: 0.85rem;">← Volver</button>
          <h2 class="section-title" style="margin: 0;">🎲 Configurar Elementos del Juego</h2>
         </div>
         <div class="game-setup"><label for="game-items">Ingresa los elementos a sortear (uno por línea):</label> <textarea id="game-items" class="bingo-textarea" rows="8" placeholder="Ejemplo:
Moisés
Abraham
David
Salomón
..."></textarea> <button class="start-game-btn" id="start-game-btn">🎯 Iniciar Juego</button>
         </div><!-- Game Active -->
         <div id="game-active" style="display: none;">
          <div class="game-controls"><button class="control-btn primary" id="spin-btn">🎲 Sortear Siguiente</button> <button class="control-btn" id="reset-game-btn">🔄 Reiniciar Juego</button>
          </div>
          <div class="game-display">
           <div class="roulette-container">
            <div class="current-item" id="current-item">
             <div class="item-label">
              Elemento Actual:
             </div>
             <div class="item-content" id="current-item-content">
              Presiona "Sortear"
             </div>
            </div>
           </div>
           <div class="game-stats">
            <div class="stat-item"><span class="stat-label">Elementos restantes:</span> <span class="stat-value" id="remaining-count">0</span>
            </div>
            <div class="stat-item"><span class="stat-label">Elementos sorteados:</span> <span class="stat-value" id="called-count">0</span>
            </div>
           </div>
          </div>
          <div class="history-section">
           <h3 class="history-title">📜 Historial de Sorteos</h3>
           <div id="history-list" class="history-list"></div>
          </div>
         </div>
        </div>
       </div>
      </div>
     </div>
    </div><!-- TRIVIA PAGE -->
    <div id="page-trivia" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">🎲 Trivia Bíblica</h1>
        <p class="tool-page-description">Preguntas y respuestas interactivas con marcador de puntos</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         🎲
        </div>
        <p class="placeholder-text">Próximamente: Trivia interactiva con preguntas bíblicas</p>
       </div>
      </div>
     </div>
    </div><!-- RULETA PAGE -->
    <div id="page-ruleta" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">🎡 Ruleta de Decisiones</h1>
        <p class="tool-page-description">Ruleta giratoria para seleccionar opciones al azar</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         🎡
        </div>
        <p class="placeholder-text">Próximamente: Ruleta visual giratoria</p>
       </div>
      </div>
     </div>
    </div><!-- EQUIPOS PAGE -->
    <div id="page-equipos" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">🃏 Generador de Equipos</h1>
        <p class="tool-page-description">Divide participantes en equipos aleatorios</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         🃏
        </div>
        <p class="placeholder-text">Próximamente: Generador automático de equipos</p>
       </div>
      </div>
     </div>
    </div><!-- TIMER PAGE -->
    <div id="page-timer" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">⏱️ Cronómetro y Timer</h1>
        <p class="tool-page-description">Temporizadores para actividades y dinámicas</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         ⏱️
        </div>
        <p class="placeholder-text">Próximamente: Cronómetro cuenta regresiva</p>
       </div>
      </div>
     </div>
    </div><!-- SORTEO PAGE -->
    <div id="page-sorteo" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">    Sorteo de Premios</h1>
        <p class="tool-page-description">Sortea nombres de participantes para premios</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         🎁
        </div>
        <p class="placeholder-text">Próximamente: Sistema de sorteos aleatorios</p>
       </div>
      </div>
     </div>
    </div><!-- ASISTENCIA PAGE -->
    <div id="page-asistencia" class="page">
     <div class="tool-page-container">
      <div class="tool-page-content">
       <div class="tool-page-header">
        <h1 class="tool-page-title">📋 Lista de Asistencia</h1>
        <p class="tool-page-description">Registro y seguimiento de participantes</p>
       </div>
       <div class="placeholder-content">
        <div class="placeholder-icon">
         📋
        </div>
        <p class="placeholder-text">Próximamente: Control de asistencia digital</p>
       </div>
      </div>
     </div>
    </div>
   </div>
  </div>
  <script>
    // Audio System - Web Audio API for sounds
    const AudioSystem = {
      context: null,
      
      init() {
        this.context = new (window.AudioContext || window.webkitAudioContext)();
      },
      
      playBeep(frequency, duration) {
        if (!this.context) this.init();
        
        const oscillator = this.context.createOscillator();
        const gainNode = this.context.createGain();
        
        oscillator.connect(gainNode);
        gainNode.connect(this.context.destination);
        
        oscillator.frequency.value = frequency;
        oscillator.type = 'sine';
        
        gainNode.gain.setValueAtTime(0.3, this.context.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, this.context.currentTime + duration);
        
        oscillator.start(this.context.currentTime);
        oscillator.stop(this.context.currentTime + duration);
      },
      
      playCountdown() {
        this.playBeep(800, 0.1);
      },
      
      playFinalBeep() {
        this.playBeep(1200, 0.3);
      },
      
      playAddPoints() {
        this.playBeep(600, 0.15);
        setTimeout(() => this.playBeep(800, 0.15), 100);
      },
      
      playSubtractPoints() {
        this.playBeep(400, 0.15);
        setTimeout(() => this.playBeep(300, 0.15), 100);
      }
    };

    const defaultConfig = {
      background_color: '#031427',
      nav_color: '#062238',
      card_color: '#0B3D91',
      text_color: '#e3f2fd',
      button_color: '#1565C0',
      font_family: 'Montserrat',
      font_size: 16,
      site_title: 'MyBibleGameHub-Iglesia Activa',
      tagline: 'Tu comunidad de fe conectada',
      welcome_title: 'Herramientas para tu Iglesia',
      welcome_text: 'Recursos interactivos para reuniones, eventos y actividades que fortalecen tu comunidad'
    };

    async function onConfigChange(config) {
      const baseSize = config.font_size || defaultConfig.font_size;
      const customFont = config.font_family || defaultConfig.font_family;
      const baseFontStack = 'system-ui, -apple-system, sans-serif';
      const fontFamily = `${customFont}, ${baseFontStack}`;
      
      const appContainer = document.querySelector('.app-container');
      appContainer.style.backgroundColor = config.background_color || defaultConfig.background_color;
      
      const pages = document.querySelectorAll('.page');
      pages.forEach(page => {
        page.style.backgroundColor = config.background_color || defaultConfig.background_color;
      });
      
      const navBar = document.querySelector('.nav-bar');
      navBar.style.backgroundColor = config.nav_color || defaultConfig.nav_color;
      
      const logo = document.getElementById('logo');
      logo.style.color = config.nav_color || defaultConfig.nav_color;
      
      document.getElementById('welcome-title').style.color = config.text_color || defaultConfig.text_color;
      document.getElementById('welcome-text').style.color = config.text_color || defaultConfig.text_color;
      
      const toolPageTitles = document.querySelectorAll('.tool-page-title');
      toolPageTitles.forEach(title => {
        title.style.color = config.text_color || defaultConfig.text_color;
      });
      
      const toolPageDescriptions = document.querySelectorAll('.tool-page-description');
      toolPageDescriptions.forEach(desc => {
        desc.style.color = config.text_color || defaultConfig.text_color;
      });
      
      document.body.style.fontFamily = fontFamily;
      
      const siteTitle = document.getElementById('site-title');
      siteTitle.style.fontSize = `${baseSize * 1.5}px`;
      siteTitle.style.fontFamily = fontFamily;
      
      const tagline = document.getElementById('tagline');
      tagline.style.fontSize = `${baseSize * 0.875}px`;
      tagline.style.fontFamily = fontFamily;
      
      const welcomeTitle = document.getElementById('welcome-title');
      welcomeTitle.style.fontSize = `${baseSize * 3.5}px`;
      welcomeTitle.style.fontFamily = fontFamily;
      
      const welcomeText = document.getElementById('welcome-text');
      welcomeText.style.fontSize = `${baseSize * 1.25}px`;
      welcomeText.style.fontFamily = fontFamily;
      
      siteTitle.textContent = config.site_title || defaultConfig.site_title;
      tagline.textContent = config.tagline || defaultConfig.tagline;
      welcomeTitle.textContent = config.welcome_title || defaultConfig.welcome_title;
      welcomeText.textContent = config.welcome_text || defaultConfig.welcome_text;
    }

    function mapToCapabilities(config) {
      return {
        recolorables: [
          {
            get: () => config.background_color || defaultConfig.background_color,
            set: (value) => {
              config.background_color = value;
              if (window.elementSdk) window.elementSdk.setConfig({ background_color: value });
            }
          },
          {
            get: () => config.nav_color || defaultConfig.nav_color,
            set: (value) => {
              config.nav_color = value;
              if (window.elementSdk) window.elementSdk.setConfig({ nav_color: value });
            }
          },
          {
            get: () => config.card_color || defaultConfig.card_color,
            set: (value) => {
              config.card_color = value;
              if (window.elementSdk) window.elementSdk.setConfig({ card_color: value });
            }
          },
          {
            get: () => config.text_color || defaultConfig.text_color,
            set: (value) => {
              config.text_color = value;
              if (window.elementSdk) window.elementSdk.setConfig({ text_color: value });
            }
          },
          {
            get: () => config.button_color || defaultConfig.button_color,
            set: (value) => {
              config.button_color = value;
              if (window.elementSdk) window.elementSdk.setConfig({ button_color: value });
            }
          }
        ],
        borderables: [],
        fontEditable: {
          get: () => config.font_family || defaultConfig.font_family,
          set: (value) => {
            config.font_family = value;
            if (window.elementSdk) window.elementSdk.setConfig({ font_family: value });
          }
        },
        fontSizeable: {
          get: () => config.font_size || defaultConfig.font_size,
          set: (value) => {
            config.font_size = value;
            if (window.elementSdk) window.elementSdk.setConfig({ font_size: value });
          }
        }
      };
    }

    function mapToEditPanelValues(config) {
      return new Map([
        ['site_title', config.site_title || defaultConfig.site_title],
        ['tagline', config.tagline || defaultConfig.tagline],
        ['welcome_title', config.welcome_title || defaultConfig.welcome_title],
        ['welcome_text', config.welcome_text || defaultConfig.welcome_text]
      ]);
    }

    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities,
        mapToEditPanelValues
      });
    }

    // Inspirational Bible Verses
    const inspirationalVerses = [
      {
        text: "Porque de tal manera amó Dios al mundo, que ha dado a su Hijo unigénito, para que todo aquel que en él cree, no se pierda, mas tenga vida eterna.",
        reference: "Juan 3:16"
      },
      {
        text: "Todo lo puedo en Cristo que me fortalece.",
        reference: "Filipenses 4:13"
      },
      {
        text: "Jehová es mi pastor; nada me faltará. En lugares de delicados pastos me hará descansar; junto a aguas de reposo me pastoreará.",
        reference: "Salmos 23:1-2"
      },
      {
        text: "Fíate de Jehová de todo tu corazón, y no te apoyes en tu propia prudencia. Reconócelo en todos tus caminos, y él enderezará tus veredas.",
        reference: "Proverbios 3:5-6"
      },
      {
        text: "El que habita al abrigo del Altísimo morará bajo la sombra del Omnipotente. Diré yo a Jehová: Esperanza mía, y castillo mío; mi Dios, en quien confiaré.",
        reference: "Salmos 91:1-2"
      },
      {
        text: "Más buscad primeramente el reino de Dios y su justicia, y todas estas cosas os serán añadidas.",
        reference: "Mateo 6:33"
      },
      {
        text: "Porque Jehová da la sabiduría, y de su boca viene el conocimiento y la inteligencia.",
        reference: "Proverbios 2:6"
      },
      {
        text: "Venid a mí todos los que estáis trabajados y cargados, y yo os haré descansar.",
        reference: "Mateo 11:28"
      },
      {
        text: "Nunca se apartará de tu boca este libro de la ley, sino que de día y de noche meditarás en él.",
        reference: "Josué 1:8"
      },
      {
        text: "No temas, porque yo estoy contigo; no desmayes, porque yo soy tu Dios que te esfuerzo.",
        reference: "Isaías 41:10"
      }
    ];

    let currentVerseIndex = 0;

    function displayVerse(index) {
      const verse = inspirationalVerses[index];
      const verseText = document.getElementById('verse-text');
      const verseReference = document.getElementById('verse-reference');
      
      if (verseText && verseReference) {
        verseText.textContent = verse.text;
        verseReference.textContent = verse.reference;
        
        const verseDisplay = document.querySelector('.verse-display');
        verseDisplay.style.animation = 'none';
        setTimeout(() => {
          verseDisplay.style.animation = 'fadeIn 0.6s ease';
        }, 10);
      }
    }

    function showToast(message) {
      const toast = document.createElement('div');
      toast.className = 'toast';
      toast.textContent = message;
      document.body.appendChild(toast);
      
      setTimeout(() => {
        toast.remove();
      }, 3000);
    }

    const nextVerseBtn = document.getElementById('next-verse-btn');
    if (nextVerseBtn) {
      nextVerseBtn.addEventListener('click', function() {
        currentVerseIndex = (currentVerseIndex + 1) % inspirationalVerses.length;
        displayVerse(currentVerseIndex);
      });
    }

    const footerLinks = document.querySelectorAll('.footer-links li');
    footerLinks.forEach(link => {
      link.addEventListener('click', function() {
        const linkText = this.textContent.trim();
        showToast(`📌 ${linkText}`);
      });
    });

    const footerCTABtn = document.querySelector('.footer-cta-btn');
    if (footerCTABtn) {
      footerCTABtn.addEventListener('click', function() {
        showToast('💬 Abriendo chat de soporte...');
      });
    }

    // ROUTING SYSTEM
    const routes = {
      '/': 'page-home',
      '/bingo': 'page-bingo',
      '/marcador': 'page-marcador',
      '/trivia': 'page-trivia',
      '/ruleta': 'page-ruleta',
      '/equipos': 'page-equipos',
      '/timer': 'page-timer',
      '/sorteo': 'page-sorteo',
      '/asistencia': 'page-asistencia'
    };

    function navigateTo(path) {
      window.location.hash = path;
    }

    function loadPage() {
      const hash = window.location.hash.slice(1) || '/';
      const pageId = routes[hash] || routes['/'];
      
      document.querySelectorAll('.page').forEach(page => {
        page.classList.remove('active');
      });
      
      const selectedPage = document.getElementById(pageId);
      if (selectedPage) {
        selectedPage.classList.add('active');
        selectedPage.scrollTop = 0;
      }
    }

    window.addEventListener('hashchange', loadPage);
    loadPage();
    
    if (window.location.hash === '' || window.location.hash === '#/') {
      displayVerse(currentVerseIndex);
    }

    // BINGO FUNCTIONALITY
    let bingoData = {
      texts: [],
      images: [],
      gridSize: 5,
      freeCenter: true,
      numCards: 4,
      gameItems: [],
      calledItems: [],
      remainingItems: []
    };

    const bibleVerses = [
      { text: "Porque de tal manera amó Dios al mundo, que ha dado a su Hijo unigénito", ref: "Juan 3:16" },
      { text: "Todo lo puedo en Cristo que me fortalece", ref: "Filipenses 4:13" },
      { text: "Jehová es mi pastor; nada me faltará", ref: "Salmos 23:1" },
      { text: "Fíate de Jehová de todo tu corazón", ref: "Proverbios 3:5" },
      { text: "El que habita al abrigo del Altísimo morará bajo la sombra del Omnipotente", ref: "Salmos 91:1" }
    ];

    document.getElementById('btn-create-bingo')?.addEventListener('click', () => {
      document.getElementById('bingo-menu').style.display = 'none';
      document.getElementById('create-bingo-section').style.display = 'block';
    });

    document.getElementById('btn-play-bingo')?.addEventListener('click', () => {
      document.getElementById('bingo-menu').style.display = 'none';
      document.getElementById('play-bingo-section').style.display = 'block';
    });

    document.getElementById('back-from-create')?.addEventListener('click', () => {
      document.getElementById('create-bingo-section').style.display = 'none';
      document.getElementById('bingo-menu').style.display = 'block';
    });

    document.getElementById('back-from-play')?.addEventListener('click', () => {
      document.getElementById('play-bingo-section').style.display = 'none';
      document.getElementById('bingo-menu').style.display = 'block';
    });

    document.querySelectorAll('.content-tab').forEach(tab => {
      tab.addEventListener('click', () => {
        const tabName = tab.dataset.tab;
        
        document.querySelectorAll('.content-tab').forEach(t => t.classList.remove('active'));
        document.querySelectorAll('.content-panel').forEach(p => p.classList.remove('active'));
        
        tab.classList.add('active');
        document.getElementById(`${tabName}-content`).classList.add('active');
      });
    });

    document.getElementById('text-input')?.addEventListener('input', (e) => {
      const lines = e.target.value.split('\n').filter(line => line.trim() !== '');
      document.getElementById('text-count').textContent = lines.length;
    });

    document.getElementById('image-input')?.addEventListener('input', (e) => {
      const lines = e.target.value.split('\n').filter(line => line.trim() !== '');
      document.getElementById('image-count').textContent = lines.length;
    });

    document.getElementById('generate-cards-btn')?.addEventListener('click', () => {
      const textInput = document.getElementById('text-input').value;
      const imageInput = document.getElementById('image-input').value;
      const gridSize = parseInt(document.getElementById('grid-size').value);
      const freeCenter = document.getElementById('free-center').checked;
      const numCards = parseInt(document.getElementById('num-cards').value);

      bingoData.texts = textInput.split('\n').filter(line => line.trim() !== '');
      bingoData.images = imageInput.split('\n').filter(line => line.trim() !== '');
      bingoData.gridSize = gridSize;
      bingoData.freeCenter = freeCenter;
      bingoData.numCards = numCards;

      const totalCells = gridSize * gridSize;
      const neededCells = freeCenter && gridSize % 2 === 1 ? totalCells - 1 : totalCells;
      const totalItems = bingoData.texts.length + bingoData.images.length;

      if (totalItems < neededCells) {
        showToast(`⚠️ Necesitas al menos ${neededCells} elementos para un cartón ${gridSize}x${gridSize}`);
        return;
      }

      generateBingoCards();
    });

    function generateBingoCards() {
      const cardsContainer = document.getElementById('cards-grid');
      cardsContainer.innerHTML = '';

      const allItems = [
        ...bingoData.texts.map(text => ({ type: 'text', content: text })),
        ...bingoData.images.map(img => ({ type: 'image', content: img }))
      ];

      for (let cardNum = 0; cardNum < bingoData.numCards; cardNum++) {
        const card = createBingoCard(allItems, cardNum + 1);
        cardsContainer.appendChild(card);
      }

      document.getElementById('cards-container').style.display = 'block';
      document.getElementById('cards-container').scrollIntoView({ behavior: 'smooth' });
    }

    function createBingoCard(allItems, cardNumber) {
      const card = document.createElement('div');
      card.className = 'bingo-card';

      const header = document.createElement('div');
      header.className = 'card-header';
      header.innerHTML = `
        <h3 class="card-title">Bingo Bíblico</h3>
        <p class="card-number">Cartón #${cardNumber}</p>
      `;
      card.appendChild(header);

      const nameSection = document.createElement('div');
      nameSection.className = 'card-name-section';
      nameSection.innerHTML = `
        <span class="card-name-label">Nombre:</span>
        <div class="card-name-line"></div>
      `;
      card.appendChild(nameSection);

      const grid = document.createElement('div');
      grid.className = 'bingo-grid';
      grid.style.gridTemplateColumns = `repeat(${bingoData.gridSize}, 1fr)`;

      const shuffled = [...allItems].sort(() => Math.random() - 0.5);
      const totalCells = bingoData.gridSize * bingoData.gridSize;
      const centerIndex = Math.floor(totalCells / 2);

      for (let i = 0; i < totalCells; i++) {
        const cell = document.createElement('div');
        cell.className = 'bingo-cell';

        if (bingoData.freeCenter && bingoData.gridSize % 2 === 1 && i === centerIndex) {
          cell.classList.add('free');
          cell.textContent = 'GRATIS';
        } else {
          const itemIndex = i > centerIndex && bingoData.freeCenter && bingoData.gridSize % 2 === 1 ? i - 1 : i;
          const item = shuffled[itemIndex % shuffled.length];

          if (item.type === 'text') {
            cell.textContent = item.content;
          } else {
            const img = document.createElement('img');
            img.src = item.content;
            img.alt = 'Imagen de bingo';
            img.onerror = function() {
              this.src = '';
              this.alt = 'Imagen no disponible';
              this.style.display = 'none';
            };
            cell.appendChild(img);
          }
        }

        grid.appendChild(cell);
      }

      card.appendChild(grid);

      const footer = document.createElement('div');
      footer.className = 'card-footer';
      const randomVerse = bibleVerses[Math.floor(Math.random() * bibleVerses.length)];
      footer.innerHTML = `
        <p class="card-verse">"${randomVerse.text}" - ${randomVerse.ref}</p>
      `;
      card.appendChild(footer);

      return card;
    }

    document.getElementById('print-cards-btn')?.addEventListener('click', () => {
      window.print();
    });

    document.getElementById('new-cards-btn')?.addEventListener('click', () => {
      generateBingoCards();
    });

    document.getElementById('start-game-btn')?.addEventListener('click', () => {
      const gameItemsInput = document.getElementById('game-items').value;
      const items = gameItemsInput.split('\n').filter(line => line.trim() !== '');

      if (items.length < 2) {
        showToast('⚠️ Necesitas al menos 2 elementos para jugar');
        return;
      }

      bingoData.gameItems = items;
      bingoData.remainingItems = [...items];
      bingoData.calledItems = [];

      document.querySelector('.game-setup').style.display = 'none';
      document.getElementById('game-active').style.display = 'block';
      
      updateGameStats();
      document.getElementById('current-item-content').textContent = 'Presiona "Sortear"';
      document.getElementById('history-list').innerHTML = '';
    });

    document.getElementById('spin-btn')?.addEventListener('click', () => {
      if (bingoData.remainingItems.length === 0) {
        showToast('🎉 ¡Todos los elementos han sido sorteados!');
        document.getElementById('spin-btn').disabled = true;
        return;
      }

      const randomIndex = Math.floor(Math.random() * bingoData.remainingItems.length);
      const drawnItem = bingoData.remainingItems[randomIndex];

      bingoData.remainingItems.splice(randomIndex, 1);
      bingoData.calledItems.push(drawnItem);

      document.getElementById('current-item-content').textContent = drawnItem;
      document.getElementById('current-item-content').style.animation = 'none';
      setTimeout(() => {
        document.getElementById('current-item-content').style.animation = 'pulse 0.5s ease';
      }, 10);

      addToHistory(drawnItem);
      updateGameStats();

      if (bingoData.remainingItems.length === 0) {
        document.getElementById('spin-btn').disabled = true;
      }
    });

    function addToHistory(item) {
      const historyList = document.getElementById('history-list');
      const historyItem = document.createElement('div');
      historyItem.className = 'history-item';
      historyItem.textContent = item;
      historyList.insertBefore(historyItem, historyList.firstChild);
    }

    function updateGameStats() {
      document.getElementById('remaining-count').textContent = bingoData.remainingItems.length;
      document.getElementById('called-count').textContent = bingoData.calledItems.length;
    }

    document.getElementById('reset-game-btn')?.addEventListener('click', () => {
      bingoData.remainingItems = [...bingoData.gameItems];
      bingoData.calledItems = [];

      document.getElementById('current-item-content').textContent = 'Presiona "Sortear"';
      document.getElementById('history-list').innerHTML = '';
      document.getElementById('spin-btn').disabled = false;

      updateGameStats();
      showToast('🔄 Juego reiniciado');
    });

    // MARCADOR FUNCTIONALITY WITH ENHANCED FEATURES
    let marcadorData = {
      teams: [],
      numTeams: 2,
      timerMode: 'countdown',
      timerMinutes: 5,
      timerSeconds: 0,
      timerTotalSeconds: 300,
      timerCurrentSeconds: 300,
      timerInterval: null,
      timerRunning: false,
      // New features
      currentRound: 1,
      totalRounds: 1,
      roundHistory: [],
      targetScore: null,
      fullscreenMode: false,
      gamePreset: 'custom',
      penalties: [],
      matchHistory: []
    };

    const defaultTeamNames = [
      'Equipo Rojo', 'Equipo Azul', 'Equipo Verde', 'Equipo Amarillo', 
      'Equipo Naranja', 'Equipo Morado', 'Equipo Rosa', 'Equipo Celeste',
      'Equipo Dorado', 'Equipo Plateado', 'Equipo Blanco', 'Equipo Negro',
      'Equipo Turquesa', 'Equipo Violeta', 'Equipo Coral'
    ];

    const gamePresets = {
      trivia: {
        name: 'Trivia Bíblica',
        timer: { mode: 'countdown', minutes: 2, seconds: 0 },
        rounds: 5,
        targetScore: null
      },
      versos: {
        name: 'Carreras de Versículos',
        timer: { mode: 'countdown', minutes: 2, seconds: 0 },
        rounds: 3,
        targetScore: null
      },
      memorization: {
        name: 'Memorización',
        timer: { mode: 'countdown', minutes: 5, seconds: 0 },
        rounds: 1,
        targetScore: 100
      }
    };

    document.getElementById('game-preset')?.addEventListener('change', (e) => {
      const preset = e.target.value;
      if (preset !== 'custom' && gamePresets[preset]) {
        const presetConfig = gamePresets[preset];
        document.getElementById('timer-minutes').value = presetConfig.timer.minutes;
        document.getElementById('timer-seconds').value = presetConfig.timer.seconds;
        document.getElementById('timer-mode').value = presetConfig.timer.mode;
        document.getElementById('total-rounds').value = presetConfig.rounds;
        document.getElementById('target-score').value = presetConfig.targetScore || '';
        showToast(`🎮 Preset "${presetConfig.name}" aplicado`);
      }
    });

    document.getElementById('btn-new-game')?.addEventListener('click', () => {
      document.getElementById('marcador-menu').style.display = 'none';
      document.getElementById('game-setup-section').style.display = 'block';
      generateTeamInputs();
    });

    document.getElementById('back-from-setup')?.addEventListener('click', () => {
      document.getElementById('game-setup-section').style.display = 'none';
      document.getElementById('marcador-menu').style.display = 'block';
    });

    document.getElementById('back-from-game')?.addEventListener('click', () => {
      const confirmDiv = document.createElement('div');
      confirmDiv.style.cssText = 'position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: linear-gradient(135deg, #1e3a5f 0%, #0d1b2a 100%); padding: 2rem; border-radius: 1rem; box-shadow: 0 10px 40px rgba(0,0,0,0.5); z-index: 10000; border: 3px solid rgba(33, 150, 243, 0.4);';
      confirmDiv.innerHTML = `
        <h3 style="color: white; margin-bottom: 1rem; font-size: 1.5rem;">¿Finalizar partida?</h3>
        <p style="color: rgba(255,255,255,0.8); margin-bottom: 1.5rem;">Los puntajes se perderán</p>
        <div style="display: flex; gap: 1rem;">
          <button id="confirm-end-yes" style="flex: 1; padding: 0.75rem; background: #f44336; color: white; border: none; border-radius: 0.5rem; font-weight: 600; cursor: pointer;">Sí, finalizar</button>
          <button id="confirm-end-no" style="flex: 1; padding: 0.75rem; background: #2196f3; color: white; border: none; border-radius: 0.5rem; font-weight: 600; cursor: pointer;">Cancelar</button>
        </div>
      `;
      document.body.appendChild(confirmDiv);

      document.getElementById('confirm-end-yes').addEventListener('click', () => {
        confirmDiv.remove();
        stopTimer();
        document.getElementById('active-game-section').style.display = 'none';
        document.getElementById('marcador-menu').style.display = 'block';
      });

      document.getElementById('confirm-end-no').addEventListener('click', () => {
        confirmDiv.remove();
      });
    });

    document.getElementById('num-teams')?.addEventListener('change', (e) => {
      marcadorData.numTeams = parseInt(e.target.value);
      generateTeamInputs();
    });

    function generateTeamInputs() {
      const container = document.getElementById('team-names-container');
      container.innerHTML = '';

      for (let i = 0; i < marcadorData.numTeams; i++) {
        const item = document.createElement('div');
        item.className = 'config-item';
        item.innerHTML = `
          <label for="team-name-${i}">Equipo ${i + 1}:</label>
          <input type="text" id="team-name-${i}" class="bingo-input" value="${defaultTeamNames[i] || 'Equipo ' + (i + 1)}" placeholder="Nombre del equipo">
        `;
        container.appendChild(item);
      }
    }

    document.getElementById('start-marcador-btn')?.addEventListener('click', () => {
      marcadorData.teams = [];

      for (let i = 0; i < marcadorData.numTeams; i++) {
        const nameInput = document.getElementById(`team-name-${i}`);
        const teamName = nameInput?.value.trim() || defaultTeamNames[i] || `Equipo ${i + 1}`;
        marcadorData.teams.push({
          id: i,
          name: teamName,
          score: 0,
          roundWins: 0
        });
      }

      // Configure rounds
      marcadorData.totalRounds = parseInt(document.getElementById('total-rounds').value);
      marcadorData.currentRound = 1;
      marcadorData.roundHistory = [];

      // Configure target score
      const targetInput = document.getElementById('target-score').value;
      marcadorData.targetScore = targetInput ? parseInt(targetInput) : null;

      document.getElementById('game-setup-section').style.display = 'none';
      document.getElementById('active-game-section').style.display = 'block';
      
      updateRoundsDisplay();
      updateTargetDisplay();
      renderScoreboard();
      resetTimerToConfig();
    });

    function updateRoundsDisplay() {
      const roundsIndicator = document.getElementById('rounds-indicator');
      if (marcadorData.totalRounds > 1) {
        roundsIndicator.style.display = 'block';
        document.getElementById('current-round-display').textContent = marcadorData.currentRound;
        document.getElementById('total-rounds-display').textContent = marcadorData.totalRounds;
        document.getElementById('next-round-btn').style.display = 'block';
      } else {
        roundsIndicator.style.display = 'none';
        document.getElementById('next-round-btn').style.display = 'none';
      }
    }

    function updateTargetDisplay() {
      const targetIndicator = document.getElementById('target-indicator');
      if (marcadorData.targetScore) {
        targetIndicator.style.display = 'block';
        document.getElementById('target-score-display').textContent = marcadorData.targetScore;
      } else {
        targetIndicator.style.display = 'none';
      }
    }

    function renderScoreboard() {
      const container = document.getElementById('scoreboard-container');
      container.innerHTML = '';
      
      const numTeams = marcadorData.teams.length;
      container.setAttribute('data-teams', numTeams);
      
      if (numTeams <= 5) {
        container.style.setProperty('--cols', numTeams);
      }

      // Sort teams by score to determine ranks
      const sortedTeams = [...marcadorData.teams].sort((a, b) => b.score - a.score);
      const rankMap = {};
      sortedTeams.forEach((team, index) => {
        rankMap[team.id] = index + 1;
      });

      marcadorData.teams.forEach(team => {
        const card = document.createElement('div');
        card.className = 'team-card';
        
        const rank = rankMap[team.id];
        let trophyBadge = '';
        if (rank === 1) {
          trophyBadge = '<div class="trophy-badge gold">🥇</div>';
        } else if (rank === 2) {
          trophyBadge = '<div class="trophy-badge silver">🥈</div>';
        } else if (rank === 3) {
          trophyBadge = '<div class="trophy-badge bronze">🥉</div>';
        }
        
        let progressBar = '';
        if (marcadorData.targetScore) {
          const progress = Math.min((team.score / marcadorData.targetScore) * 100, 100);
          progressBar = `
            <div class="progress-bar">
              <div class="progress-fill" style="width: ${progress}%"></div>
            </div>
          `;
        }

        card.innerHTML = `
          ${trophyBadge}
          <div class="team-name">${team.name}</div>
          <div class="team-score" id="score-${team.id}">${team.score}</div>
          ${progressBar}
          <div class="team-controls">
            <button class="score-btn subtract" onclick="updateScore(${team.id}, -1)">-1</button>
            <button class="score-btn add" onclick="updateScore(${team.id}, 1)">+1</button>
            <button class="score-btn add" onclick="updateScore(${team.id}, 3)">+3</button>
          </div>
          <div class="team-controls">
            <button class="score-btn add" onclick="updateScore(${team.id}, 5)">+5</button>
            <button class="score-btn add" onclick="updateScore(${team.id}, 10)">+10</button>
            <button class="score-btn add bonus-btn" onclick="updateScore(${team.id}, 50)">⭐ +50</button>
          </div>
          <div class="team-controls">
            <button class="score-btn subtract penalty-btn" onclick="applyPenalty(${team.id}, 5)">⚠️ -5</button>
            <button class="score-btn subtract penalty-btn" onclick="applyPenalty(${team.id}, 10)">⚠️ -10</button>
          </div>
        `;
        container.appendChild(card);
      });
    }

    window.updateScore = function(teamId, points) {
      const team = marcadorData.teams.find(t => t.id === teamId);
      if (team) {
        team.score = Math.max(0, team.score + points);
        
        // Play sound
        if (points > 0) {
          AudioSystem.playAddPoints();
        } else if (points < 0) {
          AudioSystem.playSubtractPoints();
        }
        
        const scoreElement = document.getElementById(`score-${teamId}`);
        if (scoreElement) {
          scoreElement.textContent = team.score;
          scoreElement.style.animation = 'none';
          setTimeout(() => {
            scoreElement.style.animation = 'pulse 0.3s ease';
          }, 10);
        }

        // Check target score
        if (marcadorData.targetScore && team.score >= marcadorData.targetScore) {
          showToast(`🏆 ¡${team.name} alcanzó ${marcadorData.targetScore} puntos!`);
        }

        // Update progress bar and ranks
        renderScoreboard();
      }
    };

    window.applyPenalty = function(teamId, points) {
      const team = marcadorData.teams.find(t => t.id === teamId);
      if (team) {
        team.score = Math.max(0, team.score - points);
        
        // Play penalty sound
        AudioSystem.playSubtractPoints();
        
        marcadorData.penalties.push({
          teamId,
          teamName: team.name,
          points,
          timestamp: new Date()
        });
        
        const scoreElement = document.getElementById(`score-${teamId}`);
        if (scoreElement) {
          scoreElement.textContent = team.score;
          scoreElement.style.animation = 'none';
          setTimeout(() => {
            scoreElement.style.animation = 'pulse 0.3s ease';
          }, 10);
        }

        showToast(`⚠️ Penalización -${points} pts a ${team.name}`);
        renderScoreboard();
      }
    };

    document.getElementById('next-round-btn')?.addEventListener('click', () => {
      if (marcadorData.currentRound >= marcadorData.totalRounds) {
        showToast('⚠️ Ya completaste todas las rondas');
        return;
      }

      // Save current round
      const roundScores = marcadorData.teams.map(t => ({
        id: t.id,
        name: t.name,
        score: t.score
      }));
      
      const winner = marcadorData.teams.reduce((max, team) => team.score > max.score ? team : max, marcadorData.teams[0]);
      winner.roundWins++;

      marcadorData.roundHistory.push({
        round: marcadorData.currentRound,
        scores: roundScores,
        winner: winner.name
      });

      // Reset scores for next round
      marcadorData.teams.forEach(team => {
        team.score = 0;
      });

      marcadorData.currentRound++;
      updateRoundsDisplay();
      renderScoreboard();
      showToast(`🔄 Iniciando Ronda ${marcadorData.currentRound}`);
    });

    document.getElementById('reset-scores-btn')?.addEventListener('click', () => {
      const confirmDiv = document.createElement('div');
      confirmDiv.style.cssText = 'position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: linear-gradient(135deg, #1e3a5f 0%, #0d1b2a 100%); padding: 2rem; border-radius: 1rem; box-shadow: 0 10px 40px rgba(0,0,0,0.5); z-index: 10000; border: 3px solid rgba(33, 150, 243, 0.4);';
      confirmDiv.innerHTML = `
        <h3 style="color: white; margin-bottom: 1rem; font-size: 1.5rem;">¿Reiniciar puntajes?</h3>
        <p style="color: rgba(255,255,255,0.8); margin-bottom: 1.5rem;">Todos los puntajes volverán a 0</p>
        <div style="display: flex; gap: 1rem;">
          <button id="confirm-reset-yes" style="flex: 1; padding: 0.75rem; background: #f44336; color: white; border: none; border-radius: 0.5rem; font-weight: 600; cursor: pointer;">Sí, reiniciar</button>
          <button id="confirm-reset-no" style="flex: 1; padding: 0.75rem; background: #2196f3; color: white; border: none; border-radius: 0.5rem; font-weight: 600; cursor: pointer;">Cancelar</button>
        </div>
      `;
      document.body.appendChild(confirmDiv);

      document.getElementById('confirm-reset-yes').addEventListener('click', () => {
        marcadorData.teams.forEach(team => {
          team.score = 0;
        });
        renderScoreboard();
        confirmDiv.remove();
        showToast('🔄 Puntajes reiniciados');
      });

      document.getElementById('confirm-reset-no').addEventListener('click', () => {
        confirmDiv.remove();
      });
    });

    document.getElementById('view-stats-btn')?.addEventListener('click', () => {
      showStatsModal();
    });

    function showStatsModal() {
      const modal = document.createElement('div');
      modal.className = 'history-modal';
      
      let content = `
        <div class="modal-header">
          <h3 class="modal-title">📊 Estadísticas del Juego</h3>
          <button class="modal-close" id="close-stats-modal">✖</button>
        </div>
      `;

      // Current scores
      content += '<div class="stats-panel"><h4 style="color: #2196f3; margin-bottom: 1rem;">Puntajes Actuales</h4><div class="stats-grid">';
      marcadorData.teams.forEach(team => {
        content += `
          <div class="stat-card">
            <div class="stat-card-label">${team.name}</div>
            <div class="stat-card-value">${team.score}</div>
            ${marcadorData.totalRounds > 1 ? `<div class="stat-card-label">Victorias: ${team.roundWins}</div>` : ''}
          </div>
        `;
      });
      content += '</div></div>';

      // Round history
      if (marcadorData.roundHistory.length > 0) {
        content += '<h4 style="color: #2196f3; margin: 1.5rem 0 1rem 0;">📜 Historial de Rondas</h4>';
        marcadorData.roundHistory.forEach(round => {
          content += `
            <div class="round-history-item">
              <div class="round-history-header">Ronda ${round.round} - Ganador: ${round.winner} 🏆</div>
              <div class="round-scores">
          `;
          round.scores.forEach(score => {
            content += `
              <div class="round-score-item">
                <span class="round-team-name">${score.name}</span>
                <span class="round-team-score">${score.score}</span>
              </div>
            `;
          });
          content += '</div></div>';
        });
      }

      // Penalties
      if (marcadorData.penalties.length > 0) {
        content += '<h4 style="color: #ffc107; margin: 1.5rem 0 1rem 0;">⚠️ Penalizaciones</h4>';
        content += '<div class="stats-grid">';
        const penaltyGroups = {};
        marcadorData.penalties.forEach(p => {
          if (!penaltyGroups[p.teamName]) penaltyGroups[p.teamName] = 0;
          penaltyGroups[p.teamName] += p.points;
        });
        Object.entries(penaltyGroups).forEach(([team, total]) => {
          content += `
            <div class="stat-card">
              <div class="stat-card-label">${team}</div>
              <div class="stat-card-value" style="color: #ffc107;">-${total}</div>
            </div>
          `;
        });
        content += '</div>';
      }

      modal.innerHTML = content;
      document.body.appendChild(modal);

      document.getElementById('close-stats-modal').addEventListener('click', () => {
        modal.remove();
      });
    }

    document.getElementById('fullscreen-btn')?.addEventListener('click', () => {
      const elem = document.getElementById('active-game-section');
      if (!document.fullscreenElement) {
        elem.requestFullscreen().catch(err => {
          showToast('⚠️ No se pudo activar pantalla completa');
        });
      } else {
        document.exitFullscreen();
      }
    });

    document.getElementById('end-game-btn')?.addEventListener('click', () => {
      let winner;
      
      if (marcadorData.totalRounds > 1) {
        winner = marcadorData.teams.reduce((max, team) => team.roundWins > max.roundWins ? team : max, marcadorData.teams[0]);
      } else {
        winner = marcadorData.teams.reduce((max, team) => team.score > max.score ? team : max, marcadorData.teams[0]);
      }
      
      const resultDiv = document.createElement('div');
      resultDiv.style.cssText = 'position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); background: linear-gradient(135deg, #1e3a5f 0%, #0d1b2a 100%); padding: 3rem; border-radius: 1rem; box-shadow: 0 10px 40px rgba(0,0,0,0.5); z-index: 10000; border: 3px solid rgba(33, 150, 243, 0.4); text-align: center; min-width: 400px;';
      
      let resultHTML = `
        <div style="font-size: 4rem; margin-bottom: 1rem;">🏆</div>
        <h2 style="color: #2196f3; margin-bottom: 1rem; font-size: 2rem;">¡Ganador!</h2>
        <h3 style="color: white; margin-bottom: 0.5rem; font-size: 1.8rem;">${winner.name}</h3>
      `;

      if (marcadorData.totalRounds > 1) {
        resultHTML += `
          <p style="color: white; font-size: 2rem; font-weight: 800; margin-bottom: 0.5rem;">${winner.roundWins} Victorias</p>
          <p style="color: rgba(255,255,255,0.7); font-size: 1.2rem; margin-bottom: 2rem;">Puntaje final: ${winner.score}</p>
        `;
      } else {
        resultHTML += `
          <p style="color: white; font-size: 3rem; font-weight: 800; margin-bottom: 2rem;">${winner.score} puntos</p>
        `;
      }

      resultHTML += `<button id="close-results" style="padding: 1rem 2rem; background: #2196f3; color: white; border: none; border-radius: 0.75rem; font-weight: 700; cursor: pointer; font-size: 1rem;">Cerrar</button>`;

      resultDiv.innerHTML = resultHTML;
      document.body.appendChild(resultDiv);

      document.getElementById('close-results').addEventListener('click', () => {
        resultDiv.remove();
      });
    });

    // TIMER FUNCTIONALITY
    document.getElementById('set-timer-btn')?.addEventListener('click', () => {
      const mode = document.getElementById('timer-mode').value;
      const minutes = parseInt(document.getElementById('timer-minutes').value) || 0;
      const seconds = parseInt(document.getElementById('timer-seconds').value) || 0;
      
      if (mode === 'countdown' && minutes === 0 && seconds === 0) {
        showToast('⚠️ Configura un tiempo mayor a 0 para cuenta regresiva');
        return;
      }

      marcadorData.timerMode = mode;
      marcadorData.timerMinutes = minutes;
      marcadorData.timerSeconds = seconds;
      marcadorData.timerTotalSeconds = minutes * 60 + seconds;
      
      if (mode === 'countdown') {
        marcadorData.timerCurrentSeconds = marcadorData.timerTotalSeconds;
      } else {
        marcadorData.timerCurrentSeconds = 0;
      }

      document.getElementById('timer-config').style.display = 'none';
      document.getElementById('timer-display-compact').style.display = 'block';
      updateTimerDisplay();
      
      const modeText = mode === 'countdown' ? 'Cuenta Regresiva' : 'Cronómetro';
      showToast(`⏱️ ${modeText} configurado`);
    });

    document.getElementById('timer-start-btn')?.addEventListener('click', () => {
      startTimer();
    });

    document.getElementById('timer-pause-btn')?.addEventListener('click', () => {
      pauseTimer();
    });

    document.getElementById('timer-reset-btn')?.addEventListener('click', () => {
      resetTimer();
    });

    document.getElementById('timer-edit-btn')?.addEventListener('click', () => {
      stopTimer();
      document.getElementById('timer-display-compact').style.display = 'none';
      document.getElementById('timer-config').style.display = 'flex';
    });

    function startTimer() {
      if (marcadorData.timerRunning) return;
      
      marcadorData.timerRunning = true;
      document.getElementById('timer-start-btn').style.display = 'none';
      document.getElementById('timer-pause-btn').style.display = 'inline-block';

      marcadorData.timerInterval = setInterval(() => {
        if (marcadorData.timerMode === 'countdown') {
          marcadorData.timerCurrentSeconds--;
          updateTimerDisplay();

          // Play countdown sound in last 10 seconds
          if (marcadorData.timerCurrentSeconds <= 10 && marcadorData.timerCurrentSeconds > 0) {
            AudioSystem.playCountdown();
          }

          if (marcadorData.timerCurrentSeconds <= 0) {
            stopTimer();
            AudioSystem.playFinalBeep();
            showTimeUpModal();
            const display = document.getElementById('timer-time-display');
            display.classList.add('danger');
          }
        } else {
          marcadorData.timerCurrentSeconds++;
          updateTimerDisplay();
        }
      }, 1000);
    }

    function pauseTimer() {
      stopTimer();
      document.getElementById('timer-start-btn').style.display = 'inline-block';
      document.getElementById('timer-pause-btn').style.display = 'none';
    }

    function stopTimer() {
      if (marcadorData.timerInterval) {
        clearInterval(marcadorData.timerInterval);
        marcadorData.timerInterval = null;
      }
      marcadorData.timerRunning = false;
    }

    function resetTimer() {
      stopTimer();
      
      if (marcadorData.timerMode === 'countdown') {
        marcadorData.timerCurrentSeconds = marcadorData.timerTotalSeconds;
      } else {
        marcadorData.timerCurrentSeconds = 0;
      }
      
      updateTimerDisplay();
      document.getElementById('timer-start-btn').style.display = 'inline-block';
      document.getElementById('timer-pause-btn').style.display = 'none';
      
      const display = document.getElementById('timer-time-display');
      display.classList.remove('warning', 'danger');
    }

    function resetTimerToConfig() {
      stopTimer();
      document.getElementById('timer-config').style.display = 'flex';
      document.getElementById('timer-display-compact').style.display = 'none';
      document.getElementById('timer-start-btn').style.display = 'inline-block';
      document.getElementById('timer-pause-btn').style.display = 'none';
    }

    function showTimeUpModal() {
      const modal = document.createElement('div');
      modal.style.cssText = 'position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.95); z-index: 100000; display: flex; align-items: center; justify-content: center; animation: fadeIn 0.3s ease;';
      
      modal.innerHTML = `
        <div style="text-align: center; animation: scaleIn 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);">
          <div style="font-size: 10rem; margin-bottom: 1rem; animation: bounceIn 0.8s ease;">⏰</div>
          <h1 style="color: #f44336; font-size: 4rem; font-weight: 900; margin-bottom: 1rem; text-shadow: 0 0 30px rgba(244, 67, 54, 0.8); animation: pulse 1s ease infinite;">¡TIEMPO TERMINADO!</h1>
          <div style="font-size: 8rem; font-weight: 900; color: #ff5722; margin: 2rem 0; font-family: 'Courier New', monospace; text-shadow: 0 0 40px rgba(255, 87, 34, 0.8); animation: pulse 1s ease infinite;">00:00</div>
          <button id="close-time-up" style="padding: 1.5rem 3rem; background: linear-gradient(135deg, #f44336 0%, #c62828 100%); color: white; border: none; border-radius: 1rem; font-weight: 800; cursor: pointer; font-size: 1.5rem; box-shadow: 0 8px 30px rgba(244, 67, 54, 0.5); transition: all 0.3s; margin-top: 2rem;">CONTINUAR</button>
        </div>
        <style>
          @keyframes scaleIn {
            from {
              transform: scale(0.5);
              opacity: 0;
            }
            to {
              transform: scale(1);
              opacity: 1;
            }
          }
          @keyframes bounceIn {
            0%, 20%, 40%, 60%, 80%, 100% {
              animation-timing-function: cubic-bezier(0.215, 0.610, 0.355, 1.000);
            }
            0% {
              opacity: 0;
              transform: scale3d(.3, .3, .3);
            }
            20% {
              transform: scale3d(1.1, 1.1, 1.1);
            }
            40% {
              transform: scale3d(.9, .9, .9);
            }
            60% {
              opacity: 1;
              transform: scale3d(1.03, 1.03, 1.03);
            }
            80% {
              transform: scale3d(.97, .97, .97);
            }
            100% {
              opacity: 1;
              transform: scale3d(1, 1, 1);
            }
          }
          #close-time-up:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 12px 40px rgba(244, 67, 54, 0.7);
          }
        </style>
      `;
      
      document.body.appendChild(modal);
      
      document.getElementById('close-time-up').addEventListener('click', () => {
        modal.style.animation = 'fadeOut 0.3s ease';
        setTimeout(() => {
          modal.remove();
        }, 300);
      });
    }

    function updateTimerDisplay() {
      const minutes = Math.floor(marcadorData.timerCurrentSeconds / 60);
      const seconds = marcadorData.timerCurrentSeconds % 60;
      const display = document.getElementById('timer-time-display');
      
      display.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
      
      display.classList.remove('warning', 'danger');
      
      if (marcadorData.timerMode === 'countdown') {
        if (marcadorData.timerCurrentSeconds <= 10) {
          display.classList.add('danger');
        } else if (marcadorData.timerCurrentSeconds <= 30) {
          display.classList.add('warning');
        }
      }
    }
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9b64300a32d01b61',t:'MTc2NzEyNTUwMC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>