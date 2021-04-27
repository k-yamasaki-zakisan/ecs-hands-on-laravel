## タスク定義の登録
```
$ aws ecs register-task-definition --cli-input-json file://${jsonファイルを指定}
```

## テストコマンド
```
$ aws ecs run-task \
--cluster ecs-hands-on \
--task-definition ecs-hands-on-for-command \
--overrides '{"containerOverrides": [{"name":"laravel","command": ["s›
›h","-c","php artisan print:helloworld"]}]}' \
--launch-type FARGATE \
--network-configuration "awsvpcConfiguration={subnets=[<作成済みのサブ ネットID>],securityGroups=[<作成済みのセキュリティグループID>],assignPublicIp=ENABLED}"
```

## Laravelデプロイ実行
```
$ aws ecs create-service \
--cluster ecs-hands-on \
--service-name ecs-hands-on-laravel \
--task-definition ecs-hands-on-for-web \
--launch-type FARGATE \
--desired-count 1 \
--network-configuration "awsvpcConfiguration={subnets=[<作成済みのサブ ネットID>],securityGroups=[<作成済みのセキュリティグループID>],assignPublicIp=ENABLED}"
```

## ECSタスク削除
次のエラーメッセージ、An error occurred (InvalidParameterException) when calling the CreateService operation: Creation of service was not idempotent が表示された場合は、cwagent-daemon-service という名前のデーモンサービスは既に作成されています。まず、次のコマンドを例として使用して、そのサービスを削除する必要があります。
```
$ aws ecs delete-service \
--cluster ecs-hands-on \
--service ecs-hands-on-laravel \
--region ap-northeast-1 \
--force
```

参考：
https://docs.aws.amazon.com/ja_jp/AmazonCloudWatch/latest/monitoring/deploy-container-insights-ECS-instancelevel.html

## IAMでタスクを実行した時に権限エラー
どれをIAMロールにアタッチしていいかわからなかったので、
admin権限を持たせて一時的に対応した

参考:
https://dev.classmethod.jp/articles/iam-pass-role/

