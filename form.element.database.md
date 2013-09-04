# Swis_Form_Element_Database

Er zijn 3 nieuwe form elements toegevoegd, op basis van Zend_Form_Element:

* Swis_Form_Element_DatabaseSelect
* Swis_Form_Element_DatabaseCheckbox
* Swis_Form_Element_DatabaseMultiselect

Deze elementen overerven de oorspronkelijke elements, zoals Zend_Form_Element_Select. 

## Configuratie
De database elementen hebben allemaal dezelfde configuratie opties:

```php
$oElement = new Swis_Form_DatabaseSelect('categories', array(
    'table'   => 'categories',
    'field'   => 'title', // wordt weergegeven in de select lijst
    'key'     => 'id', // de column die als value gebruikt wordt,
    'empty'   => '--- kies een categorie ---' // wordt toegevoegd als eerste lege optie
    'before'  => function($q) {
        
        // Je kunt hier de Zend_Db_Query nog aanpassen
        $q->orderBy('title');
    }
));
```

In de configuratie staat de 'field' standaard op 'titel' en de 'key' standaard op 'id'. 
Meestal zul je dus deze opties niet te hoeven aanpassen.

## Voorbeeld in [Swis_Form] (form.md)
```php
class ContactFormulier extends Swis_Form
{
    public function init()
    {
        // Onderwerp
        $this->addElement(new Swis_Form_Element_DatabaseSelect('onderwerp_id', array(
            'table' => 'contact_onderwerpen',
            'required' => true,
        );
        
        // Rest van de formuliervelden
    }
}
```



