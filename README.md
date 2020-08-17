# learn-host-a-web-app-with-azure-app-service

https://docs.microsoft.com/ja-jp/learn/modules/publish-azure-web-app-with-visual-studio/

## MVC アプリ雛形作成

```powershell
dotnet new mvc --name <app-name>
cd <app-name>
dotnet run
```

ブラウザから ``https://localhost:5001/``

## build & pack(zip)

```powershell
dotnet publish -o pub
cd pub
compress-archive * site.zip
```

``compress-archive * site.zip`` は pub 配下から全て圧縮してください。  
別のツールでも構いません。  

## Azure App Service

[演習 - Azure portal で Web アプリを作成する - Learn | Microsoft Docs](https://docs.microsoft.com/ja-jp/learn/modules/host-a-web-app-with-azure-app-service/3-exercise-create-a-web-app-in-the-azure-portal?pivots=csharp)

## Azure App Service deploy

``az login`` :  

deploy に ``az`` を利用するのでコンソールから Azure にログインする必要があります。

```powershell
PS > az login
```

``az webapp deployment source config-zip`` :  

```powershell
PS > az webapp deployment source config-zip `
>>     --src site.zip `
>>     --resource-group *****-********-****-****-****-************ `
>>     --name <app-service-resourcename>
Getting scm site credentials for zip deployment
Starting zip deployment. This operation can take a while to complete ...
Deployment endpoint responded with status code 202
{
  "active": true,
  "author": "N/A",
  "author_email": "N/A",
  "complete": true,
  "deployer": "Push-Deployer",
  "end_time": "2020-08-17T06:51:33.3727401Z",
  "id": "734bf50d914d4bf8b00c504dffb4c33f",
  "is_readonly": true,
  "is_temp": false,
  "last_success_end_time": "2020-08-17T06:51:33.3727401Z",
  "log_url": "https://************.scm.azurewebsites.net/api/deployments/latest/log",
  "message": "Created via a push deployment",
  "progress": "",
  "received_time": "2020-08-17T06:51:31.5681765Z",
  "site_name": "************",
  "start_time": "2020-08-17T06:51:31.7056022Z",
  "status": 4,
  "status_text": "",
  "url": "https://************.scm.azurewebsites.net/api/deployments/latest"
}
```

エラーが出る場合は、デプロイするリソース名、圧縮ファイルの階層、圧縮ツールの変更で再度デプロイしてください。  
