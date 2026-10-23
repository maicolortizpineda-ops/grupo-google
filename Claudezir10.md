<?php
// ===== app/Controllers/Home.php =====
namespace App\Controllers;

class Home extends BaseController
{
    public function __construct()
    {
        // Necesario para usar url_is(), site_url(), etc.
        helper('url');
    }

    public function index(): string
    {
        return view('welcome_message');
    }

    public function about(): string
    {
        return view('about');
    }
}
<?php
// ===== app/Config/Routes.php =====
$routes->get('/', 'Home::index');
$routes->get('about', 'Home::about');
$routes->get('contact', 'Contact::index');
<!-- ===== Menú en la vista: reemplaza los <li class="menu-item"> ===== -->
<li class="menu-item hidden">
    <a href="<?= site_url('/') ?>"
       class="<?= url_is('/') ? 'active' : '' ?>"
       <?= url_is('/') ? 'aria-current="page"' : '' ?>>Home</a>
</li>
<li class="menu-item hidden">
    <a href="<?= site_url('about') ?>"
       class="<?= url_is('about*') ? 'active' : '' ?>"
       <?= url_is('about*') ? 'aria-current="page"' : '' ?>>About</a>
</li>
<li class="menu-item hidden">
    <a href="<?= site_url('contact') ?>"
       class="<?= url_is('contact*') ? 'active' : '' ?>"
       <?= url_is('contact*') ? 'aria-current="page"' : '' ?>>Contact</a>
</li>
<li class="menu-item hidden">
    <a href="https://codeigniter.com/user_guide/" target="_blank" rel="noopener">Docs</a>
</li>
/* ===== CSS ===== */
header li.menu-item a.active {
    background-color: rgba(221, 72, 20, .15);
    color: rgba(221, 72, 20, 1);
    font-weight: 600;
}
header li.menu-item a.active::after {
    background-color: rgba(221, 72, 20, 1);
    border-radius: 2px;
    content: '';
    display: block;
    height: 3px;
    margin-top: -6px;
}
