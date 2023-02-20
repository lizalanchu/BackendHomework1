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
            $number = strrev(preg_replace('/[^d]/','',$number));
            $sum = 0;
            for ($i = 0; $i < strlen($number); $i++) {
                if (($i % 2) == 0) {
                    $val = $number[$i];
                } else {
                    $val = $number[$i] * 2;
                    if ($val > 9) $val -= 9;
                }
                $sum += $val;
            }
            return (($sum % 10) == 0);
        }

        public function emit_card($number) {
             $Visa = [41, 42, 43, 44, 45, 46, 47, 48, 49, 14];
             $MasterCard =[51, 52, 53, 54, 55, 62, 67];
             if (!$this->valid_card($number)) {
                 echo 'Не валидная';
             }
             else {
                 echo 'Валидная, ';
             }
             $a = substr($number, 0, 2);
             if (in_array($a,$Visa)){
                 echo 'Visa';
             }
             else if (in_array($a, $MasterCard)){
                 echo 'MasterCard';
            }
             else{
                 echo 'Название эмитента не определено';
             }


        }
    }
```

Можно внести часть кода, которая начинается с $a под else  и тогда платежная система будет проверятся только тогда, когда карта валидна.


- Видео работы:
https://clipchamp.com/watch/eHwjR5oGFQj
