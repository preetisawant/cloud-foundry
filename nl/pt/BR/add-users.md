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

# Incluindo Usuários em Organizações e Espaços
{: #adding_users}

Os membros de uma organização com uma função de gerenciador podem incluir membros nessa organização. Antes que os usuários possam ser incluídos em uma organização, eles devem ter pelo menos a função de visualizador para o serviço {{site.data.keyword.cfee_full}} e para o grupo de recursos ao qual a instância do {{site.data.keyword.cfee_full_notm}} pertence. Essas permissões são configuradas na página _Identidade e acesso_ sob **Gerenciar > Usuários** no cabeçalho do {{site.data.keyword.Bluemix}}.

Para incluir usuários como membros de uma organização em uma instância do {{site.data.keyword.cfee_full_notm}}:

1. Acesse a entrada **Organizações** na área de janela de navegação. Localize a organização na qual você deseja incluir um membro. Acesse o menu _Ações_ na linha da tabela e selecione **Incluir membro**. Como alternativa, é possível clicar na organização para abrir a página da organização, acessar a guia **Membros** e clicar em **Incluir membro**.
2. Na janela _Incluir membro_, localize o usuário, selecione uma **Função de organização** e clique em **Incluir**.

**Nota:** se você pretende incluir um usuário que foi convidado recentemente para sua conta do {{site.data.keyword.Bluemix_notm}}, pode levar vários minutos para que o usuário seja reconhecido na janela em que você inclui usuários em uma organização ou um espaço. Se o usuário não for reconhecido quando você inserir o nome do usuário, insira o endereço de e-mail do usuário e pressione o ícone de mais (+) para incluir o usuário.

Somente gerenciadores de espaço (ou gerenciadores da organização mãe) podem incluir membros em um espaço. Para incluir usuários como membros de um espaço em uma organização em uma instância do {{site.data.keyword.cfee_full_notm}}:

1. Acesse a entrada **Organizações** na área de janela de navegação, localize a organização na qual o espaço de destino está localizado e clique nela para abrir a página da organização.
2. Na página da organização, acesse a guia **Espaços**.
3. Localize o espaço de destino na tabela de espaços, acesse o menu _Ações_ na linha da tabela e selecione **Incluir membro**. Como alternativa, é possível clicar no espaço de destino na tabela para abrir a página do espaço e clicar em **Incluir membro**.
4. Na janela _Incluir membro_, localize o usuário, selecione uma **Função de espaço** e clique em **Incluir**.

**Nota**: os gerenciadores de organização podem incluir membros diretamente em um espaço sem incluí-los primeiro na organização mãe. Quando um gerenciador de organização inclui membros em um espaço, esses membros também se tornam membros da organização mãe.
