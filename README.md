[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=200&size=25&pause=1000&color=59F71D&random=false&width=435&lines=%D0%97%D0%B4%D1%80%D0%B0%D0%B2%D1%81%D1%82%D0%B2%D1%83%D0%B9%D1%82%D0%B5+%D0%BA%D0%BE%D0%BC%D0%BF%D0%B0%D0%BD%D0%B8%D1%8F+%D0%9A%D0%9F%D0%9C+%D0%A0%D0%B8%D1%82%D0%BC.;%D0%94%D0%B0%D0%B2%D0%B0%D0%B9%D1%82%D0%B5+%D0%BD%D0%B0%D1%87%D0%BD%D1%91%D0%BC!)](https://git.io/typing-svg)  
Тут будет описана инструкция по запуску фреймворка для тетсировния api n-point на ресурсе [Reqres](https://reqres.in/).  

Для понимания концепции работы с данным фреймворком мы будем подразумевать следующие условия:  
---
1. В рамках данного задания будут использованы следующие требования:
   ![Требования](https://github.com/Kana0o0/KPM_ritm/assets/139481206/3efaa4e4-6c59-49eb-97cc-755182155710)
2. Сценарии автоматического тестирования были созданы по тестовой документации:  
  [Чек-лист](https://docs.google.com/spreadsheets/d/1ozZea071lL9hmZbpYWRQqxy4_KhU0EoAO8cmyBbSPEg/edit?usp=sharing)  
  [Тест-кейс](https://docs.google.com/spreadsheets/d/1nG9Ti-l57cv1kVvqg79XrtEDJ-oon6sSFqIPj4fLv24/edit?usp=sharing)  
3. Для написания автоматических сценариев тестирования использовался следующий стек:  
  Python 3.10, pytest, docker, allure, pydantic.

Перед тем как запускать тесты вам потребуются следующие инструменты.  

В случае ручного запуска:
1. Установленный python версии 3.10 и выше, а так же pip.
2. Unix terminal или CMD/Powershell Windows.

В случе запуска через Docker:  
1. Установленный Docker.  

Для ручного запуска данного кода вам понадобиться выполнить следующие простые действия:  
---
1. Клонируйте репозиторий себе на локальную машину.
2. Создайте виртуальное окружение командой `python -m -venv -venv`
3. Активируйте виртуально окружение используя команду `source *Путь к вашей папке venv*/venv/bin/activate` (Для Linux) или `*Путь к вашей папке venv*/venv/Scripts/activate` (Для Windows)
4. При помощи инструментов терминала перейдите в директорию с файлом зависимости: src/requirements командой `cd *Путь к папке src*/src/requirements`
5. Далее выполните установук зависимостей командой: `pip install -r requirements.txt`
6. После чего командой: `cd *Путь к папке src*/src` вернитесь в директорию src.
7. После чего запустите тесты командой: `pytest -s -v main.py`
8. Для генерации отчётов allure перейдите в директорию `api_tests` и запустите команду `pytest -s -v src/main.py --alluredir=allure_result`, далее используйте команду `allure serve allure_result -p 7777`
9. После чего перейдите по адресу, указанному в вашем терминале:
  ![Вывод allure](https://github.com/Kana0o0/KPM_ritm/assets/139481206/03983757-e21c-4d9b-b6d3-70ee62338121)


Хотим обратить ваше внимание на то, что в данных тестах используются следующие маркеры:  

    data: for send url into fixture --используетя для отправки ссылки в фикстуру.  
    positive: marker for running only positive tests --используется для запуска всех позитивных тестов.  
    negative: marker for running only negative tests --используется для запуска всех негативных тестов.  
    pass_test:  marker for running only pass tests --используется для запуска всех пройденных тестов.  
    failed_test: marker for running only failed tests --используется для запуска всех проваленных тестов.  
    
Для запуска с маркером используйте следующую команду: `pytest -s -v -k *необходимый вам маркер* main.py` (Пример: `pytest -s -v -k positive main.py`)  

Для запуска тестов через Docker:  
---  
1. Клонируйте репозиторий себе на локальную машину.
2. При помощи инструментов терминала перейдите в директорию с Dockerfile: `cd api_tests`
3. Далее запустите на вашей машине Docker.
4. После чего командой: `docker build -t kpm_ritm_tests .` сгенирируйте Docker образ. (Для просмотра всех Docker образов используйте команду `docker images`)
5. После чего создайте контейнер на основе Docker образа командой: `docker run -d -p 6789:7777 kpm_ritm_tests` (Для просмотра логов используйте команду `docker logs -f *имя контейнера*`
6. Для просмотра результатов вам нужно перейти в браузер и ввести в адресную строку ваш localhost и порт, который вы выбрали в строке выше. (Пример: 127.0.0.1:6789)  

Поздравляем! Если вы следовали инструкции, вы смогли запустить тесты.   
---  

# Q&A

1. Почему существуют тесты которые не проходят? - Ответ: Всё достаточно просто, тесты которые были не пройдены, свидетельствуют о том, что сервис проходящий тестирование, не соответствует вышеуказанным требованиям. К каждому не пройденному тесту в тестовой документации [тест-кейс](https://docs.google.com/spreadsheets/d/1nG9Ti-l57cv1kVvqg79XrtEDJ-oon6sSFqIPj4fLv24/edit?usp=sharing) должна добавляться графа: Ссылка на баг-репорт, и устонавливаться соответствующий уровень приоретета.
2. Для чего в фреймворке присутствуют allure отчеты? - Ответ: Если коротко, то allure отчеты упрощают жизнь тестировщикам, позволяя в более удобном виде просматривать каждый отдельный тест и результат его прохождения. Так же при правильной документации кода, allure отчеты помогают выявлять деффекты и обслуживать код, как manual так и automation тестировщикам. Помимо этого предоставляют возможность создания графиков, как пример:
   ![Allure отчёты в виде графиков](https://github.com/Kana0o0/KPM_ritm/assets/139481206/10db7a47-8b0a-430c-86b8-e5b8a9265d64)
3. Оцените качество вашего покрытия в рамках задания. - Ответ: Хоть и в рамках задания я пыталась реализовать как можно большее покрытие тестов, нельзя сказать что тесты покрыты на 100%, так как в более приближенных к реалиям сценариев, требования к n-point значительно бы увеличилось. Помимо этого, как и было сказано выше, к каждому не пройденному тесту необходимо создавать баг-репорты и устонавливать приорететность.
4. Почему был использован Docker? - Ответ: В рамках данного задания Docker был реализован сугубо для предоставления удобства в запуске данного фреймворка. Docker - это решение которое поможет решить следующие проблемы: отсутствие необходимости настраивания среды для запуска тестов, удобство в использовании и просматривании тестов, изоляция проекта от среды local машин и т.п.

Большое спасибо за внимание!  
---  

![Snake animation](https://github.com/Kana0o0/Kana0o0/blob/output/github-contribution-grid-snake.svg)

