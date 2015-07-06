Использование шаблонизаторов
======================

По умолчанию в Yii используется PHP в качестве шаблонизатора, однако возможно настроить Yii для поддержки других шаблонизаторов, например, [Twig](http://twig.sensiolabs.org/) или [Smarty](http://www.smarty.net/), которые доступны в качестве расширений.

By default, Yii uses PHP as its template language, but you can configure Yii to support other rendering engines, such as [Twig](http://twig.sensiolabs.org/) or [Smarty](http://www.smarty.net/) available as extensions.

За рендеринг видов отвечает компонент `view`. Собственный шаблонизатор можно добавить внеся изменения в настройки поведения компонента.

The `view` component is responsible for rendering views. You can add a custom template engine by reconfiguring this
component's behavior:

```php
[
    'components' => [
        'view' => [
            'class' => 'yii\web\View',
            'renderers' => [
                'tpl' => [
                    'class' => 'yii\smarty\ViewRenderer',
                    //'cachePath' => '@runtime/Smarty/cache',
                ],
                'twig' => [
                    'class' => 'yii\twig\ViewRenderer',
                    'cachePath' => '@runtime/Twig/cache',
                    // Настройки Twig:
                    'options' => [
                        'auto_reload' => true,
                    ],
                    'globals' => ['html' => '\yii\helpers\Html'],
                    'uses' => ['yii\bootstrap'],
                ],
                // ...
            ],
        ],
    ],
]
```

В приведённом примере Smarty и Twig настроены для использования в файлах вида.

In the code above, both Smarty and Twig are configured to be useable by the view files. But in order to get these extensions into your project, you need to also modify your `composer.json` file to include them, too:

```
"yiisoft/yii2-smarty": "*",
"yiisoft/yii2-twig": "*",
```
That code would be added to the `require` section of `composer.json`. After making that change and saving the file, you can install the extensions by running `composer update --prefer-dist` in the command-line.

For details about using concrete template engine please refer to its documentation:

- [Twig guide](https://github.com/yiisoft/yii2-twig/tree/master/docs/guide)
- [Smarty guide](https://github.com/yiisoft/yii2-smarty/tree/master/docs/guide)
