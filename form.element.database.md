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

    // Kies de database tabel
    'table' => 'categories',
    
    // De column die wordt weergegeven in de select lijst
    // Dit staat standaard al op 'titel'.
    'field' => 'title', 
    
    // De column die als value gebruikt wordt.
    // Dit staat standaard al op 'id'.
    'key' => 'id', 
    
    // Dit wordt toegevoegd als eerste lege optie
    'empty' => '--- kies een categorie ---' 
    
    // Je kunt hier de Zend_Db_Query nog aanpassen
    'before' => function($q) {
        $q->orderBy('title');
    }
));
```

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



