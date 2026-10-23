# SpringBoot最小構成プロジェクト
- SpringBootとThymeleafで最小構成プロジェクトを作成する手順を示す.

## プロジェクト構成
Linux上で Spring Boot最小構成プロジェクトをコマンドだけで作る ならこんな感じです。

### プロジェクト作成
```bash
mkdir -p springboot-thymeleaf/src/main/java/com/example/demo  
cd springboot-thymeleaf
```
### pom.xml作成
```bash 
touch pom.xml
```

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         https://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.5.6</version>
    </parent>

    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

### メインクラス作成
```bash
touch src/main/java/com/example/demo/DemoApplication.java
```

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

### Controller作成  
```bash
touch src/main/java/com/example/demo/HelloController.java  
```

```java
package com.example.demo;  

import org.springframework.web.bind.annotation.GetMapping;  
import org.springframework.web.bind.annotation.RestController;  

@RestController  
public class HelloController {  

    @GetMapping("/hello")  
    public String hello() {  
        return "Hello Spring Boot!";  
    }
}
```

### 起動
```bash
mvn spring-boot:run
```
### 動作確認  
別ターミナル
```bash
curl http://localhost:8080/hello
```

### 結果  
Hello Spring Boot!  

### ディレクトリ構成確認  
現状ディレクトリ階層
```bash
$ tree 
``` 
```text
.
├── docs
│   ├── create-springboot-thymeleaf-memo.md
│   └── https-memo.md
├── pom.xml
├── src
│   └── main
│       ├── java
│       │   └── com
│       │       └── example
│       │           └── demo
│       │               ├── DemoApplication.java
│       │               └── controller
│       │                   └── HelloController.java
│       └── resources
│           ├── application.properties
│           └── templates
│               └── hello.html
└── target
    ├── classes
    │   ├── application.properties
    │   ├── com
    │   │   └── example
    │   │       └── demo
    │   │           ├── DemoApplication.class
    │   │           └── controller
    │   │               └── HelloController.class
    │   └── templates
    │       └── hello.html
    ├── generated-sources
    │   └── annotations
    └── maven-status
        └── maven-compiler-plugin
            └── compile
                └── default-compile
                    ├── createdFiles.lst
                    └── inputFiles.lst
24 directories, 13 files
```

### 参考
- AI先生
- spring bootの関連書籍たち

### memo
---
- まだ、springboot-thymeleafの初期構成の説明としては不十分である
  - 全体的にディレクトリ構成が頭にはいっていない
  - mkdir ,touch の実行場所が定まっていなし、整理もできない状態である
- ディレクトリにファイルがある程度配置しだい、httpからhttpsにする
  - 手順元は**https-memo.md**とする.
- Spring Boot + PostgreSQL接続 をやると、いいらしい.
  - PostgreSQLの環境構築は完了済み
  - 次の次くらいに取り組みたい(DBのテーブルデータは都道府県データを予定している)
- 
