# CodePush Server [source](https://github.com/lisong/code-push-server)

CodePush Server is a CodePush progam server! microsoft CodePush cloud is slow in China, we can use this to build our's cloud server. I use [qiniu](http://www.qiniu.com/) to store the files, because it's simple and quick!  Or you can use local storage, just modify config.json file, it's simple configure.

## EXAMPLE

cli

```shell
$ code-push login http://codepush.19910225.com:8080
```

[web](http://codepush-managerment.19910225.com:8080) http://codepush-managerment.19910225.com:8080

## INSTALL

```shell
$ cd /path/to/code-push-server
$ mysql -uroot -e"create database codepush default charset utf8;"
$ mysql -uroot codepush < ./sql/codepush.sql
$ mysql -uroot codepush < ./sql/codepush-v0.1.1.sql
$ npm install
```

## CONFIG
```shell
$ vim config/config.js
```

read [config.js](https://github.com/lisong/code-push-server/blob/master/config/config.js)


## Storage mode [local/qiniu]

## RUN

```shell
$ node ./bin/www
```

or point config file and ENV

```shell
$ CONFIG_FILE=/path/to/config.js NODE_ENV=production node ./bin/www
```

notice. you have to change `loginSecret` in config.js for security.

## Default listen Host/Port  127.0.0.1/3000 
you can change like this.

```shell
$ PORT=3000 HOST=127.0.0.1 NODE_ENV=production node ./bin/www
```

## code-push-cli 
Use code-push-cli manager CodePushServer

```shell
$ npm i code-push-cli@lastest -g
$ code-push login http://127.0.0.1:3000 #login in browser account:admin password:123456
```

[code-push-cli source](https://github.com/Microsoft/code-push)

## react-native-code-push

```shell
npm i react-native-code-push@lastest -g
```

## config react-native project
Follow the react-native-code-push docs, addition iOS add a new entry named CodePushServerURL, whose value is the key of ourself CodePushServer URL. Andriod use the new CodePush constructor in MainApplication point CodePushServerUrl

iOS eg. in file Info.plist

```xml
...
<key>CodePushDeploymentKey</key>
<string>YourCodePushKey</string>
<key>CodePushServerURL</key>
<string>YourCodePushServerUrl</string>
...
```

Android eg. in file MainApplication.java

```java
@Override
protected List<ReactPackage> getPackages() {
  return Arrays.<ReactPackage>asList(
      new MainReactPackage(),
      new CodePush(
         "YourKey",
         MainApplication.this,
         BuildConfig.DEBUG,
         "YourCodePushServerUrl" 
      )
  );
}
```

[react-native-code-push source](https://github.com/Microsoft/react-native-code-push)


## Production Manage
use [pm2](http://pm2.keymetrics.io/) to manage process.

```shell
$ npm install pm2 -g
$ cp config/config.js /path/to/production/config.js
$ vim /path/to/production/config.js #configure your env.
$ cp docs/process.yml /path/to/production/process.yml
$ vim /path/to/production/process.yml #configure your env.
$ pm2 start /path/to/production/process.yml
```

## Use [CodePush Web](https://github.com/lisong/code-push-web) manage apps

add codePushWebUrl config in ./config/config.js

eg.

```json
...
"common": {
  "loginSecret": "CodePushServer",
  "codePushWebUrl": "Your CodePush Web address",
}
...
```

## License
MIT License [read](https://github.com/lisong/code-push-server/blob/master/LICENSE)


