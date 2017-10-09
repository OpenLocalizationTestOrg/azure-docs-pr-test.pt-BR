---
title: "autenticação do Active Directory do Azure aaaConfigure - SQL | Microsoft Docs"
description: "Saiba como tooconnect tooSQL banco de dados e SQL Data Warehouse usando a autenticação do Active Directory do Azure."
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configurar e gerenciar o Azure Active Directory para autenticação com o Banco de Dados SQL ou o SQL Data Warehouse

Este artigo mostra como toocreate e preencher o AD do Azure e, em seguida, usar o Azure AD com o banco de dados do SQL Azure e SQL Data Warehouse. Para obter uma visão geral, consulte [Autenticação do Azure Active Directory](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Conectando tooSQL Server em execução em uma VM do Azure não tem suporte com uma conta do Active Directory do Azure. Use um conta de domínio do Active Directory.

## <a name="create-and-populate-an-azure-ad"></a>Criar e popular um Azure AD
Crie um Azure AD e popule-o com usuários e grupos. O AD do Azure pode ser saudação inicial do AD do Azure gerenciados domínio. O AD do Azure também pode ser um local Active Directory Domain Services que é federado com hello AD do Azure.

Para obter mais informações, consulte [integrando suas identidades locais ao Active Directory do Azure](../active-directory/active-directory-aadconnect.md), [adicionar seu próprio nome de domínio tooAzure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure agora oferece suporte à Federação com Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [administrando seu diretório do AD do Azure](https://msdn.microsoft.com/library/azure/hh967611.aspx), [gerenciar o AD do Azure usando o Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), e [identidade híbrida Portas e protocolos necessários](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Opcional: Associar ou alterar Olá active directory que está associado a sua assinatura do Azure
tooassociate seu banco de dados com o diretório de saudação do AD do Azure para sua organização, verifique a directory Olá um diretório confiável para Olá assinatura do Azure hospedagem Olá banco de dados. Para saber mais sobre as assinaturas do Azure, consulte [Como as assinaturas do Azure são associadas ao Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx).

**Informações adicionais:** cada assinatura do Azure tem uma relação de confiança com uma instância do AD do Azure. Isso significa que ele confia esse diretório tooauthenticate usuários, serviços e dispositivos. Várias assinaturas podem confiar Olá mesmo diretório, mas uma assinatura confia em apenas um diretório. Você pode ver o diretório que é confiável para sua assinatura sob Olá **configurações** guia em [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Essa relação de confiança que tem uma assinatura com um diretório é diferente de relacionamento de saudação que tem uma assinatura com todos os outros recursos do Azure (sites, bancos de dados e assim por diante), que são mais como recursos filho de uma assinatura. Se uma assinatura expira, e depois tentar acessar outros recursos associados à assinatura de saudação de toothose também será interrompido. Mas Olá diretório permanece no Azure, e você pode associar outra assinatura esse diretório e continuar a usuários de diretório Olá toomanage. Para obter mais informações sobre recursos, consulte [Noções básicas sobre o acesso a recursos no Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Olá procedimentos a seguir mostram como toochange Olá associado diretório para uma determinada assinatura.
1. Conecte-se tooyour [Portal clássico do Azure](https://manage.windowsazure.com/) usando o administrador da assinatura do Azure.
2. Na faixa de saudação à esquerda, selecione **configurações**.
3. Sua assinatura será exibida na tela de configurações de saudação. Se Olá desejado a assinatura não aparece, clique em **assinaturas** na parte superior do hello, lista suspensa Olá **filtro pelo diretório** caixa e selecione Olá diretório que contém suas assinaturas e, em seguida, clique em **Aplicar**.
   
    ![selecione a assinatura][4]
4. Em Olá **configurações** área, clique em sua assinatura e, em seguida, clique em **Editar diretório** final Olá Olá página.
   
    ![ad-settings-portal][5]
5. Em Olá **Editar diretório** caixa, selecione Olá Active Directory do Azure que está associado com o SQL Server ou SQL Data Warehouse e, em seguida, clique em seta Olá para Avançar.
   
    ![edit-directory-select][6]
6. Em Olá **confirmar** diretório de caixa de diálogo mapeamento, confirme se "**todos os coadministradores serão removidos.**"
   
    ![edit-directory-confirm][7]
7. Clique em Olá seleção tooreload Olá portal.

   > [!NOTE]
   > Quando alterar diretório hello, administradores tooall acesso, os usuários do AD do Azure e grupos e os usuários de diretório reserva recursos são removidos e não têm mais acesso toothis assinatura ou seus recursos. Somente, como um administrador de serviço, pode configurar o acesso para entidades de segurança com base no novo diretório de saudação. Essa alteração pode levar uma quantidade significativa de recursos do tempo toopropagate tooall. Alterando o diretório de hello, também alterações Olá administrador do AD do Azure para o banco de dados SQL e SQL Data Warehouse e não permitir acesso de banco de dados para usuários do AD do Azure existentes. administração de saudação do AD do Azure deve ser redefinição (conforme descrito abaixo) e do Azure AD usuários devem ser criados.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Criar um administrador do Azure AD para o Azure SQL Server
Cada servidor do SQL Azure (que hospeda um banco de dados SQL ou o SQL Data Warehouse) começa com uma conta de administrador de servidor único é administrador Olá Olá inteiro do Azure do SQL server. Um segundo administrador do SQL Server deve ser criado, que é uma conta do Azure AD. Essa entidade é criada como um usuário de banco de dados contido no banco de dados mestre hello. Como administrador, contas de administrador do servidor de saudação são membros de saudação **db_owner** função em todos os usuários de banco de dados e insira cada banco de dados do usuário como Olá **dbo** usuário. Para obter mais informações sobre contas de administrador do servidor de saudação, consulte [Gerenciando bancos de dados e logons no banco de dados do SQL Azure](sql-database-manage-logins.md).

Ao usar o Active Directory do Azure com replicação geográfica, administrador do Active Directory do Azure Olá deve ser configurado para Olá primário e os servidores secundários hello. Se um servidor não tem um administrador do Active Directory do Azure, em seguida, usuários e logons do Active Directory do Azure receberá um erro de tooserver "Não é possível conectar".

> [!NOTE]
> Os usuários que não são baseados em uma conta do AD do Azure (incluindo a conta de administrador do hello Azure SQL server), não é possível criar usuários baseado no AD do Azure, porque eles não têm permissão toovalidate proposto usuários de banco de dados com hello AD do Azure.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Provisionar um administrador do Azure Active Directory para o Azure SQL Server

Olá dois procedimentos a seguir mostra como tooprovision um administrador do Active Directory do Azure para seu servidor do SQL Azure no portal do Azure de saudação e usando o PowerShell.

### <a name="azure-portal"></a>Portal do Azure
1. Em Olá [portal do Azure](https://portal.azure.com/), no canto superior direito de hello, clique toodrop sua conexão abaixo uma lista de possíveis Active Directories. Escolha Olá corrigir do Active Directory como o padrão de saudação do AD do Azure. Essa etapa links Olá assinatura associação com o Active Directory com o servidor do SQL Azure certificando-se de que Olá a mesma assinatura que é usada para o AD do Azure e SQL Server. (hello Azure do SQL server pode hospedar o banco de dados do SQL Azure ou Azure SQL Data Warehouse.)   
    ![choose-ad][8]   
    
2. Em Olá deixado selecione faixa **servidores SQL**, selecione seu **do SQL server**e, em seguida, em Olá **do SQL Server** folha, clique em **administrador do Active Directory**.   
3. Em Olá **administrador do Active Directory** folha, clique em **definir o administrador**.   
    ![selecionar active directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. Em Olá **Adicionar administrador** folha, pesquisar um usuário, usuário Olá select ou toobe grupo um administrador e, em seguida, clique em **selecione**. (folha de administração do Active Directory Olá mostra todos os membros e grupos do Active Directory. Usuários ou grupos que estão esmaecidos não podem ser selecionados porque eles não têm suporte como administradores do AD do Azure. (Consulte lista de saudação do grupo Administradores com suporte no hello **recursos do AD do Azure e limitações** seção [uso do Azure autenticação do Active Directory para autenticação com o banco de dados SQL ou SQL Data Warehouse](sql-database-aad-authentication.md).) Controle de acesso baseado em função (RBAC) aplica-se apenas toohello portal e não é propagado tooSQL Server.   
    ![selecionar administrador](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Na parte superior de saudação do hello **administrador do Active Directory** folha, clique em **salvar**.   
    ![salvar administrador](./media/sql-database-aad-authentication/save-admin.png)   

processo de saudação do alterar Olá administrador pode levar vários minutos. Novo administrador do hello será exibido no hello **administrador do Active Directory** caixa.

   > [!NOTE]
   > Ao configurar o administrador de saudação do AD do Azure, Olá novo administrador nome (usuário ou grupo) não pode já estar presente no banco dados mestre virtual hello como um usuário de autenticação do SQL Server. Se estiver presente, a instalação de administração do AD do Azure Olá falhará; Revertendo a sua criação e indicando que tais um administrador (nome) já existirem. Como tal um usuário de autenticação do SQL Server não é parte de saudação do AD do Azure, qualquer servidor de toohello tooconnect esforço usando a autenticação do AD do Azure falhará.
   > 


toolater remover um administrador, na parte superior de saudação do hello **administrador do Active Directory** folha, clique em **remover administrador**e, em seguida, clique em **salvar**.

### <a name="powershell"></a>PowerShell
toorun cmdlets do PowerShell, você precisa toohave Azure PowerShell instalado e em execução. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

tooprovision um administrador do AD do Azure, execute Olá comandos do Azure PowerShell a seguir:

* Add-AzureRmAccount
* Select-AzureRmSubscription

Cmdlets usados tooprovision e gerenciar a administração do AD do Azure:

| Nome do cmdlet | Descrição |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Provisiona um administrador do Azure Active Directory para o Azure SQL Server ou o SQL Data Warehouse do Azure. (Deve ser da assinatura atual Olá). |
| [Remove-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Remove um administrador do Azure Active Directory para o Azure SQL Server ou para o SQL Data Warehouse do Azure. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Retorna informações sobre um administrador do Active Directory do Azure atualmente configurado para hello Azure do SQL server ou do Azure SQL Data Warehouse. |

Use o comando get-help toosee mais detalhes para cada um desses comandos, por exemplo do PowerShell ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Olá seguindo disposições de script nomeado de um grupo de administradores do AD do Azure **DBA_Group** (id de objeto `40b79501-b343-44ed-9ce7-da4c8cc7353f`) para Olá **demo_server** servidor em um grupo de recursos denominado **23 de grupo** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Olá **DisplayName** parâmetro de entrada aceita o nome de exibição de saudação do AD do Azure ou Olá Nome Principal do usuário. Por exemplo, ``DisplayName="John Smith"`` e ``DisplayName="johns@contoso.com"``. Olá somente do AD do Azure grupos do AD do Azure há suporte para o nome de exibição.

> [!NOTE]
> saudação de comando do PowerShell do Azure ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` não impede que você provisionar administradores do AD do Azure para usuários sem suporte. Um usuário sem suporte pode ser provisionado, mas não é possível conectar o banco de dados tooa. 
> 

Olá, exemplo a seguir usa Olá opcional **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Olá AD do Azure **ObjectID** é necessária quando hello **DisplayName** não é exclusivo. Olá tooretrieve **ObjectID** e **DisplayName** valores, use a seção do Active Directory de saudação do Portal clássico do Azure e exibir propriedades de saudação de um usuário ou grupo.
> 

saudação de exemplo a seguir retorna informações sobre administração Olá atual do AD do Azure para o Azure SQL server:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

saudação de exemplo a seguir remove um administrador do AD do Azure:

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

Você também pode provisionar um administrador do Active Directory do Azure usando Olá APIs REST. Para saber mais, confira [Referência da API REST de Gerenciamento de Serviços e Operações de Bancos de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
Você também pode oferecer um administrador do AD do Azure por chamada hello comandos a seguir:
| Command | Descrição |
| --- | --- |
|[az sql server ad-admin create](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Provisiona um administrador do Azure Active Directory para o Azure SQL Server ou o SQL Data Warehouse do Azure. (Deve ser da assinatura atual Olá). |
|[az sql server ad-admin delete](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Remove um administrador do Azure Active Directory para o Azure SQL Server ou para o SQL Data Warehouse do Azure. |
|[az sql server ad-admin list](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Retorna informações sobre um administrador do Active Directory do Azure atualmente configurado para hello Azure do SQL server ou do Azure SQL Data Warehouse. |
|[az sql server ad-admin update](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Atualiza o administrador do Active Directory Olá para um servidor do SQL Azure ou Azure SQL Data Warehouse. |

Para obter mais informações sobre comandos da CLI, consulte [SQL – az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>Configurar os computadores cliente
Em todos os computadores cliente, do qual seus aplicativos ou usuários conectam tooAzure banco de dados SQL ou do Azure SQL Data Warehouse usando identidades do AD do Azure, você deve instalar Olá software a seguir:

* .NET Framework 4.6 ou posterior de [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Biblioteca de autenticação do Active Directory do Azure para o SQL Server (**ADALSQL. DLL**) está disponível em vários idiomas (x86 e amd64) do Centro de download da saudação em [Microsoft Active Directory Authentication Library para Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

Você pode atender a esses requisitos:

* Instalando o [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) ou [SQL Server Data Tools para Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) atende Olá requisito do .NET Framework 4.6.
* SSMS instala a versão x86 de saudação do **ADALSQL. DLL**.
* SSDT instala a versão amd64 Olá **ADALSQL. DLL**.
* Olá Visual Studio mais recente, de [Downloads do Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) atende aos requisitos de saudação do .NET Framework 4.6, mas não instalar a versão necessária amd64 Olá **ADALSQL. DLL**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Criar usuários de banco de dados independente em seu banco de dados mapeado tooAzure identidades do AD

Autenticação do Active Directory do Azure requer toobe de usuários de banco de dados criado como usuários de banco de dados independente. Um usuário de banco de dados independente com base em uma identidade do AD do Azure, é um usuário de banco de dados que não tem um logon no banco de dados mestre hello e qual identidade de tooan mapas no hello diretório AD do Azure que está associado ao banco de dados de saudação. Olá identidade do AD do Azure pode ser uma conta de usuário individual ou um grupo. Para saber mais sobre usuários de bancos de dados independentes, veja [Usuários do bancos de dados independentes - Tornando seu banco de dados portátil](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Os usuários de banco de dados (com exceção de saudação de administradores) não podem ser criados usando o portal. Funções RBAC não são propagada tooSQL do servidor, banco de dados SQL ou SQL Data Warehouse. Funções RBAC do Azure são usadas para gerenciar recursos do Azure e não se aplicam a toodatabase permissões. Por exemplo, Olá **Colaborador do SQL Server** função não conceder acesso tooconnect toohello banco de dados SQL ou SQL Data Warehouse. permissão de acesso de saudação deve ser concedida diretamente no banco de dados de saudação usando instruções Transact-SQL.
>

toocreate um Azure usuário de banco de dados contido baseado no AD (diferente de Olá administrador do servidor que possui o banco de dados de saudação), conectar o banco de dados de toohello com uma identidade do AD do Azure, como um usuário com pelo menos Olá **ALTER ANY USER** permissão. Em seguida, use Olá sintaxe Transact-SQL a seguir:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* pode ser o nome principal de usuário de saudação de um AD do Azure Olá exibição nome de usuário ou para um grupo do AD do Azure.

**Exemplos:** toocreate um usuário de banco de dados independente que representa o AD do Azure federado ou gerenciado de usuário de domínio:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate um usuário de banco de dados independente que representa o AD do Azure ou federado grupo de domínio, forneça o nome de exibição de saudação de um grupo de segurança:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

toocreate um usuário de banco de dados independente que representa um aplicativo que se conecta usando um token do AD do Azure:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  Você não pode criar um usuário diretamente de um Active Directory do Azure que não sejam hello Azure Active Directory que é associado à sua assinatura do Azure. No entanto, os membros de outros diretórios Active que são os usuários importados no hello associado do Active Directory (conhecidos como usuários externos) podem ser adicionados a grupo do Active Directory tooan no locatário de saudação do Active Directory. Ao criar um usuário de banco de dados independente para esse grupo AD, hello usuários da saudação externo do Active Directory podem obter acesso tooSQL banco de dados.   

Para obter mais informações sobre como criar usuários de banco de dados independente baseados em identidades do Active Directory do Azure, consulte [CRIAR USUÁRIO (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Remover administrador do Active Directory do Azure Olá para o servidor do SQL Azure impede que qualquer usuário de autenticação do AD do Azure conectando o servidor toohello. Se for necessário, os usuários do Azure AD inutilizáveis poderão ser removidos manualmente por um administrador do Banco de Dados SQL.   

>  [!NOTE]
>  Se você receber um **tempo limite de Conexão expirou**, talvez seja necessário Olá tooset `TransparentNetworkIPResolution` parâmetro hello toofalse de cadeia de caracteres de conexão. Para obter mais informações, consulte [Problema de tempo limite de conexão com o .NET Framework 4.6.1 – TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Quando você cria um usuário de banco de dados, o usuário recebe Olá **conectar** permissão e podem se conectar a banco de dados toothat como um membro da saudação **pública** função. Olá inicialmente apenas permissões de usuário toohello disponíveis são as permissões concedidas toohello **pública** função ou as permissões concedidas tooany grupos do Windows que ele é membro de. Uma vez você provisionar um usuário de banco de dados contido baseado no AD do Azure, você pode conceder permissões adicionais do usuário hello, Olá mesma maneira que você conceda permissão tooany outro tipo de usuário. Normalmente conceder permissões de funções toodatabase e adicione usuários tooroles. Para saber mais, confira [Noções básicas sobre permissões do Mecanismo de Banco de Dados](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Para obter mais informações sobre funções especiais do Banco de dados SQL, veja [Gerenciando bancos de dados e logons no Banco de Dados SQL do Azure](sql-database-manage-logins.md).
Um usuário de domínio federado que é importado para um domínio de gerenciar, deve usar a identidade de domínio Olá gerenciado.

> [!NOTE]
> Os usuários do AD do Azure são marcados nos metadados do banco de dados de saudação com tipo E ((EXTERNAL_USER) e para grupos com tipo X (EXTERNAL_GROUPS). Para obter mais informações, consulte [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Conecte-se toohello depósito de dados ou banco de dados do usuário usando o SSMS ou o SSDT  
administrador de saudação do AD do Azure tooconfirm está configurado corretamente, conecte-se toohello **mestre** banco de dados usando a conta de administrador de saudação do AD do Azure.
tooprovision um Azure usuário de banco de dados contido baseado no AD (diferente de Olá administrador do servidor que possui o banco de dados de saudação), conecte-se toohello banco de dados com uma identidade do AD do Azure que tem o banco de dados do access toohello.

> [!IMPORTANT]
> O suporte à autenticação do Azure Active Directory está disponível com o [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) e o [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) no Visual Studio 2015. Olá versão de agosto de 2016 do SSMS também inclui suporte para Universal autenticação do Active Directory, que permite que os administradores toorequire usando uma chamada telefônica, mensagem de texto, os cartões inteligentes com o pin ou a notificação do aplicativo móvel do multi-Factor Authentication.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Usando um tooconnect de identidade do AD do Azure usando o SSMS ou SSDT  

Olá procedimentos a seguir mostra como tooconnect tooa SQL banco de dados com uma identidade do AD do Azure usando o SQL Server Management Studio ou ferramentas de banco de dados do SQL Server.

### <a name="active-directory-integrated-authentication"></a>Autenticação integrada do Active Directory

Use este método se você efetuou logon tooWindows usando suas credenciais do Active Directory do Azure de um domínio federado.

1. Inicie o Management Studio ou ferramentas de dados e no hello **conectar tooServer** (ou **conectar tooDatabase mecanismo**) caixa de diálogo Olá **autenticação** , selecione **Integrada ao active Directory -**. Nenhuma senha é necessária ou pode ser inserida porque suas credenciais serão apresentados para conexão hello.   

    ![Selecione Autenticação Integrada do AD][11]
2. Clique Olá **opções** botão e em Olá **propriedades de Conexão** página Olá **conectar toodatabase** caixa, digite o nome de saudação do banco de dados de usuário Olá deseja tooconnect Para. (Olá **ID de locatário ou de nome de domínio do AD**"opção tem suporte apenas para **Universal com conexão MFA** opções, caso contrário, ele fica acinzentado.)  

    ![Selecione o nome do banco de dados de saudação][13]

## <a name="active-directory-password-authentication"></a>Autenticação de senha do Active Directory

Use este método quando se conectar com um nome principal do AD do Azure usando Olá AD do Azure gerenciados domínio. Você também pode usar isso para uma conta federada sem domínio toohello de acesso, por exemplo, ao trabalhar remotamente.

Use este método se você efetuou logon tooWindows usando as credenciais de um domínio que não é federado com o Azure, ou ao usar a autenticação do AD do Azure usando o AD do Azure com base em saudação inicial ou Olá domínio do cliente.

1. Inicie o Management Studio ou ferramentas de dados e no hello **conectar tooServer** (ou **conectar tooDatabase mecanismo**) caixa de diálogo Olá **autenticação** , selecione **Do active Directory - senha**.
2. Em Olá **nome de usuário** , digite seu nome de usuário do Active Directory do Azure no formato Olá  **username@domain.com** . Isso deve ser uma conta de saudação do Azure Active Directory ou uma conta de domínio federar com hello Active Directory do Azure.
3. Em Olá **senha** caixa, digite a senha do usuário para a conta do Active Directory do Azure hello ou federado conta de domínio.

    ![Selecione Autenticação de Senha do AD][12]
4. Clique Olá **opções** botão e em Olá **propriedades de Conexão** página Olá **conectar toodatabase** caixa, digite o nome de saudação do banco de dados de usuário Olá deseja tooconnect Para. (Consulte o gráfico Olá na opção anterior hello.)

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Usando um tooconnect de identidade do AD do Azure de um aplicativo cliente

Olá procedimentos a seguir mostra como tooconnect tooa SQL banco de dados com uma identidade do AD do Azure de um aplicativo cliente.

###  <a name="active-directory-integrated-authentication"></a>Autenticação integrada do Active Directory

toouse autenticação integrada do Windows, Active Directory do domínio deve ser federado com o Active Directory do Azure. Seu aplicativo cliente (ou um serviço) conectando o banco de dados de toohello deve estar em execução em um computador ingressado no domínio com credenciais de domínio do usuário.

tooconnect tooa banco de dados usando a autenticação e uma identidade do AD do Azure integrados, palavra-chave de autenticação de saudação na cadeia de caracteres de conexão de banco de dados Olá deve ser definida como tooActive Directory integrado. Olá, exemplo de código a seguir c# usa ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

palavra-chave de cadeia de caracteres de conexão de Olá ``Integrated Security=True`` não há suporte para conexão tooAzure banco de dados SQL. Ao fazer uma conexão ODBC, será necessário tooremove espaços e definir autenticação too'ActiveDirectoryIntegrated'.

### <a name="active-directory-password-authentication"></a>Autenticação de senha do Active Directory

tooconnect tooa banco de dados usando a autenticação e uma identidade do AD do Azure integrados, palavra-chave de autenticação Olá deve ser definida como tooActive senha do diretório. cadeia de caracteres de conexão de saudação deve conter a ID de usuário/UID e palavras-chave de senha/PWD e valores. Olá, exemplo de código a seguir c# usa ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Saiba mais sobre métodos de autenticação do AD do Azure usando os exemplos de código de demonstração de Olá disponíveis em [do Azure AD Authentication GitHub demonstração](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Token do Azure AD
Esse método de autenticação permite que os serviços de camada intermediária tooconnect tooAzure banco de dados SQL ou do Azure SQL Data Warehouse obtendo um token do Azure Active Directory (AAD). Ele permite cenários sofisticados, incluindo a autenticação baseada em certificado. Você deve concluir as quatro etapas básicas toouse AD do Azure autenticação de token:

1. Registrar seu aplicativo com o Active Directory do Azure e obter o id de saudação do cliente para seu código. 
2. Crie um aplicativo hello representação do usuário de banco de dados. (Concluída anteriormente na etapa 6).
3. Crie um certificado em execuções de computador cliente Olá aplicativo hello.
4. Adicione certificado hello como uma chave para seu aplicativo.

Exemplo de cadeia de conexão:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Para obter mais informações, confira [Blog de segurança do SQL Server](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Olá instruções a seguir, conecte-se usando a versão 13.1 do sqlcmd, que está disponível no hello [Centro de Download](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Próximas etapas
- Para obter uma visão geral de acesso e controle no Banco de Dados SQL, confira [Acesso e controle de Banco de Dados SQL](sql-database-control-access.md).
- Para obter uma visão geral de logons, usuários e funções de banco de dados no Banco de Dados SQL, confira [Logons, usuários e funções de banco de dados](sql-database-manage-logins.md).
- Para obter mais informações sobre objetos de banco de dados, confira [Entidades](https://msdn.microsoft.com/library/ms181127.aspx).
- Para obter mais informações sobre as funções de banco de dados, confira [Funções de banco de dados](https://msdn.microsoft.com/library/ms189121.aspx).
- Para obter mais informações sobre as regras de firewall no Banco de Dados SQL, confira [Regras de firewall de Banco de Dados SQL](sql-database-firewall-configure.md).

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png

