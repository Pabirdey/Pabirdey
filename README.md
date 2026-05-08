<!DOCTYPE html>
<html>
<head>
    <title>Center Loader</title>

    <style>

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
            --d:22px;
            width: 4px;
            height: 4px;
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

            animation: l27 1s infinite steps(8);
        }

        @keyframes l27 {
            100% {
                transform: rotate(1turn);
            }
        }

    </style>
</head>

<body>

    <!-- Loader -->
    <div class="loader-container" id="loaderDiv">
        <div class="loader"></div>
    </div>

    <!-- Your Page Content -->
    <h1 style="text-align:center; margin-top:100px;">
        Furnace High Line Log Sheet
    </h1>

</body>
</html>