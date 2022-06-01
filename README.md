Yii PHP Framework Version 2 / NOX Behaviors
===========================================

Collection of useful behaviors for Yii Framework 2.0 (at the present there is only one behavior, the `datetime` behavior.).

[![Latest Stable Version](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/v/stable)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![Total Downloads](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/downloads)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![Latest Unstable Version](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/v/unstable)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![License](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/license)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![Monthly Downloads](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/d/monthly)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![Daily Downloads](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/d/daily)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)
[![composer.lock](https://poser.pugx.org/nyx-solutions/yii2-nyx-behaviors/composerlock)](https://packagist.org/packages/nyx-solutions/yii2-nyx-behaviors)

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```bash
php composer.phar require --prefer-dist nyx-solutions/yii2-nyx-behaviors "*"
```

or add

```
"nyx-solutions/yii2-nyx-behaviors": "*"
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
                'class'      => \nyx\behaviors\DateTimeBehavior::className(),
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

**yii2-nyx-behaviors** is released under the BSD 3-Clause License. See the bundled `LICENSE.md` for details.

![Yii2](https://img.shields.io/badge/Powered_by-Yii_Framework-green.svg?style=flat)
