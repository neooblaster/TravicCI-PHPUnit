# 1. Initialisation Git

```bash
git init .
git remote add gh git@github.com:/neooblaster/TravicCI-PHPUnit.git
git add README.md
git commit -m "Initialisation du repository"
git push -u gh master
```

# 2. S'inscrire et se connecter sur Travis CI

Si ce n'est pas déjà fais, créez un compte sur l'application Travis CI : https://travis-ci.org
puis authentifier-vous.


# 3. Initialiser le repository pour Travis CI

Pour intialiser le repository, sur le site, dans le volet de gauche listant les repositories actifs, cliquez sur "+" à droite de "My Repositories". Cherchez votre repository, activez-le à l'aide du bouton "on-off", puis cliquez sur la roue crantée pour accéder aux options. 

`Si votre repository n'apparait, pas cliquer sur 'Sync account'`

Dans la page des options, activez l'option `Build only if .travis.yml is present`


# 4. Préparation pour le premier build

D'abord, il faut créer le fichier `.travis.yml` qui permet de configurer le cycle de construction (Build LifeCycle)

Celui-ci devra contenir au minimum :
* Le langage qui doit être testé
* Pour ce langage, les versions/moteurs à tester
* Par anticipation, spécifier la commande qui va jouer les tests unitaire

##### Fichier `travis`:

```yaml
language: php

php:
    - 5.5
    - 5.6
    - 7.0
    - 7.1
    - hhvm
    
 script:
    - phpunit your_php_test_file.php
```

Ayant spécifié un fichier PHP contenant nos tests, il va falloir également le créer

##### Fichier `your_php_test_file.php`

Voici le code fournis par la documentation de PHPUnit

```php
<?php
use PHPUnit\Framework\TestCase;

class StackTest extends TestCase
{
    public function testPushAndPop()
    {
        $stack = [];
        $this->assertEquals(0, count($stack));

        array_push($stack, 'foo');
        $this->assertEquals('foo', $stack[count($stack)-1]);
        $this->assertEquals(1, count($stack));

        $this->assertEquals('foo', array_pop($stack));
        $this->assertEquals(0, count($stack));
    }
}
?>
```

Il ne restera plus qu'à faire votre commit et votre push vers GitHub.
Dès lors, sur Travis CI, le fichier `your_php_test_file.php` sera testé sur l'ensemble des versions spécifiées dans le fichier `.travis.yml` : 5.5, 5.6, 7.0, 7.1 et hhvm




