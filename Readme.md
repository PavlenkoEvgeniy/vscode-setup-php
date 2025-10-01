# Visual Studio Code for PHP developers
## Extensions (расширения):
1. bmewburn.vscode-intelephense-client
2. DEVSENSE.composer-php-vscode
3. DEVSENSE.intelli-php-vscode
4. DEVSENSE.phptools-vscode
5. ecmel.vscode-html-css
6. junstyle.php-cs-fixer
7. mblode.twig-language-2
8. mechatroner.rainbow-csv
9. MehediDracula.php-namespace-resolver
10. mikestead.dotenv
11. ms-vscode-remote.remote-ssh
12. redhat.vscode-yaml
13. rexshi.phpdoc-comment-vscode-plugin
14. TheNouillet.symfony-vscode
15. timonwong.shellcheck
16. whatwedo.twig
17. streetsidesoftware.code-spell-checker
18. streetsidesoftware.code-spell-checker-russian
19. EditorConfig.EditorConfig
20. mhutchie.git-graph
21. PKief.material-icon-theme
22. ctf0.vscode-php-getters-setters-new
23. alefragnani.project-manager
24. ericgomez.phpstorm-theme
25. ericgomez.php-string-syntax
26. ericgomez.php-debug-inline
27. download from google fonts: JetBrains Mono

## php-cs-fixer linter

1. Перейти в корень пользователя:
```bash
cd ~
```
2. Создать директорию tools:
```bash
mkdir tools
```
3. Создать в ней файл .php-cs-fixer.php с содержимым:
```php
<?php

declare(strict_types=1);

use PhpCsFixer\Finder;
use PhpCsFixer\Config;

return (new Config())
    ->setRules([
        '@Symfony' => true,
        'declare_strict_types' => true,
        'concat_space' => [
            'spacing' => 'one',
        ],
        'binary_operator_spaces' => [
            'operators' => [
                '=>' => 'align',
                '='  => 'align',
            ],
        ],
        'phpdoc_to_comment' => false,
    ])
    ->setFinder(
        (new Finder())
            ->in(['src', 'tests', 'migrations'])
            ->exclude(['vendor'])
    )
    ->setLineEnding("\n")
;
```

4. Создать директорию tools/php-cs-fixer
```bash
mkdir tools/php-cs-fixer
```
5. Перейти в неё:
```bash
cd tools/php-cs-fixer
```
6. Создать в ней файл composer.json:
```json
{
    "require-dev": {
        "friendsofphp/php-cs-fixer": "^3.57" 
    }
}
```
7. Далее притащить composer.phar:
```bash
php -r "readfile('https://getcomposer.org/installer');" | php
```
8. Запустить:
```bash
php composer.phar install
php composer.phar update
```
9. Теперь у вас есть настроенный php-cs-fixer.

Необходимо настроить visual studio code.

Считаем что расширение junstyle.php-cs-fixer вы уже поставили.

Переходим в его настройки и настраиваем:

PHP-cs-fixer: Allow Risky
Да

PHP-cs-fixer: Config:

~/tools/.php-cs-fixer.php

PHP-cs-fixer: Executable Path

~/tools/php-cs-fixer/vendor/bin/php-cs-fixer

Если всё прошло удачно, в панели Explorer при нажатии на директорию или файл будет выводиться два или один новый пункт:

    php-cs-fixer: fix
    php-cs-fixer: diff

fix -- фиксит  
diff -- показывает что будет фиксить.
