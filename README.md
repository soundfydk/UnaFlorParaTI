# UnaFlorParaTI
function dibujarHoja(x, y, angulo, escalaHoja, progreso, direccion) {

    if (progreso <= 0) return;

    const largo = 2.2 * escalaHoja;
    const ancho = 0.7 * escalaHoja;

    const largoActual = largo * progreso;
    const anchoActual = ancho * progreso;

    const px = pantallaX(x);
    const py = pantallaY(y);

    ctx.save();

    ctx.translate(px, py);

    // Rotación de la hoja
    ctx.rotate(angulo);

    // Dirección izquierda/derecha
    ctx.scale(direccion, 1);

    ctx.beginPath();

    // Base de la hoja
    ctx.moveTo(0, 0);

    // Parte izquierda de la hoja
    ctx.bezierCurveTo(
        -anchoActual * escala,
        -largoActual * 0.35 * escala,
        -anchoActual * escala,
        -largoActual * 0.75 * escala,
        0,
        -largoActual * escala
    );

    // Parte derecha de la hoja
    ctx.bezierCurveTo(
        anchoActual * escala,
        -largoActual * 0.75 * escala,
        anchoActual * escala,
        -largoActual * 0.35 * escala,
        0,
        0
    );

    ctx.closePath();

    // Degradado
    const gradiente = ctx.createLinearGradient(
        0,
        0,
        0,
        -largo * escala
    );

    gradiente.addColorStop(0, "#14532D");
    gradiente.addColorStop(0.45, "#228B22");
    gradiente.addColorStop(1, "#7CFC90");

    ctx.fillStyle = gradiente;
    ctx.strokeStyle = "#7CFC90";
    ctx.lineWidth = 2;

    ctx.fill();
    ctx.stroke();

    // Nervadura central
    ctx.beginPath();

    ctx.moveTo(0, 0);

    ctx.lineTo(
        0,
        -largoActual * 0.9 * escala
    );

    ctx.strokeStyle = "#B7F7A8";
    ctx.lineWidth = 1;

    ctx.stroke();

    ctx.restore();
}
