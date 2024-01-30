# archpkg

Менеджер пакетов архитектурного кода [DocHub](https://dochub.info/main).

Обеспечивает управление зависимостями архитектурных репозиториев созданных с использованием подхода "Архитектура как код".
Позволяет быстро и удобно устанавливать, обновлять и удалять пакеты, необходимые для работы архитектурного репозитория. 

**archpkg** разработан для того, чтобы стимулировать развитие архитектурной функции открытым сообществом. 
Призван обеспечить обмен опытом и знаниями выраженными в архитектурном коде между членами сообщества. 

Инструментализирует концепцию адаптивной метамодели. Подробнее о ней и структуре пакетов [здесь](https://dochub.info/entities/docs/blank?dh-doc-id=dochub.flex_metamodel). 

# Экосистема 

1. [DocHub](https://github.com/RabotaRu/dochub) - мультиплатформенный инструмент описания архитектуры через код (AaC);
2. https://dochub.info/ - Демонстратор технологии и документация;
3. https://registry.dochub.info/ - реестр архитектурных пакетов (TBD);
4. arckpkg - менеджер пакетов. 

# Подготовка

1. Установите [DocHub](https://github.com/RabotaRu/DocHub?tab=readme-ov-file#%D0%B1%D1%8B%D1%81%D1%82%D1%80%D1%8B%D0%B9-%D1%81%D1%82%D0%B0%D1%80%D1%82);
2. Установите [nodejs >= 20.11.0 и npm >= 10.2.3 ](https://nodejs.org/en/download).

# Использование

Используйте команду npx archpkg <Параметры> для вызова пакетного менеджера. Например:

```console
mkdir examples
cd examples
npx archpkg install dochub-examples -save
```

Данный код создаст директорию "examples" и клонирует в нее архитектурный репозиторий примеров.
Воспользуйтесь DocHub для рендеринга архитектурного репозитория.

# Команды 

## install

Устанавливает требуемые пакеты из публичного реестра. 

Пример команды:
```console
npx archpkg install
```

Если используется без параметров, ищет в текущей директории файл dochub.yaml и устанавливает определенные в нем зависимости.
Файл должен содержать следующую структуру:

```yaml
# Метаданные проекта
 $package:  
   <идентификатор_проекта>:  
       version: "<версия_проекта>"
       # Здесь указываются зависимости 
       dependencies:
         <идентификатор пакета>: "<версия>"   # Версия указывается в формате x.x.x например 1.2.11
                                              # Доступно указание правил выбора пакетов
                                              # >   выше указанной версии, например >1.2.11
                                              # >=  выше или равно указанной версии, например >=1.2.11
         ...
```

Пример файла dochub.yaml:
```yaml
$package:
  example:
    name: Пример файла зависимостей
    version: 1.0.0
    dependencies:
      dochub-examples: ">=1.0.0"
```

При выполнении команды:
```console
npx archpkg install -save
```

Будет установлен пакет примеров из репозитория https://github.com/rpiontik/DocHubExamples.
Ключ "-save" заставит archpkg добавить в dochub.yaml [импорт](https://dochub.info/entities/docs/blank?dh-doc-id=dochub.imports) подключенной зависимости.  

## install <идентификатор пакета>[@<версия пакета>]

Устанавливает конкретный пакет как зависимость. 

```console
npx archpkg install dochub-examples -save
```

Установит наиболее свежую версию пакета dochub-examples и укажет его как зависимость в текущем проекте.

```console
npx archpkg install dochub-examples@>=1.0.0 -save
```

Установит версию пакета dochub-examples старше или равную 1.0.0 и укажет его как зависимость в текущем проекте.

```console
npx archpkg install dochub-examples@1.0.0
```

Установит версию пакета dochub-examples равную 1.0.0 но не укажет его как зависимость в текущем проекте.

## remove <идентификатор пакета>

Удаляет указанный пакет из зависимостей. 

Пример команды:
```console
npx archpkg remove dochub-examples
```

## clean

Очищает вспомогательные пространства используемые archpkg для установки пакетов.

Пример:
```console
npx archpkg clean
```


# Лицензия 

GPLv3