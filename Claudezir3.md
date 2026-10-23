/* ===== CSS ===== */
#backToTop {
    background-color: rgba(221, 72, 20, .9);
    border: none;
    border-radius: 50%;
    bottom: 24px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, .25);
    color: #fff;
    cursor: pointer;
    font-size: 1.4rem;
    height: 48px;
    opacity: 0;
    pointer-events: none;
    position: fixed;
    right: 24px;
    transform: translateY(20px);
    transition: opacity .3s ease, transform .3s ease;
    width: 48px;
    z-index: 100;
}
#backToTop.visible {
    opacity: 1;
    pointer-events: auto;
    transform: translateY(0);
}
#backToTop:hover {
    background-color: rgba(221, 72, 20, 1);
}
<!-- ===== HTML ===== -->
<button id="backToTop" aria-label="Volver arriba">&uarr;</button>
// ===== JS =====
(function () {
    var btn = document.getElementById('backToTop');

    window.addEventListener('scroll', function () {
        btn.classList.toggle('visible', window.scrollY > 300);
    }, { passive: true });

    btn.addEventListener('click', function () {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });
})();
