# PHP Atac API
PHP library for Muoversi Roma Real time API

##Example
###GET method
``` php
<?php

include_once '../../Atac.php';

$data = $_GET;
$action = $data['action'];

$params = array(
    'user' => 'MY_USER',
    'key' => 'MY_KEY'
);

$atac = new Atac($params);

switch ($action) {

    case 'pathSearch':
        echo json_encode($atac->pathSearch($data['start_address'], $data['end_address'], $data['options'], $data['time']));
        break;
    case 'palineForecasts':
        $result = $atac->palineForecasts($data['id_palina']);
        echo json_encode($result);
        break;
    case 'palineStops':
        echo json_encode($atac->palineStops($data['id_path']));
        break;
    case 'palineSmartSearch':
        $results = $atac->palineSmartSearch($data['search_query_string']);
        echo json_encode($results);
        break;
    case 'palinePath':
        echo json_encode($atac->palinePath($data['id_route'], $data['id_vehicle'], $data['date_departure']));
        break;
    case 'palinePalinaRoutes':
        echo json_encode($atac->palinePalinaRoutes($data['id_palina']));
        break;
    case 'palineNextDeparture':
        echo json_encode($atac->palineNextDeparture($data['id_route']));
        break;
    case 'palinePaths':
        $results = $atac->palinePaths($data['id_palina']);
        echo json_encode($results);
        break;
    case 'palineVehicle':
        echo json_encode($atac->palineVehicle($data['id_vehicle'], $data['id_route']));
        break;
    case 'ztlList':
        echo json_encode($atac->ztlList());
        break;
    case 'ztlTimetables':
        echo json_encode($atac->ztlTimetables($data['changes'], $data['date']));
        break;
    default:
        $atac->_error(__FILE__, __LINE__, 'this function => ' . $action . ', not exist');
        break;
}
```
###POST method
``` php
<?php

include "../../Atac.php";

$action = $_POST['action'];
$query = $_POST['query'];

$params = array(
    'user' => 'MY_USER',
    'key' => 'MY_KEY'
);

$atac = new Atac($params);

if(isset($action) && $atac->getFunctionExist($action)) {

    if($atac->$action($query)) {
        header('Content-type: application/json');
        echo json_encode($atac->$action($query));
    }

    return false;
}
else {
    $atac->_error(__FILE__, __LINE__, 'this function => ' . $action . ', not exist');
}
```

## Documentation local
see documentation [readme_api](readme/readme_api) <br>
see documentation private functions [private](readme/private) <br>
see documentation public functions [public](readme/public)
## Documentation online
see online documentation [romamobilita](https://romamobilita.it/it/azienda/open-data/api-real-time)
## List id_paline
list in [html](tests/get/id_paline/id_paline_20_02_17.html)
<br>
list in [xml](tests/get/id_paline/id_paline_20_02_17.xml)
## List id_percorsi
list in [html](tests/get/id_percorsi/id_percorsi_18_02_17.html)
<br>
list in [xml](tests/get/id_percorsi/id_percorsi_18_02_17.xml)
<br>
list in [json](tests/get/id_percorsi/id_percorsi_18_02_17.json)
