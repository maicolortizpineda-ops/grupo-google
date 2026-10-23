<!-- ===== HTML: reemplaza el botón del menú ===== -->
<li class="menu-toggle">
    <button id="menuToggle"
            aria-label="Abrir menú"
            aria-expanded="false"
            aria-controls="mainMenu">&#9776;</button>
</li>
// ===== JS: reemplaza tu script actual =====
(function () {
    var toggle = document.getElementById('menuToggle');
    var items = document.getElementsByClassName('menu-item');

    function setMenu(open) {
        for (var i = 0; i < items.length; i++) {
            items[i].classList.toggle('hidden', !open);
        }
        toggle.setAttribute('aria-expanded', String(open));
        toggle.setAttribute('aria-label', open ? 'Cerrar menú' : 'Abrir menú');
        toggle.innerHTML = open ? '&times;' : '&#9776;';
    }

    function isOpen() {
        return toggle.getAttribute('aria-expanded') === 'true';
    }

    toggle.addEventListener('click', function (e) {
        e.stopPropagation();
        setMenu(!isOpen());
    });

    // Cerrar con Escape
    document.addEventListener('keydown', function (e) {
        if (e.key === 'Escape' && isOpen()) {
            setMenu(false);
            toggle.focus();
        }
    });

    // Cerrar al tocar fuera del menú
    document.addEventListener('click', function (e) {
        if (isOpen() && !e.target.closest('.menu')) {
            setMenu(false);
        }
    });

    // Al agrandar la pantalla, mostrar el menú normal
    window.addEventListener('resize', function () {
        if (window.innerWidth > 629) {
            for (var i = 0; i < items.length; i++) {
                items[i].classList.remove('hidden');
            }
            toggle.setAttribute('aria-expanded', 'false');
        }
    });
})();
