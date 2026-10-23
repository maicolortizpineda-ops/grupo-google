<?php
// ===== app/Controllers/Home.php =====
namespace App\Controllers;

class Home extends BaseController
{
    public function index(): string
    {
        $data = [
            'title'    => 'Welcome to CodeIgniter ' . \CodeIgniter\CodeIgniter::CI_VERSION,
            'subtitle' => 'The small framework with powerful features',
            'year'     => date('Y'),
            'sections' => [
                [
                    'title' => 'Learn',
                    'text'  => 'The User Guide contains an introduction, tutorial and reference.',
                    'label' => 'User Guide',
                    'url'   => 'https://codeigniter.com/user_guide/',
                ],
                [
                    'title' => 'Discuss',
                    'text'  => 'Join the community and exchange ideas with other developers.',
                    'label' => "CodeIgniter's forum",
                    'url'   => 'https://forum.codeigniter.com/',
                ],
                [
                    'title' => 'Contribute',
                    'text'  => 'CodeIgniter accepts contributions of code and documentation.',
                    'label' => 'Join us',
                    'url'   => 'https://codeigniter.com/contribute',
                ],
            ],
        ];

        return view('welcome_message', $data);
    }
}
<!-- ===== app/Views/welcome_message.php ===== -->

<!-- Título dinámico en el hero -->
<h1><?= esc($title) ?></h1>
<h2><?= esc($subtitle) ?></h2>

<!-- Bloque "Go further" generado con un foreach -->
<div class="further">
    <section>
        <h1>Go further</h1>

        <?php foreach ($sections as $item): ?>
            <h2><?= esc($item['title']) ?></h2>
            <p>
                <?= esc($item['text']) ?>
                <a href="<?= esc($item['url'], 'attr') ?>" target="_blank" rel="noopener">
                    <?= esc($item['label']) ?>
                </a>
            </p>
        <?php endforeach; ?>

    </section>
</div>

<!-- Año dinámico en el footer -->
<p>&copy; <?= esc($year) ?> CodeIgniter Foundation.</p>
