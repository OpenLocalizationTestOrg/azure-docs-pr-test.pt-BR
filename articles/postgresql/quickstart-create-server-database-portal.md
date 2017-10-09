---
title: 'Portal do Azure: criar um Banco de Dados do Azure para PostgreSQL | Microsoft Docs'
description: "Rápido iniciar toocreate guia e gerenciar o banco de dados do Azure para o servidor de PostgreSQL usando a interface de usuário do portal do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: quickstart
ms.date: 08/10/2017
ms.openlocfilehash: 61753268147d6ea283d1aa5d6baf269d2756d25a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-in-hello-azure-portal"></a>Criar um banco de dados do Azure para PostgreSQL em Olá portal do Azure

Banco de dados do Azure para PostgreSQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados PostgreSQL altamente disponíveis na nuvem hello. Este guia de início rápido mostra como toocreate um Azure banco de dados para o servidor de PostgreSQL usando Olá portal do Azure em cerca de cinco minutos.

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure
Abra seu navegador da web e navegue toohello [portal do Microsoft Azure](https://portal.azure.com/). Insira sua credenciais toosign no portal de toohello. exibição padrão de saudação é seu painel de serviço.

## <a name="create-an-azure-database-for-postgresql"></a>Criar um Banco de Dados do Azure para o PostgreSQL

Um Banco de Dados do Azure para PostgreSQL é criado com um conjunto definido de [recursos de computação e armazenamento](./concepts-compute-unit-and-storage.md). Olá servidor será criado dentro de um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

Siga essas toocreate etapas um banco de dados do Azure para o servidor PostgreSQL:
1.  Clique em Olá **novo** botão (+) localizado no canto superior esquerdo de saudação do hello portal do Azure.
2.  Selecione **bancos de dados** de saudação **novo** página e selecione **banco de dados do Azure para PostgreSQL** de saudação **bancos de dados** página.
 ![Banco de dados do Azure para PostgreSQL - criar o banco de dados de saudação](./media/quickstart-create-database-portal/1-create-database.png)

3.  Preencha novo formulário de detalhes de servidor Olá com hello seguintes informações, conforme mostrado na saudação anterior imagem:

    Configuração|Valor sugerido|Descrição
    ---|---|---
    Nome do servidor |*mypgserver-20170401*|Escolha um nome exclusivo que identifica o Banco de Dados do Azure para o servidor PostgreSQL. o nome de domínio Olá *postgres.database.azure.com* é fornecer para tooconnect de aplicativos para nome do servidor de toohello anexado. nome do servidor de saudação pode conter apenas letras minúsculas, números e caracteres de hífen (-) hello e ele deve conter de 3 a 63 caracteres.
    Assinatura|*Sua assinatura*|Olá assinatura do Azure que você deseja toouse para o servidor. Se você tiver várias assinaturas, escolha assinatura apropriada hello, no qual o recurso de saudação é cobrado para.
    Grupo de recursos|*myresourcegroup*| Você pode criar um novo nome do grupo de recursos ou usar um existente de sua assinatura.
    Logon de administrador do servidor |*mylogin*| Verifique sua própria toouse de conta de logon ao conectar-se o servidor toohello. nome de logon de administrador Olá não pode ser 'azure_superuser', 'azure_pg_admin', 'admin', 'Administrador', 'root', 'Convidado' ou 'public' e não pode começar com 'pg_'.
    Senha |*Sua escolha* | Crie uma nova senha para a conta de administrador do servidor de saudação. Deve conter de 8 caracteres too128. Sua senha deve conter caracteres de três categorias a seguir de saudação – maiusculas letras, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #, %, etc.).
    Local|*Olá região mais próxima tooyour os usuários*| Escolha local Olá usuários de tooyour mais próximos.
    Versão do PostgreSQL|*Escolha a versão mais recente da saudação*| Escolha a versão mais recente do hello, a menos que você tem requisitos específicos.
    Camada de preços | **Básico**, **50 Unidades de Computação** **50 GB** | Clique em **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo banco de dados. Escolha a camada básica na guia Olá na parte superior de saudação. Clique em extremidade esquerda Olá Olá unidades de computação controle deslizante tooadjust Olá valor toohello mínimo disponível para este guia de início rápido. Clique em **Okey** toosave Olá seleção da camada de preços. Consulte Olá captura de tela a seguir.
    | PIN toodashboard | Verificação | Verificar Olá **toodashboard Pin** opção tooallow fácil rastreamento do servidor na página de painel frontal de saudação do seu portal do Azure.

  > [!IMPORTANT]
  > Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados mais tarde nesse início rápido. Lembre-se ou registre essas informações para o uso posterior.

    ![Banco de dados do Azure para PostgreSQL - Olá pick preço](./media/quickstart-create-database-portal/2-service-tier.png)

4.  Clique em **criar** tooprovision servidor de saudação. Provisionamento leva alguns minutos, o too20 minutos máximo.

5.  Na barra de ferramentas hello, clique em **notificações** toomonitor processo de implantação de saudação.
 ![Banco de Dados do Azure para PostgreSQL – Ver notificações](./media/quickstart-create-database-portal/3-notifications.png)
   
  Por padrão, o banco de dados **postgres** é criado em seu servidor. Olá [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) banco de dados é um banco de dados padrão devem ser usados pelos usuários, utilitários e aplicativos de terceiros. 

## <a name="configure-a-server-level-firewall-rule"></a>Configurar uma regra de firewall no nível de servidor

saudação de banco de dados PostgreSQL serviço cria um firewall no nível de servidor de saudação. Esse firewall impede que aplicativos externos e ferramentas conectando toohello server e bancos de dados no servidor de saudação, a menos que uma regra de firewall será criada tooopen firewall de saudação para endereços IP específicos. 

1.  Localize seu servidor após a conclusão da implantação de saudação. Se necessário, você pode pesquisar. Por exemplo, clique em **todos os recursos** do menu esquerdo hello e digite nome do servidor de saudação (como o exemplo hello *mypgserver 20170401*) toosearch para seu servidor recém-criado. Clique no nome do seu servidor listado no resultado da pesquisa hello. Olá **visão geral** página para o servidor é aberta e oferece opções de configuração adicional.
 
    ![Banco de Dados do Azure para PostgreSQL – Pesquisar o nome do servidor](./media/quickstart-create-database-portal/4-locate.png)

2.  Na página do servidor de saudação, selecione **segurança de Conexão**. 
    ![Banco de Dados do Azure para PostgreSQL - Criar Regra de firewall](./media/quickstart-create-database-portal/5-firewall-2.png)

3.  Em Olá **as regras de Firewall** título, clique na caixa de texto em branco Olá Olá **o nome da regra** toobegin coluna criar regra de firewall de saudação. 

    Para este início rápido, vamos permitir que todos os endereços IP no servidor de saudação preenchendo Olá valores a seguir na caixa de texto de saudação em cada coluna:

    Nome da Regra | IP Inicial | IP Final 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Olá superior barra de ferramentas da página de segurança de Conexão hello, clique em **salvar**. Aguarde alguns instantes e aviso Olá notificação mostrando que a atualização de segurança de conexão foi concluído com êxito antes de continuar.

    > [!NOTE]
    > Conexões tooyour banco de dados PostgreSQL servidor se comunicam pela porta 5432. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 5432 talvez não consigam pelo firewall da rede. Nesse caso, não será capaz de tooconnect tooyour server, a menos que o departamento de TI abre a porta 5432.
    >

## <a name="get-hello-connection-information"></a>Obter informações de conexão Olá

Quando criamos nosso servidor Banco de Dados do Azure para PostgreSQL, um banco de dados padrão chamado **postgres** foi criado. servidor de banco de dados de tooyour tooconnect, é necessário tooremember Olá servidor completo administrador e o nome de credenciais de logon. Você pode observou esses valores anteriormente no artigo de início rápido de saudação. Caso contrário, você pode localizar facilmente informações de nome e logon de servidor de saudação da página de visão geral do servidor de saudação na Olá portal do Azure.

1. Abra a página **Visão geral** do servidor. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**.
    Focalize o cursor sobre cada campo e ícone para copiar Olá aparece à direita de toohello do texto de saudação. Clique o ícone para copiar hello como valores de saudação toocopy necessários.

 ![Banco de Dados do Azure para PostgreSQL – Logon de administrador do servidor](./media/quickstart-create-database-portal/6-server-name.png)

## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a>Conecte-se o banco de dados de tooPostgreSQL usando psql no Shell de nuvem

Há uma série de aplicativos, você pode usar tooconnect tooyour banco de dados para o servidor PostgreSQL. Vamos primeiro usar Olá psql utilitário de linha de comando tooillustrate como tooconnect toohello server.  Você pode usar um navegador da web e Olá Shell de nuvem do Azure conforme descrito aqui sem Olá necessário tooinstall qualquer software adicional. Se você tiver um utilitário de psql Olá instalado localmente em seu próprio computador, você pode se conectar de lá também.

1. Inicie Olá Shell de nuvem do Azure através do ícone de terminal no painel de navegação superior Olá Olá.

   ![Banco de Dados do Azure para PostgreSQL – Ícone do terminal do Azure Cloud Shell](./media/quickstart-create-database-portal/7-cloud-console.png)

2. Olá Shell de nuvem do Azure é aberto no navegador, permitindo que você comandos do shell bash tootype.

   ![Banco de Dados do Azure para PostgreSQL – Prompt de bash do Azure Shell](./media/quickstart-create-database-portal/8-bash.png)

3. No prompt de Shell de nuvem hello, conecte o banco de dados de tooa no banco de dados do Azure para o servidor PostgreSQL, digitando a linha de comando psql Olá no prompt de saudação verde.

    Olá, formato a seguir é usado tooconnect tooan banco de dados para o servidor PostgreSQL com hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilitário:
    ```bash
    psql --host=<yourserver> --port=<port> --username=<server admin login> --dbname=<database name>
    ```

    Por exemplo, Olá comando a seguir conecta o servidor de exemplo tooan:

    ```bash
    psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
    ```

    parâmetro psql |Valor sugerido|Descrição
    ---|---|---
    --host | *nome do servidor* | Especifique o valor de nome de servidor de saudação que foi usado quando você criou Olá banco de dados do Azure para PostgreSQL anteriormente. Nosso servidor de exemplo mostrado é mypgserver-20170401.postgres.database.azure.com. Use o nome de domínio totalmente qualificado hello (\*. postgres.database.azure.com) conforme mostrado no exemplo hello. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se você não lembrar o nome do servidor. 
    --port | **5432** | Sempre use a porta 5432 durante a conexão de banco de dados de tooAzure para PostgreSQL. 
    --username | *nome de logon do administrador do servidor* |Digite hello servidor admin logon nome de usuário fornecido quando você criou Olá banco de dados do Azure para PostgreSQL anteriormente. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se não lembrar o nome de usuário de saudação.  formato de saudação é  *username@servername* .
    --dbname | **postgres** | Nome de banco de dados use saudação padrão gerado pelo sistema *postgres* para conexão primeiro hello. Depois, você criará seu próprio banco de dados.

    Depois de executando o comando psql hello, com seus próprios valores de parâmetro, você estará senha do administrador do servidor Olá tootype solicitada. Essa senha é Olá mesmo que você forneceu ao criar o servidor de saudação. 

    parâmetro psql |Valor sugerido|Descrição
    ---|---|---
    Senha | *sua senha do administrador* | Observe, Olá caracteres não são mostrados em bash Olá prompt de senha digitada. Pressione enter depois que você digitou todas as tooauthenticate de caracteres hello e conecte-se.

    Uma vez conectado, o utilitário de psql Olá exibe um aviso de postgres onde você digita comandos sql. Saudação inicial de conexão de saída, um aviso pode ser exibido como Olá psql em Olá Shell de nuvem do Azure pode ser uma versão diferente hello banco de dados do Azure para a versão do servidor PostgreSQL. 
    
    Exemplo de saída psql:
    ```bash
    psql (9.5.7, server 9.6.2)
    WARNING: psql major version 9.5, server major version 9.6.
        Some psql features might not work.
    SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
    Type "help" for help.
   
    postgres=> 
    ```

    > [!TIP]
    > Se o firewall Olá não está configurada tooallow Olá endereço IP hello Shell de nuvem do Azure, hello seguinte erro ocorrerá:
    > 
    > "psql: FATAL:  no pg_hba.conf entry for host "138.91.195.82", user "mylogin", database "postgres", SSL on FATAL:  SSL connection is required. Especifique as opções de SSL e tente novamente.
    > 
    > Erro de saudação tooresolve, certifique-se de que Olá servidor configuração correspondências etapas Olá Olá *configurar uma regra de firewall de nível de servidor* Olá artigo.

4.  Crie um banco de dados em branco no hello prompt digitando Olá comando a seguir:
    ```bash
    CREATE DATABASE mypgsqldb;
    ```
    comando Olá pode levar toocomplete de alguns instantes. 

5.  No prompt de hello, execute Olá após o banco de dados do comando tooswitch conexão toohello recém-criado **mypgsqldb**.
    ```bash
    \c mypgsqldb
    ```

6.  Digite \q e, em seguida, pressione ENTER tooquit psql. Quando terminar, você poderá fechar Olá Shell de nuvem do Azure.

Agora você conectou toohello banco de dados do Azure para PostgreSQL e criou um banco de dados do usuário em branco. Continue toohello próxima seção tooconnect usar outra ferramenta comum, pgAdmin.

## <a name="connect-toopostgresql-database-using-pgadmin"></a>Conecte-se o banco de dados de tooPostgreSQL usando pgAdmin

tooconnect tooAzure PostgreSQL server usando a ferramenta Olá GUI _pgAdmin_
1.  Iniciar Olá _pgAdmin_ aplicativo no computador cliente. Você pode instalar o _pgAdmin_ de http://www.pgadmin.org/.
2.  Clique em Olá **adicionar novo servidor** ícone de saudação **Links rápidos** seção center Olá Olá da página de painel.
3.  Em Olá **criar - servidor** caixa de diálogo **geral** , insira um nome amigável exclusivo para o servidor de saudação, como **Azure PostgreSQL Server**.
![ferramenta pgAdmin – criar – servidor](./media/quickstart-create-database-portal/9-pgadmin-create-server.png)
4.  Em Olá **criar - servidor** caixa de diálogo, **Conexão** guia, use as configurações de saudação conforme especificado e clique em **salvar**.
   ![pgAdmin – Criar – Servidor](./media/quickstart-create-database-portal/10-pgadmin-create-server.png)

    parâmetro pgAdmin |Valor sugerido|Descrição
    ---|---|---
    Nome/endereço do host | *nome do servidor* | Especifique o valor de nome de servidor de saudação que foi usado quando você criou Olá banco de dados do Azure para PostgreSQL anteriormente. Nosso servidor de exemplo mostrado é mypgserver-20170401.postgres.database.azure.com. Use o nome de domínio totalmente qualificado hello (\*. postgres.database.azure.com) conforme mostrado no exemplo hello. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se você não lembrar o nome do servidor. 
    Porta | **5432** | Sempre use a porta 5432 durante a conexão de banco de dados de tooAzure para PostgreSQL.  
    Manutenção do banco de dados | **postgres** | Nome de banco de dados use saudação padrão gerado pelo sistema *postgres*.
    Nome de usuário | *nome de logon do administrador do servidor* | Digite hello servidor admin logon nome de usuário fornecido quando você criou Olá banco de dados do Azure para PostgreSQL anteriormente. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se não lembrar o nome de usuário de saudação. formato de saudação é  *username@servername* .
    Senha | *sua senha do administrador* |  senha Olá escolhido quando você criou servidor Olá anteriormente neste guia de início rápido.
    Função | *deixar em branco* | Não precisa tooprovide uma função nome neste momento. Deixe o campo de saudação em branco.
    Modo SSL | Exigência | Por padrão, todos os servidores PostgreSQL do Azure são criados com a imposição de SSL ligada. tooturn desativar impondo SSL, consulte os detalhes em [impondo SSL](./concepts-ssl-connection-security.md).
    
5.  Clique em **Salvar**.
6.  No painel esquerdo do navegador hello, expanda Olá **servidores** nó. Escolha o servidor, por exemplo **Azure PostgreSQL Server** e clique em tooconnect tooit.
7. Expanda o nó do servidor de saudação e, em seguida, expanda **bancos de dados** sob ele. Olá lista deve incluir existente *postgres* banco de dados e qualquer usuário recém-criado de banco de dados, como *mypgsqldb*, criada na seção anterior hello. Observe que você pode criar vários bancos de dados por servidor com o Banco de Dados do Azure para PostgreSQL.
8. Clique duas vezes em **bancos de dados**, escolha Olá **criar** menu e clique em **banco de dados**.
9.  Digite um nome de banco de dados de sua escolha na Olá **banco de dados** campo, como *mypgsqldb* mostrado no exemplo hello. 
10. Selecione Olá **proprietário** banco de dados de saudação de caixa de lista suspensa de saudação. Escolha o nome de logon do administrador do servidor, como o nosso exemplo *mylogin*.
10. Clique em **salvar** toocreate um novo banco de dados em branco.
11. Em Olá **navegador** painel, consulte Olá banco de dados criado na lista de saudação de bancos de dados em seu nome de servidor.
 ![pgAdmin – Criar – Banco de Dados](./media/quickstart-create-database-portal/11-pgadmin-database.png)


## <a name="clean-up-resources"></a>Limpar recursos
Limpar recursos Olá criado no início rápido do hello, excluindo Olá [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md), que inclui todos os recursos de saudação no grupo de recursos de saudação ou excluindo o recurso de um servidor de saudação se desejar tookeep Olá outros recursos intactos.

> [!TIP]
> Outros inícios rápidos nessa coleção aproveitam esse início rápido. Se você planeja toocontinue toowork com subsequentes guias de início rápido, não a limpeza hello recursos criados neste guia de início rápido. Se você não planeja toocontinue, use Olá recursos de toodelete etapas criados por este guia de início rápido no portal do Azure de saudação a seguir.

grupo de recursos inteiro de saudação toodelete incluindo Olá recém-criado server:
1.  Localize o grupo de recursos no hello portal do Azure. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do grupo de recursos, como o nosso exemplo **myresourcegroup**.
2.  Na página do seu grupo de recursos, clique em **Excluir**. Tipo hello o nome de grupo de recursos, como o nosso exemplo **myresourcegroup**em Olá exclusão de tooconfirm de caixa de texto e, em seguida, clique em **excluir**.

Ou, em vez disso, Olá toodelete recém-criado server:
1.  Localize seu servidor de saudação portal do Azure, se você não estiver com ele aberto. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos**e procure o servidor de saudação que você criou.
2.  Em Olá **visão geral** , clique em Olá **excluir** botão no painel superior hello.
![Banco de Dados do Azure para PostgreSQL - Excluir servidor](./media/quickstart-create-database-portal/12-delete.png)
3.  Confirme o nome do servidor de saudação desejado toodelete e mostrar Olá bancos de dados sob ele que são afetados. Digite o nome do servidor na caixa de texto de saudação, como o nosso exemplo **mypgserver 20170401**e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas
> [!div class="nextstepaction"]
> [Migre seu banco de dados usando Exportar e Importar](./howto-migrate-using-export-and-import.md)
