# Recipe

## Recipe 1: Building Simple Apps

create new go project `go mod init <name_project>` and paste this code into `main.go`

```go
package main

import (
	"github.com/gofiber/fiber/v2"
)

func main() {

	app := fiber.New()

	app.Get("/", func(c *fiber.Ctx) error {
		return c.SendString(":) Hello, World!")
	})

	app.Listen(":3000")
}
```



create `Dockerfile` and paste this code

```sh
FROM golang:1.17.4

WORKDIR /app


COPY go.mod /app/
COPY go.sum /app/

RUN go mod download

COPY . .

EXPOSE 3000

CMD ["go", "run", "main.go"]

```

To create image from this Dockerfile, run `docker build -t simpleapp .`. Then we can create container from this image by running `docker run --name simpleapp_container -d -p 8080:3000 simpleapp`.    

- `--name simpleapp_container` is the name of the cointainer
- `-d` daemon mode so the app will run quetely
- `-p 8080:3000` is port external:port internal
- `simpleapp` the name of container 


To create multiple container that connect each other, we can create `docker-compose.yml` and paste this code

```yaml
version: "3.3"
services:
 backend:
  build: .
  ports: 
   - "8080:8080"
  volumes:
   - .:/app
  depends_on:
   - db
 db:
  image: mysql:5.7.22
  restart: always
  environment:
   MYSQL_DATABASE: ambasador
   MYSQL_USER: root
   MYSQL_PASSWORD: root
   MYSQL_ROOT_PASSWORD: root
  volumes:
   - .dbdata:/var/lib/mysql
  ports:
   - 3306:3306
```