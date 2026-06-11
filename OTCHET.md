# Отчёт по практическому заданию «Основы Git»

**Студент:** Владосик  
**Email:** Vladkhodarev@gmail.com  
**Дата:** 11 июня 2026

---

## 1. Установка Git

### macOS (мой случай)

Git на macOS уже был установлен вместе с Xcode Command Line Tools.

**Проверка установки:**
```bash
git --version
# git version 2.50.1 (Apple Git-155)
```

**Если Git не установлен**, на macOS выполнить:
```bash
xcode-select --install
```

Альтернатива — скачать с [git-scm.com](https://git-scm.com/download/mac) или через Homebrew:
```bash
brew install git
```

На Windows: скачать установщик с [git-scm.com](https://git-scm.com/download/win).  
На Linux (Ubuntu/Debian): `sudo apt install git`.

---

## 2. Настройка пользователя

```bash
git config --global user.name "Владосик"
git config --global user.email "Vladkhodarev@gmail.com"
```

**Проверка:**
```bash
git config --global user.name
git config --global user.email
```

---

## 3. Создание локального репозитория и базовые операции

### git init
```bash
mkdir ~/Documents/git-assignment
cd ~/Documents/git-assignment
git init
# Initialized empty Git repository in .../git-assignment/.git/
```

### git add и git commit
```bash
echo "# Git Assignment Report" > README.md
git add README.md
git commit -m "Initial commit: add README"

# Второй коммит
echo "## Секция 1" >> README.md
git add README.md
git commit -m "Add section 1 to README"

# Третий коммит
echo "console.log('Hello Git');" > app.js
git add app.js
git commit -m "Add app.js with hello message"
```

### git status
```bash
git status
# On branch main
# Your branch is up to date with 'origin/main'.
# nothing to commit, working tree clean
```

### git log
```bash
git log --oneline --graph --all
```

**Результат:**
```
* f8873a3 Add section 2 from remote clone
* 53ad823 Add greet function on feature branch
* 6882915 Add app.js with hello message
* f335319 Add section 1 to README
* 8e1efe9 Initial commit: add README
```

---

## 4. Удалённый репозиторий

### Вариант A: GitHub (рекомендуется для сдачи)

1. Зайти на [github.com](https://github.com) → **New repository**
2. Имя: `git-assignment`, без README (он уже есть локально)
3. Выполнить команды, которые покажет GitHub:

```bash
cd ~/Documents/git-assignment
git remote add origin https://github.com/ВАШ_ЛОГИН/git-assignment.git
git push -u origin main
git push origin feature/new-feature
```

**Ссылка на репозиторий:** `https://github.com/ВАШ_ЛОГИН/git-assignment`

### Вариант B: Локальный bare-репозиторий (для демонстрации)

```bash
cd ~/Documents
git clone --bare git-assignment git-assignment-remote.git
cd git-assignment
git remote add origin ~/Documents/git-assignment-remote.git
git push -u origin main
```

---

## 5. Push и Pull

### git push
```bash
git push -u origin main
git push origin feature/new-feature
# Everything up-to-date / branch set up to track 'origin/main'
```

### git pull
Изменение было сделано в клоне репозитория и затем подтянуто:
```bash
# В клоне: добавили строку в README и сделали push
git pull origin main
# Updating 53ad823..f8873a3
# Fast-forward
#  README.md | 1 +
```

---

## 6. Ветвление и слияние

### Создание ветки
```bash
git checkout -b feature/new-feature
# Switched to a new branch 'feature/new-feature'
```

### Коммит в ветке
```bash
echo "function greet() { return 'Hello!'; }" >> app.js
git add app.js
git commit -m "Add greet function on feature branch"
```

### Merge в main
```bash
git checkout main
git merge feature/new-feature
# Updating 6882915..53ad823
# Fast-forward
```

### Список веток
```bash
git branch -a
#   feature/new-feature
# * main
#   remotes/origin/feature/new-feature
#   remotes/origin/main
```

---

## 7. Learn Git Branching

**Ссылка на тренажёр:** [https://learngitbranching.js.org](https://learngitbranching.js.org)

**Выполненные уровни:**
- [ ] Main (базовый уровень) — Introduction, Ramping up
- [ ] Remote (удалённые репозитории)
- [ ] Branching (ветвление) — Branches aren't bugs, New Branch, Branching in Git

> **Для сдачи:** пройти минимум базовый уровень + раздел «Branching».  
> Сделать скриншот экрана с пройденными уровнями (зелёные галочки) и вставить в отчёт.

---

## 8. Git в командной разработке

Git используется в команде для:

1. **Совместной работы над кодом** — каждый разработчик работает в своей ветке, не мешая другим.
2. **Истории изменений** — все коммиты сохраняются с автором, датой и описанием; можно откатиться к любой версии.
3. **Code review** — через Pull Request (GitHub) или Merge Request (GitLab) коллеги проверяют код перед слиянием в `main`.
4. **Разрешения конфликтов** — при слиянии веток Git показывает конфликтующие строки; разработчики договариваются о финальной версии.
5. **CI/CD** — push в репозиторий запускает автоматические тесты и деплой.
6. **Распределённость** — у каждого полная копия истории; работа возможна офлайн.

Типичный workflow: `main` → создать `feature/...` → коммиты → push → Pull Request → review → merge → pull на других машинах.

---

## Приложение: скриншоты

| № | Что снять | Команда / экран |
|---|-----------|-----------------|
| 1 | Версия Git | `git --version` |
| 2 | Настройка user | `git config --list` |
| 3 | git status | после `git add` |
| 4 | git log | `git log --oneline --graph` |
| 5 | Ветки | `git branch -a` |
| 6 | GitHub репозиторий | страница на github.com |
| 7 | Learn Git Branching | пройденные уровни |
