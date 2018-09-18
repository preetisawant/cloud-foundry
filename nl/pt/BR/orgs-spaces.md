---

copyright:
  years: 2018
lastupdated: "2018-04-18"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Criando Organizações e Espaços
{: #create_orgs}

Os apps em um {{site.data.keyword.cfee_full}} têm o escopo definido em espaços específicos. Por sua vez, existe um espaço dentro de uma organização específica. Os membros de uma organização compartilham um plano de cota, apps, instâncias de serviços e domínios customizados. Depois que as organizações e os espaços são criados, os usuários podem ser incluídos neles com funções específicas que determinam o nível de acesso e controle para essas organizações e espaços. Para criar organizações e designar gerenciadores para essas organizações, você precisa de uma função de administrador para o serviço {{site.data.keyword.cfee_full_notm}} e para a instância específica do ambiente na qual os usuários estão sendo incluídos. Essas permissões são configuradas na página _Identidade e acesso_ no menu **Gerenciar > Usuários** no cabeçalho do {{site.data.keyword.Bluemix}}.
{: shortdesc}

## Criando organizações
{: #create-org}

Para criar organizações em um  {{site.data.keyword.cfee_full_notm}}:

1. Acesse o [painel {{site.data.keyword.Bluemix_notm}} Cloud Foundry Environments](https://console.bluemix.net/dashboard/cloudfoundry?filter=cf_environments){: new_window} e abra o {{site.data.keyword.cfee_full_notm}} no qual você deseja criar organizações.
2. Na interface com o usuário do {{site.data.keyword.cfee_full_notm}}, acesse a entrada **Organizações** na área de janela de navegação para abrir a página _organizações_.
3. Clique em  ** Incluir novo **.
4. Insira um **Nome** para a nova organização.
5. Sob **Gerenciadores**, identifique pelo menos um usuário. Somente usuários com uma função de Gerenciador podem incluir membros nessa organização.
6. Em **Plano de cota**, selecione um plano disponível. Um plano de cota limita a memória disponível para apps na organização, o número máximo de instâncias de apps hospedadas e o número máximo de rotas.

Além de gerenciar a associação da organização, os gerenciadores de organização podem criar, visualizar, editar ou excluir espaços dentro da organização. Os gerenciadores de organização também podem visualizar o uso e a cota da organização, convidar usuários para a organização, gerenciar a associação e as funções na organização e gerenciar domínios customizados para a organização.

Para criar espaços dentro de uma organização, na página _Organizações_, acesse a guia **Espaços** e clique em **Incluir novo**. Os membros de uma organização também podem criar e gerenciar seus próprios espaços dentro de uma organização. Para obter mais informações sobre as funções do Cloud Foundry, consulte [Acesso ao Cloud Foundry](https://console.bluemix.net/docs/iam/cfaccess.html#cfroles){: new_window}.

**Nota**: o acesso a organizações e espaços dentro de um {{site.data.keyword.cfee_full_notm}} requer que os usuários tenham permissão para acessar o ambiente em si. Sem permissão para acessar o {{site.data.keyword.cfee_full_notm}}, os usuários não podem acessar organizações e espaços dentro do ambiente, independentemente de sua associação e função nessas organizações e espaços.
