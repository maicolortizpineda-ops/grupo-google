/* ===== CSS ===== */
.cards {
    display: grid;
    gap: 1.5rem;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
}
.card {
    background-color: var(--bg, #fff);
    border: 1px solid rgba(221, 72, 20, .15);
    border-radius: 12px;
    padding: 1.5rem;
    transition: transform .25s ease, box-shadow .25s ease, border-color .25s ease;
}
.card:hover {
    border-color: rgba(221, 72, 20, .6);
    box-shadow: 0 10px 25px rgba(221, 72, 20, .15);
    transform: translateY(-6px);
}
.card h2 {
    align-items: center;
    display: flex;
    margin: 0 0 .75rem;
    padding-top: 0;
}
.card p {
    color: inherit;
    line-height: 1.6;
    margin: 0 0 1rem;
    opacity: .85;
}
.card .card-link {
    font-weight: 600;
    text-decoration: none;
}
.card .card-link::after {
    content: ' →';
    transition: margin-left .2s ease;
}
.card .card-link:hover::after {
    margin-left: 6px;
}
<!-- ===== HTML: dentro de <section> en .further ===== -->
<h1>Go further</h1>

<div class="cards">
    <article class="card">
        <h2>Learn</h2>
        <p>The User Guide contains an introduction, tutorial and reference documentation.</p>
        <a class="card-link" href="https://codeigniter.com/user_guide/" target="_blank" rel="noopener">User Guide</a>
    </article>

    <article class="card">
        <h2>Discuss</h2>
        <p>Join the community, share ideas and solve problems together.</p>
        <a class="card-link" href="https://forum.codeigniter.com/" target="_blank" rel="noopener">Forum</a>
    </article>

    <article class="card">
        <h2>Contribute</h2>
        <p>CodeIgniter is community driven. Your code and docs are welcome.</p>
        <a class="card-link" href="https://codeigniter.com/contribute" target="_blank" rel="noopener">Join us</a>
    </article>
</div>
