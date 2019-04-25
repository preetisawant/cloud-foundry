---

copyright:
  years: 2018
lastupdated: "2019-04-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Monitoramento 
{: #monitoring}

O monitoramento de uma instância do {{site.data.keyword.cfee_full}} e de sua infraestrutura suportada é suportado por um conjunto de ferramentas de software livre consistindo no Prometheus e Grafana.  A solução permite que você analise, visualize e gerencie alertas para métricas no ambiente do Cloud Foundry.  Há três consoles da web nos quais ocorre o monitoramento: um console do Grafana, um console do Prometheus e um console do Prometheus Alert Manager.

Iniciando com o CFEE v2.2.0, as ferramentas de monitoramento não são ativadas por padrão quando um ambiente é criado.  Os administradores podem ativar o monitoramento após a criação do ambiente.  Na interface com o usuário do CFEE, vá para a página _Monitoramento_na área de janela de navegação esquerda e clique em **Ativar**. A ativação do monitoramento automaticamente provisiona nós do trabalhador adicionais do Kubernetes (na mesma conta do IBM Cloud) e instala as ferramentas de monitoramento nesses nós do trabalhador.

**Nota:** o acesso ao recurso de monitoramento em uma instância do {{site.data.keyword.cfee_full}} requer uma função de _Administrador_ ou de _Editor_ no CFEE e a função de _Operador_ no cluster Kubernetes que suporta a instância do CFEE (em adição à função de _Visualizador_ no grupo de recursos sob o qual o CFEE está agrupado). O nome padrão do cluster do Kubernetes que suporta uma instância do CFEE é _`<CFEEname>` -cluster _. 

## Prometheus.
{: #prometheus}

O Prometheus é um kit de ferramentas de monitoramento e alerta de sistemas de software livre. Desde a sua concepção em 2012, muitas empresas e organizações adotaram o Prometheus e o projeto tem uma comunidade de desenvolvedores e usuários muito ativos. 
Ele é um projeto de software livre independente e mantido independentemente de qualquer empresa. Para enfatizar isso e esclarecer a estrutura de controle do projeto, o Prometheus se associou ao Cloud Native Computing Foundation em 2016 como o segundo projeto hospedado, após o Kubernetes. Consulte a [documentação do Prometheus](https://prometheus.io/docs/introduction/overview/) para obter mais informações.

O ecossistema Prometheus consiste em múltiplos componentes, muitos dos quais são opcionais:

* O servidor Prometheus principal, que extrai e armazena dados de série temporal.</li>
* O [Alertmanager](https://prometheus.io/docs/alerting/alertmanager/) para manipular alertas.</li>
* Vários exportadores de propósito especial, como o exportador de nós, o exportador de caixa preta, etc.</li>
* Um gateway de push para suportar tarefas de curta duração.</li>

O Prometheus reúne métricas de tarefas instrumentadas, diretamente ou por meio de um gateway de push intermediário para tarefas de curta duração. Ele armazena todas as amostras reunidas localmente e executa regras sobre esses dados para agregar e registrar novas séries temporais de dados existentes ou para gerar alertas. 

## Grafana
{: #grafana}

Grafana é uma plataforma de análise de software livre para todas as métricas coletadas pelo Prometheus. A versão do Grafana implementada em seu cluster já está configurada para usar o banco de dados Prometheus subjacente. Ela também contém alguns valiosos painéis do Grafana.  Consulte [Documentação do Grafana](http://docs.grafana.org/guides/getting_started/) para obter mais informações.

## Introdução ao Monitoramento
{: #gettingStarted_monitor}

Os componentes Prometheus e Grafana que compõem a solução de monitoramento são pré-instalados na infraestrutura do Kubernetes que suporta a instância do CFEE.  Para acessar as ferramentas de monitoramento, é necessário encaminhar as portas dos servidores Prometheus, Prometheus AlertManager e Grafana.  Isso é feito por meio da CLI do Kubernetes. 
A seguir você é conduzido pelas etapas para instalar a CLI necessária, encaminhar as portas do servidor e ativar os consoles.

**Nota:** as instruções a seguir também estão disponíveis na interface com o usuário do {{site.data.keyword.cfee_full}}.  Abra a interface com o usuário da instância do CFEE, clique em **Monitoramento** na área de janela de navegação à esquerda e acesse a guia **Acesso** para ver as instruções exibidas.

### Pré-requisito

1. Verifique as [Políticas de acesso](https://console.bluemix.net/iam/#/users) para assegurar que você tenha pelo menos uma função de Visualizador no cluster do Kubernetes que suporta o ambiente.
2. Instale a  [ CLI do IBM Cloud ](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html#install_use).
3. Instale a  [ CLI do Kubernetes ](https://kubernetes.io/docs/tasks/tools/install-kubectl/).  Se você tiver uma CLI do Kubernetes existente, recomendamos que instale a versão mais recente.
4. Instale o plug-in de serviço de contêiner:
```
    ibmcloud plugin install container-service -r Bluemix
```
 
### Customizando a Configuração do Alertmanager

O Alertmanager tem um arquivo de [Configuração do Alertmanager](https://prometheus.io/docs/alerting/configuration/) que define as políticas para manipulação, agrupamento e o roteamento de notificação de alertas do Alertmanager. É possível fazer download do arquivo de configuração padrão e fazer upload de uma configuração customizada na guia **Configuração** da página _Monitoramento_.
 
### Acessar o cluster do Kubernetes

1. Efetue login na sua conta do IBM Cloud:

  ```
  logins ibmcloud -a https://api.ng.bluemix.net
  ```
  {: pre}
  
  Se você tiver um ID federado, use __ibmcloud login -sso__ para efetuar login na CLI do IBM Cloud.

2. Destine a região do IBM Cloud Container Service na qual você deseja trabalhar (por exemplo, us-south):

  ```
  ibmcloud cs region-set us-south
  ```
  {: pre}
    
3. Configure o contexto do cluster em sua CLI: 

  a. Obtenha o comando para configurar a variável de ambiente e fazer download dos arquivos de configuração do Kubernetes:

  ```
  ibmcloud cs cluster-config < CFEE_instance_name> -cluster
  ```
  {: pre}
    
  b. Configure a variável de ambiente KUBECONFIG. Copie a saída de comando anterior e cole-a no terminal. A saída de comando deve ser semelhante à seguinte:
  __export KUBECONFIG=/Users/$USER/.bluemix/plugins/container-service/clusters/cf-admin-0703-cluster/kube-config-dal10-cf-admin-0703-cluster.yml__

### Encaminhar portas do servidor
4. Configure o encaminhamento de porta no cluster do Kubernetes para os pods que executam o Prometheus, AlertManager e Grafana. Isso permitirá que você hospede as métricas de monitoramento por proxy em sua máquina local (host local):

  ```
  sh -c 'kubectl -n monitoring port-forward deployment/prometheus-server 9090 & kubectl -n monitoring port-forward deployment/prometheus-alertmanager 9093 & kubectl -n monitoring port-forward deployment/grafana 3000 &''
  ```
  {: pre}
  
### Ativar os consoles de monitoramento em seu proxy da web local

5. Ative o console do Grafana para ver a analítica nas métricas selecionadas.  Há painéis padrão do Grafana incluídos na instância do CFEE. Esses painéis padrão são interativos e fornecem uma visualização da infraestrutura usada para hospedar sua instância do CFEE. (Cluster de Kubernetes). Depois de ativar o console do Grafana, clique no botão **Página inicial** na parte superior do console do Grafana para selecionar um dos painéis pré-implementados (veja a lista a seguir), que criará o gráfico das métricas correspondentes:

   Para o CFEE v2.1.0 ou anterior, há um usuário padrão `admin` em Grafana, com a senha padrão configurada como `admin`. Recomendamos efetuar login com Userid/Senha `admin/admin` e mudá-los para novas credenciais. Para o CFEE v2.2.0 ou mais recente, os usuários são autenticados automaticamente com as suas credenciais de IBMid.

     [ Ativar console do Grafana ](https://localhost:3000)

   Os painéis padrão a seguir são fornecidos com a instância do CFEE e estão disponíveis na lista suspensa _Página inicial_.

    Painéis do Cloud Foundry:
   - _CF: capacidade de células_ 
        - Mostra o status geral das células do Cloud Foundry em que os aplicativos Cloud Foundry estão implementados.
   - _CF: painel Célula Diego_ 
        - Mostra o status das células do Cloud Foundry e dos componentes do Diego.
   - _CF: roteador_ 
        - Mostra o status do roteador do Cloud Foundry em execução em seu ambiente do CFEE.
  
   Painéis para a infraestrutura Kubernetes que suportam seu ambiente do CFEE:
   - _Implementação_ 
        - Mostra o status de suas implementações do Kubernetes.
   - _Funcionamento do cluster Kubernetes_ 
        - Mostra o funcionamento do cluster do Kubernetes.
   - _Status do cluster Kubernetes_ 
        - Mostra o status do cluster do Kubernetes.
   - _Solicitações de recurso do Kubernetes_ 
        - Mostra a CPU usada, a memória e outros parâmetros do cluster do Kubernetes.
   - _Pods_ 
        - Mostra detalhes para cada pod em execução no cluster do Kubernetes.
   - _Conjunto de réplicas_ 
        - Mostra o status dos conjuntos de réplicas do Kubernetes.       
   - _Nós do trabalhador_ 
        - Mostra detalhes para cada nó trabalhador do cluster do Kubernetes.
   - _Visão geral dos nós do trabalhador_ 
        - Mostra o uso de CPU e de memória da infraestrutura do Kubernetes, juntamente com seu tráfego de rede.
        
6. Opcionalmente, também é possível ativar o console do Prometheus para ver os dados brutos coletados pelo servidor Prometheus e o Prometheus Alertmanager para gerenciar os alertas enviados pelo servidor Prometheus:

     [ Ativar servidor Prometheus ](https://localhost:9090)

     [ Ativar servidor Prometheus Alertmanager ](https://localhost:9093)

