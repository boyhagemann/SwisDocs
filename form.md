# Swis_Form

Standaard gebruikt Swis_Form de Zend_Form_Decorators. Niet echt de meest makkelijke manier om een formulier weer te geven. 
De nieuwe Swis_Form_Renderer moet het leven een stuk makkelijker maken voor de developer.

## Voor de ongeduldige developer...
Een snel voorbeeld. 
Plaats deze code in een Swis controller.
```php
public function indexAction() {

    $oForm = new Swis_Form();
    $oForm->addElement(new Zend_Form_Element_Text(array(
      'label' => 'Titel',
      'mask' => 'default',
    )));

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
$oElement = new Zend_Form_Element_Text('title', array(
    'mask' => 'default'
));
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

Mocht je niet elke keer een 'default' willen toevoegen in de element opties, dan kun je op deze manier
altijd een default mask gebruiken
```php
$oForm->forceMask();
```

## Tokens
Zoals je hebt kunnen zien in de mask zijn er stukken tekst die vervangen moeten worden met daadwerkelijke code, 
zoals bijvoorbeeld {element}. 
Dit wordt in Swis_Form een token genoemd.
Er zijn al standaard tokens beschikbaar die gebruikt kunnen worden, zoals {label}, {element}, {error}.

### Zelf tokens toevoegen
Soms is het handig om eigen tokens toe te voegen of een bestaande token aan te passen.
Dit is een voorbeeld hoe je een eigen token toevoegt en in de code gebruikt:
```php
// Voeg een token toe
$oForm->replace('title', function($element) {
    // Doe hier iets leuks en return een titel
    return 'Een titel';
});

// Gebruik deze token in een mask
$oForm->setMask('default', '<div class="inputContainer element-{title}">{label}{element}{error}</div>');
```

### Pas een bestaande token aan
Dit kan een standaard variabele zijn, maar ook een closure of een class van een Zend_Decorator.
```php
$oForm->replace('label', 'Standaard label');
$oForm->replace('label', 'My_Form_Decorator_Label');
$oForm->replace('label', function($element) {
    return $element->getLabel() . ':';
});
$oForm->replace('label', function() {
	$label = new Zend_Form_Decorator_Label();
	$label->setOption('escape', false); // je kunt nu html code in een label zetten...
	return $label;
});
```
