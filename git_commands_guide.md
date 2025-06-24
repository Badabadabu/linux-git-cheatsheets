# 🚀 Git Commands - Полный справочник с мнемониками

> Git - это система контроля версий. Представьте, что это "машина времени" для ваших файлов!

## 🎯 Основные концепции

**Мнемоника**: Git = **G**reat **I**dea **T**racking
- **Repository** (репозиторий) = папка с историей изменений
- **Commit** (коммит) = снимок состояния файлов
- **Branch** (ветка) = параллельная линия разработки
- **Remote** (удаленный) = репозиторий на сервере (GitHub, GitLab)

## 🏗️ Начальная настройка

### Первая настройка
**Мнемоника**: "Представиться Git'у" (Introduce yourself)
```bash
git config --global user.name "Ваше Имя"
git config --global user.email "email@example.com"
git config --global init.defaultBranch main
```

### Проверить настройки
```bash
git config --list                    # Все настройки
git config user.name                 # Только имя
```

## 🌱 Создание репозитория

### `git init` - Initialize
**Мнемоника**: "Инициализировать" (Start tracking)
```bash
git init                             # Создать новый репозиторий
git init название-проекта            # Создать папку и репозиторий
```

### `git clone` - Clone
**Мнемоника**: "Клонировать" (Make a copy)
```bash
git clone https://github.com/user/repo.git
git clone https://github.com/user/repo.git новое-имя
```

## 📋 Базовые команды

### `git status` - Status
**Мнемоника**: "Статус" (What's happening?)
```bash
git status                           # Полный статус
git status -s                       # Краткий статус
```

### `git add` - Add to staging
**Мнемоника**: "Добавить на сцену" (Add to stage)
```bash
git add файл.txt                     # Добавить один файл
git add .                            # Добавить все файлы
git add *.js                         # Добавить все .js файлы
git add -A                           # Добавить все (включая удаленные)
```

### `git commit` - Commit changes
**Мнемоника**: "Зафиксировать" (Commit to memory)
```bash
git commit -m "Описание изменений"   # Коммит с сообщением
git commit -am "Сообщение"           # add + commit для отслеживаемых файлов
git commit --amend                   # Изменить последний коммит
```

## 🌿 Работа с ветками

### `git branch` - Branch management
**Мнемоника**: "Ветка дерева" (Tree branch)
```bash
git branch                           # Показать все ветки
git branch новая-ветка               # Создать новую ветку
git branch -d ветка                  # Удалить ветку
git branch -D ветка                  # Принудительно удалить ветку
git branch -m старое новое           # Переименовать ветку
```

### `git checkout` - Checkout
**Мнемоника**: "Выбрать" (Check out like hotel)
```bash
git checkout ветка                   # Переключиться на ветку
git checkout -b новая-ветка          # Создать и переключиться
git checkout файл.txt                # Отменить изменения в файле
git checkout HEAD~1                  # Перейти на 1 коммит назад
```

### `git switch` - Switch (новая команда)
**Мнемоника**: "Переключить" (Switch branches)
```bash
git switch ветка                     # Переключиться на ветку
git switch -c новая-ветка            # Создать и переключиться
git switch -                         # Вернуться к предыдущей ветке
```

## 🔄 Синхронизация с удаленным репозиторием

### `git remote` - Remote repository
**Мнемоника**: "Удаленный" (Remote control)
```bash
git remote -v                        # Показать удаленные репозитории
git remote add origin https://github.com/user/repo.git
git remote remove origin             # Удалить удаленный репозиторий
```

### `git push` - Push to remote
**Мнемоника**: "Толкнуть" (Push changes up)
```bash
git push origin main                 # Отправить в ветку main
git push -u origin main              # -u = установить upstream
git push                             # После установки upstream
git push --all                      # Отправить все ветки
```

### `git pull` - Pull from remote
**Мнемоника**: "Тянуть" (Pull changes down)
```bash
git pull                             # Получить изменения
git pull origin main                 # Получить из конкретной ветки
git pull --rebase                    # Pull с rebase вместо merge
```

### `git fetch` - Fetch from remote
**Мнемоника**: "Принести" (Fetch but don't merge)
```bash
git fetch                            # Получить данные без слияния
git fetch origin                     # Получить с конкретного remote
```

## 🔀 Слияние и конфликты

### `git merge` - Merge branches
**Мнемоника**: "Слить" (Merge lanes)
```bash
git merge другая-ветка               # Слить ветку в текущую
git merge --no-ff ветка              # Слияние без fast-forward
git merge --abort                    # Отменить слияние при конфликте
```

### `git rebase` - Rebase
**Мнемоника**: "Пересадить" (Re-base your changes)
```bash
git rebase main                      # Пересадить на main
git rebase -i HEAD~3                 # Интерактивный rebase последних 3 коммитов
git rebase --abort                   # Отменить rebase
```

## 📚 История и просмотр

### `git log` - Log history
**Мнемоника**: "Журнал" (Log book)
```bash
git log                              # Полная история
git log --oneline                    # Краткая история
git log --graph                      # Графическое представление
git log --author="Имя"               # Коммиты конкретного автора
git log -p                           # Показать изменения в коммитах
git log --since="2023-01-01"         # Коммиты с определенной даты
```

### `git show` - Show commit details
**Мнемоника**: "Показать" (Show details)
```bash
git show                             # Показать последний коммит
git show хеш-коммита                 # Показать конкретный коммит
git show HEAD~2                      # Показать коммит 2 назад
```

### `git diff` - Differences
**Мнемоника**: "Различия" (Differences)
```bash
git diff                             # Изменения в рабочей директории
git diff --staged                    # Изменения в staging area
git diff HEAD                        # Все изменения
git diff ветка1 ветка2               # Различия между ветками
```

## 🎯 Отмена изменений

### `git reset` - Reset changes
**Мнемоника**: "Сбросить" (Reset to previous state)
```bash
git reset файл.txt                   # Убрать файл из staging
git reset HEAD~1                     # Отменить последний коммит (сохранить изменения)
git reset --hard HEAD~1              # Отменить коммит и изменения
git reset --soft HEAD~1              # Отменить коммит, оставить в staging
```

### `git revert` - Revert commit
**Мнемоника**: "Обратить" (Revert back)
```bash
git revert хеш-коммита               # Создать коммит, отменяющий изменения
git revert HEAD                      # Отменить последний коммит
```

### `git restore` - Restore files (новая команда)
**Мнемоника**: "Восстановить" (Restore files)
```bash
git restore файл.txt                 # Отменить изменения в файле
git restore --staged файл.txt        # Убрать файл из staging
```

## 🏷️ Теги

### `git tag` - Tags
**Мнемоника**: "Ярлык" (Tag for release)
```bash
git tag                              # Показать все теги
git tag v1.0                         # Создать легкий тег
git tag -a v1.0 -m "Версия 1.0"      # Создать аннотированный тег
git push origin v1.0                 # Отправить тег на сервер
git push origin --tags               # Отправить все теги
```

## 🔄 Продвинутые команды

### `git stash` - Stash changes
**Мнемоника**: "Спрятать" (Stash away)
```bash
git stash                            # Спрятать изменения
git stash pop                        # Восстановить последние изменения
git stash list                       # Показать все stash'и
git stash apply stash@{0}            # Применить конкретный stash
git stash drop stash@{0}             # Удалить stash
```

### `git cherry-pick` - Cherry pick
**Мнемоника**: "Вишенка" (Pick the cherry)
```bash
git cherry-pick хеш-коммита          # Применить коммит в текущую ветку
```

### `git blame` - Blame
**Мнемоника**: "Обвинить" (Who wrote this?)
```bash
git blame файл.txt                   # Кто и когда изменял каждую строку
```

## 🔧 Конфигурация

### Полезные алиасы
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

### .gitignore файл
```bash
# Создать .gitignore
touch .gitignore

# Примеры содержимого .gitignore:
*.log                               # Игнорировать все .log файлы
node_modules/                       # Игнорировать папку node_modules
.DS_Store                          # Игнорировать системные файлы Mac
*.tmp                              # Игнорировать временные файлы
```

## 🚨 Типичные ситуации и решения

### Исправить последний коммит
```bash
# Добавить файл к последнему коммиту
git add забытый-файл.txt
git commit --amend --no-edit

# Изменить сообщение последнего коммита
git commit --amend -m "Новое сообщение"
```

### Отменить изменения
```bash
# Отменить изменения в файле
git checkout -- файл.txt

# Отменить все изменения
git checkout -- .

# Убрать файл из staging
git reset HEAD файл.txt
```

### Решение конфликтов
```bash
# При конфликте слияния:
# 1. Откройте файл с конфликтом
# 2. Найдите маркеры <<<<<<< ======= >>>>>>>
# 3. Выберите нужные изменения
# 4. Удалите маркеры
# 5. Добавьте файл и закоммитьте
git add файл-с-конфликтом.txt
git commit -m "Решен конфликт"
```

## 📊 Полезные флаги и опции

| Команда | Флаг | Описание | Мнемоника |
|---------|------|----------|-----------|
| `git add` | `-A` | Все файлы | **A**ll |
| `git commit` | `-m` | Сообщение | **M**essage |
| `git commit` | `-am` | Add + commit | **A**dd + **M**essage |
| `git log` | `--oneline` | Краткий лог | **One** line |
| `git log` | `--graph` | Граф | **Graph** |
| `git push` | `-u` | Set upstream | **U**pstream |
| `git branch` | `-d` | Удалить | **D**elete |
| `git checkout` | `-b` | Создать ветку | **B**ranch |

## 🎪 Рабочий процесс (Workflow)

### Базовый workflow
```bash
# 1. Клонировать репозиторий
git clone https://github.com/user/repo.git

# 2. Создать ветку для новой функции
git checkout -b новая-функция

# 3. Работать над кодом
# ... редактирование файлов ...

# 4. Добавить изменения
git add .

# 5. Закоммитить
git commit -m "Добавлена новая функция"

# 6. Отправить на сервер
git push -u origin новая-функция

# 7. Создать Pull Request на GitHub
# 8. После одобрения - слить в main
```

---

## 💡 Советы для запоминания

1. **Думайте о Git как о "машине времени"** для кода
2. **Коммиты = снимки** состояния проекта
3. **Ветки = параллельные вселенные** разработки
4. **origin = ваш удаленный репозиторий** (обычно на GitHub)
5. **HEAD = где вы сейчас находитесь** в истории
6. **Всегда делайте коммиты с понятными сообщениями**
7. **Часто делайте git status** - это ваш друг!

**Помните**: Git не удаляет данные, он только прячет их. Почти всё можно восстановить!