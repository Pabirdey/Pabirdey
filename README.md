title: {
    text: element + " - " + type.replaceAll("_", " "),
    left: 'center',
    textStyle: {
        fontSize: 18,
        fontWeight: 'bold',
        fontFamily: 'Segoe UI',
        color: {
            type: 'linear',
            x: 0, y: 0, x2: 1, y2: 0,
            colorStops: [
                { offset: 0, color: '#007bff' },
                { offset: 1, color: '#00c6ff' }
            ]
        }
    }
},
