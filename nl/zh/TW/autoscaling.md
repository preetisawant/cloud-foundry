---

copyright:
  years: 2019
lastupdated: "2019-03-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# 自動調整應用程式
{: #autoscale_cloud_foundry_apps}

{{site.data.keyword.Bluemix}} 具有 Cloud Foundry 應用程式的內建自動調整支援，以透過下列方式自動調整應用程式實例號碼： 
  * 根據應用程式效能度量值來動態調整。
  * 根據時間來排定調整。

此功能是根據 Cloud Foundry 開放程式碼專案 [App-Autoscaler][autoscaler_project] 所提供。請參閱[使用手冊][autoscaler_user_guide]，以開始使用。 

## 透過 CLI 管理自動調整

您可以使用 App Autoscaler 指令行介面外掛程式（又稱為 AutoScaler CLI）來管理原則、查詢度量值及調整歷程。 

### 安裝 AutoScaler CLI
使用下列指令來安裝 `AutoScaler CLI`，這是 Cloud Foundry CLI 的外掛程式。  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

如果您有先前的安裝，則可以使用相同的指令將 `AutoScaler CLI` 外掛程式更新為最新版本。 

### 使用 AutoScaler CLI

如果您已在 {{site.data.keyword.Bluemix}} 上登入 Cloud Foundry 環境，而且具有在空間中執行的應用程式（如[部署應用程式手冊][deploy_app]所述），請遵循下列步驟，為您的應用程式建立調整原則，以及查詢度量值和調整歷程。 

 *  （選用）確認依預設正確地設定 App-Autoscaler API 端點。  

    如果 Cloud Foundry API 端點呈現為 `api.<DOMAIN>`，則 App-Autoscaler API 端點應該為 `autoscaler.<DOMAIN>`。  
    使用下列指令來檢查 App-Autoscaler API 端點設定。

    ```
    cf asa
    ```
    {:codeblock} 

    如果 App-Autoscaler API 端點不正確，則需要使用下列指令予以重設：

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  在本端機器上建立原則 JSON 檔案。 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 80,
                            "operator": ">=",
                            "cool_down_secs": 120,
                            "adjustment": "+1"
                    },
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "threshold": 10,
                            "operator": "<",
                            "cool_down_secs": 120,
                            "adjustment": "-1"
                    }
            ]
    }
    EOF
    ```
    {:codeblock} 

    違反定義的臨界值至少 `120 秒`時，會使用上方的原則根據記憶體使用率來觸發調整。如需如何建立自己的自動調整原則的相關資訊，請參閱 [Cloud Foundry App-Autoscaler 使用手冊][autoscaler_user_guide]。

*  將原則連接至應用程式

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  （選用）此外，您還可以查詢應用程式的最新聚集度量值。App-Autoscaler 支援多種[度量值類型][metric_type]，但只能擷取您在原則中定義的度量值，例如，上方範例中的 `memoryutil`。  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  （選用）使用下面的指令來查詢調整歷程：

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    如需使用指令行的其他選項，請參閱 [Cloud Foundry App Autoscaler CLI 外掛程式手冊][autoscaler_cli]。 


## 透過 Stratos 主控台管理自動調整 

除了指令行介面之外，您還可以透過 Stratos 主控台來管理自動調整設定。 

如果您已在 {{site.data.keyword.cfee_full}} (CFEE) 上安裝 [Stratos][stratos]，請移至應用程式儀表板中的**自動調整**標籤，以查看自動調整原則及最新調整事件的概觀。按一下任何磚中的任何圖示，來啟動原則編輯器，並且編輯原則。

如果未定義任何自動調整原則，則概觀頁面沒有任何資訊。按一下**建立原則**，來啟動原則編輯器，並且建立原則。

建議您遵循 [Cloud Foundry App-Autoscaler 使用手冊][autoscaler_user_guide]，以瞭解適當設定自動調整原則的基本概念。 

### 度量值統計資料

根據一個以上選取的度量值類型定義原則之後，即可檢視最後 30 分鐘的最新度量值及度量值歷程。 

**附註：**度量值代表所有應用程式實例的平均資料，而不是來自每個應用程式實例的原始資料。
    
### 調整歷程

原則編輯器中的**歷程**標籤會顯示對自動調整原則觸發之應用程式所採取的調整動作。它也會顯示因調整失敗而造成的所有錯誤訊息。您可以查詢過去 30 天期間的調整歷程。 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
