Краткий перечень инструкций по статье 
### Устанавливаем maven и git (Ubuntu 14.04.1)
```
$ sudo apt-get install maven git
```

### Создание рабочей 
#### Добавляем функцию позволяющие одной командой создать каталог и перейти в него
```
$ vi ~/.bash_profile
mkcd() { mkdir -p "$@" && cd $_; }
```
#### Созданем папку с репозиторием
```
$ mkcd hello_jsf.git
```
### Создаем пустой репозиторий
```
$ git init --bare
Initialized empty Git repository in /home/java/hello_jsf.git/
```

### Создание папки и репозитория, а также скачивание шаблонов
```
$ mkcd hello_jsf
$ git init
$ curl -O https://raw.githubusercontent.com/olegslavkin/jee7/master/.gitignore
$ curl -O https://raw.githubusercontent.com/olegslavkin/jee7/master/templates/pom.xml
```
### Редактируем pom.xml
```
$ edit pom.xml
    <groupId>info.slavkin.jee</groupId>
    <artifactId>hello_jsf</artifactId>
    <version>0.1</version>
```
### Создаем необходимые каталоги и скачиваем шаблон 
```
$ mkcd src/main/webapp/WEB-INF/
$ curl -O https://raw.githubusercontent.com/olegslavkin/jee7/master/templates/web.xml
$ cd ../../../../
$ mkdir ./src/main/resources
```
### Добавляем созданные файлы в репозиторий
```
$ git add .
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   .gitignore
	new file:   pom.xml
	new file:   src/main/webapp/WEB-INF/web.xml
```
### Первый коммит
```
$ git commit -m "initial commit"
[master (root-commit) 87682df] initial commit
 4 files changed, 40 insertions(+)
 create mode 100644 hellojsf/pom.xml
 create mode 100644 hellojsf/src/main/webapp/WEB-INF/web.xml
 create mode 100644 hellojsf/src/main/webapp/index.jsp
 create mode 100644 src/main/webapp/WEB-INF/web.xml
```
Скачиваем простейший html в стиле "Hello World"
```
$ cd src/main/webapp/
$ curl -O https://raw.githubusercontent.com/olegslavkin/jee7/master/templates/index.html
$ cd ../../../
```
### Добавляем скаченный файл в репозиторий и делаем коммит
```
$ git add src/main/webapp/index.html
$ git commit -m "Add index.html"
```
### Скачиваем и устанавливаем maven
```
$ sudo mkdir /usr/local/apache-maven
$ curl -O http://apache-mirror.rbc.ru/pub/apache/maven/maven-3/3.2.3/binaries/apache-maven-3.2.3-bin.zip
$ sudo unzip -d /usr/local/ apache-maven-3.2.3-bin.zip
$ sudo ln -s /usr/local/apache-maven-3.2.3 /usr/local/apache-maven
```
### Добавляем необходимые переменные окружения
```
$ vi ~/.bash_profile
# Maven
export M2_HOME=/usr/local/apache-maven/
export M2=$M2_HOME/bin
export MAVEN_OPTS="-Xms256m -Xmx512m"

launchctl setenv M2_HOME $M2_HOME
launchctl setenv M2 $M2


# PATH
export PATH=$M2:$PATH
```
### Проверяем версию maven
```
$ mvn -version
Apache Maven 3.2.3 (33f8c3e1027c3ddde99d3cdebad2656a31e8fdf4; 2014-08-12T00:58:10+04:00)
Maven home: /usr/local/apache-maven
Java version: 1.6.0_65, vendor: Apple Inc.
Java home: /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
Default locale: ru_RU, platform encoding: MacCyrillic
OS name: "mac os x", version: "10.10.1", arch: "x86_64", family: "mac"
```
### Создаем приложение
```
$ mvn package
```
### Листинг созданных каталогов и файлов в результате выполнения команды
```
$ ls -1 target/
 classes
 hello_jsf-0.1
 hello_jsf-0.1.war <!-- Web Archive
 maven-archiver
```
# Просмотр списка файлов архива
```
$ jar tf target/hello_jsf-0.1.war

META-INF/
META-INF/MANIFEST.MF
WEB-INF/
WEB-INF/classes/
index.html
WEB-INF/web.xml
META-INF/maven/
META-INF/maven/info.slavkin.jee/
META-INF/maven/info.slavkin.jee/hello_jsf/
META-INF/maven/info.slavkin.jee/hello_jsf/pom.xml
META-INF/maven/info.slavkin.jee/hello_jsf/pom.properties
```
### Deploy application
* autodeploy
```
$ sudo chown -R java:java /opt/glassfish4/glassfish/domains/domain1/autodeploy/ (remote)
$ scp target/hello_jsf-0.1.war java@10.1.1.12:/opt/glassfish4/glassfish/domains/domain1/autodeploy/
``` 
* web deploy
``` 
 $ scp target/hello_jsf-0.1.war  java@10.1.1.12:/home/java
```
``` 
$ curl http://10.1.1.12:8080/hello_jsf-0.1/
<!DOCTYPE html>
<html>
<head>
    <meta charset=utf-8>
    <title>Hello!</title>
</head>
<body>
  <h1>Hello World!</h1>
</body>
</html>
```
### Добавляем удаленный репозиторий
```
$ git remote add origin ssh://java@х.х.х.х:/path/to/hello_jsf.git
$ git remote -v
```
### Push'им в удаленный репозиторий
```
$ git push origin master
Counting objects: 18, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (18/18), 2.21 KiB | 0 bytes/s, done.
Total 18 (delta 2), reused 0 (delta 0)
To ssh://java@10.1.1.12:/home/java/hello_jsf.git
 * [new branch]      master -> master
```
