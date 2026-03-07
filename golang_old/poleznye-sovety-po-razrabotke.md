---
order: 3.5
title: Полезные советы по разработке
---

Врапить ошибки, то есть добавлять контекст в ошибки

Правильно

```

import "fmt"
func readFile(path string) error {
    data, err := os.ReadFile(path)
    if err != nil {
        return fmt.Errorf("readFile: cannot read %s: %w", path, err)
        // %w — специальный маркер для враппинга
    }
    fmt.Println(string(data))
    return nil
}
```

### 🔹 Пример "голой" ошибки

```
func readFile(path string) error {
    data, err := os.ReadFile(path)
    if err != nil {
        return err // "голая" ошибка
    }
    fmt.Println(string(data))
    return nil
}
```



Для трассировки запросов можно использовать Middleware Request id чтобы с запросом отправлялись request id (Это нужно для расследований определенных запросов)

Также есть Middleware Logger для логирования запросов

### **Логировать запросы - это хорошая практика**



Закрывать соединения при работе с postgres в gracefull shutdown

оборачивать в App запуск всех зависимостей приложения

фиксировать где были ошибки в константе op в отправлять в log для ускорения поиска ошибки





#### \#Факт

При каких пустых значениях лучше не указывать как

`if id == 0` 

а создавать константу const emptyValue ==0  и в коде уже писать 

`if id == emptyValue`





errors.Is() ???








