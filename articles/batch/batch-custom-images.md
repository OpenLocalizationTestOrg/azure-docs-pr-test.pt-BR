---
title: pools de imagens personalizadas de aaaProvision lote do Azure | Microsoft Docs
description: "Você pode criar um lote de computação de pool de uma imagem personalizada tooprovision nós que contêm software hello e os dados que você precisa para seu aplicativo. Imagens personalizadas são uma maneira eficiente tooconfigure toorun de nós de computação suas cargas de trabalho em lotes."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Usar uma imagem personalizada de toocreate um pool de máquinas virtuais

Quando você cria um pool de máquinas virtuais em lote do Azure, você pode especificar uma imagem de máquina virtual (VM) que fornece um sistema de operacional Olá para cada nó de computação no pool de saudação. Você pode criar um pool de máquinas virtuais usando uma imagem do Azure Marketplace ou fornecendo uma imagem de VHD personalizada que você preparou. Quando você fornece uma imagem personalizada, você tem controle sobre como sistema operacional de saudação é configurado no tempo de saudação que cada nó de computação é provisionado. Sua imagem personalizada também pode incluir aplicativos e dados de referência que estão disponíveis em Olá nó de computação assim que ela é provisionada.

Usar uma imagem personalizada pode economizar tempo na obtenção de nós de computação do pool pronto toorun sua carga de trabalho em lotes. Embora você sempre possa usar uma imagem do Azure Marketplace e instalar o software em cada nó de computação depois de ele ser configurado, essa abordagem pode ser menos eficiente do que usar uma imagem personalizada. 

Alguns motivos toouse uma imagem personalizada que está configurada para seu cenário incluem a necessidade de:

- **Configurar o sistema operacional de saudação (SO)** qualquer configuração especial do sistema de operacional Olá pode ser executada em imagem personalizada hello. 
- **Instalar aplicativos grandes.** Instalar aplicativos em uma imagem personalizada é mais eficiente do que instalá-los em cada nó de computação após seu provisionamento.
- **Copiar quantidades significativas de dados.** Se dados Olá imagem personalizada toohello copiado, ele só precisa toobe copiado de uma vez, em vez do nó de computação tooeach, economizando tempo e largura de banda.
- **Reinicialize Olá VM durante o processo de instalação hello.** Reinicializando Olá VM pode ser um processo demorado, especialmente se você tiver um número de nós de computação.

## <a name="prerequisites"></a>Pré-requisitos

- **Uma conta de lote criada com o modo de alocação de pool Olá assinatura de usuário.** toouse pools de máquina Virtual de tooprovision uma imagem personalizada, crie sua conta em lotes com hello assinatura de usuário [modo de alocação de pool](batch-api-basics.md#pool-allocation-mode). Com esse modo, pools de lote são alocados na assinatura Olá onde reside a conta de saudação. Consulte Olá [conta](batch-api-basics.md#account) seção [soluções com o lote de computação paralela em grande escala desenvolver](batch-api-basics.md) para obter informações sobre como definir o modo de alocação de pool de hello quando você criar uma conta de lote.

- **Uma conta de Armazenamento do Azure.** toocreate um pool de máquinas virtuais usando uma imagem personalizada, você precisa de uma conta de armazenamento do Azure padrão, para fins gerais no hello mesma assinatura e região. Se você criar uma imagem personalizada de uma VM do Azure, você copiará Olá imagem toohello conta de armazenamento onde reside do disco do sistema operacional da VM hello e você não precisará toocreate uma conta de armazenamento separada. 
    
## <a name="prepare-a-custom-image"></a>Preparar uma imagem personalizada

tooprepare uma imagem personalizada para uso com o lote, você deve generalizar uma instalação existente do Windows ou do Linux. Generalizar uma instalação de sistema operacional remove informações específicas do computador. resultado de saudação é uma imagem que pode ser instalada em outros computadores ou VMs.  

> [!IMPORTANT]
> Em lotes atualmente não dá suporte usando o Azure gerenciados imagens tooprovision um pool. imagem personalizada Olá você usar tooprovision que um pool deve ser armazenado no armazenamento do Azure. 
>
> Ao preparar sua imagem personalizada, lembre-Olá mente pontos a seguir:
> - Certifique-se de que imagem do sistema operacional base Olá usar tooprovision os pools de lote não tem qualquer pré-instalado extensões do Azure, como a extensão de Script personalizado hello. Se a imagem de saudação contém uma extensão pré-instalados, Azure poderá encontrar problemas Implantando Olá VM.
> - Verifique se essa imagem do sistema operacional base Olá que é fornecer usa Olá unidade temporária do padrão, como hello agente do nó de lote no momento espera unidade temporária do saudação padrão.
>
>

Você pode usar qualquer imagem preparada existente do Windows ou Linux como uma imagem personalizada. Por exemplo, se você deseja que uma imagem local toouse, carregar Olá imagem tooan conta de armazenamento Azure que está em Olá a mesma assinatura e região que sua conta do lote usando [AzCopy](../storage/storage-use-azcopy.md) ou outra ferramenta de carregamento.

Você também pode preparar uma imagem personalizada de uma VM do Azure nova ou existente. Se você estiver criando uma nova VM, você pode usar uma imagem do Azure Marketplace como imagem de base Olá para sua imagem personalizada e, em seguida, personalizá-lo. imagem de base toocustomize Olá, criar uma VM do Azure e adicionar os aplicativos ou dados tooit. Em seguida, generalizar Olá VM tooserve como sua imagem personalizada e salve-a como tooAzure armazenamento. 

tooprepare uma imagem personalizada de uma VM do Azure, siga estas etapas:

1. Crie uma VM do Azure **não gerenciada** em uma imagem do Azure Marketplace. O Azure Marketplace inclui imagens para [Windows](../virtual-machines/windows/quick-create-portal.md) e [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    Na etapa 3 do hello processo de criação de VM, certifique-se de que você selecione **não** para **armazenamento: usar discos gerenciados** opção. Também observe nome de conta de armazenamento Olá para o disco do sistema operacional da VM hello, como a conta de armazenamento também é onde o Azure salvará sua imagem personalizada:

    ![Criar uma VM não gerenciado e o nome de conta de armazenamento Olá Observação](media/batch-custom-images/vm-create-storage.png)
 
2. Concluir o processo de saudação de criar sua VM e aguarde toobe alocado pelo Azure. Aqui está uma imagem que mostra uma VM no portal do Azure no estado de execução de saudação do hello:

    ![Criar uma VM de uma imagem do Marketplace](media/batch-custom-images/vm-status-running.png)

3. Uma vez Olá VM está em execução, conecte-se tooit via RDP (para Windows) ou SSH (para Linux). Instalar qualquer software necessário ou copiar os dados desejados e, em seguida, generalizar Olá VM. Execute as etapas de saudação descritas em [generalizar Olá VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Execute as etapas de saudação muito[login tooAzure PowerShell](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). tooinstall Azure PowerShell, consulte [visão geral do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Em seguida, execute as etapas de saudação muito[Deallocate Olá VM e o conjunto Olá estado toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    Olá portal do Azure, observe que Olá que VM é desalocada:

    ![Certifique-se de que Olá que VM é desalocada.](media/batch-custom-images/vm-status-deallocated.png)

6.  Criar e salvar tooAzure de imagem VM Olá armazenamento usando Olá [AzureRmVMImage salvar](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) cmdlet do PowerShell. Siga as instruções de saudação descritas em [criar imagem de saudação](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    imagem VM Olá é salvo toohello conta de armazenamento do Azure criada quando Olá VM foi criada, conforme mostrado na etapa 1 deste procedimento. Olá salvar AzureRmVMImage cmdlet salva Olá imagem toohello **sistema** contêiner na conta de armazenamento. Olá `-DestinationContainername` nomes de parâmetro de um diretório virtual Olá **sistema** contêiner. Olá `-VHDNamePrefix` parâmetro especifica um prefixo de nome de blob hello. Esse prefixo é o nome de blob de toohello antecedendo com um hífen. 

    Por exemplo, suponha que você chamar Save AzureRmVMImage com hello parâmetros a seguir:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    a imagem resultante Olá é salvo toohello local e o nome do blob mostrado aqui:

    ![Local do VHD salvo no contêiner do sistema](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Uma VM não gerenciada do Azure cria várias contas de armazenamento para finalidades diferentes. Se você não observe o nome de Olá Olá do contêiner de armazenamento de disco Olá SO quando hello VM foi criada, localizar a conta de armazenamento Olá associado que contém Olá **sistema** contêiner. Navegar pelos Olá **sistema** toofind Olá personalizado imagem de contêiner usando valores hello especificados para Olá **AzureRmVMImage salvar** comando.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Criar um pool de uma imagem personalizada no portal de saudação

Após ter salvo sua imagem personalizada e quando souber sua localização, você pode criar um pool do Lote dessa imagem. Siga essas etapas toocreate um pool do hello portal do Azure:

1. Navegue tooyour conta de lote no hello portal do Azure. Essa conta deve ser no hello mesma assinatura e região como armazenamento Olá conta contendo imagem personalizada do hello. 
2. Em Olá **configurações** janela saudação à esquerda, selecione Olá **Pools** item de menu.
3. Em Olá **Pools** janela, selecione Olá **adicionar** comando.
4. Em Olá **Adicionar Pool** janela, selecione **imagem personalizada (Windows/Linux)** de saudação **tipo de imagem** lista suspensa. portal de saudação exibe Olá **imagem personalizada** seletor. Navegue toohello conta de armazenamento onde se encontra a imagem personalizada, e selecione Olá VHD desejado de contêiner de saudação. 
5. Selecione Olá correto **oferta/publicador/Sku** para seu VHD personalizado.
6. Especificar Olá restantes necessárias configurações, incluindo Olá **tamanho de nó**, **dedicado de nós de destino**, e **baixa nós prioridade**, bem como qualquer desejado configurações opcionais.

    Por exemplo, para uma imagem personalizada do Microsoft Windows Server Datacenter 2016, Olá **Adicionar Pool** janela aparece como mostrado aqui:

    ![Adicionar pool de uma imagem personalizada do Windows](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck se um pool existente se baseia em uma imagem personalizada, consulte Olá **sistema operacional** propriedade na seção de resumo de recursos Olá da saudação **Pool** janela. Se o pool de saudação foi criado de uma imagem personalizada, é definido muito**imagem de VM personalizada**.

Todos os VHDs personalizados associados a um pool são exibidos no pool de saudação **propriedades** janela.
 
## <a name="next-steps"></a>Próximas etapas

- Para uma visão geral detalhada do Lote, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md).
- Para obter informações sobre como criar uma conta de lote, consulte [criar uma conta de lote com hello portal do Azure](batch-account-create-portal.md).
