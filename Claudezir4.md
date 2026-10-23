/* ===== CSS ===== */
.reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity .7s ease, transform .7s ease;
}
.reveal.in-view {
    opacity: 1;
    transform: translateY(0);
}
.reveal:nth-child(2) { transition-delay: .1s; }
.reveal:nth-child(3) { transition-delay: .2s; }
.reveal:nth-child(4) { transition-delay: .3s; }

@media (prefers-reduced-motion: reduce) {
    .reveal {
        opacity: 1;
        transform: none;
        transition: none;
    }
}
<!-- ===== HTML: agrega la clase "reveal" a lo que quieras animar ===== -->
<section class="reveal">
    <h1>About this page</h1>
    ...
</section>

<p class="reveal">The User Guide contains an introduction...</p>
// ===== JS =====
(function () {
    var elements = document.querySelectorAll('.reveal');

    if (!('IntersectionObserver' in window)) {
        elements.forEach(function (el) {
            el.classList.add('in-view');
        });
        return;
    }

    var observer = new IntersectionObserver(function (entries) {
        entries.forEach(function (entry) {
            if (entry.isIntersecting) {
                entry.target.classList.add('in-view');
                observer.unobserve(entry.target); // solo una vez
            }
        });
    }, { threshold: 0.15 });

    elements.forEach(function (el) {
        observer.observe(el);
    });
})();
