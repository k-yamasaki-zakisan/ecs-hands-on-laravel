# ECS Fargeteへのデプロイハンズオン
FW(laravel)での教材は貴重なので購入した

## AWC CLIでECRにログイン
ECRにpushしようとすると
```
denied: Your authorization token has expired. Reauthenticate and try again.
```
トークンが期限切れと言われた。再度ログインします。


```
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin https://<AWS id>.dkr.ecr.<region>.amazonaws.com
```
https://qiita.com/mSakakibara/items/e5b60877c8724d5bf89d

## 参考
https://booth.pm/ja/items/2539342