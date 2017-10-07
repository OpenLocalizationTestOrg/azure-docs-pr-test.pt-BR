---
title: "Início rápido: criar servidor do Banco de Dados do Azure para MySQL – Portal do Azure | Microsoft Docs"
description: "Esta etapa artigo você usando Olá tooquickly portal do Azure cria um banco de dados de exemplo para MySQL server em cerca de cinco minutos."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Criar um servidor de Banco de Dados do Azure para MySQL usando o portal do Azure
Banco de dados do Azure para MySQL é um serviço gerenciado que permite que você toorun, gerenciar e dimensionar os bancos de dados MySQL altamente disponíveis na nuvem hello. Este guia de início rápido mostra como toocreate um Azure banco de dados para o servidor MySQL usando Olá portal do Azure em cerca de cinco minutos. 

Se você não tiver uma assinatura do Azure, crie uma conta [gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure
Abra seu navegador da web e navegue toohello [portal do Microsoft Azure](https://portal.azure.com/). Insira sua credenciais toosign no portal de toohello. exibição padrão de saudação é seu painel de serviço.

## <a name="create-azure-database-for-mysql-server"></a>Criar um servidor de Banco de Dados do Azure para MySQL
Um Banco de Dados do Azure para o servidor MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md). Olá servidor será criado dentro de um [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md).

Siga essas etapas toocreate um banco de dados do Azure para o servidor MySQL:

1. Clique em Olá **novo** botão (+) localizado no canto superior esquerdo de saudação do hello portal do Azure.

2. Selecione **bancos de dados** de saudação **novo** página e selecione **banco de dados do Azure para MySQL** de saudação **bancos de dados** página. Você também pode digitar **MySQL** em Olá novo página caixa toofind Olá serviço de pesquisa.
![Portal do Azure – novo – banco de dados – MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Preencha novo formulário de detalhes de servidor Olá com hello seguintes informações, conforme mostrado na saudação anterior imagem:

    **Configuração** | **Valor sugerido** | **Descrição do Campo** 
    ---|---|---
    Nome do servidor | myserver4demo | Escolha um nome exclusivo que identifica o Banco de Dados do Azure para o servidor MySQL. o nome de domínio Olá *mysql.database.azure.com* é fornecer para tooconnect de aplicativos para nome do servidor de toohello anexado. nome do servidor de saudação pode conter apenas letras minúsculas, números e caracteres de hífen (-) hello e ele deve conter de 3 a 63 caracteres.
    Assinatura | Sua assinatura | Olá assinatura do Azure que você deseja toouse para o servidor. Se você tiver várias assinaturas, escolha assinatura apropriada hello, no qual o recurso de saudação é cobrado para.
    Grupo de recursos | myresourcegroup | Você pode criar um novo nome do grupo de recursos ou usar um existente de sua assinatura.
    Logon de administrador do servidor | myadmin | Verifique sua própria toouse de conta de logon ao conectar-se o servidor toohello. nome de logon de administrador Olá não pode ser 'azure_superuser', 'admin', 'Administrador', 'root', 'Convidado' ou 'public'.
    Senha | *Sua escolha* | Crie uma nova senha para a conta de administrador do servidor de saudação. Deve conter de 8 caracteres too128. Sua senha deve conter caracteres de três categorias a seguir de saudação – maiusculas letras, letras minúsculas, números (0-9) e caracteres não alfanuméricos (!, $, #, %, etc.).
    Confirmar senha | *Sua escolha*| Confirme a senha da conta de administrador hello.
    Local | *Olá região mais próxima tooyour os usuários*| Escolha o local de saudação usuários mais próximos de tooyour ou outros aplicativos do Azure.
    Versão | *Escolha a versão mais recente da saudação*| Escolha a versão mais recente do hello, a menos que você tem requisitos específicos.
    Camada de preços | **Básico**, **50 Unidades de Computação** **50 GB** | Clique em **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo banco de dados. Escolha **camada básica** na guia Olá na parte superior da saudação. Clique em extremidade esquerda Olá Olá **unidades de computação** toohello de valor do controle deslizante tooadjust Olá menos valor disponível para este guia de início rápido. Clique em **Okey** toosave Olá seleção da camada de preços. Consulte Olá captura de tela a seguir.
    PIN toodashboard | Verificação | Verificar Olá **toodashboard Pin** opção tooallow fácil rastreamento do servidor na página de painel frontal de saudação do seu portal do Azure.

    > [!IMPORTANT]
    > Olá administrador logon e senha que você especificar aqui são toolog necessária no servidor de toohello e seus bancos de dados posteriormente neste guia de início rápido. Lembre-se ou registre essas informações para o uso posterior.
    > 

    ![Portal do Azure - criar MySQL, fornecendo a entrada de formulário Olá necessária](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Clique em **criar** tooprovision servidor de saudação. Provisionamento leva alguns minutos, o too20 minutos máximo.
   
5.  Na barra de ferramentas hello, clique em **notificações** processo de implantação (ícone de sino) toomonitor hello.

## <a name="configure-a-server-level-firewall-rule"></a>Configurar uma regra de firewall no nível de servidor

saudação de banco de dados do Azure para o serviço MySQL cria um firewall no nível de servidor de saudação. Esse firewall impede que aplicativos externos e ferramentas conectando toohello server e bancos de dados no servidor de saudação, a menos que uma regra de firewall será criada tooopen firewall de saudação para endereços IP específicos. 

1.  Localize seu servidor após a conclusão da implantação de saudação. Se necessário, você pode pesquisar. Por exemplo, clique em **todos os recursos** do menu esquerdo hello e digite nome do servidor de saudação (como o exemplo hello *myserver4demo*) toosearch para seu servidor recém-criado. Clique no nome do seu servidor listado no resultado da pesquisa hello. Olá **visão geral** página para o servidor é aberta e oferece opções de configuração adicional.

2. Na página do servidor de saudação, selecione **segurança de Conexão**.

3.  Em Olá **as regras de Firewall** título, clique na caixa de texto em branco Olá Olá **o nome da regra** toobegin coluna criar regra de firewall de saudação. 

    Para este guia de início rápido, vamos permitir que todos os endereços IP no servidor de saudação preenchendo Olá valores a seguir na caixa de texto de saudação em cada coluna:

    Nome da Regra | IP Inicial | IP Final 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Na barra de ferramentas superior de Olá Olá **segurança de Conexão** , clique em **salvar**. Aguarde alguns instantes e aviso Olá notificação mostrando que a atualização de segurança de conexão foi concluído com êxito antes de continuar.

    > [!NOTE]
    > Conexões tooAzure banco de dados MySQL se comunicam pela porta 3306. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 3306 talvez não consigam pelo firewall da rede. Nesse caso, não será capaz de tooconnect tooyour server, a menos que o departamento de TI abre a porta 3306.
    > 

## <a name="get-hello-connection-information"></a>Obter informações de conexão Olá
servidor de banco de dados de tooyour tooconnect, é necessário tooremember Olá servidor completo administrador e o nome de credenciais de logon. Você pode observou esses valores anteriormente no artigo de início rápido de saudação. Caso contrário, você pode localizar facilmente servidor Olá informações de nome e logon do servidor de saudação **visão geral** página ou hello **propriedades** página Olá portal do Azure.

1. Abra a página **Visão geral** do servidor. Anote Olá **nome do servidor** e **nome de logon do administrador de servidor**. 
    Focalize o cursor sobre cada campo e ícone para copiar Olá aparece à direita de toohello do texto de saudação. Clique o ícone para copiar hello como valores de saudação toocopy necessários.

    Neste exemplo, o nome do servidor de saudação é *myserver4demo.mysql.database.azure.com*, e o logon de administrador do servidor de saudação é  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Conecte-se tooMySQL usando a ferramenta de linha de comando do mysql
Há uma série de aplicativos, você pode usar tooconnect tooyour banco de dados do Azure para o MySQL server. Vamos primeiro usar Olá [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) de linha de comando ferramenta tooillustrate como tooconnect toohello server.  Você pode usar um navegador da web e Olá Shell de nuvem do Azure conforme descrito aqui sem Olá necessário tooinstall qualquer software adicional. Se você tiver um utilitário de mysql Olá instalado localmente em seu próprio computador, você pode se conectar de lá também.

1. Iniciar Olá Shell de nuvem do Azure por meio do ícone de terminal hello (> _) no hello parte superior direita da saudação página da web do portal do Azure.

2. Olá Shell de nuvem do Azure é aberto no navegador, permitindo que você comandos do shell bash tootype.

    ![Prompt de comando – exemplo de linha de comando mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. No prompt de Shell de nuvem hello, conecte-se tooyour banco de dados do Azure para o MySQL server, digitando a linha de comando do mysql Olá no prompt de saudação verde.

    Olá formato a seguir é usado tooconnect tooan banco de dados do Azure para o MySQL server com o utilitário de mysql hello:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Por exemplo, Olá comando a seguir conecta o servidor de exemplo tooour:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    parâmetro mysql |Valor sugerido|Descrição
    ---|---|---
    --host | *nome do servidor* | Especifique o valor de nome de servidor de saudação que foi usado quando você criou Olá banco de dados do Azure para MySQL anteriormente. Nosso servidor de exemplo mostrado é myserver4demo.mysql.database.azure.com. Use o nome de domínio totalmente qualificado hello (\*. mysql.database.azure.com) conforme mostrado no exemplo hello. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se você não lembrar o nome do servidor. 
    --user | *nome de logon do administrador do servidor* |Digite hello servidor admin logon nome de usuário fornecido quando você criou Olá banco de dados do Azure para MySQL anteriormente. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se não lembrar o nome de usuário de saudação.  formato de saudação é  *username@servername* .
    --password | *aguarde até a solicitação* | Você será solicitado muito "Digite a senha" depois que você insira o comando hello. Quando solicitado, digite Olá mesma senha que você forneceu ao criar o servidor de saudação.  Saudação de Observação digitado senha caracteres não são mostrados em bash Olá prompt quando digitá-los. Pressione enter depois que você digitou todas as tooauthenticate de caracteres hello e conecte-se.

   Uma vez conectado, o utilitário de mysql Olá exibe um `mysql>` solicitar que você tootype comandos. 

    Exemplo de saída de mysql:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Se o firewall Olá não está configurada tooallow Olá endereço IP hello Shell de nuvem do Azure, hello seguinte erro ocorrerá:
    >
    > Erro 2003 (28000): O cliente com endereço IP 123.456.789.0 não é permitido tooaccess servidor de saudação.
    >
    > Erro de saudação tooresolve, certifique-se de que Olá servidor configuração correspondências etapas Olá Olá *configurar uma regra de firewall de nível de servidor* Olá artigo.

4. Modo servidor status tooensure Olá conexão estará funcional. Tipo `status` no mysql hello > Solicitar depois que ele está conectado.
    ```sql
    status
    ```

   > [!TIP]
   > Para saber mais sobre outros comandos, veja [Manual de Referência do MySQL 5.7 – Capítulo 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Criar um banco de dados em branco no mysql hello > prompt digitando Olá comando a seguir:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    comando Olá pode levar toocomplete de alguns instantes. 

    Dentro de um banco de dados do Azure para o servidor MySQL, você pode criar um ou mais bancos de dados. Você pode aceitar toocreate um único banco de dados por servidor tooutilize todos os recursos de hello, ou criar tooshare de bancos de dados de vários recursos hello. Não há nenhum toohello limitar o número de bancos de dados que podem ser criadas, mas vários bancos de dados compartilham Olá mesmos recursos de servidor. 

6. Listar bancos de dados Olá no mysql hello > prompt digitando Olá comando a seguir:

    ```sql
    SHOW DATABASES;
    ```

7.  Tipo `\q` e, em seguida, pressione ferramenta de mysql ENTER tooquit hello. Quando terminar, você poderá fechar Olá Shell de nuvem do Azure.

Agora você conectou toohello banco de dados do Azure para MySQL e criou um banco de dados do usuário em branco. Continuar toohello toorepeat próximo da seção um toohello de tooconnect exercício semelhante mesmo servidor usar outra ferramenta comuns, MySQL Workbench.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Conecte-se o servidor toohello usando a ferramenta de GUI do MySQL Workbench Olá
tooconnect tooAzure MySQL server usando a ferramenta de saudação GUI MySQL Workbench:

1.  Inicie Olá aplicativo MySQL Workbench no computador cliente. É possível baixar e instalar o MySQL Workbench [aqui](https://dev.mysql.com/downloads/workbench/).

2.  Em **Conexão nova instalação** caixa de diálogo, digite Olá seguintes informações sobre **parâmetros** guia:

    ![configurar nova conexão](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Configuração** | **Valor sugerido** | **Descrição do Campo** |
    |---|---|---|
    |   Nome da Conexão | Conexão de demonstração | Especifique um rótulo para essa conexão. |
    | Método de Conexão | Padrão (TCP/IP) | Padrão (TCP/IP) é suficiente. |
    | Nome do host | *nome do servidor* | Especifique o valor de nome de servidor de saudação que foi usado quando você criou Olá banco de dados do Azure para MySQL anteriormente. Nosso servidor de exemplo mostrado é myserver4demo.mysql.database.azure.com. Use o nome de domínio totalmente qualificado hello (\*. mysql.database.azure.com) conforme mostrado no exemplo hello. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se você não lembrar o nome do servidor.  |
    | Porta | 3306 | Sempre use a porta 3306 durante a conexão tooAzure banco de dados para MySQL. |
    | Nome de Usuário |  *nome de logon do administrador do servidor* | Digite hello servidor admin logon nome de usuário fornecido quando você criou Olá banco de dados do Azure para MySQL anteriormente. Nosso nome de usuário de exemplo é myadmin@myserver4demo. Siga etapas Olá Olá seção tooget Olá conexão as informações anteriores se não lembrar o nome de usuário de saudação. formato de saudação é  *username@servername* .
    | Senha | sua senha | Clique em armazenar no cofre de senha do botão toosave hello.... |

    Clique em **Conexão de teste** tootest se todos os parâmetros estão configurados corretamente. Clique em toosave Okey Olá conexão. 

    > [!NOTE]
    > SSL é imposto por padrão em seu servidor e requer configuração adicional no pedido tooconnect com êxito. Consulte [conectividade de configurar SSL em seu aplicativo toosecurely tooAzure banco de dados de conexão para MySQL](./howto-configure-ssl.md).  Se você quiser toodisable SSL para este guia de início rápido, visite Olá portal do Azure e clique em Olá Conexão segurança página toodisable Olá impor SSL conexão botão de alternância.

## <a name="clean-up-resources"></a>Limpar recursos
Limpar recursos Olá criado no início rápido do hello, excluindo Olá [grupo de recursos do Azure](../azure-resource-manager/resource-group-overview.md), que inclui todos os recursos de saudação no grupo de recursos de saudação ou excluindo o recurso de um servidor de saudação se desejar tookeep Olá outros recursos intactos.

> [!TIP]
> Outros Guias de Início Rápido na coleção aproveitam este Guia de Início Rápido. Se você planeja toocontinue toowork com subsequentes guias de início rápido, não a limpeza hello recursos criados neste guia de início rápido. Se você não planeja toocontinue, use Olá seguindo as etapas toodelete todos os recursos criados por este guia de início rápido no portal do Azure de saudação.
>

grupo de recursos inteiro de saudação toodelete incluindo Olá recém-criado server:
1.  Localize o grupo de recursos no hello portal do Azure. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do grupo de recursos, como o nosso exemplo **myresourcegroup**.
2.  Na página do seu grupo de recursos, clique em **Excluir**. Tipo hello o nome de grupo de recursos, como o nosso exemplo **myresourcegroup**em Olá exclusão de tooconfirm de caixa de texto e, em seguida, clique em **excluir**.

Ou, em vez disso, Olá toodelete recém-criado server:
1.  Localize seu servidor de saudação portal do Azure, se você não estiver com ele aberto. No menu esquerdo de saudação no portal do Azure, clique em **todos os recursos**e procure o servidor de saudação que você criou.
2.  Em Olá **visão geral** , clique em Olá **excluir** botão no painel superior hello.
![Banco de Dados do Azure para MySQL - Excluir servidor](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Confirme o nome do servidor de saudação desejado toodelete e mostrar Olá bancos de dados sob ele que são afetados. Digite o nome do servidor na caixa de texto de saudação, como o nosso exemplo **myserver4demo**e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar seu primeiro Banco de Dados do Azure para o banco de dados do MySQL](./tutorial-design-database-using-portal.md)

