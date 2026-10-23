/* ===== CSS ===== */
section pre {
    position: relative;
}
.copy-btn {
    background-color: rgba(221, 72, 20, .85);
    border: none;
    border-radius: 4px;
    color: #fff;
    cursor: pointer;
    font-size: .75rem;
    padding: .3rem .6rem;
    position: absolute;
    right: 8px;
    top: 8px;
}
.copy-btn:hover {
    background-color: rgba(221, 72, 20, 1);
}
.copy-btn.copied {
    background-color: #2e9e5b;
}
// ===== JS =====
(function () {
    document.querySelectorAll('section pre').forEach(function (pre) {
        var btn = document.createElement('button');
        btn.className = 'copy-btn';
        btn.type = 'button';
        btn.textContent = 'Copiar';
        pre.appendChild(btn);

        btn.addEventListener('click', function () {
            var code = pre.querySelector('code').innerText.trim();

            function done() {
                btn.textContent = '¡Copiado!';
                btn.classList.add('copied');
                setTimeout(function () {
                    btn.textContent = 'Copiar';
                    btn.classList.remove('copied');
                }, 1800);
            }

            if (navigator.clipboard) {
                navigator.clipboard.writeText(code).then(done);
            } else {
                // Respaldo para navegadores antiguos
                var area = document.createElement('textarea');
                area.value = code;
                document.body.appendChild(area);
                area.select();
                document.execCommand('copy');
                document.body.removeChild(area);
                done();
            }
        });
    });
})();
