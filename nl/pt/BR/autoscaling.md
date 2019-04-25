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

# Aplicativos de auto-scaling
{: #autoscale_cloud_foundry_apps}

O {{site.data.keyword.Bluemix}} tem um suporte de auto-scaling integrado para aplicativos do Cloud Foundry para ajustar o número da instância do aplicativo automaticamente por meio de 
  * Ajuste de escala dinâmico com base nas métricas de desempenho do aplicativo.
  * Ajuste de escala planejado com base no tempo.

Esse recurso é oferecido com base no projeto de software livre do [App-Autoscaler][autoscaler_project] do Cloud Foundry. Consulte o [guia do usuário][autoscaler_user_guide] para a introdução. 

## Gerenciando o auto-scaling por meio da CLI

É possível usar o plug-in da interface da linha de comandos do App Autoscaler (também conhecido como CLI do AutoScaler) para gerenciar a política, as métricas de consulta e o histórico de ajuste de escala. 

### Instalando a CLI do AutoScaler
Use o comando a seguir para instalar a `CLI do AutoScaler`, que é um plug-in da CLI do Cloud Foundry.  

``` 
cf install-plugin -r CF-Community app-autoscaler-plugin
```
{:codeblock} 

O mesmo comando poderá ser usado para atualizar o plug-in do `AutoScaler CLI` para a versão mais recente se você tiver uma instalação anterior. 

### Usando a CLI do AutoScaler

Se você já tiver efetuado login em um ambiente do Cloud Foundry no {{site.data.keyword.Bluemix}} e tiver aplicativos em execução em seu espaço conforme descrito em [implementando o guia de apps][deploy_app], siga as etapas abaixo para criar uma política de ajuste de escala para o seu aplicativo e para consultar métricas e o histórico de ajuste de escala. 

 *  (opcional) Confirme que o terminal de API do App-Autoscaler está configurado corretamente por padrão.  

    Se o terminal da API do Cloud Foundry for apresentado como `api.<DOMAIN>`, o terminal da API do App-Autoscaler deverá ser `autoscaler.<DOMAIN>`.  
    Use o comando a seguir para verificar a configuração do terminal da API do App-Autoscaler.

    ```
    cf asa
    ```
    {:codeblock} 

    Se o terminal da API do App-Autoscaler estiver incorreto, será necessário reconfigurá-lo com o comando:

    ```
    cf asa autoscaler.<DOMAIN>
    ```
    {:codeblock} 


*  Crie um arquivo de JSON de política em sua máquina local. 

    ```
    cat > <YOUR_POLICY_FILE> << EOF
    {
            "instance_min_count": 1,
            "instance_max_count": 5,
            "scaling_rules": [
                    {
                            "metric_type": "memoryutil",
                            "breach_duration_secs": 120,
                            "limite": 80,
                            "operador": ">= ",
                            "cool_down_secs": 120,
                            "ajuste": "+ 1"
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

    A política acima será usada para acionar o ajuste de escala com base na utilização de memória quando o limite definido for violado por pelo menos `120 seconds`. Consulte o [Guia do usuário do App-Autoscaler do Cloud Foundry][autoscaler_user_guide] para saber como criar a sua própria política de ajuste automático de escala.

*  Anexe a política em seu aplicativo

    ```
    cf aasp <YOUR_APP> <YOUR_POLICY_FILE>
    ```
    {:codeblock} 

*  (opcional) Além disso, é possível consultar as métricas agregadas mais recentes de seu aplicativo. O App-Autoscaler suporta múltiplos [tipos de métricas][metric_type], mas somente as métricas definidas em sua política poderiam ser recuperadas, ou seja, `memoryutil` no exemplo acima.  

    ```
    cf asm <YOUR_APP> <METRIC_TYPE> --desc
    ```
    {:codeblock} 

*  (opcional) Utilize o comando a seguir para consultar o histórico de ajuste de escala:

    ```
    cf ash <YOUR_APP> --desc
    ```
    {:codeblock} 

    Consulte [Guia de plug-in da CLI do App Autoscaler do Cloud Foundry][autoscaler_cli] para obter mais opções para usar a linha de comandos. 


## Gerenciando o auto-scaling por meio do console do Stratos 

Além da interface da linha de comandos, também é possível gerenciar as configurações de auto-scaling por meio do console do Stratos. 

Se você instalou [stratos][stratos] em seu {{site.data.keyword.cfee_full}} (CFEE), acesse a guia **"Auto-scaling**" no painel do aplicativo para ver uma visão geral da política de ajuste automático de escala e dos eventos de ajuste de escala mais recentes.
Clique em qualquer um dos ícones em qualquer um dos ladrilhos para ativar o editor de política e editar a política.

Se nenhuma política de ajuste automático de escala estiver definida, a página de visão geral não terá informações.  Clique em **Criar política** para ativar o editor de políticas e criar uma política.

Recomendamos passar pelo [Guia do usuário do App-Autoscaler do Cloud Foundry][autoscaler_user_guide] para entender os conceitos básicos para configurar uma política de ajuste automático de escala adequadamente. 

### Estatísticas de métrica

Após você ter definido uma política com base em um ou mais tipos de métricas selecionados, será possível visualizar os valores de métricas mais recentes e o histórico de métricas nos últimos 30 minutos. 

**Nota:**Métricas representam dados com média calculada sobre todas as instâncias do aplicativo, não dados brutos de cada instância do aplicativo.
    
### Histórico de ajuste de escala

a guia **Histórico** no editor de políticas mostra que as ações de ajuste de escala foram tomadas em seu aplicativo acionadas pela política de ajuste automático de escala. Ela também mostra quaisquer mensagens de erro resultantes de falhas de ajuste de escala. É possível consultar o histórico de ajuste de escala durante os últimos 30 dias. 


[autoscaler_project]: https://github.com/cloudfoundry-incubator/app-autoscaler
[autoscaler_user_guide]: https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md
[autoscaler_cli]: https://github.com/cloudfoundry-incubator/app-autoscaler-cli-plugin#cloud-foundry-cli-autoscaler-plug-in-
[metric_type]:https://github.com/cloudfoundry-incubator/app-autoscaler/blob/master/docs/Readme.md#metric-types
[deploy_app]:https://cloud.ibm.com/docs/cloud-foundry/deploy-apps.html#dep_apps
[stratos]: https://cloud.ibm.com/docs/cloud-foundry/getting-started.html#install-stratos
