---
title: "configuração de aaaStorage para VMs do SQL Server | Microsoft Docs"
description: "Este tópico descreve como o Azure configura o armazenamento para VMs do SQL Server durante o provisionamento (modelo de implantação do Resource Manager). Também explica como você pode configurar o armazenamento para suas VMs existentes do SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Configuração de armazenamento para VMs do SQL Server
Quando você configurar uma imagem de máquina virtual do SQL Server no Azure, Olá Portal ajuda tooautomate sua configuração de armazenamento. Isso inclui anexar armazenamento toohello VM, tornando esse tooSQL acessível do armazenamento servidor e configurá-lo toooptimize para suas necessidades específicas de desempenho.

Este tópico explica como o Azure configura o armazenamento para suas VMs do SQL Server durante o provisionamento e para VMs existentes. Essa configuração é baseada na Olá [práticas recomendadas de desempenho](virtual-machines-windows-sql-performance.md) para VMs do Azure executando o SQL Server.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Pré-requisitos
Olá toouse automatizada de definições de configuração de armazenamento, sua máquina virtual requer Olá características a seguir:

* Deve ser provisionada com uma [imagem da galeria do SQL Server](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing).
* Olá usa [modelo de implantação do Gerenciador de recursos](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Deve usar o [Armazenamento Premium](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Novas VMs
Olá seções a seguir descrevem como armazenamento tooconfigure para novas máquinas virtuais de SQL Server.

### <a name="azure-portal"></a>Portal do Azure
Ao provisionar uma VM do Azure usando uma imagem da Galeria do SQL Server, você pode escolher tooautomatically configurar armazenamento Olá para sua nova VM. Especifique o tamanho do armazenamento hello, limites de desempenho e o tipo de carga de trabalho. Olá seguinte captura de tela mostra folha de configuração de armazenamento Olá usada durante a VM do SQL de provisionamento.

![Configuração de armazenamento da VM do SQL Server durante o provisionamento](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

Com base nas suas escolhas, o Azure executa Olá tarefas de configuração de armazenamento a seguir depois de criar hello VM:

* Cria e anexa a máquina de virtual toohello do discos de dados de armazenamento premium.
* Configura tooSQL de acessível toobe Server de discos de dados hello.
* Configura os discos de dados Olá no armazenamento de um pool com base em Olá especificado requisitos tamanho e desempenho (IOPS e taxa de transferência).
* Associa o pool de armazenamento Olá com uma nova unidade na máquina virtual de saudação.
* Otimiza essa nova unidade com base em seu tipo de carga de trabalho especificado (Data warehouse, Processamento transacional ou Geral).

Para obter mais detalhes sobre como o Azure configura as configurações de armazenamento, consulte Olá [seção de configuração de armazenamento](#storage-configuration). Para obter uma explicação completa de como toocreate uma VM do SQL Server no hello Portal do Azure, consulte [Olá provisionamento tutorial](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Modelos do Resource Manager
Se você usar Olá modelos do Gerenciador de recursos a seguir, dois discos de dados premium são conectados por padrão, sem nenhuma configuração de pool de armazenamento. No entanto, você pode personalizar esses modelos toochange Olá quantos discos de dados premium que são anexados toohello máquina de virtual.

* [Criar VM com backup automatizado](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Criar VM com aplicação de patch automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Criar VM com integração de AKV](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>VMs existentes
Para VMs existentes do servidor SQL, você pode modificar algumas configurações de armazenamento no hello portal do Azure. Selecione sua VM, vá toohello área de configurações e, em seguida, selecione a configuração do SQL Server. folha de configuração do SQL Server Olá mostra o uso de armazenamento atual Olá da VM. Todas as unidades que existem na sua VM são exibidas neste gráfico. Para cada unidade, o espaço de armazenamento Olá exibe quatro seções:

* Dados SQL
* Log do SQL
* Outros (armazenamento não SQL)
* Disponível

![Configurar o armazenamento para a VM do SQL Server existente](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure Olá armazenamento tooadd uma nova unidade ou estender um disco existente, clique Olá Editar link acima gráfico hello.

Opções de configuração de saudação que você consulte varia dependendo se você usou esse recurso antes. Ao usar o para hello primeira vez, você pode especificar os requisitos de armazenamento para uma nova unidade. Se você tiver usado toocreate esse recurso uma unidade, você pode escolher tooextend armazenamento da unidade.

### <a name="use-for-hello-first-time"></a>Use para Olá primeira vez
Se estiver usando esse recurso pela primeira vez, você pode especificar Olá limites de tamanho e desempenho de armazenamento para uma nova unidade. Essa experiência é semelhante toowhat que você veria no tempo de provisionamento. Olá principal diferença é que você não tem permissão toospecify tipo de carga de trabalho de saudação. Essa restrição impede que interromper quaisquer configurações existentes do SQL Server na máquina virtual de saudação.

![Configurar controles deslizantes de armazenamento do SQL Server](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

O Azure cria uma nova unidade com base em suas especificações. Nesse cenário, o Azure executa Olá tarefas de configuração de armazenamento a seguir:

* Cria e anexa a máquina de virtual toohello do discos de dados de armazenamento premium.
* Configura tooSQL de acessível toobe Server de discos de dados hello.
* Configura os discos de dados Olá no armazenamento de um pool com base em Olá especificado requisitos tamanho e desempenho (IOPS e taxa de transferência).
* Associa o pool de armazenamento Olá com uma nova unidade na máquina virtual de saudação.

Para obter mais detalhes sobre como o Azure configura as configurações de armazenamento, consulte Olá [seção de configuração de armazenamento](#storage-configuration).

### <a name="add-a-new-drive"></a>Adicionar uma nova unidade
Se você já tiver configurado o armazenamento na sua VM do SQL Server, a expansão do armazenamento apresenta duas opções novas. Olá primeira opção é tooadd uma nova unidade, o que pode aumentar o nível de desempenho de saudação da VM.

![Adicionar um novo tooa de unidade SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

No entanto, depois de adicionar unidade Olá, você deve executar algumas aumento de desempenho de configuração manual extra tooachieve hello.

### <a name="extend-hello-drive"></a>Estenda a unidade de saudação
Olá outra opção para expandir o armazenamento é a unidade do tooextend Olá existente. Essa opção aumenta a saudação de armazenamento disponível para sua unidade, mas ele não aumenta o desempenho. Com pools de armazenamento, você não pode alterar o número de saudação de colunas depois Olá pool de armazenamento é criado. número de saudação de colunas determina o número de saudação de gravações paralelas, que podem ser distribuídos em discos de dados de saudação. Portanto, os discos de dados não podem aumentar o desempenho. Só podem fornecer mais armazenamento para dados hello está sendo gravados. Essa limitação também significa que, ao estender unidade hello, número de saudação de colunas determina número mínimo de saudação de discos de dados que você pode adicionar. Então se você criar um pool de armazenamento com discos de quatro dados, Olá número de colunas é também quatro. Qualquer momento que você estender o armazenamento hello, você deve adicionar discos de dados de pelo menos quatro.

![Estender uma unidade para uma VM do SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Configuração de armazenamento
Esta seção fornece uma referência para alterações de configuração do armazenamento hello Azure executa automaticamente durante o provisionamento de VM do SQL ou a configuração em Olá Portal do Azure.

* Se você tiver selecionado menos de dois TBs de armazenamento para sua VM, o Azure não criará um pool de armazenamento.
* Se você tiver selecionado pelo menos de dois TBs de armazenamento para sua VM, o Azure configurará um pool de armazenamento. Olá próxima seção deste tópico fornece detalhes de saudação de configuração do pool de armazenamento hello.
* A configuração de armazenamento automática sempre usa discos de dados P30 do [armazenamento premium](../../../storage/common/storage-premium-storage.md) . Consequentemente, há um mapeamento 1:1 entre o número selecionado de Terabytes e número de saudação de discos de dados anexado tooyour VM.

Para obter informações sobre preços, consulte Olá [preços de armazenamento](https://azure.microsoft.com/pricing/details/storage) página Olá **armazenamento em disco** guia.

### <a name="creation-of-hello-storage-pool"></a>Criação de pool de armazenamento Olá
O Azure usa Olá após o pool de armazenamento configurações toocreate Olá em VMs do SQL Server.

| Configuração | Valor |
| --- | --- |
| Tamanho da distribuição |256 KB (Data warehouse); 64 KB (Transacional) |
| Tamanhos do disco |1 TB cada |
| Cache |Ler |
| Tamanho da alocação |Tamanho da unidade de alocação de NTFS de 64 KB |
| Inicialização de arquivo instantânea |Habilitado |
| Bloquear páginas na memória |Habilitado |
| Recuperação |Recuperação simples (sem resiliência) |
| Número de colunas |Número de discos de dados<sup>1</sup> |
| Local do TempDB |Armazenados em discos de dados<sup>2</sup> |

<sup>1</sup> depois que o pool de armazenamento Olá é criado, não é possível alterar o número de saudação de colunas no pool de armazenamento de saudação.

<sup>2</sup> essa configuração só se aplica a primeira unidade de toohello você cria usando o recurso de configuração de armazenamento de saudação.

## <a name="workload-optimization-settings"></a>Configurações de otimização da carga de trabalho
Olá tabela a seguir descreve Olá três cargas de trabalho tipo opções disponíveis e seus otimizações correspondentes:

| Tipo de carga de trabalho | Descrição | Otimizações |
| --- | --- | --- |
| **Geral** |Configuração padrão que oferece suporte à maioria das cargas de trabalho |Nenhum |
| **Processamento transacional** |Otimiza o armazenamento de saudação para cargas de trabalho OLTP de banco de dados tradicional |Sinalizador de Rastreamento 1117<br/>Sinalizador de Rastreamento 1118 |
| **Data warehouse** |Otimiza o armazenamento de saudação para cargas de trabalho de análise e emissão de relatórios |Sinalizador de Rastreamento 610<br/>Sinalizador de Rastreamento 1117 |

> [!NOTE]
> Você só pode especificar o tipo de carga de trabalho hello quando você provisionar uma máquina virtual do SQL, selecionando-o na etapa de configuração de armazenamento de saudação.
>
>

## <a name="next-steps"></a>Próximas etapas
Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-server-iaas-overview.md).
