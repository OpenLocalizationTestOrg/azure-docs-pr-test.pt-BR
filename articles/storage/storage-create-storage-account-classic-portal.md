---
title: "aaaHow toocreate, gerenciar ou excluir uma conta de armazenamento no portal clássico do Azure da saudação | Microsoft Docs"
description: "Criar uma nova conta de armazenamento, gerenciar suas chaves de acesso de conta ou excluir uma conta de armazenamento Olá portal do Azure. Saiba mais sobre contas de armazenamento standard e premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Sobre as contas de armazenamento do Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Visão geral
Um dá conta de armazenamento do Azure acessar os serviços do Azure Blob, fila, tabela e arquivo toohello no armazenamento do Azure. Sua conta de armazenamento fornece um namespace exclusivo Olá para seus objetos de dados de armazenamento do Azure. Por padrão, dados de saudação em sua conta são tooyou somente disponível, proprietário da conta Olá.

Existem dois tipos de contas de armazenamento:

* Uma conta de armazenamento padrão inclui armazenamento de Blob, Tabela e Fila.
* Atualmente, uma conta de armazenamento premium dá suporte apenas aos discos de máquina virtual do Azure. Confira [Armazenamento Premium: Armazenamento de Alto Desempenho para as Cargas de Trabalho da Máquina Virtual do Azure](storage-premium-storage.md) para ter uma visão geral detalhada do Armazenamento Premium.

## <a name="storage-account-billing"></a>Cobrança de conta de armazenamento
Você é cobrado pelo uso do Armazenamento do Azure com base na sua conta de armazenamento. Os custos de armazenamento baseiam-se em quatro fatores: capacidade de armazenamento, esquema de replicação, transações de armazenamento e saída de dados.

* Capacidade de armazenamento se refere a toohow muito de sua alocação de conta de armazenamento, você estiver usando dados de toostore. custo de saudação de simplesmente armazenar seus dados é determinado pela quantidade de dados que você está armazenando e como eles são replicados.
* A replicação determina quantas cópias dos seus dados são mantidas de uma só vez e em quais locais.
* Transações consulte tooall leitura e gravação operações tooAzure armazenamento.
* Saída de dados refere-se toodata transferido fora de uma região do Azure. Quando dados de saudação em sua conta de armazenamento são acessados por um aplicativo que não está em execução no hello mesma região, se que o aplicativo é um serviço de nuvem ou algum outro tipo de aplicativo, em seguida, você é cobrado pela saída de dados. (Para serviços do Azure, você pode fazer as etapas toogroup seus dados e serviços em Olá mesmo dados centers tooreduce ou eliminar encargos de saída de dados.)  

Olá [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage) página fornece informações detalhadas de preços para capacidade de armazenamento, replicação e transações. Olá [detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/) página fornece informações detalhadas de preços para saída de dados.

Para obter detalhes sobre a capacidade e produtividade da conta de armazenamento, confira [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md).

> [!NOTE]
> Quando você cria uma máquina virtual do Azure, uma conta de armazenamento é criada para você automaticamente no local de implantação de saudação se você ainda não tiver uma conta de armazenamento no local. Portanto, não é necessário toofollow etapas de saudação abaixo toocreate uma conta de armazenamento para os discos de máquina virtual. o nome de conta de armazenamento Olá se baseará no nome da máquina virtual hello. Consulte Olá [documentação de máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) para obter mais detalhes.
> 
> 

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
1. Entrar toohello [Portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **novo** na barra de tarefas Olá final Olá Olá página. Escolha **Serviços de Dados** | **Armazenamento** e clique em **Criação Rápida**.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. Em **URL**, insira um nome para a conta de armazenamento.
   
   > [!NOTE]
   > Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.
   > 
   > O nome da sua conta de armazenamento deve ser exclusivo no Azure. Olá Portal clássico do Azure indicará se o nome de conta de armazenamento Olá que selecionar já existe.
   > 
   > 
   
    Consulte [pontos de extremidade de conta de armazenamento](#storage-account-endpoints) abaixo para obter detalhes sobre como o nome de conta de armazenamento hello serão usados tooaddress seus objetos no armazenamento do Azure.
4. Em **local/grupo de afinidade**, selecione um local para sua conta de armazenamento é fechar clientes tooyou ou tooyour. Se dados em sua conta de armazenamento serão acessados de outro serviço do Azure, como uma máquina virtual do Azure ou o serviço de nuvem, talvez você queira tooselect um grupo de afinidade de saudação lista toogroup sua conta de armazenamento Olá mesmo data center com outros serviços do Azure Se você estiver usando tooimprove desempenho e reduzir os custos.
   
    Vale lembrar que você deve selecionar um grupo de afinidades durante a criação de sua conta de armazenamento. Você não pode mover um grupo de afinidade tooan conta existente. Para saber mais sobre grupos de afinidade, confira [Colocalização de serviços com um grupo de afinidade](#service-co-location-with-an-affinity-group) abaixo.
   
   > [!IMPORTANT]
   > toodetermine quais locais estão disponíveis para sua assinatura, você pode chamar hello [lista todos os provedores de recursos](https://msdn.microsoft.com/library/azure/dn790524.aspx) operação. provedores de toolist do PowerShell, chame [Get-AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). No .NET, use Olá [lista](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) método hello ProviderOperationsExtensions classe.
   > 
   > Além disso, veja [Regiões do Azure](https://azure.microsoft.com/regions/#services) para obter mais informações sobre quais serviços estão disponíveis em uma região específica.
   > 
   > 
5. Se você tiver mais de uma assinatura do Azure, Olá **assinatura** campo é exibido. Em **assinatura**, digite Olá assinatura do Azure que deseja que a conta de armazenamento Olá toouse com.
6. Em **replicação**, selecione Olá nível desejado de replicação para sua conta de armazenamento. Olá recomendado a opção de replicação é a replicação com redundância geográfica, o que fornece a durabilidade máxima para seus dados. Para obter mais detalhes sobre as opções de replicação do Armazenamento do Azure, confira [Replicação do Armazenamento do Azure](storage-redundancy.md).
7. Clique em **Criar Conta de Armazenamento**.
   
    Pode levar alguns toocreate de minutos sua conta de armazenamento. status de saudação toocheck, você pode monitorar notificações Olá final Olá Olá Portal clássico do Azure. Depois que tiver sido criada a conta de armazenamento hello, sua nova conta de armazenamento tem **Online** status e está pronto para uso.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Pontos de extremidade da conta de armazenamento
Cada objeto armazenado no Armazenamento do Azure tem um endereço de URL exclusivo. formulários de nome de conta de armazenamento Olá Olá subdomínio do endereço. Hello combinação de nome de subdomínio e domínio, que é o serviço tooeach específico, constitui um *ponto de extremidade* para sua conta de armazenamento.

Por exemplo, se sua conta de armazenamento é chamada *mystorageaccount*, e em seguida, Olá pontos de extremidade padrão para sua conta de armazenamento são:

* Serviço Blob: http://*mystorageaccount*.blob.core.windows.net
* Serviço Tabela: http://*mystorageaccount*.table.core.windows.net
* Serviço Fila: http://*mystorageaccount*.queue.core.windows.net
* Serviço Arquivo: http://*mystorageaccount*.file.core.windows.net

Você pode ver os pontos de extremidade Olá para sua conta de armazenamento no painel de armazenamento de saudação do hello [Portal clássico do Azure](https://manage.windowsazure.com) quando Olá conta foi criada.

Olá URL para acessar um objeto em uma conta de armazenamento é criada, acrescentando o local do objeto Olá no ponto de extremidade toohello conta de armazenamento de saudação. Por exemplo, um endereço de blob pode ter este formato: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

Você também pode configurar um toouse de nome de domínio personalizado com sua conta de armazenamento. Confira [Configurar um nome de domínio personalizado para seu ponto de extremidade do armazenamento de blobs](storage-custom-domain-name.md) para obter detalhes.

### <a name="service-co-location-with-an-affinity-group"></a>Colocalização de serviços com um grupo de afinidade
Um *grupo de afinidades* é um agrupamento geográfico de seus serviços Azure e VMs na conta de armazenamento do Azure. Um grupo de afinidade pode melhorar o desempenho do serviço Localizando cargas de trabalho do computador no mesmo data center ou quase Olá usuário público-alvo de saudação. Além disso, não há cobranças incorrem para saída quando os dados em uma conta de armazenamento são acessados de outro serviço que faz parte da saudação mesmo grupo de afinidade.

> [!NOTE]
> toocreate um grupo de afinidade, hello abrir <b>configurações</b> área da saudação [Portal clássico do Azure](https://manage.windowsazure.com), clique em <b>grupos de afinidade</b>e, em seguida, clique em <b>adicionar um grupo de afinidade</b> ou hello <b>adicionar</b> botão. Você também pode criar e gerenciar grupos de afinidade usando Olá API de gerenciamento de serviços do Azure. Veja <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Operações em grupo de afinidades</a> para saber mais.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>exibir, copiar e regenerar chaves de acesso de armazenamento
Quando você cria uma conta de armazenamento, o Azure gera duas chaves de acesso de armazenamento de 512 bits, que são usadas para autenticação quando a conta de armazenamento Olá é acessada. Fornecendo duas chaves de acesso de armazenamento, o Azure permite que você tooregenerate chaves de saudação com nenhum serviço de armazenamento de tooyour de interrupção ou acesso toothat.

> [!NOTE]
> Recomendamos que você evite compartilhar suas chaves de acesso de armazenamento com outras pessoas. recursos de toostorage toopermit acesso sem emitir suas chaves de acesso, você pode usar um *assinatura de acesso compartilhado*. Uma assinatura de acesso compartilhado fornece acesso tooa recursos em sua conta para um intervalo que você define e com permissões de saudação que você especificar. Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para saber mais.
> 
> 

Em Olá [Portal clássico do Azure](https://manage.windowsazure.com), use **gerenciar chaves** no painel de saudação ou hello **armazenamento** página tooview, copiar e chaves de acesso do armazenamento regenerar hello são usadas tooaccess Olá serviços Blob, tabela e fila.

### <a name="copy-a-storage-access-key"></a>Copiar uma chave de acesso de armazenamento
Você pode usar **gerenciar chaves** toocopy um toouse de chave de acesso de armazenamento em uma cadeia de caracteres de conexão. cadeia de caracteres de conexão de saudação requer o nome de conta de armazenamento hello e uma chave toouse na autenticação. Para obter informações sobre como configurar a conexão cadeias de caracteres tooaccess serviços de armazenamento do Azure, consulte [configurar cadeias de Conexão de armazenamento do Azure](storage-configure-connection-string.md).

1. Em Olá [Portal clássico do Azure](https://manage.windowsazure.com), clique em **armazenamento**e, em seguida, clique em nome de saudação do painel da conta Olá armazenamento tooopen hello.
2. Clique em **Gerenciar Chaves**.
   
     **Gerenciar Chaves de Acesso** é aberta.
   
    ![Managekeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy uma chave de acesso de armazenamento, texto de saudação selecione chave. Em seguida, clique com o botão direito do mouse e clique em **Copiar**.

### <a name="regenerate-storage-access-keys"></a>Regenerar chaves de acesso de armazenamento
É recomendável que você altere a conta de armazenamento de tooyour periodicamente toohelp manter suas conexões de armazenamento seguro de chaves de acesso Olá. Duas chaves de acesso são atribuídas para que você pode manter conta de armazenamento toohello conexões usando uma chave de acesso enquanto você regenera Olá outra chave de acesso.

> [!WARNING]
> Regenerar suas chaves de acesso pode afetar os serviços no Azure, bem como seus próprios aplicativos que dependem da conta de armazenamento hello. Todos os clientes que usam a conta de armazenamento Olá acesso tooaccess chave Olá devem ser a nova chave de saudação toouse atualizado.
> 
> 

**Serviços de mídia** -se você tiver serviços de mídia que dependem de sua conta de armazenamento, você deverá ressincronizar as chaves de acesso de saudação com o serviço de mídia após você regenerar chaves de saudação.

**Aplicativos** - se você tiver aplicativos da web ou essa conta de armazenamento de saudação do uso de serviços de nuvem, você perderá conexões Olá se você regenerar chaves, a menos que você reverter suas chaves. 

**Gerenciadores de armazenamento** - se você estiver usando qualquer [aplicativos do Gerenciador de armazenamento](storage-explorers.md), você provavelmente precisará de chave de armazenamento de saudação tooupdate usado por esses aplicativos.

Este é o processo de saudação para trocar suas chaves de acesso de armazenamento:

1. Atualize cadeias de conexão de saudação em sua chave de acesso secundária do aplicativo código tooreference Olá Olá da conta de armazenamento.
2. Regenere a chave de acesso primária Olá para sua conta de armazenamento. Em Olá [Portal clássico do Azure](https://manage.windowsazure.com), no painel de saudação ou Olá **configurar** , clique em **gerenciar chaves**. Clique em **regenerar** em Olá chave de acesso primária e, em seguida, clique em **Sim** tooconfirm que você deseja toogenerate uma nova chave.
3. Atualize cadeias de conexão de saudação em código tooreference Olá nova chave de acesso primária.
4. Regenere a chave de acesso secundária hello.

## <a name="delete-a-storage-account"></a>Excluir uma conta de armazenamento
tooremove uma conta de armazenamento que você não está usando, use **excluir** no painel de saudação ou hello **configurar** página. **Excluir** exclusões Olá conta de armazenamento inteira, incluindo todos os blobs hello, tabelas e filas na conta de saudação.

> [!WARNING]
> É uma conta de armazenamento excluído o toorestore não é possível ou recuperar conteúdo de saudação que continha antes da exclusão. Ser tooback-se de que qualquer valor que você deseja toosave antes de excluir a conta de saudação. Isso também ocorre para todos os recursos na conta Olá — depois de excluir um blob, tabela, fila ou arquivo, ele será excluído permanentemente.
> 
> Se sua conta de armazenamento contiver arquivos VHD para uma máquina virtual do Azure, você deve excluir qualquer imagens e discos que usam esses arquivos VHD antes de excluir a conta de armazenamento hello. Primeiro interrompa a máquina virtual de saudação se ele está em execução e, em seguida, excluí-lo. discos toodelete, navegar toohello **discos** guia e excluir todos os discos de lá. imagens toodelete, navegar toohello **imagens** guia e excluir as imagens que estão armazenadas na conta de saudação.
> 
> 

1. Em Olá [Portal clássico do Azure](https://manage.windowsazure.com), clique em **armazenamento**.
2. Clique em qualquer lugar na entrada de conta de armazenamento Olá exceto nome hello e, em seguida, clique em **excluir**.
   
     -Ou-
   
    Clique em nome de saudação do painel da conta Olá armazenamento tooopen hello e, em seguida, clique em **excluir**.
3. Clique em **Sim** tooconfirm que deseja que a conta de armazenamento toodelete hello.

## <a name="next-steps"></a>Próximas etapas
* toolearn mais sobre o armazenamento do Azure, consulte Olá [documentação de armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).
* Visite Olá [Blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)

