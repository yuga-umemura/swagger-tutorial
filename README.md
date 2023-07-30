# Reference
https://qiita.com/KNR109/items/7e094dba6bcf37ed73cf
# Swagger
SwaggerはOpenAPIを利用しREST APIを設計するために使用するツールセットのことを指します。

# モックサーバの環境構築

## React×TypeScriptの環境構築
```$ npx create-react-app . --template typescript```

## mockサーバーの準備
package.jsonにmockapiを立ち上げるコマンドを記述
モックサーバはDockerで用意されているPrismを利用する
```json
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "mockapi": "docker run --rm -it -p 3001:4010 -v ${PWD}:/tmp -P stoplight/prism:4 mock -h 0.0.0.0 --cors /tmp/openapi.yaml"
  }

```

## OpenAPIファイルを作成する
```yaml
openapi: "3.0.3"

info:
  title: "Sample API"
  version: "1.0.0"

paths:
  "/api/v1/hello":
    get:
      summary: "hello"
      responses:
        "200":
          description: "成功"
          content:
            application/json:
              schema:
                type: string
                example: "hello"

```

## モックサーバを起動する
Dockerデスクトップを起動したら、先ほどpakcage.jsonに追記した下記のコマンドを実行する
```$ npm run mockapi```

## アクセス
下記のURLにアクセスする
```http://localhost:3001/api/v1/hello```
