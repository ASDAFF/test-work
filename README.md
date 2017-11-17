# Тестовые задания для кандидата на позицию «WEB-разработчик»
1. Задание
После оформления заказа менеджеру и покупателю отправляются два письма с описанием заказа, одно менеджеру, другое - покупателю. Необходимо в письмо менеджеру добавить 10 последних посещенных покупателем страниц до того, как тот оформил заказ, в обратном хронологическом порядке.
Файл init.php
```php
AddEventHandler("sale", "OnOrderNewSendEmail", "bxModifySaleMails");
function bxModifySaleMails($orderID, &$eventName, &$arFields)
{
    $userID = $_SESSION['SESS_AUTH']['USER_ID'];
    $arFilter = array(
        'USER_ID' => $userID,
    );
// получим список записей
    $rs = CHit::GetList(
        ($by = "s_date_hit"),
        ($order = "desc"),
        $arFilter
    );

// выведем все записи
    while ($hit = $rs->Fetch()) {
        $arHits[] = $hit['URL_FROM'];
    }
    $result = array_unique($arHits);
    $array = array_slice($result, 0, 11);

    $arFields["HITS_LIST"] = $array;
}
```