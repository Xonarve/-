---
marp: true
---
# Цель работы:
Освоение на практике применение режима однократного гаммирования.

---
# Ход работы
Нужно подобрать ключ, чтобы получить сообщение «С Новым Годом, друзья!». Разработаем приложение, позволяющее шифровать и дешифровать данные в режиме однократного гаммирования.

---
# Выполнение работы:
Импортировали необходимые модули, сохранили пользовательский ввод.
```
import random
import string

inpt = input("Введите строку: ")
```

---
# Выполнение работы:
Написали функцию генерации случайного ключа, заданного размера. Написали функцию, преобразующую исходный символьный формат в шестнадцатеричный.
```
def key_gener(size = 6, chars = string.ascii_letters + string.digits):
    return ''.join(random.choice(chars) for _ in range(size))
def chan(s):
    return ":".join ("{:02x}".format(ord(c)) for c in s)
```

---
# Выполнение работы:
Сгенерировали случайный ключ, распечатали его.
```
key = key_gener(len(inpt))
print(f'Ключ в виде строки: {key}')
```

---
# Выполнение работы:
Создали функцию гаммирования.
```
def gam(inpt, key):
    inpt_ascii = [ord(i) for i in inpt]
    key_ascii = [ord(i) for i in key]
    enc_str = ''.join(chr(s ^ k) for s, k, in zip(inpt_ascii, key_ascii))
    return enc_str
```

---
# Выполнение работы:
Создали функцию поиска истинного ключа, который однозначно формируется из исходного и шифрованного текста.
```
def find_truekey(inpt, enc_str):
    sm_ascii = [ord(i) for i in inpt]
    enc_str_ascii = [ord(i) for i in enc_str]
    true_key = ''.join(chr(s ^ k) for s, k in zip(enc_str_ascii, sm_ascii))
    return true_key
```

---
# Выполнение работы:
Сформировали функцию, которая расшифровывает текст с помощью данного ей ключа.
```
def unencrypt(enc_str, key):
    enc_str_ascii = [ord(i) for i in enc_str]
    key_ascii = [ord(i) for i  in key]
    true_str = ''.join(chr(s ^ k) for s, k in zip(enc_str_ascii, key_ascii))
    return true_str
```

---
# Выполнение работы:
Зашифровали пользовательскую строку, используя заранее сгенерированный случайный ключ к данной строке.
```
enc_str = gam(inpt, key)
```

---
# Выполнение работы:
Попытались сформировать ключ для шифрованной строки и расшифровать ее с помощью данного ключа, получили некую последовательность символов.

Выполнили попытку расшифровки строки с помощью истинного ключа, получили исходную строку.
```
new_key = key_gener(len(enc_str))
unencrypted_new_key = unencrypt(enc_str, new_key)
true_key = find_truekey(inpt, enc_str)
unencrypted_true_key = unencrypt(enc_str, true_key)
```

---
# Выполнение работы:
```
print(f'Закодированная строка: {enc_str}')
print(f'В шестнадцатиричной системе: {chan(enc_str)}')
Закодированная строка: їFФѐѹмьGѩѤѽѤюjsѲАЪѽЩЭL
В шестнадцатиричной системе: 457:46:424:450:479:43c:44c...
```

---
# Выполнение работы:
```
print(f'Подобранный ключ: {new_key}')
print(f'Строка, расшифрованная подобранным ключем: {unencrypted_new_key}')
print(f'Настоящий ключ: {true_key}')
print(f'Декодированная строка: {unencrypted_true_key}')
Подобранный ключ: o5GWu1sgSXBLQsCq9xWzmr
Строка, расшифрованная подобранным ключем: иsѣЇЌЍп кмпШП0ЃЩђЪѓр>
Настоящий ключ: vf9nKwpgzZIZrFSFPiJebm
Декодированная строка: С Новым Годом, друзья!
```

---
# Вывод:
В ходе выполнения лабораторной работы была изучена теория режима однократного гаммирования и освоена на практике.