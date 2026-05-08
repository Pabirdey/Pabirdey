body {
    /* Full screen overlay */
        .loader-container{
            position: fixed;
            top: 0;
            left: 0;

            width: 100%;
            height: 100vh;

            display: flex;
            justify-content: center;
            align-items: center;

            background: rgba(255,255,255,0.7);

            z-index: 9999;
        }

        /* Loader */
        .loader {
    --d: 22px;
    width: 4px; /* The center point */
    aspect-ratio: 1; /* Ensures a square box for rotation */
    border-radius: 50%;
    color: #25b09b;

    box-shadow:
        calc(1*var(--d))      calc(0*var(--d))      0 0,
        calc(0.707*var(--d))  calc(0.707*var(--d)) 0 1px,
        calc(0*var(--d))      calc(1*var(--d))      0 2px,
        calc(-0.707*var(--d)) calc(0.707*var(--d)) 0 3px,
        calc(-1*var(--d))     calc(0*var(--d))      0 4px,
        calc(-0.707*var(--d)) calc(-0.707*var(--d)) 0 5px,
        calc(0*var(--d))      calc(-1*var(--d))     0 6px;

    /* The animation now rotates the entire coordinate system of the shadows */
    animation: l27 1s infinite steps(8);
}

@keyframes l27 {
    100% {
        transform: rotate(1turn);
    }
}

}
