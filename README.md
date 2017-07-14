Class qui simplifie l'utilisation de la PDO.

Exemple de Bundle pour Symfony :

```php
<?php
namespace Core\Bundle\BdD;

use Core\Kernel\Bundle\Bundle;

class BdD extends Bundle {
	public function boot($dev = false) { // chargement
		if ($dev) { return $this->bootdev(); }

		$this->class = new \BdD\BdD();
	}

	public function bootdev() {
		$this->class = new \BdD\BdDWithDebugBar();
	}

	public function build() { // connexion
		$h = \Core\Kernel\Kernel::getCore()->getConfigPDO();
		$this->class->connect($h["host"], $h["dbname"], $h["user"], $h["password"]);
	}
}
```

Pour préparer une requête et obtenir directement la variable nombre :

```php
$nbrtag = $BdD->lire("SELECT COUNT(*) as nombre FROM tag WHERE tag = ?", array(4), "nombre");
```

etc...