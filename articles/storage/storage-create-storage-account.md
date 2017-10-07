---
title: "aaaHow toocreate, gerenciar ou excluir uma conta de armazenamento no portal do Azure de saudação | Microsoft Docs"
description: "Criar uma nova conta de armazenamento, gerenciar suas chaves de acesso de conta ou excluir uma conta de armazenamento Olá portal do Azure. Saiba mais sobre contas de armazenamento standard e premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: c11c6509e192170db4812f47c389fc1009b94daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Sobre as contas de armazenamento do Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Visão geral
Uma conta de armazenamento do Azure fornece um namespace exclusivo toostore e acessar os objetos de dados de armazenamento do Azure. Todos os objetos em uma conta de armazenamento são cobrados juntos como um grupo. Por padrão, dados de saudação em sua conta são tooyou somente disponível, proprietário da conta Olá.

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Cobrança de conta de armazenamento
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Quando você cria uma máquina virtual do Azure, uma conta de armazenamento é criada para você automaticamente no local de implantação de saudação se você ainda não tiver uma conta de armazenamento no local. Portanto, não é necessário toofollow etapas de saudação abaixo toocreate uma conta de armazenamento para os discos de máquina virtual. o nome de conta de armazenamento Olá se baseará no nome da máquina virtual hello. Consulte Olá [documentação de máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) para obter mais detalhes.
> 
> 

## <a name="storage-account-endpoints"></a>Pontos de extremidade da conta de armazenamento
Cada objeto armazenado no Armazenamento do Azure tem um endereço de URL exclusivo. formulários de nome de conta de armazenamento Olá Olá subdomínio do endereço. Hello combinação de nome de subdomínio e domínio, que é o serviço tooeach específico, constitui um *ponto de extremidade* para sua conta de armazenamento.

Por exemplo, se sua conta de armazenamento é chamada *mystorageaccount*, e em seguida, Olá pontos de extremidade padrão para sua conta de armazenamento são:

* Serviço Blob: http://*mystorageaccount*.blob.core.windows.net
* Serviço Tabela: http://*mystorageaccount*.table.core.windows.net
* Serviço Fila: http://*mystorageaccount*.queue.core.windows.net
* Serviço Arquivo: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Uma conta de armazenamento de Blob expõe apenas o ponto de extremidade de serviço de Blob hello.
> 
> 

Olá URL para acessar um objeto em uma conta de armazenamento é criada, acrescentando o local do objeto Olá no ponto de extremidade toohello conta de armazenamento de saudação. Por exemplo, um endereço de blob pode ter este formato: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

Você também pode configurar um toouse de nome de domínio personalizado com sua conta de armazenamento. Para as contas de armazenamento clássicas, veja [Configurar um Nome de domínio personalizado para o Ponto de Extremidade do Armazenamento de Blobs](storage-custom-domain-name.md) para obter detalhes. Para contas de armazenamento do Gerenciador de recursos, esse recurso não foi adicionado toohello [portal do Azure](https://portal.azure.com) ainda, mas você pode configurá-lo com o PowerShell. Para obter mais informações, consulte Olá [AzureRmStorageAccount conjunto](https://msdn.microsoft.com/library/mt607146.aspx) cmdlet.  

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, selecione **novo** -> **armazenamento** -> **conta de armazenamento**.
3. Insira um nome para a conta de armazenamento. Consulte [pontos de extremidade de conta de armazenamento](#storage-account-endpoints) para obter detalhes sobre como o nome de conta de armazenamento hello serão usados tooaddress seus objetos no armazenamento do Azure.
   
   > [!NOTE]
   > Os nomes da conta de armazenamento devem ter entre 3 e 24 caracteres e podem conter apenas números e letras minúsculas.
   > 
   > O nome da sua conta de armazenamento deve ser exclusivo no Azure. Olá portal do Azure indicará se o nome de conta de armazenamento Olá que selecionar já está em uso.
   > 
   > 
4. Especificar Olá toobe de modelo de implantação usado: **Gerenciador de recursos de** ou **clássico**. **Gerenciador de recursos** Olá recomenda-se o modelo de implantação. Para saber mais, confira [Noções básicas sobre a implantação do Gerenciador de Recursos e a implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > Contas de armazenamento de blob só podem ser criadas usando o modelo de implantação do Gerenciador de recursos de saudação.
   > 
   > 
5. Selecione o tipo de saudação da conta de armazenamento: **geral** ou **armazenamento de Blob**. **Finalidade geral** é saudação padrão.
   
    Se **geral** foi selecionado, especifique o nível de desempenho Olá: **padrão** ou **Premium**. saudação padrão é **padrão**. Para obter mais detalhes sobre as contas de armazenamento standard e premium, consulte [tooMicrosoft Introdução armazenamento do Azure](storage-introduction.md) e [armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquina Virtual do Azure](storage-premium-storage.md).
   
    Se **armazenamento de Blob** foi selecionado, especifique o nível de acesso de saudação: **acesso** ou **moderado**. saudação padrão é **acesso**. Confira [Armazenamento de Blobs do Azure: camadas Estática e Dinâmica](storage-blob-storage-tiers.md) para saber mais.
6. Selecionar opção de replicação Olá Olá conta de armazenamento: **LRS**, **GRS**, **RA-GRS**, ou **ZRS**. saudação padrão é **RA-GRS**. Para obter mais detalhes sobre as opções de replicação do Armazenamento do Azure, confira [Replicação do Armazenamento do Azure](storage-redundancy.md).
7. Selecione a assinatura Olá no qual você deseja toocreate Olá nova conta de armazenamento.
8. Especifique um novo grupo de recursos ou selecione um grupo de recursos existente. Para saber mais sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
9. Selecione a localização geográfica Olá para sua conta de armazenamento. Veja [Regiões do Azure](https://azure.microsoft.com/regions/#services) para saber mais sobre quais serviços estão disponíveis em qual região.
10. Clique em **criar** toocreate conta de armazenamento de saudação.

## <a name="manage-your-storage-account"></a>Gerenciar sua conta de armazenamento
### <a name="change-your-account-configuration"></a>Alterar a configuração da conta
Depois de criar sua conta de armazenamento, você pode modificar sua configuração, como alterar a opção de replicação Olá usada para a conta hello ou camada de acesso Olá alteração para uma conta de armazenamento de Blob. Em Olá [portal do Azure](https://portal.azure.com), navegar tooyour conta de armazenamento, localize e clique em **configuração** em **configurações** tooview e/ou alteração de configuração de conta hello.

> [!NOTE]
> Dependendo da camada de desempenho Olá escolhidas durante a criação de conta de armazenamento Olá, algumas opções de replicação podem não estar disponíveis.
> 
> 

Alterando a opção de replicação Olá alterará o preço. Para saber mais, veja a página [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) .

Blob contas de armazenamento, alteração da camada de acesso de saudação podem incorrer em encargos de saudação alteram Além disso toochanging o preço. Consulte Olá [Blob contas de armazenamento - preços e faturamento](storage-blob-storage-tiers.md#pricing-and-billing) para obter mais detalhes.

### <a name="manage-your-storage-access-keys"></a>Gerenciar as chaves de acesso de armazenamento
Quando você cria uma conta de armazenamento, o Azure gera duas chaves de acesso de armazenamento de 512 bits, que são usadas para autenticação quando a conta de armazenamento Olá é acessada. Fornecendo duas chaves de acesso de armazenamento, o Azure permite que você tooregenerate chaves de saudação com nenhum serviço de armazenamento de tooyour de interrupção ou acesso toothat.

> [!NOTE]
> Recomendamos que você evite compartilhar suas chaves de acesso de armazenamento com outras pessoas. recursos de toostorage toopermit acesso sem emitir suas chaves de acesso, você pode usar um *assinatura de acesso compartilhado*. Uma assinatura de acesso compartilhado fornece acesso tooa recursos em sua conta para um intervalo que você define e com permissões de saudação que você especificar. Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para saber mais.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Exibir e copiar as chaves de acesso de armazenamento
Em Olá [portal do Azure](https://portal.azure.com), navegar tooyour conta de armazenamento, clique em **todas as configurações** e, em seguida, clique em **chaves de acesso** tooview, copiar e regenerar suas chaves de acesso da conta. Olá **chaves de acesso** folha também inclui cadeias de caracteres de conexão pré-configurada usando suas chaves primárias e secundárias que você pode copiar toouse em seus aplicativos.

#### <a name="regenerate-storage-access-keys"></a>Regenerar chaves de acesso de armazenamento
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
2. Regenere a chave de acesso primária Olá para sua conta de armazenamento. Em Olá **chaves de acesso** folha, clique em **regenerar Key1**e, em seguida, clique em **Sim** tooconfirm que você deseja toogenerate uma nova chave.
3. Atualize cadeias de conexão de saudação em código tooreference Olá nova chave de acesso primária.
4. Acesso secundário Olá regenerar chave Olá mesmo maneira.

## <a name="delete-a-storage-account"></a>Excluir uma conta de armazenamento
tooremove uma conta de armazenamento que você está usando não navegue toohello conta de armazenamento Olá [portal do Azure](https://portal.azure.com)e clique em **excluir**. Excluir uma conta de armazenamento Exclui toda a conta hello, incluindo todos os dados na conta de saudação.

> [!WARNING]
> É uma conta de armazenamento excluído o toorestore não é possível ou recuperar conteúdo de saudação que continha antes da exclusão. Ser tooback-se de que qualquer valor que você deseja toosave antes de excluir a conta de saudação. Isso também ocorre para todos os recursos na conta Olá — depois de excluir um blob, tabela, fila ou arquivo, ele será excluído permanentemente.
> 
> 

toodelete uma conta de armazenamento que está associada uma máquina virtual do Azure, você deve primeiro certifique-se de que nenhum disco de máquina virtual ter sido excluído. Se você não excluir os discos da máquina virtual pela primeira vez, em seguida, quando você tenta toodelete sua conta de armazenamento, você verá uma mensagem de erro semelhante a:

    Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.

Se a conta de armazenamento Olá usa o modelo de implantação clássico hello, você pode remover o disco da máquina virtual Olá seguindo estas etapas no hello [portal do Azure](https://manage.windowsazure.com):

1. Navegue toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Navegue toohello guia de máquinas virtuais.
3. Clique Olá discos guia.
4. Selecione o disco de dados e clique em Excluir o Disco.
5. imagens de disco toodelete, navegue guia imagens da toohello e exclua as imagens que estão armazenadas na conta de saudação.

Para obter mais informações, consulte Olá [documentação de máquina Virtual do Azure](http://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="next-steps"></a>Próximas etapas
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [Armazenamento de Blobs do Azure: camadas estáticas e dinâmicas](storage-blob-storage-tiers.md)
* [Replicação de Armazenamento do Azure](storage-redundancy.md)
* [Configurar cadeias de conexão do Armazenamento do Azure](storage-configure-connection-string.md)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)
* Visite Olá [Blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).

