# Banzilla SDK for PHP

#Cargo directo con Tarjetas

Integracion a la API de Banzilla version 1.0 a traves del lenguaje PHP, para ello es necesarion contar con la libreria curl.
Para hacer un cargo directo con tarjeta, primero hay que instanciar la clase banzilla:

```php
$banzilla = Banzilla::getInstance('ID-COMERCIO', 'API-KEY');
```

El siguiente paso es injectar os parametros al metodo de cargo con tarjeta:

```php
$chargeCard = $banzilla->charges->create($chargeData);
```

Para ello previamente el sistema deve tener los datos en una arreglo que en el ejemplo anterior nombramos $chargeData dichos datos algunos vienen de formulario otros de base de datos
```php
$chargeData = array(
                 "Method" => "card",
                 "Card"=> array (
                        "HolderName"   =>  "Nombre Completo",
                        "CardNumber"   => "4426175029604087",
                        "SecurityCode" => "562",
                        "ExpMonth"     => "03",
                        "ExpYear"      => "19",
                        "Address" => array(
                                    "Street"  => "Sócrates",
                                    "Number"  => "130",
                                    "City"    => "Ciudad de México",
                                    "State"   => "CX",
                                    "Country" => "MEX",
                                    "ZipCode" => "11550"
                                    )
                        ),
                "Order"=> array(
                        "Reference" => "102580",
                        "Amount"    => 20.50,
                        "Currency"  => "MXN"
                        ),
                "Customer"=> array (
                        "FirstName"  => "Nombre",
                        "MiddleName" => "Apellido Paterno",
                        "LastName"   => "Apellido Materno",
                        "Email"      => "mail@midominio.com",
                        "Address"    => array (
                                    "Street" => "Sócrates",
                                    "Number" => "130",
                                    "City"   => "Ciudad de México",
                                    "State"  => "CX",
                                    "Country"=> "MEX",
                                    "ZipCode"=> "11550"
                                    )
                        )
            );
```
El ejemplo de como procesar la respuesta de la API aeria:

```php
$responseCard = array(
                    'id_transaction' => $chargeCard->idtransaction,
                    'date_creation' => $chargeCard->creationdate,
                    'id_request' => $chargeCard->idrequest,
                    'method' => $chargeCard->method,
                    'gateway' => $chargeCard->gateway,
                    'Status' => $chargeCard->status,
                    'card_payment' => $chargeCard->cardpayment,
                    'order' => $chargeCard->order,
                    'customer' => $chargeCard->customer
                    
                );
```
#Solicitud de cargo en tiendas OXXO

Para un cargo directo en tiendas OXXO, de igual modo tomamos la instancia de la clase Banzilla e inyectamos los parametros correspondientes al metodo de cargo en tiendas:
```php
$ChargeOxxo = $banzilla->charges->create($oxxoData);
```
estos parametros tambien provienen de la base algunos y otros del formulario de pago

```php
$oxxoData = array(
                "Method" => "store",
                "DueDate" => "11/04/2016",
                "Order"=> array(
                        "Reference" => "247",
                        "Amount"    => 20.00,
                        "Currency"  => "MXN"
                        ),
                "Customer"=> array (
                        "FirstName"  => "Nombre",
                        "MiddleName" => "Apellido Paterno",
                        "LastName"   => "Apellido Materno",
                        "Email"      => "mail@midominio.com",
                        "Address"    => array (
                                    "Street" => "Sócrates",
                                    "Number" => "130",
                                    "City"   => "Ciudad de México",
                                    "State"  => "CX",
                                    "Country"=> "MEX",
                                    "ZipCode"=> "11550"
                                    )
                        )
            );
```

El ejemplo para guardar la respuesta de la API es la siguiente:

```php
$responseOxxo = array(
                    'id_transaction' => $ChargeOxxo->idtransaction,
                    'date_creation' => $ChargeOxxo->creationdate,
                    'id_request' => $ChargeOxxo->idrequest,
                    'method' => $ChargeOxxo->method,
                    'gateway' => $ChargeOxxo->gateway,
                    'recurring' => $ChargeOxxo->isrecurring,
                    'order' => $ChargeOxxo->order,
                    'customer' => $ChargeOxxo->customer,
                    'store_payment' => $ChargeOxxo->storepayment
                    
                );
```
#Solicitud de cargo a traves de SPEI

Para solicitud de cargo SPEI el metodo tambien ocuamos misma instancia de la clase Banzilla y pasamos parametros al metodo, de la sigiente manera:

```php
$chargeSpei = $banzilla->charges->create($speiData);
```
Al igual que los anteriores casos la informacion enviada al metodo puede venir de la base de datos y de el formulario de pago

```php
$speiData = array(
                "Method" => "transfer",
                "DueDate" => "11/07/2016",
                "Order"=> array(
                        "Reference" => "10285100-3322",
                        "Amount"    => 30,
                        "Currency"  => "MXN"
                        ),
                "Customer"=> array (
                        "FirstName"  => "Nombre",
                        "MiddleName" => "Apellido Paterno",
                        "Email"      => "mail@midominio.com",
                        "Address"    => array (
                                    "Street" => "Sócrates",
                                    "Number" => "130",
                                    "City"   => "Ciudad de México",
                                    "State"  => "CX",
                                    "Country"=> "MEX",
                                    "ZipCode"=> "11550"
                                    )
                        )
            );
```
El ejemplo para guardar los datos del response en un array es el siguiente:

```php
$responseSpei = array(
                    'id_transaction' => $chargeSpei->idtransaction,
                    'date_creation' => $chargeSpei->creationdate,
                    'id_request' => $chargeSpei->idrequest,
                    'method' => $chargeSpei->method,
                    'gateway' => $chargeSpei->gateway,
                    'Status' => $chargeSpei->status,
                    'card_payment' => $chargeSpei->cardpayment,
                    'order' => $chargeSpei->order,
                    'customer' => $chargeSpei->customer
                    
                );
```
