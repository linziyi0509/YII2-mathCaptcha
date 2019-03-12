# YII2-mathCaptcha

直接安装
```
php composer.phar require --prefer-dist math/MathCaptcha "*"
```

扩展用于composer.json中
```
"math/MathCaptcha": "*"
```

download之后进行安装
1.下载
2.将文件放在vendor下
3.配置autoload_psr4.php中的路由
```
'math\\MathCaptcha\\' => array($vendorDir . '/customcaptcha/mathcaptcha'),//算法验证码
```
4.在应用处引用即可

```php
use yii\web\Controller;

class SiteController extends Controller
{
    public function actions()
    {
        return [
            ...
            'captcha' => [
                'class' => 'math\MathCaptcha\MathCaptchaAction',
                'fixedVerifyCode' => YII_ENV_TEST ? '42' : null,
                'height' => 34,
                'width' => 120,
            ],
        ];
    }
}

```



```php

<?php $form = ActiveForm::begin([]); ?>

....

<?= $form->field($model,'CAPTCHA',['enableAjaxValidation'=>true,'enableClientValidation' => false,])
->widget(Captcha::className(),
[
	'captchaAction'=>'signup/captcha',
	'options' => ['class' => 'form-control'],
	'template'=>'<p style="float:left">{input}</p> {image} ',
	'imageOptions'=>['alt'=>Yii::t('app','点击换图'),'title'=>Yii::t('app','点击换图'), 'style'=>'cursor:pointer']
]); 
?>

....

<?php ActiveForm::end(); ?>

```