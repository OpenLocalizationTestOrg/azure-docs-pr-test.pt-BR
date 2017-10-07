---
title: "toodo aaaWhat no evento de saudação de uma interrupção de armazenamento do Azure | Microsoft Docs"
description: "Quais toodo no evento de saudação de uma interrupção de armazenamento do Azure"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: 93e1e831c35b96b8bf190fa2b56ab89350bbac13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Quais toodo se ocorrer uma interrupção de armazenamento do Azure
Na Microsoft, trabalhamos toomake rígido se que nossos serviços estão sempre disponíveis. Às vezes, forças além do nosso controle nos afetam de formas que causam interrupções de serviço não planejadas em uma ou mais regiões. toohelp tratar essas ocorrências raras, fornecemos Olá seguindo as instruções de alto nível para serviços de armazenamento do Azure.

## <a name="how-tooprepare"></a>Como tooprepare
É essencial para cada cliente tooprepare seu próprio plano de recuperação de desastres. Olá esforço toorecover uma queda de armazenamento normalmente envolve a equipe de operações e procedimentos automatizados na ordem tooreactivate seus aplicativos em um estado de funcionamento. Consulte toohello documentação do Azure abaixo toobuild seu próprio plano de recuperação de desastres:

* [Recuperação de desastre e alta disponibilidade para aplicativos do Azure](/azure/architecture/resiliency/disaster-recovery-high-availability-azure-applications.md)
* [Orientações técnicas de resiliência do Azure](/azure/architecture/resiliency.md)
* [Serviço do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Replicação de Armazenamento do Azure](storage-redundancy.md)
* [Serviço de Backup do Azure](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Como toodetect
Olá recomendado Olá toodetermine de maneira status do serviço do Azure é toosubscribe toohello [painel de integridade do serviço Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Quais toodo se ocorrer uma interrupção de armazenamento
Se um ou mais serviços de armazenamento estão disponíveis no momento em uma ou mais regiões, há duas opções para você tooconsider. Se desejar que os dados de tooyour acesso imediato, considere a opção 2.

### <a name="option-1-wait-for-recovery"></a>Opção 1: aguardar a recuperação
Nesse caso, nenhuma ação sua é necessária. Estamos trabalhando cuidadosamente disponibilidade de serviço do Azure Olá toorestore. Você pode monitorar o status de serviço Olá Olá [painel de integridade do serviço Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Opção 2: copiar os dados do secundário
Se você escolheu [armazenamento com redundância geográfica com acesso de leitura (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (recomendado) para suas contas de armazenamento, você terá acesso de leitura tooyour dados da região secundária hello. Você pode usar ferramentas como [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md)e hello [biblioteca de movimentação de dados do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy dados da região de saudação secundária em outra conta de armazenamento em uma região unimpacted e aponte seu armazenamento de toothat aplicativos de conta para leitura e gravação de disponibilidade.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Quais tooexpect se ocorrer um failover de armazenamento
Se você tiver escolhido [GRS (armazenamento com redundância geográfica)](storage-redundancy.md#geo-redundant-storage) ou [RA-GRS (armazenamento com redundância geográfica de acesso de leitura)](storage-redundancy.md#read-access-geo-redundant-storage) (recomendado), o Armazenamento do Azure mantém seus dados duráveis em duas regiões (primária e secundária). Em ambas as regiões, o Armazenamento do Azure mantém constantemente várias réplicas de seus dados.

Quando um desastre regional afeta sua região primária, tentaremos primeiro serviço de saudação toorestore nessa região. Depende da natureza Olá desastres hello e seus impactos, em algumas situações raras talvez não seja região primária do toorestore capaz de saudação. Nesse ponto, executaremos um failover geográfico. replicação de dados entre regiões Olá é um processo assíncrono que pode envolver um atraso, portanto, é possível que as alterações que ainda não foram replicadas região secundária toohello pode ser perdido. Você pode consultar Olá ["Hora da última sincronização" da sua conta de armazenamento](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget detalhes sobre o status de replicação de saudação.

Alguns pontos sobre Olá experiência de failover geográfico de armazenamento:

* Somente failover geográfico do armazenamento será disparado pela equipe de armazenamento do Azure hello – não é necessária nenhuma ação do cliente.
* O serviço de armazenamento existente, pontos de extremidade para blobs, tabelas, filas e arquivos permanecerão Olá mesmo após o failover de saudação; Olá entrada DNS será necessário tooswitch toobe atualizado da região secundária do toohello Olá região primária.
* Antes e durante a saudação failover geográfico, você não terá acesso de gravação tooyour conta de armazenamento devido toohello impacto do desastre Olá mas você pode ler de saudação secundária se sua conta de armazenamento tiver sido configurada como RA-GRS.
* Conta de armazenamento de acesso de leitura e gravação tooyour será retomada quando failover geográfico Olá foi concluído e Olá propagadas de alterações DNS, Isso indica toobe toowhat usado seu ponto de extremidade secundário. 
* Observe que você terá acesso de gravação se você tiver o GRS ou RA-GRS configurado para a conta de armazenamento hello. 
* Você pode consultar ["Último geográfica tempo de Failover" da sua conta de armazenamento](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget mais detalhes.
* Após o failover hello, sua conta de armazenamento será totalmente funcional, mas em um estado "degradado", como ela é realmente hospedada em uma região autônomo com nenhuma possíveis de replicação geográfica. toomitigate risco, vamos restaurar região primária original do hello e, em seguida, fazer um failback geográfica toorestore Olá original estado. Se a região primária original de saudação é irrecuperável, podemos alocará outra região secundária.
  Para obter mais detalhes sobre a infraestrutura de saudação de replicação geográfica de armazenamento do Azure, consulte toohello artigo no blog da equipe de armazenamento Olá sobre [opções de redundância e RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Melhores Práticas para proteger seus dados
Há alguns tooback abordagens recomendadas backup de seus dados de armazenamento regularmente.

* Discos de VM – Olá Use [serviço de Backup do Azure](https://azure.microsoft.com/services/backup/) tooback os discos VM Olá usados por suas máquinas virtuais do Azure.
* Os blobs de bloco – criar um [instantâneo](https://msdn.microsoft.com/library/azure/hh488361.aspx) de cada blob de bloco ou copie a conta de armazenamento Olá blobs tooanother em outra região usando [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), ou hello [ Biblioteca de movimentação de dados do Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Usar tabelas – [AzCopy](storage-use-azcopy.md) tooexport dados da tabela Olá em outra conta de armazenamento em outra região.
* Usar arquivos – [AzCopy](storage-use-azcopy.md) ou [Azure PowerShell](storage-powershell-guide-full.md) toocopy conta de armazenamento tooanother arquivos em outra região.

Para obter informações sobre como criar aplicativos que se beneficiam do recurso Olá RA-GRS, faça check-out [criação altamente disponível de aplicativos usando o armazenamento de RA-GRS](../storage-designing-ha-apps-with-ragrs.md)

