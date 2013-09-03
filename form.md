# Swis_Form

Standaard gebruikt Swis_Form de Zend_Form_Decorators. Niet echt de meest makkelijke manier om een formulier weer te geven. 
De nieuwe Swis_Form_Renderer moet het leven een stuk makkelijker maken voor de developer.

### Een snel voorbeeld
Plaats deze code in een Swis controller.
```php
public function indexAction() {

    $oForm = new Swis_Form
    $oForm->addElement(new Zend_Form_Element_Text(array(
      'label' => 'Titel',
      'mask' => 'default',
    ));

    $this->view->assign('oForm', $oForm);
  
    // Render template
    $this->render($this->_getParam('template') . '/' . $this->_getParam('block'), $this->_getParam('block'));
}
```

Plaats de volgende code in de view
```php
{$oForm}
```

Dit is genoeg om een Swis_Form te renderen in een view zonder dat er vieze decorators gebruikt worden.

## Masks
Het handige van FormHandler zijn voornamelijk de masks. 
Je kunt kleine stukjes html aan de formulierelementen koppelen.
Deze handigheid zit dus nu ook in de Swis_Form

Om een mask te gebruiken hoef je alleen maar de volgende regel aan de element opties mee te geven.
```php
array(
    'mask' => 'default'
)
```

Om een andere mask dan de 'default' te gebruiken doe je het volgende. 
In de Swis_Form voeg je een mask toe:
```php
$oForm->setMask('titel', '<div class="titel">{element}</div>');
```

Je kunt ook direct een custom mask meegeven als optie:
```php
array(
    'mask' => '<div class="inputContainer">{label}{element}{error}</div>' 
)
```
