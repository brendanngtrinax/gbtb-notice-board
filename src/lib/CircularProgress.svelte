<svg viewBox="0 0 250 250" class="circular-progress w-20">
  <circle class="bg"></circle>
  <circle class="fg"></circle>
</svg>

<style>
  .circular-progress {
    --size: 250px;
    --half-size: calc(var(--size) / 2);
    --stroke-width: 20px;
    --radius: calc((var(--size) - var(--stroke-width)) / 4);
    --circumference: calc(var(--radius) * pi * 2);
    --dash: calc((var(--progress) * var(--circumference)) / 100);
    animation: progress-animation 30s linear infinite;
  }
  .circular-progress circle {
    cx: var(--half-size);
    cy: var(--half-size);
    r: var(--radius);
    stroke-width: var(--stroke-width);
    fill: none;
    stroke-linecap: round;
  }
  .circular-progress circle.bg {
    stroke: #ddd;
  }
  .circular-progress circle.fg {
    transform: rotate(-90deg);
    transform-origin: var(--half-size) var(--half-size);
    stroke-dasharray: var(--dash) calc(var(--circumference) - var(--dash));
    transition: stroke-dasharray 0.3s linear 0s;
    stroke: black;
  }
  @property --progress {
    syntax: "<number>";
    inherits: false;
    initial-value: 0;
  }
  @keyframes progress-animation {
    0% {
      --progress: 0;
    }
    95% {
      --progress: 100;
    }
    100% {
      --progress: 0;
    }
  }
</style>
