---
title: aaaSecure seu banco de dados SQL do Azure | Microsoft Docs
description: "Saiba mais sobre toosecure técnicas e recursos de seu banco de dados do SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Proteger o Banco de Dados SQL do Azure

Banco de dados SQL protege seus dados por meio da limitação tooyour banco de dados usando regras de firewall, exigindo usuários tooprove sua identidade e autorização toodata por meio de permissões e associações de função, bem como por meio de mecanismos de autenticação segurança em nível de linha e mascaramento de dados dinâmicos.

Você pode melhorar a proteção de saudação do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples. Neste tutorial, você aprenderá a: 

> [!div class="checklist"]
> * Configurar regras de firewall no nível de servidor para o servidor de saudação portal do Azure
> * Configurar regras de firewall no nível do banco de dados para o seu banco de dados usando SSMS
> * Conecte-se o banco de dados de tooyour usando uma cadeia de caracteres de conexão segura
> * Gerenciar o acesso de usuário
> * Proteger seus dados com criptografia
> * Habilitar a auditoria do Banco de Dados SQL
> * Habilitar a detecção de ameaças do Banco de Dados SQL

Se você não tiver uma assinatura do Azure, [crie uma conta gratuita](https://azure.microsoft.com/free/) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial, verifique se você tem Olá a seguir:

- A versão mais recente instalada saudação do [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- O Microsoft Excel instalado
- Criado um servidor do SQL Azure e o banco de dados - consulte [criar um banco de dados do SQL Azure no portal do Azure de saudação](sql-database-get-started-portal.md), [criar um único banco de dados SQL do Azure usando Olá CLI do Azure](sql-database-get-started-cli.md), e [criar um único SQL Azure banco de dados usando o PowerShell](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Faça logon no toohello portal do Azure

Faça logon no toohello [portal do Azure](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Criar uma regra de firewall de nível de servidor no hello portal do Azure

Os banco de dados SQL são protegidos por um firewall no Azure. Por padrão, todas as conexões toohello server Olá bancos de dados e no servidor de saudação são rejeitados com exceção de conexões de outros serviços do Azure. Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).

configuração mais segura de saudação é tooset 'Permitir acesso serviços tooAzure' tooOFF. Se você precisar tooconnect toohello banco de dados de um serviço de nuvem ou VM do Azure, você deve criar um [IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md) e permitir acesso somente de saudação reservado IP endereço através do firewall do hello. 

Siga estas etapas toocreate um [regra de firewall de nível de servidor de banco de dados SQL](sql-database-firewall-configure.md) suas conexões de servidor tooallow de um endereço IP específico. 

> [!NOTE]
> Se você tiver criado um banco de dados de exemplo no Azure usando um dos tutoriais anteriores hello ou guias de início rápido e são executar este tutorial em um computador com hello mesmo endereço IP que ele tinha quando você analisou os tutoriais, você pode ignorar esta etapa, você terá já criou uma regra de firewall de nível de servidor.
>

1. Clique em **bancos de dados SQL** de saudação esquerdo menu e clique em Olá banco de dados você gostaria que regra de firewall de saudação tooconfigure para em Olá **bancos de dados SQL** página. Olá, página de visão geral para o banco de dados abre, mostrando a você Olá totalmente qualificado nome do servidor (como **mynewserver 20170313.database.windows.net**) e fornece opções de configuração adicional.

      ![regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Clique em **definir o firewall do servidor** na barra de ferramentas Olá conforme mostrado na imagem anterior hello. Olá **configurações de Firewall** página para o servidor de banco de dados SQL Olá é aberta. 

3. Clique em **Adicionar IP do cliente** Olá barra de ferramentas tooadd Olá endereço IP público do portal de toohello conectado Olá computador com ou inserir a regra de firewall Olá manualmente e, em seguida, clique em **salvar**.

      ![definir regra de firewall do servidor](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Clique em **Okey** e, em seguida, clique em Olá **X** tooclose Olá **configurações de Firewall** página.

Agora você pode conectar o banco de dados tooany no servidor de saudação com hello especificado um intervalo de endereços IP ou endereço IP.

> [!NOTE]
> O Banco de Dados SQL se comunica pela porta 1433. Se você estiver tentando tooconnect de dentro de uma rede corporativa, o tráfego de saída pela porta 1433 talvez não consigam pelo firewall da rede. Nesse caso, não será tooconnect capaz de servidor de banco de dados SQL de tooyour, a menos que o departamento de TI abre a porta 1433.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Criar uma regra de firewall no nível do banco de dados usando SSMS

Regras de firewall de nível de banco de dados permitem que você toocreate as configurações de firewall diferentes para bancos de dados diferentes em Olá mesmo firewall de servidor e toocreate lógico as regras de portátil - que significa que sigam o banco de dados de saudação durante um [failover ](sql-database-geo-replication-overview.md) em vez de serem armazenados no SQL server de saudação. Regras de firewall de nível de banco de dados só podem ser configurado usando instruções Transact-SQL e somente depois que você configurou a primeira regra de firewall de nível de servidor de saudação. Para saber mais, confira [Regras de firewall no nível do servidor e no nível do banco de dados do Banco de Dados SQL do Azure](sql-database-firewall-configure.md).

Segue essas etapas toocreate uma regra de firewall de banco de dados específico.

1. Conecte-se o banco de dados tooyour, por exemplo, usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. No Pesquisador de objetos, clique com botão direito no banco de dados de saudação desejado tooadd regra para de um firewall e clique em **nova consulta**. Uma janela de consulta em branco é aberto que é conectado tooyour banco de dados.

3. Na janela de consulta Olá, modifique Olá IP endereço tooyour endereço IP público e, em seguida, execute Olá consulta a seguir:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Na barra de ferramentas hello, clique em **Execute** toocreate regra de firewall de saudação.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Exibir como tooconnect tooyour um aplicativo de banco de dados usando uma cadeia de caracteres de conexão segura

tooensure uma conexão segura e criptografada entre um aplicativo cliente e o banco de dados SQL, a cadeia de caracteres de conexão Olá tem toobe configurado para:

- Solicitar uma conexão criptografada, e
- certificado do servidor da saudação toonot confiável. 

Isso estabelece uma conexão usando a segurança de camada de transporte (TLS) e reduz o risco de saudação de ataques man-in-the-middle. Você pode obter cadeias de caracteres de conexão configurada corretamente para seu banco de dados SQL para o cliente com suporte drivers de saudação portal do Azure conforme mostrado para ADO.net nesta captura de tela.

1. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página.

2. Em Olá **visão geral** para seu banco de dados, clique em **Mostrar cadeias de conexão de banco de dados**.

3. Saudação de revisão completa **ADO.NET** cadeia de caracteres de conexão.

    ![Cadeia de conexão do ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Criar usuários de banco de dados

Antes de criar os usuários, primeiro você deve escolher um dos dois tipos de autenticação com suporte no Banco de Dados SQL do Azure: 

**Autenticação do SQL**, que usa o nome de usuário e senha para logons e usuários que são válidos somente no contexto de um banco de dados específico dentro de um servidor lógico de hello. 

**Autenticação do Azure Active Directory**, que usa identidades gerenciadas pelo Azure Active Directory. 

Se você quiser toouse [Active Directory do Azure](./sql-database-aad-authentication.md) tooauthenticate no banco de dados SQL, um Azure Active Directory preenchida deve existir antes de prosseguir.

Siga estas etapas toocreate um usuário usando a autenticação do SQL:

1. Conecte-se o banco de dados tooyour, por exemplo, usando [SQL Server Management Studio](./sql-database-connect-query-ssms.md) usando suas credenciais de administrador do servidor.

2. No Pesquisador de objetos, clique com botão direito no banco de dados de saudação desejado tooadd um novo usuário em e clique em **nova consulta**. Uma janela de consulta em branco é aberto que é conectado toohello banco de dados selecionado.

3. Na janela de consulta hello, digite Olá consulta a seguir:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Na barra de ferramentas hello, clique em **Execute** toocreate usuário de saudação.

5. Por padrão, o usuário de Olá pode se conectar a banco de dados toohello, mas não tem permissões tooread ou gravar dados. toogrant toohello essas permissões usuário recém-criado, execute Olá dois comandos em uma nova janela de consulta a seguir

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

É melhor toocreate prática essas contas não-administrador no hello tooyour de tooconnect de nível de banco de dados do banco de dados, a menos que você precisa tooexecute tarefas do administrador como a criação de novos usuários. Analise Olá [tutorial do Active Directory do Azure](./sql-database-aad-authentication-configure.md) sobre como tooauthenticate usando o Active Directory do Azure.


## <a name="protect-your-data-with-encryption"></a>Proteger seus dados com criptografia

Criptografia de dados transparente de banco de dados SQL do Azure (TDE) criptografa automaticamente os dados em repouso, sem a necessidade de quaisquer alterações toohello aplicativo acessando Olá banco de dados criptografado. Para bancos de dados recém-criados, a TDE estará ativada por padrão. tooenable TDE para seu banco de dados ou tooverify TDE está ativada, siga estas etapas:

1. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 

2. Clique em **criptografia transparente de dados** tooopen página de configuração de saudação para TDE.

    ![Transparent Data Encryption](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Se necessário, defina **criptografia de dados** tooON e clique em **salvar**.

Inicia o processo de criptografia Olá no plano de fundo de saudação. Você pode monitorar o progresso de saudação pelo banco de dados usando conexão tooSQL [SQL Server Management Studio](./sql-database-connect-query-ssms.md) consultando a coluna encryption_state Olá Olá `sys.dm_database_encryption_keys` exibição.

## <a name="enable-sql-database-auditing-if-necessary"></a>Habilitar a auditoria do Banco de Dados SQL, se for necessário

Auditoria de banco de dados SQL Azure rastreia eventos de banco de dados e grava o log de auditoria tooan em sua conta de armazenamento do Azure. A auditoria pode ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar potenciais violações de segurança. Siga essas etapas toocreate uma política de auditoria padrão do banco de dados SQL:

1. Selecione **bancos de dados SQL** no menu esquerdo do hello e clique em seu banco de dados em Olá **bancos de dados SQL** página. 

2. Na folha de configurações hello, selecione **auditoria e detecção de ameaças**. Observe que a auditoria de nível de servidor é diabled e que haja um **exibir configurações de servidor** link que permite que você tooview ou modificar configurações de auditoria de servidor de saudação neste contexto.

    ![Folha Auditoria](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Se você preferir tooenable uma auditoria tipo (ou local?) diferente da saudação especificada no nível do servidor de saudação, ativar **ON** auditoria e escolha Olá **Blob** tipo de auditoria. Se o servidor Blob auditoria estiver habilitada, auditoria de banco de dados configurado Olá existirá lado a lado com a auditoria de Blob do servidor de saudação.

    ![Ativar a auditoria](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Selecione **detalhes armazenamento** tooopen Olá folha de armazenamento de Logs de auditoria. Conta de armazenamento do Azure hello selecione onde os logs serão salvas e período de retenção hello, após o qual Olá logs antigos serão excluídos, clique em **Okey** na parte inferior da saudação. 

   > [!TIP]
   > Use Olá a mesma conta de armazenamento para todos os Olá de tooget auditados bancos de dados máximo Olá auditoria modelos de relatórios.
   > 

5. Clique em **Salvar**.

> [!IMPORTANT]
> Se você quiser toocustomize eventos de saudação auditado, você pode fazer isso por meio do PowerShell ou REST API - consulte Olá [automação (PowerShell / API REST)](sql-database-auditing.md#subheading-7) seção para obter mais detalhes.
>

## <a name="enable-sql-database-threat-detection"></a>Habilitar a detecção de ameaças do Banco de Dados SQL

A detecção de ameaças fornece uma nova camada de segurança, que permite que os clientes toodetect e responde a ameaças de toopotential conforme elas ocorrem, fornecendo alertas de segurança em atividades anormais. Os usuários podem explorar eventos suspeitos hello, usando a auditoria de banco de dados do SQL toodetermine se eles são provenientes de um tooaccess tentativa, violação ou exploram dados no banco de dados de saudação. A detecção de ameaças torna simples tooaddress potenciais ameaças toohello banco de dados sem a necessidade de saudação toobe um especialista em segurança ou gerenciar os sistemas de monitoramento de segurança avançada.
Por exemplo, a Detecção de Ameaças detecta determinadas atividades anormais do banco de dados que indicam possíveis tentativas de injeção de SQL. Injeção de SQL é um dos Olá Web aplicativo problemas de segurança comuns em Olá Internet, os aplicativos usados tooattack controladas por dados. Os invasores tirar proveito de aplicativo vulnerabilidades tooinject de instruções SQL mal-intencionadas nos campos de entrada do aplicativo, para serem violados ou modificar dados no banco de dados de saudação.

1. Navegue toohello folha de configuração de saudação deseja toomonitor do banco de dados do SQL. Na folha de configurações hello, selecione **auditoria e detecção de ameaças**.

    ![Painel de navegação](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. Em Olá **auditoria e detecção de ameaças** configuração folha ativar **ON** auditoria, que exibirá as configurações de detecção de ameaças hello.

3. **ATIVE** a detecção de ameaças.

4. Configure Olá lista de endereços de email que receberão alertas de segurança após a detecção de atividades anormais de banco de dados.

5. Clique em **salvar** em Olá **detecção de auditoria e ameaças** toosave folha Olá nova ou atualizada política de detecção de ameaças e auditoria.

    ![Painel de navegação](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Se forem detectadas atividades anormais de banco de dados, você receberá uma notificação por email na detecção das atividades anormais do banco de dados. email Olá fornecerá informações sobre eventos de segurança suspeitos Olá incluindo natureza Olá de atividades anormais Olá, nome do banco de dados, a hora de evento de nome e hello do servidor. Além disso, ele fornecerá informações sobre possíveis causas e recomendado tooinvestigate ações e reduzir Olá potenciais ameaças toohello banco de dados de. exame de etapas Avançar Olá você através do qual toodo você deve receber um email:

    ![Email de detecção de ameaças](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. No email de saudação, clique em Olá **o Log de auditoria do SQL Azure** link, o que iniciará Olá portal do Azure e exibir registros de auditoria relevantes Olá em torno de tempo de saudação do evento suspeitas Olá.

    ![Registros de auditoria](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Clique em tooview de registros de auditoria hello mais detalhes sobre atividades de banco de dados suspeito hello, como a instrução SQL, IP de cliente e o motivo da falha.

    ![Detalhes do registro](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Na folha de registros de auditoria de saudação, clique em **abrir no Excel** tooopen previamente configurada do excel tooimport de modelo e executar uma análise mais profunda do log de auditoria Olá em torno de tempo de saudação do evento suspeitas hello.

    > [!NOTE]
    > No Excel 2010 ou posterior, o Power Query e Olá **combinação rápida** configuração é necessária.

    ![Abrir registros no Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. Olá tooconfigure **combinação rápida** configuração - no hello **POWER QUERY** guia de faixa de opções, selecione **opções** toodisplay caixa de diálogo de opções de saudação. Selecione a seção de privacidade hello e escolha Olá segunda opção - 'Ignorar Olá níveis de privacidade e potencialmente melhorar o desempenho':

    ![Combinação Rápida do Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. logs de auditoria do SQL tooload, verifique se Olá parâmetros na guia Configurações de saudação estão definidos corretamente e, em seguida, selecione a faixa de opções de 'Dados' hello e clique o botão 'Atualizar tudo' hello.

    ![Parâmetros do Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. resultados de saudação aparecem na Olá **os Logs de auditoria do SQL** folha que permite que você toorun uma análise mais profunda de atividades anormais de saudação que foram detectadas e reduzir o impacto de saudação do evento de segurança de saudação em seu aplicativo.


## <a name="next-steps"></a>Próximas etapas
Você pode melhorar a proteção de saudação do banco de dados contra usuários mal-intencionados ou acesso não autorizado com apenas algumas etapas simples. Neste tutorial, você aprenderá a: 

> [!div class="checklist"]
> * Configurar regras de firewall para seu servidor e/ou banco de dados
> * Conecte-se o banco de dados de tooyour usando uma cadeia de caracteres de conexão segura
> * Gerenciar o acesso de usuário
> * Proteger seus dados com criptografia
> * Habilitar a auditoria do Banco de Dados SQL
> * Habilitar a detecção de ameaças do Banco de Dados SQL

> [!div class="nextstepaction"]
>[Melhore o desempenho do banco de dados SQL](sql-database-performance-tutorial.md)

