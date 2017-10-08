---
title: "uma conta de lote no portal do Azure de saudação do aaaCreate | Microsoft Docs"
description: "Saiba como conta toocreate um lote do Azure em Olá toorun portal do Azure cargas de trabalho paralelas em grande escala na nuvem Olá"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Crie uma conta de lote com hello portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](batch-account-create-portal.md)
> * [.NET de Gerenciamento do Lote](batch-management-dotnet.md)
>
>

Saiba como a conta toocreate um lote do Azure no hello [portal do Azure][azure_portal]e escolha Propriedades de conta de saudação que se adaptam a seu cenário de computação. Saiba onde toofind propriedades de conta importantes como chaves de acesso e as URLs de conta.

Para obter informações sobre cenários e contas em lotes, consulte Olá [visão geral de recursos](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Criar uma conta do Batch

Use Olá portal toocreate uma conta de lote em uma saudação dois *modos de alocação de pool*: **serviço de lote** modo ou hello mais recente **assinatura de usuário** modo, o que requer mais configuração. Para obter informações sobre esses dois modos, consulte Olá [visão geral de recursos](batch-api-basics.md#account). Para os recursos Olá assinatura de modo de usuário, consulte também Olá [postagem de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Modo de serviço do Lote



1. Entrar toohello [portal do Azure][azure_portal].
2. Clique em **Novo** > **Computação** > **Serviço de Lote**.

    ![Lote em Olá Marketplace][marketplace_portal]
3. Olá **nova conta de lote** folha é exibida. Consulte as descrições de saudação abaixo de cada elemento da folha.

    ![Criar uma conta do Batch][account_portal]

    a. **Nome da conta**: nome de conta de lote Olá você escolher deve ser exclusivo dentro Olá região do Azure em que a conta de saudação é criada (consulte **local** abaixo). nome da conta Olá pode conter apenas caracteres em minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.

    b. **Assinatura**: Olá assinatura no qual Olá toocreate conta do lote. Se você tiver somente uma assinatura, ela será selecionada por padrão.

    c. **Modo de alocação de pool**: selecione **Serviço Lote**.

    c. **Grupo de recursos**: selecione um grupo de recursos para sua nova conta do Lote ou, opcionalmente, crie um novo.

    d. **Local**: Olá região do Azure no qual Olá toocreate conta do lote. Olá regiões de somente tem suportados por sua assinatura e o grupo de recursos são exibidas como opções.

    e. **Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote. Isso é recomendado para a maioria das contas do Lote. Confira [Conta do Armazenamento do Azure vinculada](#linked-azure-storage-account) mais adiante neste artigo para obter mais detalhes.

4. Clique em **criar** toocreate conta de saudação.

   portal de saudação indica a implantação está em andamento. Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.

## <a name="user-subscription-mode"></a>Modo de assinatura do usuário

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Permitir tooaccess de lote do Azure assinatura hello (operação única)
Ao criar sua primeira conta de lote no modo de usuário de assinatura, execute Olá tooregister as etapas a seguir sua assinatura com o lote. (Se anteriormente você fez isso, ignore toohello próxima seção).

1. Entrar toohello [portal do Azure][azure_portal].

2. Clique em **mais serviços** > **assinaturas**e clique em assinatura Olá desejar toouse para Olá conta do lote.

3. Em Olá **assinatura** folha, clique em **(IAM) do controle de acesso** > **adicionar**.

    ![Controle de acesso de assinatura][subscription_access]

4. Em Olá **adicionar permissões** folha, selecione Olá **Colaborador** função, procure Olá API de lote. Pesquisar para cada uma dessas cadeias de caracteres até encontrar hello API:
    1. **MicrosoftAzureBatch**.
    2. **Lote do Microsoft Azure**. Os locatários mais recentes do Azure AD podem usar esse nome.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** é identificação Olá Olá API de lote. 

5. Depois de encontrar hello API de lote, selecione-o e clique em **salvar**.

    ![Adicionar permissões do Lote][add_permission]

### <a name="create-a-key-vault"></a>Criar um cofre de chave
No modo de usuário de assinatura, um cofre de chaves do Azure é necessário que pertence a toothe mesmo grupo de recursos Olá toobe de conta de lote criado. Verifique se o grupo de recursos de saudação está em uma região em que o lote é [disponível](https://azure.microsoft.com/regions/services/) e que oferece suporte à sua assinatura.

1. Em Olá [portal do Azure][azure_portal], clique em **novo** > **segurança + identidade** > **Cofre de chaves** .

2. Em Olá **criar Cofre de chaves** folha, insira um nome para o Cofre de chaves hello e criar um grupo de recursos na região Olá você deseja para sua conta do lote. Deixe Olá restantes valores padrão das configurações, clique em **criar**.

### <a name="create-a-batch-account"></a>Criar uma conta do Batch

1. Em Olá [portal do Azure][azure_portal], clique em **novo** > **de computação** > **doserviçodelote**.

    ![Lote em Olá Marketplace][marketplace_portal]
3. Olá **nova conta de lote** folha é exibida. Consulte as descrições de saudação abaixo de cada elemento da folha.

    ![Criar uma conta do Batch][account_portal_byos]

    a. **Nome da conta**: nome de conta de lote Olá você escolher deve ser exclusivo dentro Olá região do Azure em que a conta de saudação é criada (consulte **local** abaixo). nome da conta Olá pode conter apenas caracteres em minúsculas ou números e deve ter 3 a 24 caracteres de comprimento.

    b. **Assinatura**: se você tiver mais de uma assinatura, selecione a assinatura de saudação que você registrou com o serviço de lote de saudação.

    c. **Modo de alocação de pool**: selecione **Assinatura de usuário**.

    d. **Cofre de chaves**: Cofre de chaves Olá selecione criado para sua conta do lote na seção anterior hello. Opcionalmente, crie um novo cofre de chaves. Depois de selecionar um cofre hello, selecione caixa de seleção Olá toohello toogrant do Azure Batch acesso chave cofre.

    c. **Grupo de recursos**: grupo de recursos de saudação Select em que você criou o Cofre de chaves hello.

    d. **Local**: Olá região do Azure em que você criou o Cofre de chaves Olá para conta do lote hello.

    e. **Conta de armazenamento** (opcional): uma conta do Armazenamento do Azure de uso geral que você associa à sua nova conta do Lote. Isso é recomendado para a maioria das contas do Lote. Confira [Conta vinculada do Armazenamento do Azure](#linked-azure-storage-account) abaixo para obter mais detalhes.

4. Clique em **criar** toocreate conta de saudação.

   portal de saudação indica a implantação está em andamento. Após a conclusão, uma notificação de **Implantações bem-sucedidas** aparece em **Notificações**.



## <a name="view-batch-account-properties"></a>Exibir propriedades de conta do Lote
Olá conta foi criada, é possível abrir Olá **folha de conta de lote** tooaccess suas propriedades e configurações. Você pode acessar todas as configurações de conta e propriedades usando menus de saudação à esquerda da folha de conta de lote de saudação.

![Folha Conta do Lote no portal do Azure][account_blade]

* **A URL da conta do lote**: ao desenvolver um aplicativo com hello [lote APIs](batch-apis-tools.md#azure-accounts-for-batch-development), você precisará uma tooaccess de URL de conta de seus recursos de lote. Uma URL de conta de lote tem Olá formato a seguir:

    `https://<account_name>.<region>.batch.azure.com`

![URL de conta do Lote no portal][account_url]

* **Chaves de acesso** (modo de serviço de lote): tooauthenticate acesso tooyour conta em lotes do seu aplicativo, você precisará de uma chave de acesso da conta. (Essa configuração não está disponível no modo de assinatura do usuário, em que você usa a autenticação do Azure Active Directory.)

    tooview ou regenerar chaves de acesso da conta em lotes, digite `keys` no menu esquerdo Olá **pesquisa** caixa na folha de conta de lote hello, em seguida, selecione **chaves**.

    ![Chaves de conta do Lote no portal do Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Conta vinculada do Armazenamento do Azure

Opcionalmente, você pode vincular um tooyour de conta de armazenamento do Azure para fins gerais conta do lote. Olá [pacotes de aplicativos](batch-application-packages.md) recurso de lote usa o armazenamento de BLOBs do Azure, como o hello [.NET de convenções de arquivo em lotes](batch-task-output.md) biblioteca. Esses recursos opcionais ajudá-lo Implantando aplicativos Olá que executam as tarefas de lote e manter dados Olá geram.

É recomendável que você crie uma nova conta de armazenamento exclusivamente para uso com sua conta do Lote.

![Criando uma conta de armazenamento de uso geral][storage_account]

> [!NOTE]
> Lote do Azure atualmente suporta apenas Olá para fins gerais armazenamento tipo de conta. Esse tipo de conta é descrito na etapa 5, [Criar uma conta de armazenamento] (../storage/common/storage-create-storage-account.md#create-a-storage-account), em [Sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Tenha cuidado ao regenerar as chaves de acesso de saudação de uma conta de armazenamento vinculada. Gerar apenas uma chave de conta de armazenamento e clique em **sincronizar as chaves** em Olá vinculado folha da conta de armazenamento. Aguarde cinco minutos tooallow Olá chaves toopropagate toohello nós de computação em seus pools, em seguida, regenerar e sincronizar Olá outra chave, se necessário. Se você regenerar as chaves no hello mesmo tempo, seus nós de computação não será capaz de toosynchronize qualquer chave e ele perderá a conta de armazenamento toohello de acesso.
>
>

![Regeneração de chaves da conta de armazenamento][4]

## <a name="batch-service-quotas-and-limits"></a>Cotas e limites de serviço do Lote
Esteja ciente de que como com sua assinatura do Azure e outros Azure serviços, determinados [cotas e limites](batch-quota-limit.md) aplicar tooBatch contas. Cotas atuais para uma conta de lote aparecerá no portal de saudação na conta Olá **propriedades**.

![Cotas de conta do Lote no portal do Azure][quotas]



Além disso, muitas dessas cotas podem ser aumentadas simplesmente com uma solicitação de suporte de produto livre enviada no hello portal do Azure. Consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre como solicitar o aumento de cota.

## <a name="other-batch-account-management-options"></a>Outras opções de gerenciamento de conta do Lote
Além disso, toousing Olá portal do Azure, você também pode criar e gerenciar contas de lote com os seguintes hello:

* [Cmdlets do PowerShell do Lote](batch-powershell-cmdlets-get-started.md)
* [CLI do Azure](batch-cli-get-started.md)
* [.NET de Gerenciamento do Lote](batch-management-dotnet.md)

## <a name="next-steps"></a>Próximas etapas
* Consulte Olá [visão geral do recurso de lote](batch-api-basics.md) toolearn mais sobre recursos e conceitos do serviço de lote. Olá artigo aborda os principais recursos de lote hello, como pools, nós de computação, trabalhos e tarefas e fornece uma visão geral da saudação recursos do serviço que permitem a execução da carga de trabalho de computação em larga escala.
* Conheça os fundamentos de saudação do desenvolvimento de um aplicativo habilitado para lote usando Olá [biblioteca cliente .NET do lote](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Esses artigos introdutórios guiá-lo por meio de um aplicativo de trabalho que usa tooexecute de serviço de lote Olá uma carga de trabalho em vários nós de computação e inclui o uso de armazenamento do Azure para recuperação e preparação de arquivo de carga de trabalho.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Regeneração de chaves da conta de armazenamento"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
