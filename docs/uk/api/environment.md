# Середовище

Spaceship використовує префікс `SPACESHIP_` для змінних та `spaceship::` для функцій, щоб уникати конфліктів з глобальним оточенням. Всі секції, включаючи власні секції користувачів, мають використовувати префікс ` spaceship_` на початку їх назв для правильного завантаження.

## Змінні командного рядка

### `SPACESHIP_VERSION`

Змінна середовища, яка визначає версію запущеної версії командного рядка Spaceship. Може використовуватися для надсилання звітів про проблеми або налагодження.

Доступна для будь-якої програми або скрипту, що працює в поточній сесії оболонки.

```zsh
echo $SPACESHIP_VERSION
#> 3.0.0
```

### `SPACESHIP_ROOT`

<!-- prettier-ignore -->
!!! danger "Обережно"
    Ця змінна доступна тільки для читання. Змінна значення може призвести для пошкодження встановлення Spaceship!

Змінна середовища, яка визначає шлях до місця встановлення командного рядка Spaceship. Spaceship використовує цю змінну для визначення шляху до секцій та утиліт.

Доступна для будь-якої програми або скрипту, що працює в поточній сесії оболонки.

```zsh
echo $SPACESHIP_ROOT
#> /path/to/spaceship-prompt
```

### `SPACESHIP_CONFIG_PATH`

Масив зі шляхами до файлів налаштувань. Spaceship буде шукати файли налаштувань в порядку елементів масиву. Буде використано перший файл, який існує.

Типові місця:

```zsh
$HOME/.spaceshiprc
$HOME/.spaceshiprc.zsh
$HOME/.config/spaceship.zsh
$HOME/.config/spaceship/spaceship.zsh
$XDG_CONFIG_HOME/spaceship.zsh
/etc/xdg/spaceship.zsh
$XDG_CONFIG_DIRS/spaceship.zsh
```

### `SPACESHIP_CONFIG`

Змінна, яка зберігає шлях до файлу налаштувань. Зазвичай ця змінна містить один зі шляхів з масиву [`SPACESHIP_CONFIG_PATH`](#spaceship_config_path).

Ви можете вказати власний шлях до файлу налаштувань, вказавши його у змінній `SPACESHIP_CONFIG_FILE`, наприклад:

```zsh title="$HOME/.zshrc"
export SPACESHIP_CONFIG_FILE="$HOME/.dotfiles/path/to/spaceship.zsh"
```

Змінна міститиме пусте значення, якщо файл налаштувань відсутній, або не знайдений.

### `SPACESHIP_CACHE`

!!! danger "Обережно"
    Змінна має використовуватись тільки для читання. Зміна значення може спричинити некоректну поведінку командного рядка Spaceship.

Асоційований масив, який зберігає кешовані значення секцій. Кеш зберігає дані між візуалізаціями та очищається після кожного запиту.

Кешем не варто маніпулювати безпосередньо.

### `SPACESHIP_JOBS`

!!! danger "Обережно"
    Змінна має використовуватись тільки для читання. Зміна значення може спричинити некоректну поведінку командного рядка Spaceship.

Масив зараз обробляє асинхронні секції. Може бути використовуватись для перевірки того, які асинхронні секції показуються.

Назва секції додається до масиву під час показу асинхронної секції. Після завершення асинхронної роботи назва вилучається з масиву.

## Асинхронне середовище виконання

Spaceship використовує [`zsh-async`](https://github.com/mafredri/zsh-async) бібліотеку для виконання асинхронних завдань. Ця бібліотека постачається разом з Spaceship та регулярно оновлюється до найсвіжішої версії.

`zsh-async` завантажується автоматично, коли Spaceship завантажується, коли всі ці умови є істиною:

1. Асинхронний показ увімкнено (див. [Асинхронний показ](#asynchronous-rendering))
2. Існує щонайменше одна секція, що показується асинхронно.
3. `zsh-async` не було завантажено до цього.

В іншому випадку Spaceship пропустить завантаження `zsh-async`.

### Завантаження `zsh-async` вручну

Якщо ви плануєте використовувати `zsh-async` для цілей, окрім як показ Spaceship, рекомендується завантажити її явним чином, перед завантаженням Spaceship.

Ось приклад того, як завантажити `zsh-async` вручну:

=== "antigen"

    ```zsh title=".zshrc"
    antigen bundle mafredri/zsh-async
    ```

=== "antibody"

    ```zsh title=".zshrc"
    antibody bundle mafredri/zsh-async
    ```

=== "zinit"

    ```zsh title=".zshrc"
    zinit light mafredri/zsh-async
    ```

=== "zgen"

    ```zsh title=".zshrc"
    zgen load mafredri/zsh-async
    ```

=== "zplug"

    ```zsh title=".zshrc"
    zplug mafredri/zsh-async, from:github
    ```

=== "sheldon"

    ```zsh title=".sheldon/plugins.toml"
    [plugins.zsh-async]
    github = 'mafredri/zsh-async'
    ```
