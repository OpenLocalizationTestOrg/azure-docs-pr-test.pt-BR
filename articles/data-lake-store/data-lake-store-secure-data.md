---
title: "aaaSecuring dados armazenados no repositório Azure Data Lake | Microsoft Docs"
description: "Saiba como listas de controle de dados toosecure no repositório Azure Data Lake usando grupos e acesso"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Protegendo os dados armazenados no repositório Azure Data Lake
A proteção de dados no repositório Azure Data Lake é uma abordagem de três etapas.

1. Comece criando grupos de segurança no Active Directory do Azure (AAD). Esses grupos de segurança são usados tooimplement controle de acesso baseado em função (RBAC) no Portal do Azure. Para saber mais, consulte [Controle de acesso baseado em função no Microsoft Azure](../active-directory/role-based-access-control-configure.md).
2. Atribua grupos de segurança do hello AAD toohello repositório Azure Data Lake conta. Isso controla o acesso toohello repositório Data Lake conta da saudação portal de gerenciamento de operações e portal hello ou APIs.
3. Atribua grupos de segurança do AAD hello como listas de controle de acesso (ACLs) no sistema de arquivos do repositório Data Lake hello.
4. Além disso, você também pode definir um intervalo de endereços IP para clientes que podem acessar dados Olá repositório Data Lake.

Este artigo fornece instruções sobre como toouse Olá Olá tooperform portal do Azure acima tarefas. Para obter informações detalhadas sobre como o repositório Data Lake implementa segurança no nível de conta e dados hello, consulte [segurança no repositório Azure Data Lake](data-lake-store-security-overview.md). Para obter informações detalhadas sobre como ACLs são implementadas no Azure Data Lake Store, consulte [Visão geral do controle de acesso no armazenamento do Data Lake Store](data-lake-store-access-control.md).

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Criar grupos de segurança no Active Directory do Azure
Para obter instruções sobre como grupos de segurança do AAD toocreate e como tooadd grupo de toohello de usuários, consulte [gerenciar grupos de segurança no Active Directory do Azure](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> Você pode adicionar usuários e outros grupos tooa grupo no AD do Azure usando Olá portal do Azure. No entanto, em ordem tooadd um grupo de tooa principal do serviço, use [módulo do PowerShell do AD do Azure](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Atribuir usuários ou grupos de segurança de contas do repositório Data Lake tooAzure
Quando você atribuir usuários ou contas do repositório Data Lake tooAzure os grupos de segurança, você pode controlar operações de gerenciamento do acesso toohello na conta hello usando hello portal do Azure e APIs do Gerenciador de recursos do Azure. 

1. Abra uma conta do repositório Azure Data Lake. No painel esquerdo do hello, clique em **procurar**, clique em **repositório Data Lake**e clique em Olá toowhich de nome de conta você deseja tooassign um usuário ou grupo de segurança da folha de repositório Data Lake hello,.

2. Na folha de configurações da conta Data Lake Store, clique em **Controle de Acesso (IAM)**. folha de saudação por listas de padrão **administradores de assinatura** grupo como proprietário.
   
    ![Atribuir segurança grupo tooAzure repositório Data Lake conta](./media/data-lake-store-secure-data/adl.select.user.icon.png "atribuir a conta de repositório Data Lake de tooAzure de grupo de segurança")

    Há tooadd de duas maneiras de um grupo e atribuir funções relevantes.
   
    * Adicionar uma conta de usuário/grupo toohello e, em seguida, atribuir uma função, ou
    * Adicionar uma função e, em seguida, atribuir usuários/grupos toorole.
     
    Nesta seção, vamos examinar primeira abordagem de hello, adicionando um grupo e, em seguida, atribuir funções. Você pode executar seleção de toofirst etapas semelhantes uma função e, em seguida, atribua a função de toothat de grupos.
4. Em Olá **usuários** folha, clique em **adicionar** tooopen Olá **adicionar acesso** folha. Em Olá **adicionar acesso** folha, clique em **selecionar uma função**e, em seguida, selecione uma função de usuário/grupo Olá.
   
    ![Adicionar uma função de usuário Olá](./media/data-lake-store-secure-data/adl.add.user.1.png "adicionar uma função de usuário de saudação")
   
    Olá **proprietário** e **Colaborador** função fornecem acesso tooa diversas funções de administração na conta Olá data lake. Para usuários que irão interagir com dados em lake de dados hello, você pode adicioná-los toohello * * leitor * * função. Olá o escopo dessas funções é limitado toohello gerenciamento operações relacionadas toohello conta do repositório Azure Data Lake.
   
    Para dados de permissões de sistema de arquivos individuais de operações definem o que os usuários de saudação podem fazer. Portanto, um usuário que tem uma função de leitor podem apenas exibir configurações administrativas associadas à conta hello, mas pode potencialmente leitura e gravação dados com base em permissões do sistema de arquivos atribuídas toothem. Permissões de sistema de arquivos do repositório data Lake estão descritas no [atribuir o grupo de segurança como toohello ACLs de sistema de arquivos do repositório Azure Data Lake](#filepermissions).
5. Em Olá **adicionar acesso** folha, clique em **adicionar usuários** tooopen Olá **adicionar usuários** folha. Nessa folha, procure o grupo de segurança Olá criado anteriormente no Active Directory do Azure. Se você tiver muitos grupos toosearch do, use a caixa de texto de saudação em toofilter superior de Olá Olá pelo nome de grupo. Clique em **Selecionar**.
   
    ![Adicionar um grupo de segurança](./media/data-lake-store-secure-data/adl.add.user.2.png "adicionar um grupo de segurança")
   
    Se você quiser tooadd um grupo/usuário não estiver listado, você pode convidá-los usando Olá **convidar** ícone e especificando o endereço de email Olá Olá usuário/grupo.
6. Clique em **OK**. Você deve ver o grupo de segurança Olá adicionado, como mostrado abaixo.
   
    ![Grupo de segurança adicionado](./media/data-lake-store-secure-data/adl.add.user.3.png "o grupo de segurança adicionado")

7. O grupo de segurança do usuário agora tem acesso toohello repositório Azure Data Lake conta. Se você desejar tooprovide acesso toospecific usuários, você pode adicioná-los toohello grupo de segurança. Da mesma forma, se você quiser toorevoke acesso para um usuário, você poderá removê-los do grupo de segurança de saudação. Você também pode atribuir vários grupos de segurança tooan conta. 

## <a name="filepermissions"></a>Atribuir usuários ou grupo de segurança como toohello ACLs de sistema de arquivos do repositório Azure Data Lake
Ao atribuir grupos de segurança do usuário de sistema de arquivos do Azure Data Lake toohello, você deve definir o controle de acesso nos dados de saudação armazenados no repositório Azure Data Lake.

1. Na folha de sua conta do Repositório Data Lake, clique em **Gerenciador de Dados**.
   
    ![Crie diretórios na conta do Data Lake Store](./media/data-lake-store-secure-data/adl.start.data.explorer.png "criar diretórios na conta Data Lake")
2. Em Olá **Data Explorer** folha, clique em arquivo hello ou pasta para a qual deseja tooconfigure Olá ACL e, em seguida, clique em **acesso**. arquivo de tooa ACL tooassign, você deve clicar em **acesso** de saudação **a visualização de arquivo** folha.
   
    ![Configurar ACLs no sistema de arquivos do Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "definir ACLs no sistema de arquivos do Data Lake")
3. Olá **acesso** folha lista padrão de acesso a saudação e acesso personalizado já atribuído toohello raiz. Clique em Olá **adicionar** nível personalizado de ícone tooadd ACLs.
   
    ![Lista de acesso padrão e personalizado](./media/data-lake-store-secure-data/adl.acl.2.png "lista de acesso padrão e personalizado")
   
   * **Acesso padrão** é hello estilo UNIX acesso, em que você especificar ler, gravar, executar classes de usuário distintas toothree (rwx): proprietário, grupo e outros.
   * **Acesso personalizado** corresponde toohello POSIX ACLs que permite que você tooset permissões para usuários nomeados específicos ou grupos e não apenas Olá proprietário ou grupo do arquivo. 
     
     Para saber mais, consulte [ACLs HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Para saber mais sobre como as ACLs são implementadas no Data Lake Store, veja [Controle de acesso no Data Lake Store](data-lake-store-access-control.md).
4. Clique em Olá **adicionar** saudação do ícone tooopen **adicionar personalizado acesso** folha. Nessa folha, clique em **Selecionar usuário ou grupo**e, em seguida, em **Selecionar usuário ou grupo** folha, procure o grupo de segurança Olá criado anteriormente no Active Directory do Azure. Se você tiver muitos grupos toosearch do, use a caixa de texto de saudação em toofilter superior de Olá Olá pelo nome de grupo. Clique em Olá grupo você deseja tooadd e, em seguida, clique em **selecione**.
   
    ![Adicionar um grupo](./media/data-lake-store-secure-data/adl.acl.3.png "Adicionar um grupo")
5. Clique em **selecionar permissões**, selecione permissões hello e se você deseja que as permissões de saudação tooassign como uma ACL padrão, para acessar a ACL, ou ambos. Clique em **OK**.
   
    ![Atribuir permissões toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "atribuir permissões toogroup")
   
    Para obter mais informações sobre permissões no Data Lake Store e ACLs de acesso/padrão, consulte [Controle de acesso no Data Lake Store](data-lake-store-access-control.md).
6. Em Olá **adicionar personalizado acesso** folha, clique em **Okey**. Olá recém-adicionado grupo com permissões de saudação associada, agora será listado no hello **acesso** folha.
   
    ![Atribuir permissões toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "atribuir permissões toogroup")
   
   > [!IMPORTANT]
   > Na versão atual do hello, você só pode ter 9 entradas **acesso personalizado**. Se você quiser tooadd 9 mais de usuários, você deve criar grupos de segurança, adicionar usuários toosecurity grupos, adicionar fornecer acesso toothose grupos de segurança para Olá conta do repositório Data Lake.
   > 
   > 
7. Se necessário, você também pode modificar as permissões de acesso Olá depois que você adicionou o grupo de saudação. Olá marque ou desmarque a caixa de seleção para cada permissão digite (ler, gravar e executar) com base em se você quer tooremove ou atribuir o grupo de segurança toohello permissão. Clique em **salvar** toosave alterações de hello, ou **descartar** tooundo alterações de saudação.

## <a name="set-ip-address-range-for-data-access"></a>Definir o intervalo de endereços IP para acesso a dados
Repositório Azure Data Lake permite bloquear toofurther acessar o repositório de dados tooyour no nível da rede. Você pode habilitar o firewall e definir um intervalo de endereços IP para seus clientes confiáveis. Uma vez habilitada, somente os clientes que têm endereços IP hello dentro do intervalo definido podem se conectar toohello repositório.

![Configurações de firewall e acesso IP](./media/data-lake-store-secure-data/firewall-ip-access.png "Endereço IP e configurações de firewall")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Remova grupos de segurança de uma conta do repositório Azure Data Lake.
Quando você remove grupos de segurança de contas do repositório Azure Data Lake, você está alterando apenas operações de gerenciamento do acesso toohello na conta hello usando hello Portal do Azure e APIs do Gerenciador de recursos do Azure.

1. Na folha de sua conta do Data Lake Store, clique em **Configurações**. De saudação **configurações** folha, clique em **usuários**.
   
    ![Atribuir segurança grupo tooAzure Data Lake conta](./media/data-lake-store-secure-data/adl.select.user.icon.png "atribuir segurança grupo tooAzure Data Lake conta")
2. Em Olá **usuários** folha clique Olá grupo de segurança tooremove.
   
    ![Tooremove do grupo de segurança](./media/data-lake-store-secure-data/adl.add.user.3.png "tooremove do grupo de segurança")
3. Na folha de Olá Olá grupo de segurança, clique em **remover**.
   
    ![Removido do grupo de segurança](./media/data-lake-store-secure-data/adl.remove.group.png "removido do grupo de segurança")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Remover ACLs do grupo de segurança do sistema de arquivos do repositório Azure Data Lake
Quando você remove as ACLs de grupos de segurança do sistema de arquivos do repositório Azure Data Lake, você pode alterar acesso toohello dados Olá repositório Data Lake.

1. Na folha de sua conta do Repositório Data Lake, clique em **Gerenciador de Dados**.
   
    ![Criar diretórios na conta do Data Lake](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Criar diretórios na conta do Data Lake")
2. Em Olá **Data Explorer** folha, clique em arquivo hello ou pasta para a qual você deseja tooremove Olá ACL e clique em Olá na folha de sua conta, **acesso** ícone. tooremove ACL para um arquivo, você deve clicar em **acesso** de saudação **a visualização de arquivo** folha.
   
    ![Configurar ACLs no sistema de arquivos do Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "definir ACLs no sistema de arquivos do Data Lake")
3. Em Olá **acesso** folha da saudação **acesso personalizado** seção, clique em Olá grupo de segurança tooremove. Em Olá **acesso personalizado** folha, clique em **remover** e, em seguida, clique em **Okey**.
   
    ![Atribuir permissões toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "atribuir permissões toogroup")

## <a name="see-also"></a>Consulte também
* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
* [Copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Introdução ao Repositório Data Lake usando o PowerShell](data-lake-store-get-started-powershell.md)
* [Introdução ao Repositório Data Lake usando o SDK do .NET](data-lake-store-get-started-net-sdk.md)
* [Acessar os logs de diagnóstico do Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

