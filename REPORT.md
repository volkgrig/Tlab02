## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>  # инициализируем переменные
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace # переходим в директорию workspace
$ source scripts/activate # активируем скрипт
```

```ShellSession
$ mkdir ~/.config # создам директорию
$ cat > ~/.config/hub <<EOF # редактируем файл конфигурации 
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https # применяем его
```

```ShellSession
$ mkdir projects/lab02 && cd projects/lab02 # создаём директорию
$ git init # инициализируем пустой репозиторий
$ git config --global user.name ${GITHUB_USERNAME} # настраиваем конфигурацию
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git # забираем данные из ветки master
$ git pull origin master
$ touch README.md # устанавливаем время последнего изменения
$ git status # смотрим статус файлов репозитория
$ git add README.md # добавляем файл в будущий коммит
$ git commit -m"added README.md" # создаём коммит
$ git push origin master # пушим в ветку master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
$ git pull origin master # качаем ветку master
$ git log # смотрим логи
```

```ShellSession
$ mkdir sources # создаём директории
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF # редактируем файл
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```ShellSession
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
$ edit README.md # редактируем файл
```

```ShellSession
$ git status # смотрим статус
$ git add . # добавляем все файлы в коммит
$ git commit -m"added sources" # комиттим
$ git push origin master # пушим в ветку master
```

## Report

```ShellSession
$ cd ~/workspace/labs/ # переходим  эту директорию
$ export LAB_NUMBER=02 # устанавливаем значение переменной
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER} # клонируем репозиторий
$ mkdir reports/lab${LAB_NUMBER} # создаём директорию
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md # копируем файл
$ cd reports/lab${LAB_NUMBER} # переходим в директорию
$ edit REPORT.md # редактитуем отчёт
$ gistup -m "lab${LAB_NUMBER}" # создаём гист
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com). # через гитхаб
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`. 
cat > homework/lab02-homework/hello_world.cpp << EOF и дальше код
4. Добавьте этот файл в локальную копию репозитория. 
git add .
5. Закоммитьте изменения с *осмысленным* сообщением.
git commit -m "commit simple task"
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
cat > homework/lab02-homework/hello_world.cpp << EOF и дальше код
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
git commit -m "some correct"
8. Запуште изменения в удалёный репозиторий.
git push origin master
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
git checkout -b patch1
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
Через cat и тд

3.add, **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
pull request -> New pull request
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
Merge pull request
git push origin --delete patch1
10. Локально выполните **pull**
git pull origin master
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.
git branch -d patch1

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
git checkout -b patch2
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
*clang-format -i -style=Mozilla .cpp
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
git pull origin patch2
git rebase master
7. Сделайте *force push* в ветку `patch2`
git push --force origin master
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.
Merge pull request

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
