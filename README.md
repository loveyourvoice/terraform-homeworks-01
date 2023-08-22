# Задание 1

## 1.1
![Image](https://i.imgur.com/3W6udH3.png)

## 1.2
Согласно файлу gitignore можно сохранить секретную информацию в папке .terraform и в файле у которого название начинается с .terraform

Так же все файлы с раширением .tfstate и файлы у которых в названии есть .tfstate.

А так же в файле personal.auto.tfvars.

## 1.3
"result": "gcpBojbT9UNA3FZK"

## 1.4
Пропущено название для docker_image. А так же в контейнере был указ название образа,вместо ссылки уже объявленного созданного ресурса-образа, ну и проблема с именем была.

`
resource "docker_image" **"nginx"**{
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" **"nginx_container"** {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 8000
  }
}
`
## 1.5
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
37d65c2185b0   eea7b3dcba7e   "/docker-entrypoint.…"   6 seconds ago   Up 5 seconds   0.0.0.0:8000->80/tcp   example_gcpBojbT9UNA3FZK

## 1.6
Ключ -auto-approve автоматически применяет без моего дополнительного подтверждения все измнения, можно случайно удалять ненужное или изменить.
В данном случае произошло следующие - первый контейнер уже удалился, а новый не запустился, потому что контейнер с точности таким именем уже существует.
![Image](https://i.imgur.com/fpNcPlN.png)

## 1.7
`
{
  "version": 4,
  "terraform_version": "1.5.0",
  "serial": 20,
  "lineage": "86b0f8b5-83e9-f7f4-4442-d9c7285b6ebc",
  "outputs": {},
  "resources": [],
  "check_results": null
}
`
## 1.8
Потому что по умолчанию скаченные образы не удаляются вместо с деплоем, но если применить ключ про который я взял информацию из регистра, то можно сделать чтобы и удалился.

**keep_locally (Boolean) If true, then the Docker image won't be deleted on destroy operation. If this is false, it will delete the image from the docker local storage on destroy operation**