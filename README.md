Yii PHP Framework Version 2 / NOX Behaviors
===========================================

Collection of useful behaviors for Yii Framework 2.0 (at the present there is only one behavior, the `datetime` behavior.).

[![Latest Stable Version](https://poser.pugx.org/nox-it/yii2-nox-behaviors/v/stable)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![Total Downloads](https://poser.pugx.org/nox-it/yii2-nox-behaviors/downloads)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![Latest Unstable Version](https://poser.pugx.org/nox-it/yii2-nox-behaviors/v/unstable)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![License](https://poser.pugx.org/nox-it/yii2-nox-behaviors/license)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![Monthly Downloads](https://poser.pugx.org/nox-it/yii2-nox-behaviors/d/monthly)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![Daily Downloads](https://poser.pugx.org/nox-it/yii2-nox-behaviors/d/daily)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)
[![composer.lock](https://poser.pugx.org/nox-it/yii2-nox-behaviors/composerlock)](https://packagist.org/packages/nox-it/yii2-nox-behaviors)

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```bash
php composer.phar require --prefer-dist nox-it/yii2-nox-behaviors "*"
```

or add

```
"nox-it/yii2-nox-behaviors": "*"
```

to the require section of your `composer.json` file.

## Usage

In your base ActiveRecord Model you can add the following `behaviors` method:

```php
namespace common\models;

use \yii\helpers\ArrayHelper;

/**
 * Class ActiveRecordModel
 *
 * @package common\models
 */
class ActiveRecordModel extends \yii\db\ActiveRecord
{
    #region Behaviors
    /**
     * @inheritdoc
     */
    public function behaviors()
    {
        $behaviors = [];

        if ($this->hasAttribute('createdAt') && $this->hasAttribute('updatedAt')) {
            $behaviors['datetime'] = [
                'class'      => \nox\behaviors\DateTimeBehavior::className(),
                'attributes' => [
                    ActiveRecord::EVENT_BEFORE_INSERT => ['createdAt', 'updatedAt'],
                    ActiveRecord::EVENT_BEFORE_UPDATE => 'updatedAt'
                ]
            ];
        }
        
        return ArrayHelper::merge(parent::behaviors(), $behaviors);
    }
    #endregion
}
```

## License

**yii2-nox-behaviors** is released under the BSD 3-Clause License. See the bundled `LICENSE.md` for details.

![Yii2](https://img.shields.io/badge/Powered_by-Yii_Framework-green.svg?style=flat)
