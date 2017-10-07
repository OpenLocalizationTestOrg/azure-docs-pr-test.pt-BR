---
title: aaaOverview de lote do Azure para desenvolvedores | Microsoft Docs
description: "Saiba mais recursos de saudação do serviço de lote Olá e suas APIs do ponto de vista do desenvolvimento."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Desenvolva soluções de computação paralela em larga escala com o Lote

Nesta visão geral de componentes essenciais Olá Olá serviço de lote do Azure, vamos abordar os recursos de serviço principal de hello e recursos que os desenvolvedores de lote podem usar paralela em grande escala toobuild soluções de computação.

Se você estiver desenvolvendo um aplicativo de computação distribuído ou serviço que emite direto [API REST] [ batch_rest_api] chamadas ou você estiver usando um Olá [SDKs de lote](batch-apis-tools.md#azure-accounts-for-batch-development), você usará muitos dos recursos de saudação e recursos discutidos neste artigo.

> [!TIP]
> Para um nível mais alto toohello Introdução serviço de lote, consulte [Noções básicas do lote do Azure](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Fluxo de trabalho de serviço do Lote
Olá a seguinte fluxo de trabalho de alto nível é típico de quase todos os aplicativos e serviços que usam o serviço de lote Olá para o processamento de cargas de trabalho paralelas:

1. Carregar Olá **arquivos de dados** que você deseja tooprocess tooan [armazenamento do Azure] [ azure_storage] conta. Lote inclui suporte interno para acessar o armazenamento de BLOBs do Azure e suas tarefas podem baixar esses arquivos muito[nós de computação](#compute-node) quando as tarefas de saudação são executadas.
2. Carregar Olá **arquivos de aplicativo** que as tarefas serão executadas. Esses arquivos podem ser binários ou scripts e suas dependências e são executados por tarefas de saudação em seus trabalhos. As tarefas podem baixar esses arquivos em sua conta de armazenamento, ou você pode usar o hello [pacotes de aplicativos](#application-packages) recurso de lote para implantação e gerenciamento de aplicativos.
3. Crie um [pool](#pool) de nós de computação. Quando você cria um pool, você especifica o número de saudação de nós de computação para o pool de saudação, tamanho e sistema operacional de saudação. Quando cada tarefa no trabalho é executado, ele é atribuído tooexecute em um de nós de saudação em seu pool.
4. Crie um [trabalho](#job). Um trabalho gerencia uma coleção de tarefas. Associe cada pool específico de trabalho tooa onde as tarefas do trabalho serão executado.
5. Adicionar [tarefas](#task) toohello trabalho. Cada tarefa executa o aplicativo hello ou script que você carregou os arquivos de dados de saudação tooprocess baixa de sua conta de armazenamento. Como cada tarefa é concluída, ela pode carregar seu armazenamento de tooAzure de saída.
6. Monitorar o andamento do trabalho e recuperar a saída de tarefa de saudação do armazenamento do Azure.

Olá seções a seguir discutem esses e Olá outros recursos do lote que permitem que seu cenário de computação distribuído.

> [!NOTE]
> É necessário um [conta de lote](#account) toouse Olá serviço de lote. A maioria das soluções do Lote também usa uma conta de [Armazenamento do Azure][azure_storage] para o armazenamento de arquivos e a recuperação. Lote atualmente suporta apenas Olá **geral** tipo de conta de armazenamento, conforme descrito na etapa 5 do [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) na [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Recursos do serviço de lote
Alguns dos Olá recursos – contas a seguir computação nós, pools, trabalhos e tarefas — seja exigidas por todas as soluções que usam o serviço de lote de saudação. Outros, como agendas de trabalho e pacotes de aplicativos, são recursos úteis, mas opcionais.

* [Conta](#account)
* [Nó de computação](#compute-node)
* [Pool](#pool)
* [Trabalho](#job)

  * [Agendas de trabalho](#scheduled-jobs)
* [Tarefa](#task)

  * [Iniciar tarefa](#start-task)
  * [Tarefa do Gerenciador de Trabalhos](#job-manager-task)
  * [Tarefas de preparação e liberação do trabalho](#job-preparation-and-release-tasks)
  * [MPI (tarefa de várias instâncias)](#multi-instance-tasks)
  * [Dependências da tarefa](#task-dependencies)
* [Pacotes de aplicativos](#application-packages)

## <a name="account"></a>Conta
Uma conta de lote é uma entidade identificada exclusivamente no serviço de lote de saudação. Todo o processamento é feito por meio de uma conta do Lote.

Você pode criar uma conta de lote do Azure usando Olá [portal do Azure](batch-account-create-portal.md) ou programaticamente, como com hello [biblioteca Batch Management .NET](batch-management-dotnet.md). Ao criar conta hello, você pode associar uma conta de armazenamento do Azure.

### <a name="pool-allocation-mode"></a>Modo de alocação de pools

Quando você cria uma conta do Lote, pode especificar como os [pools](#pool) dos nós de computação são alocados. Você pode escolher tooallocate pools de nós de computação em uma assinatura gerenciada pelo lote do Azure, ou pode ser alocada em sua própria assinatura. Olá *modo de alocação de pool* propriedade conta Olá determina onde os pools são alocados. 

toodecide qual pool toouse do modo de alocação, considere que melhor se adapta a sua situação:

* **Serviço de lote**: serviço de lote é o modo para alocação de pool do padrão hello, no qual os pools são alocados em segundo plano da saudação em assinaturas gerenciado do Azure. Tenha em mente estes pontos-chave sobre o modo de alocação de pool de serviço de lote hello:

    - modo de alocação de pool de serviço de lote Olá oferece suporte a pools de serviço de nuvem e máquina Virtual.
    - Olá modo de alocação de pool do serviço de lote oferece suporte tanto a autenticação chave compartilhada ou [autenticação do Active Directory do Azure](batch-aad-auth.md) (AD do Azure). 
    - Você pode usar qualquer um de nós de computação dedicado ou de baixa prioridade em pools alocados com o modo de alocação de pool de serviço de lote hello.
    - Não use o modo de alocação de pool de serviço de lote Olá se você planeja toocreate pools de máquina virtual do Azure de imagens VM personalizadas, ou se você planejar toouse uma rede virtual. Crie sua conta com o modo de alocação de pool Olá assinatura de usuário.
    - Pools de máquina virtual provisionados em uma conta criada com o modo de alocação de pool de serviço de lote Olá devem ser criados de [Marketplace de máquinas virtuais do Azure] [ vm_marketplace] imagens.

* **Assinatura de usuário**: com o modo de alocação de pool de assinatura de usuário hello, pools de lote são alocados em Olá assinatura do Azure em que a conta de saudação é criada. Tenha em mente estes pontos-chave sobre o modo de alocação de pool de assinatura de usuário hello:
     
    - modo de alocação de pool de assinatura de usuário Olá oferece suporte a apenas os pools de máquina Virtual. Ele não dá suporte a pools dos Serviços de Nuvem.
    - pools de máquina Virtual toocreate de imagens da VM ou toouse uma rede virtual personalizado com pools de máquina Virtual, você deve usar o modo de alocação de pool de assinatura de usuário hello.  
    - Você deve usar [autenticação do Active Directory do Azure](batch-aad-auth.md) com pools são alocados na assinatura de usuário hello. 
    - Você deve configurar um cofre de chaves do Azure para sua conta de lote se o modo de alocação de pool de saudação é definido tooUser assinatura. 
    - Você pode usar nós de computação dedicado somente nos pools em uma conta criada com o modo de alocação de pool Olá assinatura de usuário. Não há suporte para nós de baixa prioridade.
    - Pools de máquina virtual provisionados em uma conta com o modo de alocação de pool Olá assinatura de usuário podem ser criados de [Marketplace de máquinas virtuais do Azure] [ vm_marketplace] imagens ou de personalizado imagens que você fornece.

Olá, a tabela a seguir compara os modos de alocação de pool de serviço de lote e assinatura de usuário de saudação.

| **Modo de alocação de pools**                 | **Serviço em Lotes**                                                                                       | **Assinatura de Usuário**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Os pools são alocados em**               | Em uma assinatura gerenciada pelo Azure                                                                           | assinatura de usuário Olá no qual Olá lote conta é criada                        |
| **Configurações com suporte**             | <ul><li>Configuração do Serviço de Nuvem</li><li>Configuração da Máquina Virtual (Linux e Windows)</li></ul> | <ul><li>Configuração da Máquina Virtual (Linux e Windows)</li></ul>                |
| **Imagens de VM com suporte**                  | <ul><li>Imagens do Azure Marketplace</li></ul>                                                              | <ul><li>Imagens do Azure Marketplace</li><li>Imagens personalizadas</li></ul>                   |
| **Tipos de nós de computação com suporte**         | <ul><li>Nós dedicados</li><li>Nós de baixa prioridade</li></ul>                                            | <ul><li>Nós dedicados</li></ul>                                                  |
| **Autenticação com suporte**             | <ul><li>Chave compartilhada</li><li>AD do Azure</li></ul>                                                           | <ul><li>AD do Azure</li></ul>                                                         |
| **Azure Key Vault obrigatório**             | Não                                                                                                      | Sim                                                                                |
| **Cota de núcleos**                           | Determinado pela cota de núcleos do Lote                                                                          | Determinado pela cota de núcleos da assinatura                                              |
| **Suporte a VNet (Rede Virtual) do Azure** | Pools criados com hello configuração de serviço de nuvem                                                      | Pools criados com hello configuração da máquina Virtual                               |
| **Modelo de implantação de rede virtual com suporte**      | VNets criadas com o modelo de implantação clássico                                                             | Vnets criado com o modelo de implantação clássico hello ou Gerenciador de recursos do Azure |

## <a name="azure-storage-account"></a>Conta de Armazenamento do Azure

A maioria das soluções do Lote usa o Armazenamento do Azure para armazenar arquivos de recurso e de saída.  

Lote atualmente suporta apenas tipo de conta de armazenamento de uso geral hello, conforme descrito na etapa 5 do [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) na [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md). As tarefas do Lote (incluindo as tarefas padrão, tarefas iniciais, tarefas de preparação do trabalho e tarefas de liberação do trabalho) devem especificar os arquivos de recurso que residem nas contas de armazenamento de finalidade geral.


## <a name="compute-node"></a>Nó de computação
Um nó de computação é uma máquina virtual do Azure (VM) ou a máquina virtual que é dedicado tooprocessing uma parte da carga de trabalho do aplicativo de serviço de nuvem. tamanho de saudação de um nó determina o número de saudação de núcleos de CPU, capacidade de memória e tamanho do sistema de arquivo local que é alocado toohello nó. Você pode criar pools de nós do Windows ou Linux por meio de serviços de nuvem do Azure, imagens de saudação [Marketplace de máquinas virtuais do Azure][vm_marketplace], ou imagens personalizadas que você preparar. Veja a seguir Olá [Pool](#pool) para obter mais informações sobre essas opções.

Nós podem executar qualquer script ou executável que é suportado pelo ambiente de sistema operacional de saudação do nó de saudação. Isso inclui \*.exe, \*.cmd, \*.bat e os scripts do PowerShell para Windows e binários, shell e scripts Python para Linux.

Todos os nós de computação no Lote também incluem:

* Uma [estrutura de pastas](#files-and-directories) padrão e as [variáveis de ambiente](#environment-settings-for-tasks) associadas disponíveis para a referência por tarefas.
* **Firewall** as configurações que são definidas toocontrol acesso.
* [Acesso remoto](#connecting-to-compute-nodes) tooboth Windows Remote Desktop Protocol (RDP) e nós do Linux (Secure Shell (SSH)).

## <a name="pool"></a>pool
Um pool é uma coleção de nós na qual seu aplicativo é executado. Olá pool pode ser criado manualmente por você ou automaticamente pelo serviço de lote de hello quando você especificar Olá toobe de trabalho concluído. Você pode criar e gerenciar um pool que atenda aos requisitos de recursos de saudação do seu aplicativo. Um pool pode ser usado somente por conta do lote Olá no qual ele foi criado. Uma conta do Batch pode ter mais de um pool.

Criar pools de lote do Azure na parte superior da plataforma de computação do Azure Olá principal. Eles fornecem alocação em larga escala, instalação de aplicativos, distribuição de dados, monitoramento de integridade e ajuste flexível do número de saudação de nós de computação em um pool ([dimensionamento](#scaling-compute-resources)).

Cada nó que é adicionado tooa pool é atribuído um nome exclusivo e o endereço IP. Quando um nó for removido de um pool, quaisquer alterações feitas no sistema de operacional toohello ou arquivos serão perdidas, e seu nome e endereço IP são liberados para uso futuro. Quando um nó deixa um pool, seu tempo de vida termina.

Quando você cria um pool, você pode especificar Olá atributos a seguir. Algumas configurações forem diferentes, dependendo do modo de alocação de pool Olá de saudação lote [conta](#account):

- Sistema operacional e versão do nó de computação
- Tipo de nó de computação e número de nós de destino
- Tamanho de nós de computação Olá
- Política de dimensionamento
- Política de agendamento de tarefas
- Status de comunicação de nós de computação
- Tarefas iniciais para nós de computação
- pacotes de aplicativos
- Configuração de rede

Cada uma dessas configurações é descrita mais detalhadamente nas seções a seguir de saudação.

> [!IMPORTANT]
> Contas de lote criadas com o modo de alocação de pool de serviço de lote Olá têm uma cota padrão que limita o número de saudação de núcleos em uma conta de lote. número de saudação de núcleos corresponde toohello número de nós de computação. Você pode encontrar as cotas de padrão de saudação e instruções sobre como muito[aumentar cota](batch-quota-limit.md#increase-a-quota) na [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md). Se o pool não é para alcançar seu número de destino de nós, cota de núcleo Olá pode ser motivo de saudação.
>
>Contas de lote criadas com o modo de alocação de pool de assinatura de usuário Olá não observar as cotas do serviço de lote hello. Em vez disso, eles compartilham em Olá Olá cota principal especificado assinatura. Para saber mais, confira[Limites das Máquinas Virtuais](../azure-subscription-service-limits.md#virtual-machines-limits) e [Assinatura e limites de serviço, cotas e restrições do Azure](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Sistema operacional e versão do nó de computação

Quando você cria um pool de lote, você pode especificar a configuração de máquina virtual do Azure hello e o tipo de saudação de deseja toorun em cada nó de computação no pool de saudação do sistema operacional. Olá dois tipos de configurações disponíveis em lote são:

- Olá **configuração de máquina Virtual**, que especifica o pool Olá é composta de máquinas virtuais do Azure. Essas máquinas virtuais podem ser criadas de imagens Linux ou Windows. 

    Quando você cria um pool com base em Olá configuração da máquina Virtual, você deve especificar não somente o tamanho de saudação de nós hello e origem de saudação do hello imagens usadas toocreate-los, mas também Olá **referência de imagem de máquina virtual** e hello Lote **agente nó SKU** toobe instalada em nós de saudação. Para saber mais sobre como especificar essas propriedades de pool, confira [Provisionar nós de computação do Linux em pools do Lote do Azure](batch-linux-nodes.md).

- Olá **configuração de serviços de nuvem**, que especifica o pool Olá é composto por nós de serviços de nuvem do Azure. Os Serviços de Nuvem fornecem *somente* nós de computação do Windows.

    Sistemas operacionais disponíveis para pools de configuração de serviços de nuvem são listados no hello [versões do sistema operacional de convidado do Azure e matriz de compatibilidade do SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Quando você cria um pool que contém nós de serviços de nuvem, é necessário que o tamanho de nó toospecify hello e sua *família de sistemas operacionais*. Serviços de nuvem são implantado tooAzure mais rapidamente do que as máquinas virtuais que executam o Windows. Se você deseja ter pools de nós de computação do Windows, pode achar os Serviços de Nuvem mais vantajosos no desempenho em relação a tempo de implantação.

    * Olá *família de sistemas operacionais* também determina quais versões do .NET são instalados com hello sistema operacional.
    * Como com funções de trabalho em serviços de nuvem, você pode especificar um *versão do sistema operacional* (para obter mais informações sobre funções de trabalho, consulte Olá [sobre serviços de nuvem](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) seção Olá [serviços de nuvem Visão geral](../cloud-services/cloud-services-choose-me.md)).
    * Como com funções de trabalho, é recomendável que você especifique `*` para Olá *versão do sistema operacional* para que nós Olá são atualizados automaticamente, e não há nenhum trabalho necessário toocater toonewly lançada versões. caso de uso primário Olá para selecionar uma versão específica do sistema operacional é tooensure compatibilidade de aplicativos, que permite que o teste toobe executada antes de permitir Olá versão toobe atualizado de compatibilidade com versões anteriores. Após a validação, Olá *versão do sistema operacional* Olá pool pode ser atualizado e pode ser instalada a nova imagem do SO hello – tarefas em execução são interrompidas e retirada da fila.

Quando você cria um pool, você precisa tooselect Olá apropriado **nodeAgentSkuId**, dependendo da saudação de sistema operacional da imagem de base de saudação do seu VHD. Você pode obter um mapeamento de nó disponível agente IDs de SKU tootheir referências de imagem do sistema operacional, chamada hello [lista suporte nó agente SKUs](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) operação.

Consulte Olá [conta](#account) seção para obter informações sobre como definir o modo de alocação de pool de hello quando você criar uma conta de lote.

#### <a name="custom-images-for-virtual-machine-pools"></a>Imagens personalizadas para pools de máquina virtual

toouse pools de máquina Virtual de tooprovision uma imagem personalizada, crie sua conta em lotes com o modo de alocação de pool de assinatura de usuário hello. Com esse modo, pools de lote são alocados na assinatura Olá onde reside a conta de saudação. Consulte Olá [conta](#account) seção para obter informações sobre como definir o modo de alocação de pool de hello quando você criar uma conta de lote.

toouse uma imagem personalizada, você precisará imagem de saudação tooprepare generalizando-lo. Para obter informações sobre como preparar imagens personalizadas do Linux de VMs do Azure, consulte [toouse uma VM do Linux do Azure como um modelo de captura](../virtual-machines/linux/capture-image-nodejs.md). Para obter informações sobre como preparar imagens personalizadas do Windows de VMs do Azure, confira [Criar imagens de VM personalizadas com o Azure PowerShell](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Ao preparar sua imagem personalizada, lembre-se no seguinte de saudação mente:
> - Certifique-se de que imagem do sistema operacional base Olá usar tooprovision os pools de lote não tem qualquer pré-instalado extensões do Azure, como a extensão de Script personalizado hello. Se a imagem de saudação contém uma extensão pré-instalados, Azure poderá encontrar problemas Implantando Olá VM.
> - Verifique se essa imagem do sistema operacional base Olá que é fornecer usa Olá unidade temporária do padrão, como hello agente do nó de lote no momento espera unidade temporária do saudação padrão.
>
>

toocreate um pool de configuração de máquina Virtual usando uma imagem personalizada, você precisará de um ou mais padrão armazenamento do Azure contas toostore suas imagens VHD personalizadas. As imagens personalizadas são armazenadas como blobs. tooreference personalizados imagens quando você cria um pool, especifique Olá URIs de blobs VHD de imagem personalizada Olá para Olá [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) propriedade Olá [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) propriedade.

Certifique-se de que suas contas de armazenamento atendem Olá critérios a seguir:   

- contas de armazenamento Olá contendo Olá imagem personalizada VHD blobs necessário toobe em Olá mesma assinatura conforme Olá conta em lotes (assinatura de usuário Olá).
- Olá especificado contas de armazenamento precisam toobe em Olá mesma região Olá conta do lote.
- No momento, somente as contas de armazenamento padrão de uso geral têm suporte. Armazenamento Premium do Azure terão suporte na Olá futuras.
- Você pode especificar uma conta de armazenamento com vários blobs VHD personalizados ou várias contas de armazenamento, cada uma com um único blob. Recomendamos que você toouse contas de armazenamento vários tooget um melhor desempenho.
- Pode dar suporte a um blob VHD de imagem personalizada exclusivo too40 que instâncias de VM do Linux ou 20 instâncias de VM do Windows. Você precisará toocreate cópias dos pools de toocreate de blob Olá VHD com mais VMs. Por exemplo, um pool com 200 máquinas virtuais do Windows precisa 10 blobs VHD exclusivos especificados para Olá **osDisk** propriedade.

toocreate um pool de uma imagem personalizada usando Olá portal do Azure:

1. Navegue tooyour conta de lote no hello portal do Azure.
2. Em Olá **configurações** folha, selecione Olá **Pools** item de menu.
3. Em Olá **Pools** folha, selecione Olá **adicionar** comando; Olá **Adicionar pool** folha será exibida.
4. Selecione **imagem personalizada (Windows/Linux)** de saudação **tipo de imagem** lista suspensa. portal de saudação exibe Olá **imagem personalizada** seletor. Escolha um ou mais VHDs Olá Olá mesmo do contêiner e clique em **selecione** botão. 
    Suporte para vários VHDs de contas de armazenamento diferentes e diferentes contêineres será adicionado em Olá futuras.
5. Selecione Olá correto **oferta/publicador/Sku** para seus VHDs personalizados, selecione Olá desejado **cache** modo, em seguida, preencha todas Olá outros parâmetros para o pool de saudação.
6. toocheck se um pool é baseado em uma imagem personalizada, consulte Olá **sistema operacional** propriedade na seção de resumo de recursos Olá da saudação **Pool** folha. Olá valor dessa propriedade deve ser **imagem de VM personalizada**.
7. Todos os VHDs personalizados associados a um pool são exibidos no pool de saudação **propriedades** folha.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Tipo de nó de computação e número de nós de destino

Quando você cria um pool, você pode especificar quais tipos de nós de computação desejado e hello número de destino para cada um. Olá dois tipos de nós de computação são:

- **Nós de computação dedicados.** Nós de computação dedicados são reservados para suas cargas de trabalho. Eles são mais caros do que nós de baixa prioridade, mas eles não têm garantia toonever superado.

- **Nós de computação de baixa prioridade.** Nós de baixa prioridade tirar proveito da capacidade excedente no Azure toorun suas cargas de trabalho em lotes. Nós de baixa prioridade são mais baratos por hora do que nós dedicados e permitem cargas de trabalho que exigem muita capacidade de computação. Para obter mais informações, consulte [Usar VMs de baixa prioridade com o Lote](batch-low-pri-vms.md).

    Pode ocorrer preempção de nós de computação de baixa prioridade quando o Azure tem capacidade excedente insuficiente. Se um nó é superado durante a execução de tarefas, tarefas de saudação são retirada da fila e execute novamente depois que um nó de computação fica disponível novamente. Os nós de baixa prioridade são uma boa opção para cargas de trabalho em que o tempo de conclusão do trabalho de saudação é flexível e trabalho Olá é distribuído entre vários nós. Antes de decidir toouse nós de baixa prioridade para seu cenário, certifique-se de que qualquer trabalho perdido devido toopreemption será toorecreate mínima e fácil.

    Nós de computação de baixa prioridade estão disponíveis apenas para contas de lote criadas com o modo de alocação de pool de saudação definido muito**serviço de lote**.

É possível ter ambos os nós de computação dedicado e de baixa prioridade em Olá mesmo pool. Cada tipo de nó &mdash; dedicado e de baixa prioridade &mdash; tem sua própria configuração de destino, para o qual você pode especificar o número de saudação desejado de nós. 
    
Olá, número de nós de computação é chamado tooas um *destino* porque, em algumas situações, o pool pode não alcançar número desejado de saudação de nós. Por exemplo, um pool talvez não obtenha o destino de saudação se atingir Olá [cota de núcleo](batch-quota-limit.md) de lote de sua conta primeiro. Ou, o pool de saudação talvez não obtenha o destino Olá se você aplicou um dimensionamento automático pool toohello fórmulas que limita o número máximo de saudação de nós.

Para informações sobre preços de ambos os nós de computação de baixa prioridade e dedicado, consulte [Preços de Lote](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Tamanho de nós de computação Olá

**Configuração dos Serviços de Nuvem** são listados em [Tamanhos para Serviços de Nuvem](../cloud-services/cloud-services-sizes-specs.md). O Lote dá suporte a todos os tamanhos de Serviços de Nuvem, exceto `ExtraSmall`, `STANDARD_A1_V2` e `STANDARD_A2_V2`.

Os tamanhos de nós de computação da **Configuração de Máquina Virtual** são listados em [Tamanhos de máquinas virtuais no Azure](../virtual-machines/linux/sizes.md) (Linux) e [Tamanhos de máquinas virtuais no Azure](../virtual-machines/windows/sizes.md) (Windows). O Lote dá suporte a todos os tamanhos de VM do Azure, exceto `STANDARD_A0` e aqueles com armazenamento premium (série `STANDARD_GS`, `STANDARD_DS` e `STANDARD_DSV2`).

Ao selecionar um tamanho de nó de computação, considere as características de saudação e requisitos de aplicativos de saudação que em nós hello, você executará. Aspectos como se o aplicativo hello é multi-threaded e a quantidade de memória consome pode ajudar a determinam o tamanho de nó de mais adequada e econômica de saudação. É típico tooselect um tamanho de nó, supondo que uma tarefa será executada em um nó por vez. No entanto, é possível toohave várias tarefas (e, portanto, várias instâncias de aplicativo) [executados em paralelo](batch-parallel-node-tasks.md) em nós de computação durante a execução do trabalho. Nesse caso, é comum toochoose uma maior nó tamanho tooaccommodate Olá maior demanda de execução de tarefas paralelas. Confira [Política de agendamento](#task-scheduling-policy) de tarefas para obter mais informações.

Todos os nós de saudação em um pool de são Olá mesmo tamanho. Se você pretende toorun aplicativos com diferentes requisitos de sistema e/ou níveis de carga, é recomendável que você use grupos separados.

### <a name="scaling-policy"></a>Política de dimensionamento

Para cargas de trabalho dinâmicas, você pode escrever e aplicar um [fórmula de dimensionamento automático](#scaling-compute-resources) tooa pool. Olá serviço de lote periodicamente avalia a fórmula e ajusta Olá número de nós no pool de saudação com base no pool, trabalho e parâmetros da tarefa que você pode especificar vários.

### <a name="task-scheduling-policy"></a>Política de agendamento de tarefas

Olá [máximo de tarefas por nó](batch-parallel-node-tasks.md) opção de configuração determina o número de máximo de saudação de tarefas que podem ser executados em paralelo em cada nó de computação no pool de saudação.

configuração padrão de saudação especifica que uma tarefa de cada vez é executado em um nó, mas há situações em que é benéfico toohave duas ou mais tarefas executadas simultaneamente em um nó. Consulte Olá [cenário de exemplo](batch-parallel-node-tasks.md#example-scenario) em Olá [tarefas simultâneas do nó](batch-parallel-node-tasks.md) toosee artigo como você pode se beneficiar de várias tarefas por nó.

Você também pode especificar um *tipo de preenchimento* que determina se a opção em lotes distribui tarefas Olá igualmente entre todos os nós em um pool ou pacotes de cada nó com o número máximo de saudação de tarefas antes de atribuir o nó de tooanother de tarefas.

### <a name="communication-status-for-compute-nodes"></a>Status de comunicação de nós de computação

Na maioria dos cenários, tarefas operam de forma independente e não é necessário toocommunicate uns com os outros. No entanto, há alguns aplicativos em que as tarefas precisam se comunicar, como os [cenários MPI](batch-mpi.md).

Você pode configurar um pool tooallow **na comunicação**, de modo que nós dentro de um pool podem se comunicar em tempo de execução. Quando a comunicação entre nós é habilitada, os nós nos pools de Configuração dos Serviços de Nuvem podem comunicar-se uns com os outros nas portas acima de 1100 e os pools de Configuração da Máquina Virtual não restringem o tráfego em nenhuma porta.

Observe que habilitar na comunicação também afeta o posicionamento de saudação de nós de saudação em clusters e pode limitar o número máximo de saudação de nós em um pool de devido a restrições de implantação. Se seu aplicativo não precisar de comunicação entre os nós, Olá serviço de lote pode alocar pool toohello de um número potencialmente grande de nós de clusters diferentes muitas e data centers tooenable maior capacidade de processamento paralelo.

### <a name="start-tasks-for-compute-nodes"></a>Tarefas iniciais para nós de computação

Olá opcional *Iniciar tarefa* como nó une pool Olá, e cada vez que um nó é reiniciado ou recriar a imagem é executado em cada nó. tarefa de início de saudação é especialmente útil para preparar nós de computação para a execução de tarefas, como a instalação de aplicativos de saudação que as tarefas executar em nós de computação de saudação hello.

### <a name="application-packages"></a>pacotes de aplicativos

Você pode especificar [pacotes de aplicativos](#application-packages) toodeploy toohello nós de computação no pool de saudação. Pacotes de aplicativos fornecem uma implantação simplificada e controle de versão de aplicativos Olá executar suas tarefas. Os pacotes de aplicativos que você especifica para um pool são instalados em cada nó que ingressa no pool e sempre que um nó é reinicializado ou sua imagem é recriada.

> [!NOTE]
> Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017. Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem. Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos. Para obter mais informações sobre como usar o aplicativo pacotes toodeploy seus nós de lote de tooyour de aplicativos, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Configuração de rede

Você pode especificar a sub-rede de saudação de um Azure [rede virtual (VNet)](../virtual-network/virtual-networks-overview.md) na computação do pool que Olá nós devem ser criados. Consulte Olá [configuração do Pool de rede](#pool-network-configuration) para obter mais informações.


## <a name="job"></a>Trabalho
Um trabalho é uma coleção de tarefas. Ele gerencia como computação é executada por suas tarefas em nós de computação de saudação em um pool.

* trabalho de saudação especifica Olá **pool** no qual Olá trabalho é toobe executar. Você pode criar um novo pool para cada trabalho ou usar um pool para vários trabalhos. Você pode criar um pool para cada trabalho associado a um agendamento de trabalho ou para todos os trabalhos associados a um agendamento de trabalho.
* Você pode especificar uma **prioridade de trabalho**opcional. Quando um trabalho é enviado com uma prioridade mais alta que os trabalhos que estão atualmente em andamento, tarefas Olá para o trabalho de maior prioridade Olá são inseridas na fila de saudação à frente de tarefas para trabalhos de prioridade mais baixa hello. As tarefas com prioridade mais baixa que já estejam em execução não são antecipadas.
* Você pode usar o trabalho **restrições** toospecify certos limites para os seus trabalhos:

    Você pode definir um **tempo máximo wallclock**, de modo que se um trabalho for executado por mais de tempo de wallclock máximo de saudação for especificado, o trabalho hello e todas as suas tarefas são encerradas.

    O Lote pode detectar e repetir as tarefas com falha. Você pode especificar Olá **número máximo de tentativas de tarefa** como uma restrição, incluindo se uma tarefa é *sempre* ou *nunca* repetida. Repetir uma tarefa significa que essa tarefa Olá toobe retirada da fila, execute novamente.
* O aplicativo cliente pode adicionar o trabalho de tooa de tarefas, ou você pode especificar um [tarefa do Gerenciador de trabalho](#job-manager-task). Uma tarefa do Gerenciador de trabalho contém informações de saudação que é necessário toocreate Olá necessário tarefas para um trabalho, com a tarefa do Gerenciador de trabalho hello está sendo executada em uma saudação nós de computação no pool de saudação. Olá tarefa do Gerenciador de trabalho é tratada especificamente pelo lote – ele está na fila assim que o trabalho Olá é criado e é reiniciado quando ele falhar. É uma tarefa do Gerenciador de trabalho *necessária* para trabalhos que são criados por um [agenda de trabalho](#scheduled-jobs) porque ele é Olá somente toodefine Olá tarefas antes do trabalho de saudação é instanciado.
* Por padrão, trabalhos permanecem no estado ativo hello quando todas as tarefas no trabalho Olá forem concluídas. Você pode alterar esse comportamento para que hello trabalho será encerrado automaticamente quando todas as tarefas no trabalho Olá forem concluídas. Do trabalho de conjunto Olá **onAllTasksComplete** propriedade ([OnAllTasksComplete] [ net_onalltaskscomplete] no lote .NET) muito*terminatejob* tooautomatically Encerre trabalho hello quando todas as suas tarefas estão em estado de saudação concluída.

    Observe que o serviço de lote Olá considera um trabalho com *sem* toohave tarefas conclusão de todas as suas tarefas. Portanto, essa opção é mais comumente usada com uma [tarefa do gerenciador de trabalhos](#job-manager-task). Se desejar que o encerramento do trabalho automática toouse sem um Gerenciador de trabalhos, inicialmente você deve definir um novo trabalho **onAllTasksComplete** propriedade muito*noaction*, em seguida, defini-lo muito*terminatejob* somente depois que você terminar de adicionar o trabalho de toohello de tarefas.

### <a name="job-priority"></a>prioridade de trabalho
Você pode atribuir um toojobs de prioridade que você cria no lote. Olá serviço de lote usa o valor de prioridade de saudação da ordem de saudação do hello trabalho toodetermine de agendamento de trabalho em uma conta (isso não é toobe confundido com um [trabalho agendado](#scheduled-jobs)). os valores de prioridade Olá variam de -1000 too1000, com -1000 sendo a prioridade mais baixa hello e 1000 hello mais alta. prioridade de saudação tooupdate de um trabalho, chamada hello [atualizar propriedades de saudação de um trabalho] [ rest_update_job] operação em lote REST (), ou modificar Olá [CloudJob.Priority] [ net_cloudjob_priority] propriedade (lote .NET).

Dentro de saudação mesma conta, maior prioridade trabalhos têm precedência sobre os trabalhos de prioridade mais baixa de agendamento. Um trabalho com valor de prioridade mais alto em uma conta não tem precedência no agendamento sobre outro trabalho com valor de prioridade mais baixo em uma conta diferente.

O plano de trabalho em pools é independente. Entre pools diferentes, não é garantido que um trabalho com prioridade mais alta seja agendado primeiro, caso faltem nós ociosos em seu pool associado. Em Olá mesmo pool, trabalhos com hello mesmo nível de prioridade têm a mesma chance de ser agendado.

### <a name="scheduled-jobs"></a>Trabalhos agendados
[Agendas de trabalho] [ rest_job_schedules] permitem toocreate de trabalhos recorrentes em Olá serviço de lote. Uma agenda de trabalho especifica quando toorun trabalhos e inclui as especificações de saudação de saudação trabalhos toobe executar. Você pode especificar a duração de saudação da agenda hello – quanto tempo e quando agenda hello está em vigor – e frequência os trabalhos são criados durante a saudação agendado período.

## <a name="task"></a>Tarefa
Uma tarefa é uma unidade de computação que está associada a um trabalho. Ela é executada em um nó. Tarefas atribuídas nó tooa para execução ou são enfileiradas até que um nó fique livre. Em suma, uma tarefa executa um ou mais programas ou scripts em um computação nó tooperform Olá trabalho que é necessário.

Ao criar uma tarefa, você pode especificar:

* Olá **linha de comando** para tarefas de saudação. Esta é a linha de comando Olá que executa o aplicativo ou script no nó de computação hello.

    É importante toonote que Olá a linha de comando não executa em um shell. Portanto, ele nativamente não pode tirar proveito dos recursos de shell como [variável de ambiente](#environment-settings-for-tasks) expansão (Isso inclui Olá `PATH`). tootake proveito desses recursos, você deve chamar shell Olá na linha de comando hello – por exemplo, iniciando `cmd.exe` em nós do Windows ou `/bin/sh` no Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Se precisarem de suas tarefas toorun um aplicativo ou script que não está em Olá do nó `PATH` ou fazer referência a variáveis de ambiente, invoque o shell Olá explicitamente na linha de comando de tarefa de saudação.
* **Arquivos de recurso** que contêm Olá toobe de dados processada. Esses arquivos são copiados automaticamente toohello nó do armazenamento de Blob em uma conta de armazenamento do Azure para fins gerais antes de linha de comando da tarefa Olá é executada. Para obter mais informações, consulte as seções de saudação [tarefa inicial](#start-task) e [arquivos e diretórios](#files-and-directories).
* Olá **variáveis de ambiente** que são exigidas por seu aplicativo. Para obter mais informações, consulte Olá [configurações de ambiente para tarefas](#environment-settings-for-tasks) seção.
* Olá **restrições** sob qual Olá tarefa deve ser executada. Por exemplo, as restrições incluem o tempo máximo de saudação tarefa Olá é permitida toorun, o número de vezes que uma tarefa com falha deve ser repetida, máximo hello e máximo de saudação hora em que os arquivos no diretório de trabalho da tarefa Olá são mantidos.
* **Pacotes de aplicativos** toodeploy toohello em qual Olá a tarefa está agendada toorun de nó de computação. [Pacotes de aplicativos](#application-packages) fornecem uma implantação simplificada e controle de versão de aplicativos Olá executar suas tarefas. Pacotes de aplicativos de nível de tarefa são especialmente úteis em ambientes de pool compartilhado, onde diferentes trabalhos são executados em um pool e pool de saudação não será excluído quando um trabalho é concluído. Se o trabalho tiver menos tarefas que os nós no pool hello, pacotes de aplicativos de tarefa podem minimizar transferência de dados desde que o aplicativo é implantado toohello apenas nós que executam tarefas.

Além disso tootasks definir tooperform computação em um nó, Olá tarefas especiais a seguir também é fornecido pelo serviço de lote hello:

* [Iniciar tarefa](#start-task)
* [Tarefa do Gerenciador de Trabalhos](#job-manager-task)
* [Tarefas de preparação e liberação do trabalho](#job-preparation-and-release-tasks)
* [MPI (Tarefas de várias instâncias)](#multi-instance-tasks)
* [Dependências da tarefa](#task-dependencies)

### <a name="start-task"></a>Iniciar tarefa
Associando um **Iniciar tarefa** com um pool, você pode preparar Olá de seus nós o ambiente operacional. Por exemplo, você pode executar ações como instalação de aplicativos de saudação que executam as tarefas ou iniciar processos em segundo plano. tarefa de início de saudação é executado sempre que um nó é iniciado, desde que ela permaneça no pool de hello – incluindo ao nó de saudação é adicionado primeiro pool toohello e quando ele for reiniciado ou recriar a imagem.

O principal benefício Olá da tarefa de início é que ele pode conter todas as informações de saudação que é necessário tooconfigure um nó de computação e instalar aplicativos de saudação que são necessários para a execução da tarefa. Portanto, o aumento Olá número de nós em um pool é tão simple quanto especificando a nova contagem de nó de destino hello. tarefa de início de saudação fornece informações Olá de serviço de lote de Olá Olá tooconfigure necessários novos nós e prepará-los para aceitar tarefas.

Como com qualquer tarefa em lote do Azure, você pode especificar uma lista de **arquivos de recurso** na [armazenamento do Azure][azure_storage], além de tooa **linha de comando** toobe executado. serviço de lote Olá copia primeiro nó de toohello de arquivos de recurso de saudação do armazenamento do Azure e, em seguida, executa a linha de comando de saudação. Para uma tarefa de início do pool, lista de arquivos Olá normalmente contém Olá tarefa aplicativo e suas dependências.

No entanto, tarefas de início Olá também podem incluir toobe de dados de referência usado por todas as tarefas que estão em execução no nó de computação hello. Por exemplo, a linha de comando de início da tarefa pode executar um `robocopy` operação toocopy arquivos de aplicativo (que foram especificados como arquivos de recurso e baixado toohello nó) do hello Iniciar tarefa [diretório de trabalho](#files-and-directories) toohello [pasta compartilhada](#files-and-directories), e, em seguida, execute um MSI ou `setup.exe`.

É geralmente preferível para toowait de serviço de lote Olá para Olá Iniciar tarefa toocomplete antes de considerar Olá tarefas do nó pronto toobe atribuído, mas você pode configurá-la.

Se uma tarefa inicial falhar em um nó de computação, hello estado do nó de saudação será atualizado tooreflect Olá falha e nó Olá não está atribuído a todas as tarefas. Uma tarefa inicial pode falhar se houver um problema copiando seus arquivos de recursos de armazenamento, ou se o processo de saudação executado por sua linha de comando retorna um código de saída diferente de zero.

Se você adicionar ou atualizar a tarefa de início de saudação para um pool existente, você deve reiniciar os nós de computação Olá Iniciar tarefa toobe aplicada toohello nós.

>[!NOTE]
> Olá tamanho total de uma tarefa de início deve ser menor ou igual too32768 caracteres, incluindo arquivos de recurso e variáveis de ambiente. tooensure sua tarefa de início atende a esse requisito, você pode usar uma das duas abordagens:
>
> 1. Você pode usar aplicativos de toodistribute de pacotes de aplicativo ou dados em cada nó no pool de lote. Para obter mais informações sobre pacotes de aplicativos, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).
> 2. Você pode criar um arquivo compactado que contém os arquivos de aplicativos manualmente. Carregar seu arquivo compactado de tooAzure armazenamento como um blob. Especifique o arquivo hello compactado como um arquivo de recurso para a tarefa de início. Antes de executar a linha de comando Olá para sua tarefa de início, descompacte o arquivo Olá Olá linha de comando. 
>
>    arquivamento de saudação toounzip, você pode usar Olá, ferramenta de sua escolha de arquivamento. Você precisará tooinclude ferramenta de saudação que você use o arquivamento de saudação toounzip como um arquivo de recurso para a tarefa inicial de saudação.
>
>

### <a name="job-manager-task"></a>Tarefa do Gerenciador de Trabalhos
Você normalmente usa um **tarefa do Gerenciador de trabalho** toocontrol e/ou o monitor de execução – por exemplo, toocreate de trabalho e enviar tarefas de saudação para um trabalho, determinar toorun tarefas adicionais e determinar quando o trabalho for concluído. No entanto, uma tarefa do Gerenciador de trabalho não é restrito toothese atividades. É uma tarefa totalmente o que pode executar as ações que são necessárias para o trabalho de saudação. Por exemplo, uma tarefa do Gerenciador de trabalho pode baixar um arquivo que é especificado como um parâmetro, analisar o conteúdo de saudação do arquivo e enviar tarefas adicionais com base em desses conteúdos.

Uma tarefa do gerenciador de trabalho é iniciada antes de todas as outras tarefas. Ele fornece Olá recursos a seguir:

* Ele é automaticamente enviado como uma tarefa pelo serviço de lote de saudação quando Olá trabalho é criado.
* Ele é agendado tooexecute antes Olá outras tarefas em um trabalho.
* O nó associado é Olá toobe última removido de um pool ao pool hello está sendo reduzida.
* Seu encerramento pode ser associado toohello término de todas as tarefas no trabalho de saudação.
* Uma tarefa do Gerenciador de trabalho tem prioridade mais alta de saudação quando ele precisa toobe reiniciado. Se um nó ocioso não estiver disponível, Olá serviço de lote pode terminar uma saudação outras tarefas em execução no toomake espaço pool Olá Olá toorun de tarefa de Gerenciador de trabalho.
* Uma tarefa do Gerenciador de trabalho em um trabalho não têm prioridade sobre tarefas de saudação de outros trabalhos. Entre diferentes trabalhos, somente as prioridades de nível de trabalho são observadas.

### <a name="job-preparation-and-release-tasks"></a>Tarefas de preparação e liberação do trabalho
O Lote fornece tarefas de preparação do trabalho para a instalação de execução pré-trabalho. As tarefas de liberação do trabalho são para a manutenção ou a limpeza pós-trabalho.

* **Tarefa de preparação de trabalho**: uma tarefa de preparação de trabalho é executado em todos os nós de computação são tarefas agendadas toorun, antes de qualquer Olá outras tarefas de trabalho são executadas. Você pode usar dados toocopy de tarefa de preparação um trabalho que são compartilhados por todas as tarefas, mas é exclusivo toohello trabalho, por exemplo.
* **Tarefa de liberação de trabalho**: quando um trabalho for concluída, uma tarefa de liberação de trabalho é executado em cada nó no pool de saudação que pelo menos uma tarefa executada. Você pode usar um trabalho versão toodelete dados da tarefa que são copiados pela tarefa de preparação de trabalho hello, ou toocompress e upload log dados de diagnóstico, por exemplo.

Ambos preparação de trabalho e tarefas de versão permitem toospecify toorun uma linha de comando quando a tarefa de saudação é invocada. Elas oferecem recursos, como download de arquivo, execução elevada, variáveis de ambiente personalizadas, duração máxima da execução, contagem de repetição e tempo de retenção do arquivo.

Para saber mais sobre tarefas de preparação e de liberação de trabalho, consulte [Executar tarefas de preparação e de conclusão de trabalhos em nós de computação do Lote do Azure](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Tarefa de várias instâncias
Um [tarefas de várias instâncias](batch-mpi.md) é uma tarefa que é configurado toorun em mais de um nó de computação simultaneamente. Com tarefas de várias instâncias, você pode habilitar o alto desempenho cenários de computação que exigem um grupo de nós de computação que estão alocados juntos tooprocess uma única carga de trabalho (como Interface MPI (Message Passing)).

Para obter uma discussão detalhada sobre como executar trabalhos MPI em lote usando biblioteca de lote .NET Olá, confira [Use a instância várias tarefas toorun passando Interface aplicativos MPI (Message) em lote do Azure](batch-mpi.md).

### <a name="task-dependencies"></a>Dependências da tarefa
[Dependências de tarefa](batch-task-dependencies.md), como Olá nome implica, permitem que você toospecify uma tarefa depende da conclusão de saudação de outras tarefas antes de sua execução. Este recurso fornece suporte para situações em que uma tarefa de "downstream" consome saída saudação de uma tarefa de "upstream" ou quando uma tarefa upstream executa algumas inicialização necessária para uma tarefa de downstream. toouse esse recurso, você deve primeiro habilitar dependências em seu trabalho em lotes. Em seguida, para cada tarefa que depende de outro (ou outros), você especificar tarefas Olá que essa tarefa depende.

Com dependências de tarefa, você pode configurar cenários como Olá a seguir:

* A *tarefaB* depende da *tarefaA* (a *tarefaB* não começará sua execução até que a *tarefaA* tenha terminado).
* A *tarefaC* depende da *tarefaA* e da *tarefaB*.
* A *tarefaD* depende de várias tarefas, como as tarefas de *1* a *10*, antes de ser executada.

Check-out [tarefas dependências em lote do Azure](batch-task-dependencies.md) e hello [TaskDependencies] [ github_sample_taskdeps] exemplo de código Olá [exemplos de lote do azure] [ github_samples] Repositório GitHub para mais detalhes sobre esse recurso.

## <a name="environment-settings-for-tasks"></a>Configurações do ambiente para tarefas
Cada tarefa executada pelo serviço de lote de saudação tem variáveis de tooenvironment de acesso que ele define nós de computação. Isso inclui variáveis de ambiente definidas pelo serviço de lote de saudação ([definido pelo serviço][msdn_env_vars]) e variáveis de ambiente personalizado que você pode definir para suas tarefas. executar suas tarefas de scripts e aplicativos de saudação tem acesso toothese as variáveis de ambiente durante a execução.

Você pode definir variáveis de ambiente personalizadas no nível de tarefa ou trabalho Olá preenchendo Olá *configurações de ambiente* propriedade dessas entidades. Por exemplo, consulte Olá [adicionar um trabalho tooa] [ rest_add_task] operação (API REST do lote) ou hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] e [ CloudJob.CommonEnvironmentSettings] [ net_job_env] propriedades no .NET de lote.

Seu aplicativo cliente ou serviço pode obter variáveis de ambiente da tarefa, definido pelo serviço e personalizadas, usando Olá [obter informações sobre uma tarefa] [ rest_get_task_info] operação (em lote REST) ou acessando Olá [CloudTask.EnvironmentSettings] [ net_cloudtask_env] propriedade (lote .NET). Processos em execução em um nó de computação podem acessar essas e outras variáveis de ambiente no nó hello, por exemplo, usando Olá familiar `%VARIABLE_NAME%` (Windows) ou `$VARIABLE_NAME` sintaxe (Linux).

Você pode encontrar uma lista completa de todas as variáveis de ambiente definidas pelo serviço em [Variáveis de ambiente do nó de computação][msdn_env_vars].

## <a name="files-and-directories"></a>Arquivos e diretórios
Cada tarefa tem um *diretório de trabalho* em que ela cria zero ou mais arquivos e diretórios. Esta pasta de trabalho pode ser usada para armazenar o programa hello executado pela tarefa hello, dados de saudação que ele processa, e Olá saída de processamento de hello, que ele executa. Todos os arquivos e diretórios de uma tarefa pertencem Olá usuário de tarefa.

Olá serviço de lote expõe uma parte do sistema de arquivos de saudação em um nó como Olá *diretório raiz*. Tarefas podem acessar o diretório raiz de saudação referenciando Olá `AZ_BATCH_NODE_ROOT_DIR` variável de ambiente. Para saber mais sobre como usar as variáveis de ambiente, consulte [Configurações de ambiente para tarefas](#environment-settings-for-tasks).

diretório raiz de saudação contém Olá estrutura de diretórios a seguir:

![Estrutura de diretórios do nó de computação][1]

* **compartilhado**: este diretório fornece acesso de leitura/gravação muito*todos os* tarefas que são executados em um nó. Qualquer tarefa que é executado no nó Olá pode criar, ler, atualizar e excluir arquivos nesse diretório. Tarefas podem acessar este diretório referenciando Olá `AZ_BATCH_NODE_SHARED_DIR` variável de ambiente.
* **inicialização**– esse diretório é usado por uma tarefa inicial como seu diretório de trabalho. Todos os arquivos de saudação que são baixados toohello nó pela tarefa de início de saudação são armazenados. Olá Iniciar tarefa pode criar, ler, atualizar e excluir arquivos nesse diretório. Tarefas podem acessar este diretório referenciando Olá `AZ_BATCH_NODE_STARTUP_DIR` variável de ambiente.
* **Tarefas**: um diretório é criado para cada tarefa que é executado no nó de saudação. Ele é acessado referenciando Olá `AZ_BATCH_TASK_DIR` variável de ambiente.

    Dentro de cada diretório de tarefa, Olá serviço de lote cria um diretório de trabalho (`wd`) cujo caminho exclusivo é especificado pelo Olá `AZ_BATCH_TASK_WORKING_DIR` variável de ambiente. Este diretório fornece tarefas de toohello de acesso de leitura/gravação. tarefa Olá pode criar, ler, atualizar e excluir arquivos nesse diretório. Esse diretório é mantido com base em Olá *RetentionTime* restrição especificada para a tarefa de saudação.

    `stdout.txt`e `stderr.txt`: esses arquivos são gravados toohello pasta de tarefas durante a execução de saudação da tarefa de saudação.

> [!IMPORTANT]
> Quando um nó é removido do pool de saudação *todos os* de saudação arquivos que são armazenados no nó de saudação são removidos.
>
>

## <a name="application-packages"></a>pacotes de aplicativos
Olá [pacotes de aplicativos](batch-application-packages.md) recurso fornece fácil gerenciamento e implantação de aplicativos de nós de computação toohello em seus pools. Você pode carregar e gerenciar várias versões de saudação aplicativos executados por suas tarefas, incluindo seus binários e arquivos de suporte. Em seguida, você pode implantar automaticamente uma ou mais toohello esses aplicativos nós de computação no pool de.

Você pode especificar os pacotes de aplicativos no nível de pool e tarefa hello. Quando você especifica pacotes de aplicativos do pool, o aplicativo hello é nó tooevery implantado no pool de saudação. Quando você especifica os pacotes de aplicativos de tarefa, aplicativo hello é implantado toonodes somente que são toorun agendada pelo menos uma das tarefas do trabalho hello, antes de saudação a linha de comando da tarefa é executada.

Identificadores de lote Olá detalhes do trabalho com o armazenamento do Azure toostore seus pacotes de aplicativos e implantação-las toocompute nós, portanto o código e o gerenciamento de sobrecarga pode ser simplificada.

toofind mais informações sobre o recurso de pacote de aplicativo hello, check-out [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).

> [!NOTE]
> Se você adicionar o pool aplicativo pacotes tooan *existente* pool, você deve reinicializar seus nós de computação para o aplicativo hello pacotes toobe implantado toohello nós.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Tempo de vida de nó de computação e de pool
Ao projetar sua solução de lote do Azure, você tem toomake uma decisão de design sobre como e quando os pools são criados e computação quanto nós dentro desses pools estejam disponíveis.

Em uma extremidade do espectro hello, você pode criar um pool para cada trabalho que você enviar e excluir pool Olá assim que concluir suas tarefas a execução. Isso maximiza a utilização porque nós Olá são alocados somente quando necessário e desligar assim que elas são ociosas. Enquanto isso significa que o trabalho Olá deve aguardar Olá nós toobe alocada, é importante toonote tarefas são agendadas para execução como nós individualmente disponíveis, são alocados, e Olá tarefa inicial foi concluída. Lote *não* Aguarde até que todos os nós dentro de um pool estão disponíveis antes de atribuir tarefas toohello nós. Isso garante a máxima utilização de todos os nós disponíveis.

Em Olá outra ponta do espectro Olá, se ter trabalhos iniciar imediatamente é a prioridade mais alta do hello, você pode criar um pool antecipadamente e disponibilizar seus nós para que os trabalhos são enviados. Nesse cenário, as tarefas podem iniciar imediatamente, mas nós podem ficam ociosos ao aguardar que eles toobe atribuído.

Uma abordagem combinada normalmente é usada para lidar com uma carga variável, mas em andamento. Você pode ter um pool que são enviados para vários trabalhos, mas podem dimensionar o número de saudação de nós para cima ou para baixo de acordo com a carga de trabalho toohello (consulte [recursos de computação de escala](#scaling-compute-resources) em Olá seção a seguir). Isso pode ser feito de maneira reativa, com base na carga atual, ou proativamente, se a carga puder ser prevista.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configuração de firewall e VNet (rede virtual) 

Quando você provisiona um conjunto de nós de computação em lote do Azure, você pode associar pool Olá com uma sub-rede de um Azure [rede virtual (VNet)](../virtual-network/virtual-networks-overview.md). toolearn mais sobre como criar uma rede virtual com sub-redes, consulte [criar uma rede virtual do Azure com sub-redes](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Olá associada a um pool de rede virtual deve ser:

   * Em hello Azure mesmo **região** como Olá conta de lote do Azure.
   * Em Olá mesmo **assinatura** como Olá conta de lote do Azure.

* tipo de saudação da rede virtual com suporte depende como pools estão sendo alocados para Olá conta do lote:

    - Se o modo de alocação de pool Olá para sua conta do lote é definido tooBatch serviço, você pode atribuir um toopools somente de rede virtual criada com hello **configuração de serviços de nuvem**. Além disso, Olá especificado que redes devem ser criados com o modelo de implantação clássico hello. Não há suporte para VNets criados com o modelo de implantação do Azure Resource Manager hello.
 
    - Se o modo de alocação de pool Olá para sua conta do lote é definido tooUser assinatura, você pode atribuir um toopools somente de rede virtual criada com hello **configuração de máquina Virtual**. Pools criados com hello **configuração do serviço de nuvem** não têm suporte. Olá que redes associadas podem ser criadas com o modelo de implantação do Azure Resource Manager hello ou modelo de implantação clássico hello.

    Para uma tabela de resumo de suporte de rede virtual de acordo com o modo de alocação toopool, consulte Olá [modo de alocação de Pool](#pool-allocation-mode) seção.

* Se o modo de alocação de pool de saudação para sua conta do lote for definido tooBatch serviço, você deve fornecer permissões para Olá tooaccess principal do serviço de lote Olá VNet. Olá VNet deve atribuir Olá [Classic Virtual Machine Contributor Role-Based acesso RBAC (controle)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) entidade de serviço de lote de toohello de função. Se Olá especificado função RBAC não for fornecida, o serviço de lote de saudação retorna 400 (solicitação incorreta). função de saudação tooadd em Olá portal do Azure:

    1. Selecione Olá **VNet**, em seguida, **(IAM) do controle de acesso** > **funções** > **colaborador da máquina Virtual**  >  **Adicionar**.
    2. Em Olá **adicionar permissões** folha, selecione Olá **colaborador da máquina Virtual** função.
    3. Em Olá **adicionar permissões** folha, procure Olá API de lote. Pesquise para cada uma dessas cadeias de caracteres por sua vez até encontrar hello API:
        1. **MicrosoftAzureBatch**.
        2. **Lote do Microsoft Azure**. Os locatários mais recentes do Azure AD podem usar esse nome.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** é identificação Olá Olá API de lote. 
    3. Selecione Olá entidade de serviço de API de lote. 
    4. Clique em **Salvar**.

        ![Atribuir a entidade de serviço de tooBatch de função de Colaborador de VM](./media/batch-api-basics/iam-add-role.png)


* Olá especificado sub-rede deve ter suficiente livre **endereços IP** tooaccommodate Olá número total de nós de destino; ou seja, Olá soma de saudação `targetDedicatedNodes` e `targetLowPriorityNodes` propriedades de pool de saudação. Se a sub-rede de saudação não tiver endereços IP suficientes livres, Olá serviço de lote parcialmente aloca nós de computação Olá no pool de saudação e retornará um erro de redimensionamento.

* Olá especificado sub-rede deve permitir tooschedule capaz de tarefas de comunicação de toobe de serviço de lote Olá em nós de computação de saudação. Se nós de computação de comunicação toohello é negado por um **grupo de segurança de rede (NSG)** associado Olá rede virtual, e em seguida, Olá serviço de lote define o estado de Olá Olá de nós de computação muito**inutilizável**.

* Se Olá especificado a rede virtual associada **grupos de segurança de rede (NSGs)** e/ou um **firewall**, e algumas portas reservado do sistema devem ser ativadas para comunicação de entrada:

- Para pools criados com uma configuração de máquina virtual, habilite as portas 29876 e 29877, bem como a porta 22 para Linux e a porta 3389 para Windows. 
- Para pools criados com uma configuração de serviço de nuvem, habilite as portas 10100, 20100 e 30100. 
- Habilite conexões de saída tooAzure armazenamento na porta 443. Além disso, verifique se seu ponto de extremidade do Armazenamento do Azure pode ser resolvido por servidores DNS personalizados que servem sua rede virtual. Especificamente, uma URL do formulário de saudação `<account>.table.core.windows.net` deve ser resolvido.

    Olá, tabela a seguir descreve Olá portas que você precisa tooenable para pools que você criou com a configuração de máquina virtual de saudação de entrada:

    |    Portas de destino    |    Endereço IP de origem      |    O Lote adiciona NSGs?    |    Necessário para a VM toobe utilizável?    |    Ação do usuário   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Para pools criados com a configuração de máquina virtual Olá: 29876, 29877</li><li>Para pools criados com a configuração de serviço de nuvem Olá: 10100, 20100, 30100</li></ul>         |    Endereços IP com função de serviço Somente Lote |    Sim. Lote adiciona os NSGs no nível de saudação da rede interfaces (NIC) anexados tooVMs. Essas NSGs permitem o tráfego somente de endereços IP com função de serviço do Lote. Mesmo se você abrir essas portas para web inteiro Olá, tráfego de saudação será bloqueado, a saudação NIC. |    Sim  |  Não é necessário toospecify um NSG, porque o lote permite que somente os endereços IP de lote. <br /><br /> No entanto, se você especificar um NSG, verifique se essas portas estão abertas para tráfego de entrada. <br /><br /> Se você especificar * como hello IP de origem em seu NSG, lote ainda adiciona os NSGs no nível de saudação do tooVMs NIC conectada. |
    |    3389, 22               |    Máquinas de usuário, usadas para depuração, para que você pode acessar remotamente o hello VM.    |    Não                                    |    Não                     |    Adicione os NSGs toopermit toohello de acesso remoto (RDP/SSH) VM.   |                 

    Olá, a tabela a seguir descreve a porta de saída Olá que você precisa tooenable toopermit acesso tooAzure armazenamento:

    |    Portas de saída    |    Destino    |    O Lote adiciona NSGs?    |    Necessário para a VM toobe utilizável?    |    Ação do usuário    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Armazenamento do Azure    |    Não    |    Sim    |    Se você adicionar qualquer NSGs, certifique-se de que essa porta é aberto toooutbound tráfego.    |


## <a name="scaling-compute-resources"></a>Dimensionando os recursos de computação
Com [o dimensionamento automático](batch-automatic-scaling.md), você pode ter o serviço de lote Olá ajustar dinamicamente o número de saudação de nós de computação em um pool de acordo com toohello atual carga de trabalho e uso de recursos do seu cenário de computação. Isso permite toolower Olá custo geral da execução do seu aplicativo usando apenas os recursos de saudação é necessário e liberar aqueles não é necessário.

Você habilita o dimensionamento automático escrevendo uma [fórmula de dimensionamento automático](batch-automatic-scaling.md#automatic-scaling-formulas) e associando-a a um pool. Olá serviço de lote usa Olá toodetermine fórmula Olá destino quantos nós no pool Olá Olá próximo escala intervalo (um intervalo que você pode configurar). Você pode especificar Olá configurações automáticas de escala para um pool ao criá-lo ou habilitar mais tarde o dimensionamento de um pool. Você também pode atualizar Olá dimensionamento configurações em um pool de dimensionamento habilitado.

Por exemplo, talvez um trabalho requer que você enviar um grande número de tarefas toobe executado. Você pode atribuir um pool de fórmula toohello escala que ajusta Olá número de nós no pool de saudação com base no número atual de saudação de tarefas em fila e a taxa de conclusão de saudação de tarefas Olá no trabalho de saudação. Olá serviço de lote periodicamente avalia a fórmula hello e redimensiona o pool hello, com base na carga de trabalho e as outras configurações de fórmula. Olá serviço adiciona nós, conforme necessário quando há um grande número de tarefas em fila e remove nós quando não existem tarefas em execução ou na fila.

Uma fórmula de dimensionamento pode ser baseada em Olá métricas a seguir:

* **Métricas de tempo** são baseadas em estatísticas coletadas a cada cinco minutos no Olá especificado número de horas.
* **métricas do recurso** são baseadas nos usos da CPU, da largura de banda e da memória, e no número de nós.
* As **métricas de tarefa** são baseadas no estado da tarefa, como *Ativa* (na fila), *Em execução* ou *Concluída*.

Quando o dimensionamento automático diminui o número de saudação de nós de computação em um pool, você deve considerar como toohandle tarefas em execução no momento de saudação do hello diminuir a operação. tooaccommodate, lote fornece um *opção de desalocação de nó* que você pode incluir em suas fórmulas. Por exemplo, você pode especificar que as tarefas em execução são interrompidas imediatamente, interrompidas imediatamente e, em seguida, retirada da fila para execução em outro nó ou permitidas toofinish antes que o nó de saudação é removido do pool de saudação.

Para saber mais sobre o dimensionamento automático de um aplicativo, consulte [Dimensionar automaticamente nós de computação em um pool do Lote do Azure](batch-automatic-scaling.md).

> [!TIP]
> toomaximize utilização de recursos de computação, definir o número de destino de saudação de nós toozero final Olá de um trabalho, mas permitir toofinish de tarefas em execução.
>
>

## <a name="security-with-certificates"></a>Segurança com certificados
Você normalmente precisa de certificados toouse ao criptografar ou descriptografar informações confidenciais para tarefas, como chave Olá para um [conta de armazenamento do Azure][azure_storage]. toosupport isso, você pode instalar certificados em nós. Os segredos criptografados são transmitidos tootasks por meio do parâmetros de linha de comando ou incorporados em um dos recursos da tarefa de saudação e certificados Olá instalado podem ser usado toodecrypt-los.

Use Olá [Adicionar certificado] [ rest_add_cert] operação (em lote REST) ou [CertificateOperations.CreateCertificate] [ net_create_cert] método (lote .NET) tooadd tooa um certificado conta do lote. Em seguida, você pode associar certificado Olá com um grupo novo ou existente. Quando um certificado está associado um pool, Olá serviço de lote instala certificado Olá em cada nó no pool de saudação. Olá serviço de lote instala certificados apropriados hello quando o nó de saudação é iniciado, antes de iniciar as tarefas (incluindo a tarefa inicial de saudação e a tarefa do Gerenciador de trabalho).

Se você adicionar certificados tooan *existente* pool, você deve reinicializar seus nós de computação Olá certificados toobe aplicada toohello nós.

## <a name="error-handling"></a>Tratamento de erros
Talvez seja necessário toohandle falhas de tarefa e o aplicativo em sua solução de lote.

### <a name="task-failure-handling"></a>Manipulação de falha de tarefa
As falhas de tarefas se enquadram nestas categorias:

* **Falhas de pré-processamento**

    Se uma tarefa falhar toostart, um erro de pré-processamento está definido para a tarefa de saudação.  

    Pré-processando erros pode ocorrer se moveram os arquivos de recursos da tarefa hello, Olá conta de armazenamento não está mais disponível ou outro problema foi encontrado que Olá impediu a cópia bem-sucedida dos arquivos toohello nó.

* **Falhas de carregamento de arquivo**

    Se o carregamento de arquivos que são especificados para uma tarefa falhar por algum motivo, um erro de carregamento de arquivo é definido para a tarefa de saudação.

    Podem ocorrer erros se hello SAS fornecidos para acessar o armazenamento do Azure é inválido ou não fornecer permissões de gravação, se a conta de armazenamento Olá não está mais disponível ou se outro problema foi encontrado que impediu o hello com êxito a cópia dos arquivos de carregamento de arquivo nó de saudação.    

* **Falhas de aplicativo**

    processo de saudação que é especificado pela linha de comando da tarefa Olá também pode falhar. Olá processo é considerado toohave falha quando um código de saída diferente de zero é retornado pelo processo de saudação que é executado pela tarefa de saudação (consulte *códigos de saída de tarefa* na próxima seção, Olá).

    Falhas de aplicativo, você pode configurar o lote tooautomatically repetição Olá tarefa tooa número especificado de vezes.

* **Falhas de restrição**

    Você pode definir uma restrição que especifica Olá duração de execução máximo para um trabalho ou tarefa, hello *maxWallClockTime*. Isso pode ser útil para finalizar as tarefas que não tooprogress.

    Quando o período de tempo máximo Olá foi excedido, a tarefa de saudação é marcada como *concluída*, mas o código de saída de hello está definido muito`0xC000013A` e hello *schedulingError* campo está marcado como `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Falhas de depuração de aplicativos
* `stderr` e `stdout`

    Durante a execução, um aplicativo pode produzir saída de diagnóstico que você pode usar tootroubleshoot problemas. Conforme mencionado em Olá anteriormente nesta seção [arquivos e diretórios](#files-and-directories), Olá serviço de lote grava a saída padrão e erro padrão de saída muito`stdout.txt` e `stderr.txt` arquivos no diretório de tarefa de saudação em Olá nó de computação. Você pode usar Olá portal do Azure ou um toodownload de SDKs de lote Olá esses arquivos. Por exemplo, você pode recuperar esses e outros arquivos para fins de solução de problemas usando [ComputeNode.GetNodeFile] [ net_getfile_node] e [CloudTask.GetNodeFile] [ net_getfile_task] na biblioteca do .NET em lotes de saudação.

* **Códigos de saída de tarefas**

    Como mencionado anteriormente, uma tarefa está marcada como falha pelo serviço de lote Olá se o processo de saudação que é executado pela tarefa de saudação retorna um código de saída diferente de zero. Quando uma tarefa executa um processo, lote preenche a propriedade de código de saída da tarefa Olá com hello *código de retorno do processo de saudação*. É importante toonote que o código de saída da tarefa é **não** determinado pelo serviço de lote de saudação. Código de saída da tarefa é determinado pelo próprio processo de saudação ou sistema operacional Olá qual processo Olá executado.

### <a name="accounting-for-task-failures-or-interruptions"></a>Contabilidade de interrupções ou de falhas de tarefas
As tarefas podem falhar ou ser interrompidas ocasionalmente. Hello tarefa aplicativo em si pode falhar, nó Olá no qual Olá tarefa está em execução pode ser reinicializado ou nó Olá pode ser removido do pool de saudação durante uma operação de redimensionamento se hello, política de desalocação do pool é conjunto tooremove nós imediatamente sem aguardar toofinish de tarefas. Em todos os casos, tarefa Olá pode ser automaticamente retirada da fila de lote para execução em outro nó.

Ele também é possível que um problema intermitente de toocause toohang uma tarefa ou coloque tooexecute muito longo. Você pode definir o intervalo de saudação de execução máximo para uma tarefa. Se o intervalo de saudação de execução máximo for excedido, Olá serviço de lote interrupções de aplicativo de tarefa hello.

### <a name="connecting-toocompute-nodes"></a>Conectando nós toocompute
Você pode executar adicionais de depuração e solução de problemas ao entrar no nó de computação tooa remotamente. Você pode usar o hello toodownload portal do Azure um arquivo de protocolo de área de trabalho remota (RDP) para nós do Windows e obter informações de conexão Secure Shell (SSH) para nós do Linux. Você também pode fazer isso usando Olá lote APIs – por exemplo, com [Batch .NET] [ net_rdpfile] ou [lote Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> nó de tooa tooconnect via RDP ou SSH, você primeiro deve criar um usuário no nó de saudação. toodo isso, você pode usar o hello portal do Azure, [adicionar um nó de tooa de conta de usuário] [ rest_create_user] usando Olá API REST do lote, chame Olá [ComputeNode.CreateComputeNodeUser] [ net_create_user] método no .NET em lotes ou chamada hello [add_user] [ py_add_user] método no módulo de lote Python hello.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Solucionando os nós de computação problemáticos
Em situações em que algumas das suas tarefas estão falhando, seu aplicativo de cliente do lote ou o serviço pode examinar metadados de saudação do hello falhado tarefas tooidentify um nó com comportamento inadequado. Cada nó em um pool recebe uma ID exclusiva e nó Olá no qual uma tarefa é executada está incluída nos metadados da tarefa de saudação. Após identificar um nó com problemas, você poderá executar várias ações nele:

* **Reinicie o nó de saudação** ([REST][rest_reboot] | [.NET][net_reboot])

    Nó de saudação reiniciar às vezes pode limpar latentes problemas como processos presos ou falha. Observe que se o pool usa uma tarefa inicial ou uma tarefa de preparação de trabalho usa o seu trabalho, elas são executadas quando Olá nó é reiniciado.
* **Refazer a imagem de nó Olá** ([REST][rest_reimage] | [.NET][net_reimage])

    Isso reinstala o sistema de operacional de saudação no nó de saudação. Com a reinicialização de um nó, iniciar tarefas e tarefas de preparação de trabalho executar novamente depois que o nó de saudação foi criado.
* **Remover nó de saudação do pool de saudação** ([REST][rest_remove] | [.NET][net_remove])

    Às vezes, é necessário toocompletely remover nó de saudação do pool de saudação.
* **Desabilitar o agendamento de tarefas no nó Olá** ([REST][rest_offline] | [.NET][net_offline])

    Isso efetivamente leva nó Olá off-line de forma que nenhuma tarefa adicional recebem tooit, mas permite Olá nó tooremain em execução no pool de saudação. Isso permite que você tooperform mais investigação Olá causa de falhas de saudação sem perda de dados da tarefa com falha Olá e sem nó Olá causando falhas de tarefas adicionais. Por exemplo, você pode desabilitar um agendamento de tarefas no nó hello, em seguida, [entrar remotamente](#connecting-to-compute-nodes) tooexamine Olá logs de eventos do nó ou executar outra solução de problemas. Depois de concluir sua investigação, você poderá colocar nó de saudação on-line, permitindo o agendamento de tarefas ([REST][rest_online] | [.NET] [ net_online]), ou executar uma saudação outras ações discutidas anteriormente.

> [!IMPORTANT]
> Com cada ação que é descrita nesta seção – reinicializar, a recriação de imagem, remover e desabilitar agendamento de tarefas – será capaz de toospecify como tarefas atualmente em execução no nó de saudação são tratadas quando você executar a ação de saudação. Por exemplo, quando você desativar o agendamento de tarefas em um nó usando a biblioteca de cliente .NET do lote hello, você pode especificar um [DisableComputeNodeSchedulingOption] [ net_offline_option] toospecify o valor de enumeração se muito**Terminate** executar tarefas, **Requeue** -los para o agendamento em outros nós, ou permitir toocomplete de tarefas em execução antes de executar a ação de saudação (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [ferramentas e APIs de lote](batch-apis-tools.md) disponíveis para criar soluções de lote.
* Percorrer um passo a passo no exemplo de aplicativo de lote [começar com hello biblioteca do lote do Azure para .NET](batch-dotnet-get-started.md). Também há um [versão do Python](batch-python-tutorial.md) tutorial Olá que executa uma carga de trabalho no Linux nós de computação.
* Baixe e criar hello [Explorer lote] [ github_batchexplorer] projeto de exemplo para uso ao desenvolver suas soluções de lote. Olá lote Explorer pode executar a seguir hello e muito mais:

  * Monitorar e manipular pools, trabalhos e tarefas em sua conta do Lote
  * Baixe `stdout.txt`, `stderr.txt` e outros arquivos de nós
  * Criar usuários em nós e baixar arquivos RDP para logon remoto
* Saiba como muito[criar pools de nós de computação Linux](batch-linux-nodes.md).
* Visite Olá [Fórum do Azure Batch] [ batch_forum] no MSDN. Fórum de saudação é um bom colocar tooask perguntas, se você estiver aprendendo apenas ou um especialista em lote de uso.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
