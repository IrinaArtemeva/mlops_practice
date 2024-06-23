# mlops_practice
# УрФУ/Skillfactory. Автоматизация администрирования MLOps
# Практическое задание №3

Приложение осуществляет загрузку датасета IRIS из библиотеки sklearn и далее осуществляет
обучение модели "Случайный лес". Готовая модель сохраняется в файл **model/model.joblib**.

Для обращения к модели и получения предсказания служит API приложение на основе FastAPI.

Для запуска API приложения необходимо дать команду:

$ uvicorn src.api_app:app --host 0.0.0.0 --port 8000

или запустить командный файл **start.bat** (Windows), **start.sh** (*nix like).

Для получения предсказания необходимо передать запрос методом POST содержащий json строку вида:
{
    "sepal_length": 7.7,
    "sepal_width": 2.6,
    "petal_length": 6.9,
    "petal_width": 2.3
}

Автоматизировать проверку работы приложения можно при помощи командного файла с утилитой curl:

$ predict.bat (predict.sh)

При этом осуществляется обращение к API приложению методом POST по пути /predict. Получаем в ответ 
предсказание - число 0, 1 или 2 (вид цветка).

Для создания docker образа микросервиса создан файл Dokerfile.
Создание образа вручную осуществляется командой:

$ docker build -t mlops-lab3-app .

Запуск контейнера из образа:

$ docker run -d --name mlops-lab3 mlops-lab3-app:latest

Автоматическая сборка образа и запуск контейнера осуществляется при помощи
файла-сценария docker-compose.yml. Для этого необходимо выполнить команду:

$ docker-compose up -d