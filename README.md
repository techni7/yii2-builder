yii2-builder
============

A form builder extension that allows you to build both single view and multi-view/tabular forms for Yii Framework 2.0. The extension contains these widgets:

## Form

`\kartik\builder\Form`

The Form Builder widget allows you to build a form through a configuration array. Key features available:

- Configure your form fields from a model extending `yii\base\model` or `yii\db\ActiveRecord`.
- Ability to support various Bootstrap 3.x form layouts. Uses the advanced [`kartik\widgets\ActiveForm`](http://demos.krajee.com/widget-details/active-form).
- Use Bootstrap column/builder layout styling by just supplying `columns` property.
- Build complex layouts (for example single, double, or multi columns in the same layout) - by reusing the widget for building your attributes.
- Tweak ActiveForm defaults to control field options, styles, templates, and layouts.
- Various Bootstrap 3.x styling features are available by default. However, one can easily customize and theme it to one's liking using any CSS framework.
- Supports and renders HTML input types (uses [`kartik\widgets\ActiveField`](http://demos.krajee.com/widget-details/active-field)) including input widgets and more:
    - `INPUT_TEXT` or `textInput`
    - `INPUT_TEXTAREA` or `textarea`
    - `INPUT_PASSWORD` or `passwordInput`
    - `INPUT_DROPDOWN_LIST` or `dropdownList`
    - `INPUT_LIST_BOX` or `listBox`
    - `INPUT_CHECKBOX` or `checkbox`
    - `INPUT_RADIO` or `radio`
    - `INPUT_CHECKBOX_LIST` or `checkboxList`
    - `INPUT_RADIO_LIST` or `radioList`
    - `INPUT_MULTISELECT` or `multiselect`
    - `INPUT_STATIC` or `staticInput`
    - `INPUT_FILE` or `fileInput`
    - `INPUT_HTML5` or `input`
    - `INPUT_WIDGET` or `widget`
    - `INPUT_RAW` or `raw` (any free text or html markup)

Refer the [documentation](http://demos.krajee.com/builder-details/form) for more details.

## Tabular Form 

`kartik\builder\TabularForm`

The tabular form allows you to update information from multiple models (typically used in master-detail forms). Key features

- Supports all input types as mentioned in the `Form` builder widget
- The widget works like a Yii GridView and uses an ActiveDataProvider to read the models information. 
- Supports features of the builderview like pagination and sorting.
- Allows you to highlight and select table rows
- Allows you to add and configure action buttons for each row.
- Various Bootstrap 3.x styling features are available by default. However, one can easily customize and theme it to one's liking using any CSS framework.
- Advanced table styling, columns, and layout configuration by using the features available in the [`kartik\builder\GridView`]([`kartik\widgets\ActiveForm`](http://demos.krajee.com/builder) widget.
- One can easily read and manage the tabular input data using the `loadMultiple` and `validateMultiple` functions in `yii\base\Model`.

### Demo
You can see detailed [documentation](http://demos.krajee.com/builder) on usage of the extension.

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
$ php composer.phar require kartik-v/yii2-builder "dev-master"
```

or add

```
"kartik-v/yii2-builder": "dev-master"
```

to the ```require``` section of your `composer.json` file.

## Usage

### Form
```php
use kartik\builder\Form;
$form = ActiveForm::begin();
echo Form::widget([
    'model' => $model,
    'form' => $form,
    'columns' => 2,
    'attributes' => [
        'username' => ['type'=>Form::INPUT_TEXT, 'options'=>['placeholder'=>'Enter username...']],
        'password' => ['type'=>Form::INPUT_PASSWORD, 'options'=>['placeholder'=>'Enter password...']],
        'rememberMe' => ['type'=>Form::INPUT_CHECKBOX],
    ]
]);
ActiveForm::end();
```

### TabularForm
```php
use kartik\builder\TabularForm;
$form = ActiveForm::begin();
$form = ActiveForm::begin();
echo TabularForm::widget([
    'form' => $form,
    'dataProvider' => $dataProvider,
    'attributes' => [
        'id' => ['type' => TabularForm::INPUT_STATIC, 'columnOptions'=>['hAlign'=>GridView::ALIGN_CENTER]],
        'name' => ['type' => TabularForm::INPUT_TEXT],
        'color' => [
            'type' => TabularForm::INPUT_WIDGET, 
            'widgetClass' => \kartik\widgets\ColorInput::classname()
        ],
        'author_id' => [
            'type' => TabularForm::INPUT_DROPDOWN_LIST, 
            'items'=>ArrayHelper::map(Author::find()->orderBy('name')->asArray()->all(), 'id', 'name')
        ],
        'buy_amount' => [
            'type' => TabularForm::INPUT_TEXT, 
            'options'=>['class'=>'form-control text-right'], 
            'columnOptions'=>['hAlign'=>GridView::ALIGN_RIGHT]
        ],
        'sell_amount' => [
            'type' => TabularForm::INPUT_STATIC, 
            'columnOptions'=>['hAlign'=>GridView::ALIGN_RIGHT]
        ],
    ],
    'gridSettings' => [
        'floatHeader' => true,
        'panel' => [
            'heading' => '<h3 class="panel-title"><i class="glyphicon glyphicon-book"></i> Manage Books</h3>',
            'type' => GridView::TYPE_PRIMARY,
            'after'=> 
                Html::a(
                    '<i class="glyphicon glyphicon-plus"></i> Add New', 
                    $createUrl, 
                    ['class'=>'btn btn-success']
                ) . '&nbsp;' . 
                Html::a(
                    '<i class="glyphicon glyphicon-remove"></i> Delete', 
                    $deleteUrl, 
                    ['class'=>'btn btn-danger']
                ) . '&nbsp;' .
                Html::submitButton(
                    '<i class="glyphicon glyphicon-floppy-disk"></i> Save', 
                    ['class'=>'btn btn-primary']
                )
        ]
    ]     
]); 
ActiveForm::end(); 
```

## License

**yii2-builder** is released under the BSD 3-Clause License. See the bundled `LICENSE.md` for details.
