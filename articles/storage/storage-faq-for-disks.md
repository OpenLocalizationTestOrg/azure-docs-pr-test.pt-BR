---
title: FAQ (perguntas frequentes) sobre discos de VM IaaS do Azure | Microsoft Docs
description: "Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium (gerenciados e não gerenciados)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium gerenciados e não gerenciados

Este artigo responde a algumas perguntas frequentes sobre o Azure Managed Disks e o Armazenamento Premium do Azure.

## <a name="managed-disks"></a>Managed Disks

**O que é o Azure Managed Disks?**

Managed Disks é um recurso que simplifica o gerenciamento de disco para VMs IaaS do Azure manipulando o gerenciamento de conta de armazenamento para você. Para obter mais informações, consulte Olá [visão geral de discos gerenciados](storage-managed-disks-overview.md).

**Se eu criar um disco gerenciado standard com base em um VHD existente que tem 80 GB, quanto isso custará?**

Um disco gerenciado padrão criado a partir de um VHD de 80 GB é tratado como Olá próximo padrão tamanho de disco disponível, que é um disco S10. Você será cobrado de acordo toohello S10 disco preços. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Existem custos de transação de discos gerenciados standard?**

Sim. Você é cobrado por cada transação. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Para um disco gerenciado standard, serei ser cobrado para tamanho real de Olá Olá dados hello ou para capacidade de saudação provisionada de disco Olá?**

Você será cobrado com base na capacidade de saudação provisionada de disco de saudação. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**O preço dos discos premium gerenciados é diferente do preço dos discos não gerenciados?**

saudação de preços de discos premium gerenciado é Olá igual a discos premium não gerenciado.

**Alterar Olá armazenamento tipo de conta (Standard ou Premium) de meus discos gerenciados?**

Sim. Você pode alterar o tipo de conta de armazenamento Olá discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.

**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**

Sim. Você pode exportar os discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.

**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado com uma assinatura diferente?**

Não.

**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado em uma região diferente?**

Não.

**Existem limitações de escala para clientes que usam discos gerenciados?**

Discos gerenciados elimina os limites de saudação associados às contas de armazenamento. No entanto, o número de saudação de discos gerenciados por assinatura é limitado too2, 000 por padrão. Você pode chamar o suporte tooincrease esse número.

**Posso fazer um instantâneo incremental de um disco gerenciado?**

Não. recurso de instantâneo atual Olá cria uma cópia completa de um disco gerenciado. No entanto, nós estamos planejando toosupport de instantâneos incrementais em Olá futuras.

**As VMs em um conjunto de disponibilidade podem consistir de uma combinação de discos gerenciados e não gerenciados?**

Não. Olá VMs em um conjunto de disponibilidade deve usar discos todas gerenciados ou todos os discos não gerenciados. Quando você cria um conjunto de disponibilidade, você pode escolher qual tipo de disco desejado toouse.

**É a opção de padrão de saudação de discos gerenciados no hello portal do Azure?**

Não no momento, mas ela ficará padrão Olá Olá futuras.

**É possível criar um disco gerenciado vazio?**

Sim. Você pode criar um disco vazio. Um disco gerenciado pode ser criado independentemente de uma VM, por exemplo, sem anexá-lo tooa VM.

**O que é a contagem de domínios de falha de saudação com suporte para um conjunto de disponibilidade que usa discos gerenciados?**

Dependendo da região de saudação onde o conjunto de disponibilidade de saudação que usa discos gerenciado está localizado, a contagem de domínios de falha de saudação com suporte é 2 ou 3.

**Como é a conta de armazenamento padrão de saudação para configurar um diagnóstico?**

Você configura uma conta de armazenamento privado para diagnóstico da VM. Em Olá futuro, planejamos diagnóstico tooswitch tooManaged discos também.

**O tipo de suporte ao Controle de Acesso Baseado em Função está disponível para o Managed Disks?**

O Managed Disks oferece suporte a três funções principais padrão:

* Proprietário: pode gerenciar tudo, incluindo o acesso
* Colaborador: pode gerenciar tudo, exceto o acesso
* Leitor: pode ver tudo, mas não pode fazer alterações

**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**

Você pode obter uma assinatura de acesso compartilhado somente leitura URI para Olá gerenciado em disco e usá-lo toocopy Olá conteúdo tooa privada local ou conta de armazenamento.

**Posso criar uma cópia do meu disco gerenciado?**

Os clientes podem tirar um instantâneo dos seus discos gerenciados e usar Olá instantâneo toocreate outro disco gerenciado.

**Ainda há suporte para discos não gerenciados?**

Sim. Há suporte para discos gerenciados e não gerenciados. É recomendável que você use discos gerenciados para novas cargas de trabalho e migra seus discos de toomanaged cargas de trabalho atual.


**Se eu criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, serei ser cobrado para tamanho de disco seguinte hello (512 GB)?**

Sim.

**Posso criar armazenamento com redundância local, armazenamento com redundância geográfica e discos de armazenamento com redundância de zona gerenciados?**

O Azure Managed Disks atualmente dá suporte apenas a discos gerenciados de armazenamento com redundância local.

**Posso reduzir ou diminuir o tamanho de meus discos gerenciados?**

Não. Não há suporte para esse recurso no momento. 

**Alterar propriedade de nome de computador hello quando um especializada (não criada usando a ferramenta de preparação do sistema hello ou generalizado) operacional do disco do sistema é usado tooprovision uma máquina virtual?**

Não. Você não pode atualizar a propriedade de nome de computador hello. Olá nova VM herda-lo do hello pai VM, que era o disco do sistema operacional Olá toocreate usado. 

**Onde encontrar o exemplo do Azure Resource Manager modelos toocreate VMs com discos gerenciados?**
* [Lista de modelos que usam o Managed Disks](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Managed Disks e Criptografia de Serviço de Armazenamento 

**A Criptografia do Serviço de Armazenamento do Azure fica habilitada por padrão quando crio um disco gerenciado?**

Sim.

**Quem gerencia as chaves de criptografia Olá?**

A Microsoft gerencia chaves de criptografia de saudação.

**Posso desabilitar a Criptografia do Serviço de Armazenamento para meus discos gerenciados?**

Não.

**A Criptografia do Serviço de Armazenamento só está disponível em regiões específicas?**

Não. Ele está disponível em todas as regiões de saudação em discos gerenciado está disponível. O Managed Disks está disponível em todas as regiões públicas e na Alemanha.

**Como posso descobrir se o disco gerenciado está criptografado?**

Você pode descobrir a hora de saudação quando um disco gerenciado foi criado de saudação portal do Azure, Olá CLI do Azure e do PowerShell. Se houver tempo Olá após 9 de junho de 2017, o disco está criptografado. 

**Como faço para criptografar meus discos existentes que foram criados antes de 10 de junho de 2017?**

A partir de 10 de junho de 2017, novos dados gravados discos tooexisting gerenciado são criptografados automaticamente. Nós também estamos planejando tooencrypt os dados existentes e criptografia Olá acontecerá assincronamente no plano de fundo de saudação. Se você precisar criptografar os dados existentes agora, crie uma cópia do disco. Os novos discos serão criptografados.

* [Copiar discos gerenciados usando Olá CLI do Azure](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Copiar discos gerenciados usando o PowerShell](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Os instantâneos gerenciados e as imagens são criptografados?**

Sim. Todos os instantâneos e imagens criados após 9 de junho de 2017 são criptografados automaticamente. 

**Pode converter máquinas virtuais com discos não gerenciados que estão localizados em contas de armazenamento ou foram discos toomanaged previamente criptografado?**

Sim

**Um VHD exportado de um disco gerenciado ou instantâneo também será criptografado?**

Não. Mas se você exportar um VHD tooan criptografado conta de armazenamento de um disco gerenciado criptografado ou instantâneo e, em seguida, ele é criptografado. 

## <a name="premium-disks-managed-and-unmanaged"></a>Discos Premium: gerenciados e não gerenciados

**Se uma VM usa uma série de tamanho que dá suporte ao Armazenamento Premium, como um DSv2, é possível anexar discos de dados standard e premium?** 

Sim.

**É possível anexar premium e standard discos tooa tamanho séries de dados não dá suporte a armazenamento Premium, como a série D, Dv2, G ou F?**

Não. Você pode anexar apenas tooVMs de discos padrão para dados que não usam uma série de tamanho que dá suporte ao armazenamento Premium.

**Se criar um disco de dados premium com base em um VHD existente que tinha 80 GB, quanto isso custará?**

Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como o tamanho de disco disponíveis para o próximo premium Olá, é um disco P10. Você será cobrado de acordo toohello P10 disco preços.

**Há transações custos toouse armazenamento Premium?**

Há um custo fixo para cada tamanho de disco, que vem provisionado com limites específicos de IOPS e taxa de transferência. Olá outros custos são largura de banda de saída e a capacidade de instantâneo, se aplicável. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Quais são os limites de saudação de IOPS e taxa de transferência que posso obter do cache de disco Olá?**

Olá combinado de limites para cache e SSD local para uma série DS são 4.000 IOPS por núcleo e 33 MB por segundo por núcleo. Olá série GS oferece a 5.000 IOPS por núcleo e 50 MB por segundo por núcleo.

**É hello que SSD local tem suporte para uma VM de discos gerenciados?**

Olá SSD local é o armazenamento temporário que acompanha uma VM de discos gerenciados. Não há custo adicional para esse armazenamento temporário. É recomendável que você não use esse toostore SSD local os dados do aplicativo porque ele não é mantido no armazenamento de BLOBs do Azure.

**São existe qualquer repercussões para Olá usar de TRIM em discos premium?**

Não há nenhum uso de toohello desvantagem de TRIM em discos do Azure em uma premium ou discos padrão.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Novos tamanhos de disco: gerenciados e não gerenciados

**Qual é Olá maior tamanho de disco com suporte para o sistema operacional e discos de dados?**

tipo de partição de Hello Azure oferece suporte para um disco do sistema operacional é Olá mestre de inicialização MBR (registro). formato MBR Olá dá suporte a um tamanho de disco até too2 TB. Olá maior tamanho que o Azure oferece suporte para um disco do sistema operacional é de 2 TB. O Azure suporta até too4 TB para discos de dados. 

**O que é Olá maior blob tamanho de página com suporte?**

Olá página blob maior que o Azure suporta é 8 TB (8.191 GB). Não há suporte para blobs de página maiores que 4 TB (4.095 GB) anexado tooa VM como dados ou discos do sistema operacional.

**É necessário toouse uma nova versão de ferramentas do Azure toocreate, anexar, redimensionar e carregar discos maiores que 1 TB?**

Você não precisa tooupgrade seu toocreate de ferramentas do Azure existente, anexar ou redimensionar discos maiores que 1 TB. tooupload seu VHD arquivo local diretamente tooAzure como um blob de página ou disco não gerenciado, é necessário conjuntos de ferramentas toouse hello mais recentes:

|Ferramentas do Azure      | Versões com suporte                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Número de versão 4.1.0: versão de junho de 2017 ou posterior|
|CLI do Azure v1     | Número de versão 0.10.13: versão de maio de 2017 ou posterior|
|AzCopy           | Número de versão 6.1.0: versão de junho de 2017 ou posterior|

suporte a saudação v2 CLI do Azure e o Azure Storage Explorer estará disponível em breve. 

**Os tamanhos de disco P4 e P6 têm suporte para discos não gerenciados ou blobs de página?**

Não. Os tamanhos de disco P4 (32 GB) e P6 (64 GB) têm suporte somente para discos gerenciados. O suporte a discos não gerenciados e blobs de página será lançado em breve.

**Se o meu premium existente gerenciado disco menor do que 64 GB foi criado antes da habilitação do disco pequeno hello (em torno de 15 de junho de 2017), como ele é cobrado?**

Discos premium pequeno existentes com menos de 64 GB continuar preço de acordo toohello P10 toobe cobrado. 

**Como alternar da camada de disco Olá de discos premium pequeno menor do que 64 GB de tooP4 P10 ou P6?**

Você pode tirar um instantâneo dos discos pequenos e, em seguida, crie uma saudação de comutador do disco tooautomatically tooP4 da camada de preços ou P6 com base no tamanho de saudação provisionado. 


## <a name="what-if-my-question-isnt-answered-here"></a>E se dúvida não foi respondida aqui?

Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta. Você pode postar uma pergunta no final deste artigo Olá nos comentários de saudação. tooengage com a equipe de armazenamento do Azure hello e outros membros da comunidade sobre neste artigo, use Olá MSDN [Fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

recursos toorequest, enviar sua solicitações e ideias toohello [Fórum de comentários do armazenamento do Azure](https://feedback.azure.com/forums/217298-storage).
