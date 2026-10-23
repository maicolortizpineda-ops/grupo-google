/* ===== CSS ===== */
#cookieBanner {
    align-items: center;
    background-color: rgba(33, 37, 41, .97);
    bottom: 0;
    box-shadow: 0 -4px 16px rgba(0, 0, 0, .25);
    color: #fff;
    display: none;
    flex-wrap: wrap;
    gap: 1rem;
    justify-content: space-between;
    left: 0;
    padding: 1rem 1.75rem;
    position: fixed;
    right: 0;
    z-index: 200;
}
#cookieBanner p {
    flex: 1 1 300px;
    margin: 0;
}
#cookieBanner a {
    color: #ff9b73;
}
#cookieBanner button {
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: .95rem;
    padding: .6rem 1.2rem;
}
#cookieAccept {
    background-color: rgba(221, 72, 20, 1);
    color: #fff;
}
#cookieReject {
    background-color: transparent;
    border: 1px solid #888 !important;
    color: #ddd;
}
<!-- ===== HTML ===== -->
<div id="cookieBanner" role="dialog" aria-label="Aviso de cookies">
    <p>
        Usamos cookies para mejorar tu experiencia.
        <a href="<?= site_url('privacidad') ?>">Más información</a>
    </p>
    <div>
        <button id="cookieReject" type="button">Rechazar</button>
        <button id="cookieAccept" type="button">Aceptar</button>
    </div>
</div>
// ===== JS =====
(function () {
    var banner = document.getElementById('cookieBanner');

    try {
        if (localStorage.getItem('cookieConsent')) return; // ya decidió
    } catch (e) {}

    banner.style.display = 'flex';

    function save(value) {
        try {
            localStorage.setItem('cookieConsent', value);
        } catch (e) {}
        banner.style.display = 'none';
    }

    document.getElementById('cookieAccept').addEventListener('click', function () {
        save('accepted');
        // Aquí puedes cargar Google Analytics u otros scripts
    });
    document.getElementById('cookieReject').addEventListener('click', function () {
        save('rejected');
    });
})();
