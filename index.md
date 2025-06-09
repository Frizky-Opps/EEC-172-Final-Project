<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>2048 on Embedded System – TI CC3200</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f8f9fa;
      margin: 0;
      padding: 0;
      color: #333;
    }
    header {
      background-color: #343a40;
      color: white;
      padding: 2rem 1rem;
      text-align: center;
    }
    header h1 {
      font-size: 3.5rem;
      margin: 0;
    }
    header p {
      font-size: 1.2rem;
      margin: 0.5rem 0 0;
    }
    main {
      max-width: 800px;
      margin: 2rem auto;
      padding: 2rem;
      background: white;
      box-shadow: 0 2px 6px rgba(0,0,0,0.1);
      border-radius: 8px;
    }
    h2 {
      color: #343a40;
    }
    video, img {
      width: 100%;
      border-radius: 6px;
      margin-top: 1rem;
    }
    ul {
      margin-left: 1.5rem;
    }
    footer {
      text-align: center;
      padding: 1rem;
      font-size: 0.9em;
      color: #777;
    }
  </style>
</head>
<body>
  <header>
    <h1>2048</h1>
    <p>Arun Khanijau and Jesse Gomez – Embedded Systems Final Project (EEC172)</p>
  </header>

  <main>
    <h2>Project Demonstration</h2>
    <video controls>
      <source src="Demo1.mp4" type="video/mp4">
      Your browser does not support the video tag.
    </video>
    <p>
      The video above shows the startup sequence and early gameplay of the embedded 2048 system.
      It demonstrates how tiles move and merge in real-time on the OLED display as directional inputs are received.
    </p>

    <h2>Project Description</h2>
    <p>
      This project implements the puzzle game <strong>2048</strong> on a standalone embedded system using the TI CC3200 microcontroller.
      The board is displayed on an Adafruit SSD1351 OLED screen, and inputs are handled through both UART (keyboard) and onboard accelerometer-based tilt gestures.
    </p>
    <ul>
      <li>Real-time gameplay and tile merging logic</li>
      <li>Grid and number rendering using Adafruit GFX library</li>
      <li>Accelerometer-based tilt input with debounce and cooldown</li>
      <li>Post-game stats sent to AWS IoT over HTTPS</li>
    </ul>
    <p>
      A planned feature to dynamically change tile colors based on ambient temperature was not implemented due to hardware constraints.
    </p>

    <h2>Full Game Example</h2>
    <img src="Demo2.gif" alt="Full 2048 gameplay gif" />
    <p>
      This animated GIF shows a full session of the game—from the first moves to the game-over screen.
      It highlights the core gameplay loop and end-of-game score reporting.
    </p>
  </main>

  <footer>
    &copy; 2025 Arun Khanijau • Embedded Systems Final Project
  </footer>
</body>
</html>
