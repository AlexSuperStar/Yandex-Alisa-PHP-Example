# Yandex-Alisa-PHP-Example
Пример PHP скрипта для навыка Алисы Яндекса.
# Установка
Устанавливаем необходимые компоненты
```sh
composer init
composer require alexsuperstar/jsonmaker
composer install
```

Создание скрипта обрабатывающего запросы от Алисы
Создаем файл index.php
```php
header('Content-type:application/json;charset=utf-8');
include 'vendor/autoload.php';
$in = new \alexstar\JsonMaker(file_get_contents('php://input'));
if(isset($in->version)){
    # если есть параметр version то будем считать что  входные данные в порядке
    # формируем ответ
    $out = new \alexstar\JsonMaker();
    #  необходимые параметры ответа
    $out->version = '1.0';
    $out->response->end_session = false;
    $out->session->session_id = $in->session->session_id;
    $out->session->message_id = $in->session->message_id;
    $out->session->user_id = $in->session->user_id;
    # Ответ Алисы
    $out->response->text='Привет';
    # Например ссылка под текстом
    $out->response->buttons[0]->title = 'Открыть сайт разработчика';
    $out->response->buttons[0]->url = 'https://alexstar.ru/';
    echo $out;
}
```

