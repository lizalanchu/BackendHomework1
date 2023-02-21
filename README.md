# BackendHomework

- card.php:

```php
<?php include_once ('ver/index.php') ?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Card</title>
</head>
<body>
<form action= '' method="post">
    <input type="number" name="card">
    <input type="submit" name="send" value="Отправить">
</form>
<?php
if (!empty(($_POST))){
$Card = $_POST['card'];
$value = new Card;
$massage = $value->emit_card($Card);
echo $massage;}
?>  
</body>
</html>
```

- index.php:

```php
<?php
class Card{
    public function valid_card($number) {
        $number = strrev(preg_replace('/[^\d]/','',$number));

        $sum = 0;
        for ($i = 0, $j = strlen($number); $i < $j; $i++) {

            if (($i % 2) == 0) {
                $val = $number[$i];
            } else {
                $val = $number[$i] * 2;
                if ($val > 9)  $val -= 9;
            }
            $sum += $val;
        }

        return (($sum % 10) == 0);
    }


    public function emit_card($number) {
        if (!$this->valid_card($number)) {
            echo 'Не валидная, ';
        }
        else {
            echo 'Валидная, ';
        }
        if (preg_match('/^4[0-9]\d{14}$|^14\d{14}$/', $number)){
            echo 'Visa';
        }
        else if (preg_match('/^5[1-5]\d{14}$|^62\d{14}$|^67\d{14}$/', $number)){
            echo 'MasterCard';
        }
        else{
            echo 'Название эмитента не определено';
        }


    }
}

```

Можно внести часть кода, которая определяет платежнуюсистему под else  и тогда платежная система будет проверятся только тогда, когда карта валидна.


- Видео работы:
https://clipchamp.com/watch/eHwjR5oGFQj

