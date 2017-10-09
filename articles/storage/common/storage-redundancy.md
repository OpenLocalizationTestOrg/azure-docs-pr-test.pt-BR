---
title: "replicação aaaData no armazenamento do Azure | Microsoft Docs"
description: "Os dados na sua conta do Armazenamento do Microsoft Azure são replicados para garantir durabilidade e alta disponibilidade. Opções de replicação incluem LRS (armazenamento com redundância local), ZRS (armazenamento com redundância de zona), GRS (armazenamento com redundância geográfica) RA-GRS (armazenamento com redundância geográfica com acesso de leitura)."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Replicação de Armazenamento do Azure

dados de saudação em sua conta de armazenamento é sempre do Microsoft Azure replicados tooensure durabilidade e alta disponibilidade. Cópias de replicação nos seus dados Olá mesmo data center ou tooa segundo data center, dependendo da opção de replicação que você escolher. A replicação protege seus dados e preserva o seu aplicativo tempo em caso de saudação de falhas de hardwares temporárias. Se os dados forem replicados tooa segundo data center, ele é protegido contra uma falha catastrófica no local primário hello.

A replicação garante que sua conta de armazenamento atende Olá [contrato de nível de serviço (SLA) para armazenamento](https://azure.microsoft.com/support/legal/sla/storage/) mesmo em face de saudação de falhas. Consulte Olá SLA para obter informações sobre o armazenamento do Azure garante a disponibilidade e durabilidade.

Quando você cria uma conta de armazenamento, você pode selecionar uma saudação as opções de replicação a seguir:

* [Armazenamento com redundância local (LRS)](#locally-redundant-storage)
* [Armazenamento com redundância de zona (ZRS)](#zone-redundant-storage)
* [Armazenamento com redundância geográfica (GRS)](#geo-redundant-storage)
* [Armazenamento com redundância geográfica com acesso de leitura (RA-GRS)](#read-access-geo-redundant-storage)

Armazenamento com redundância geográfica com acesso de leitura (RA-GRS) é a opção de padrão de hello quando você cria uma conta de armazenamento.

Olá, a tabela a seguir fornece uma visão geral das diferenças de saudação entre LRS, ZRS, GRS e RA-GRS, enquanto as seções lidam com cada tipo de replicação mais detalhadamente.

| Estratégia de replicação | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Os dados são replicados entre vários datacenters. |Não |Sim |Sim |Sim |
| Dados podem ser lidos a partir de um local secundário, bem como o local principal hello. |Não |Não |Não |Sim |
| Número de cópias de dados mantidas em nós separados. |3 |3 |6 |6 |

Consulte [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/) para informações de preços para opções de redundância diferentes de saudação.

> [!NOTE]
> O Armazenamento Premium dá suporte apenas ao LRS (armazenamento com redundância local). Para obter informações sobre o Armazenamento Premium, consulte [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquina virtual do Azure](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Armazenamento com redundância local
Armazenamento localmente redundante (LRS) replica seus dados três vezes dentro de uma unidade de escala de armazenamento, que é hospedado em um datacenter em Olá região em que você criou sua conta de armazenamento. Uma solicitação de gravação retorna com êxito depois que ele foi escrito tooall três réplicas. Essas três réplicas residem em domínios de falha e domínios de atualização separados dentro de uma unidade de escala de armazenamento.

Uma unidade de escala de armazenamento é uma coleção de racks de nós de armazenamento. Um domínio de falha (FD) é um grupo de nós que representam uma unidade física de falha e pode ser considerado como nós pertencentes toohello mesmo rack físico. Um domínio de atualização (UD) é um grupo de nós que são atualizados em conjunto durante o processo de saudação de uma atualização de serviço (rollout). Olá três réplicas estão espalhadas por UDs e FDs dentro de um armazenamento tooensure de unidade de escala que dados estejam disponíveis, mesmo se a falha de hardware afeta um único rack ou quando os nós são atualizados durante a distribuição.

LRS é a opção de menor custo hello e oferece menos opções de tooother em comparação comparada a durabilidade. Em caso de saudação de um desastre de nível de datacenter (incêndio, inundação etc.) todas as três réplicas podem ser perdidas ou irrecuperável. Armazenamento redundante da replicação geográfica (GRS) toomitigate esse risco, é recomendado para a maioria dos aplicativos.

O armazenamento com redundância local ainda pode ser desejável em determinados cenários:

* Fornece largura de banda máxima das opções de replicação do Armazenamento do Azure.
* Se seu aplicativo armazenar dados que possam ser facilmente reconstruídos, você pode optar por LRS.
* Alguns aplicativos são restritos tooreplicating dados apenas dentro de um país devido a requisitos de governança toodata. Uma região emparelhada poderia estar em outro país. Para obter mais informações sobre pares de regiões, consulte [Regiões do Azure](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Armazenamento com redundância de zona
Armazenamento com redundância de zona (ZRS) replica seus dados de forma assíncrona em data centers dentro de uma ou duas regiões em réplicas adição toostoring três semelhante tooLRS, assim, fornecendo maior durabilidade do que o LRS. Dados armazenados em ZRS serão duráveis, mesmo se o datacenter primário hello está indisponível ou irrecuperável.
Os clientes que planejam toouse ZRS devem estar cientes que:

* O ZRS está disponível apenas para blobs de blocos em contas de armazenamento de finalidades gerais e é compatível apenas com o serviço de armazenamento nas versões 2014-02-14 e posteriores.
* Como replicação assíncrona envolve um atraso, em caso de saudação de um desastre local, é possível que as alterações que ainda não foram replicadas toohello secundário poderá ser perdido se dados saudação não podem ser recuperados da saudação primária.
* réplica Olá pode não estar disponível até que a Microsoft inicia o failover toohello secundário.
* Não podem ser convertidas contas ZRS, GRS ou tooLRS posterior. Da mesma forma, uma conta existente de LRS ou GRS não pode ser convertido de conta ZRS tooa.
* As contas do ZRS não têm recursos de log ou métricas.

## <a name="geo-redundant-storage"></a>Armazenamento com redundância geográfica
Armazenamento com redundância geográfica (GRS) replica seu dados tooa região secundária centenas de milhas de distância região primária hello. Se sua conta de armazenamento permitiu GRS, então seus dados serão duráveis mesmo no caso de saudação de uma interrupção regional completa ou um desastre no qual Olá região primária não é recuperável.

Para uma conta de armazenamento com GRS habilitado, uma atualização é primeiro região primária toohello confirmada, onde é replicada três vezes. E atualização de saudação é replicada de forma assíncrona toohello de região secundária, onde também é replicada três vezes.

Com o GRS, ambas as regiões primária e secundária do hello gerenciar réplicas em domínios de falha e domínios dentro de uma unidade de escala de armazenamento conforme descrito com LRS de atualização.

Considerações:

* Desde que a replicação assíncrona envolve um atraso, em caso de saudação de um desastre regional, é possível que as alterações que ainda não foram replicados região secundária toohello serão perdida se dados saudação não podem ser recuperados da região primária hello.
* réplica de saudação não está disponível a menos que a Microsoft inicia a região secundária do toohello de failover. Se o Microsoft iniciar uma região secundária do toohello de failover, você terá dados toothat de acesso de leitura e gravação depois Olá failover foi concluído. Para obter mais informações, confira [Guia de Recuperação de Desastres](../storage-disaster-recovery-guidance.md). 
* Se um aplicativo deseja tooread da região secundária hello, usuário Olá deve habilitar RA-GRS.

Quando você cria uma conta de armazenamento, selecione a região primária Olá para conta de saudação. região secundária Olá é determinado com base na região primária Olá e não pode ser alterado. Olá a tabela a seguir mostra os emparelhamentos de regiões principais e secundárias hello.

| Primário | Secundário |
| --- | --- |
| Centro-Norte dos EUA |Centro-Sul dos Estados Unidos |
| Centro-Sul dos Estados Unidos |Centro-Norte dos EUA |
| Leste dos EUA |Oeste dos EUA |
| Oeste dos EUA |Leste dos EUA |
| Leste dos EUA 2 |Centro dos EUA |
| Centro dos EUA |Leste dos EUA 2 |
| Norte da Europa |Europa Ocidental |
| Europa Ocidental |Norte da Europa |
| Sudeste da Ásia |Ásia Oriental |
| Ásia Oriental |Sudeste da Ásia |
| China Oriental |Norte da China |
| Norte da China |China Oriental |
| Leste do Japão |Oeste do Japão |
| Oeste do Japão |Leste do Japão |
| Sul do Brasil |Centro-Sul dos Estados Unidos |
| Leste da Austrália |Sudeste da Austrália |
| Sudeste da Austrália |Leste da Austrália |
| Sul da Índia |Centro da Índia |
| Centro da Índia |Sul da Índia |
| Oeste da Índia |Sul da Índia |
| Gov do Iowa nos EUA |Gov. dos EUA – Virgínia |
| Gov. dos EUA – Virgínia |Governo dos EUA do Texas |
| Governo dos EUA do Texas |Governo dos EUA do Arizona |
| Governo dos EUA do Arizona |Governo dos EUA do Texas |
| Canadá Central |Leste do Canadá |
| Leste do Canadá |Canadá Central |
| Oeste do Reino Unido |Sul do Reino Unido |
| Sul do Reino Unido |Oeste do Reino Unido |
| Alemanha Central |Nordeste da Alemanha |
| Nordeste da Alemanha |Alemanha Central |
| Oeste dos EUA 2 |Centro-Oeste dos EUA |
| Centro-Oeste dos EUA |Oeste dos EUA 2 |

Para obter informações atualizadas sobre regiões com suporte do Azure, confira [Regiões do Azure](https://azure.microsoft.com/regions/).

>[!NOTE]  
> A região secundária do US Gov - Virgínia é US Gov - Texas. Anteriormente, o US Gov - Virgínia utilizada o US Gov - Iowa como uma região secundária. Contas de armazenamento ainda aproveitar Iowa nos Gov conforme uma região secundária estão sendo migrados Texas de Gov tooUS como uma região do secundário. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Armazenamento com redundância geográfica com acesso de leitura
Armazenamento com redundância geográfica com acesso de leitura (RA-GRS) maximiza a disponibilidade da sua conta de armazenamento, fornecendo dados de toohello acesso somente leitura no local secundário do hello, além de replicação toohello em duas regiões fornecidas por GRS.

Quando você habilita o acesso somente leitura de dados de tooyour na região secundária hello, seus dados estão disponíveis em um ponto de extremidade secundário, adição toohello principal ponto de extremidade para sua conta de armazenamento. ponto de extremidade secundário Olá é semelhante toohello ponto de extremidade primário, mas acrescenta o sufixo Olá `–secondary` toohello nome da conta. Por exemplo, se o ponto de extremidade primário para Olá serviço Blob é `myaccount.blob.core.windows.net`, em seguida, o ponto de extremidade secundário é `myaccount-secondary.blob.core.windows.net`. chaves de acesso de saudação para sua conta de armazenamento são Olá mesmo para ambos Olá pontos de extremidade primários e secundários.

Considerações:

* Seu aplicativo tiver toomanage qual ponto de extremidade está interagindo com ao usar RA-GRS.
* Desde que a replicação assíncrona envolve um atraso, em caso de saudação de um desastre regional, é possível que as alterações que ainda não foram replicados região secundária toohello serão perdida se dados saudação não podem ser recuperados da região primária hello.
* Se Microsoft inicia a região secundária do toohello de failover, você terá dados toothat de acesso de leitura e gravação depois Olá failover foi concluído. Para obter mais informações, confira [Guia de Recuperação de Desastres](../storage-disaster-recovery-guidance.md). 
* O RA-GRS é para fins de alta disponibilidade. Para obter diretrizes sobre a escalabilidade, examine Olá [lista de verificação de desempenho](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Perguntas frequentes

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Como alterar o tipo de replicação geográfica Olá da minha conta de armazenamento?

   Você pode alterar o tipo de replicação geográfica Olá da sua conta de armazenamento entre LRS, GRS, e RA-GRS usando Olá [portal do Azure](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) ou programaticamente, usando um dos nossos muitos cliente de armazenamento Bibliotecas. Observe que as contas ZRS não podem ser convertidas em LRS ou GRS. Da mesma forma, uma conta existente de LRS ou GRS não pode ser convertido de conta ZRS tooa.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Haverá qualquer tempo de inatividade se alterar tipo de replicação de saudação da minha conta de armazenamento?

   Não, não haverá tempo inoperante.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Haverá qualquer custo adicional se alterar tipo de replicação de saudação da minha conta de armazenamento?

   Sim. Se você alterar de LRS tooGRS (ou RA-GRS) para sua conta de armazenamento, ele seria gera um custo adicional de saída usado para copiar os dados existentes do local secundário do local primário toohello. Depois que os dados iniciais Olá são copiados não é mais taxa de saída adicionais para geográfica replicando dados de saudação do local do hello toosecondary primário. detalhes de saudação de encargos de largura de banda podem ser encontrados em Olá [página de preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/blobs/). Se você alterar de tooLRS GRS, não há nenhum custo adicional, mas seus dados serão excluídos do local secundário hello.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Como RA-GRS pode me ajudar?
   
   Armazenamento GRS fornece replicação de seus dados de uma região secundária tooa primário centenas de milhas de distância região primária hello. Nesse caso, seus dados sejam duráveis mesmo no caso de saudação de uma interrupção regional completa ou um desastre no qual Olá região primária não é recuperável. Armazenamento de RA-GRS inclui isso mais adiciona dados de saudação do hello capacidade tooread do local secundário hello. Para algumas ideias sobre como tooleverage essa capacidade, consulte muito[criação altamente disponível de aplicativos usando o armazenamento de RA-GRS](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Há uma maneira para que eu toofigure limite quanto tempo tooreplicate meus dados da região secundária do hello toohello primária?
   
   Se você estiver usando o armazenamento de RA-GRS, você pode verificar Olá hora da última sincronização da sua conta de armazenamento. Hora da última sincronização é um valor de data/hora GMT; todas as gravações primárias antes Olá hora da última sincronização foi gravou com êxito toohello de local secundário, que significa que estão disponível toobe ler no local secundário de saudação do. Gravações primárias após Olá hora da última sincronização pode ou não estar disponível para leituras ainda. Você pode consultar esse valor usando Olá [portal do Azure](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), ou programaticamente usando Olá API REST ou um de saudação bibliotecas de cliente de armazenamento. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Como alternar a região secundária toohello se houver uma interrupção na região primária Olá?
   
   Consulte o artigo toohello [que toodo se ocorrer uma interrupção de armazenamento do Azure](../storage-disaster-recovery-guidance.md) para obter mais detalhes.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. O que é Olá RPO e RTO com GRS?
   
   Objetivo de ponto de recuperação (RPO): GRS e RA-GRS, armazenamento de saudação do serviço assincronamente geográfica replica dados de saudação do local secundário do primário toohello hello. Se houver um desastre regional principal e um failover tiver toobe executada, alterações delta recentes que não foram replicados geograficamente podem ser perdidas. número de saudação de minutos de perda potencial de dados é chamado tooas Olá RPO (o que significa ponto Olá nos dados de toowhich de tempo pode ser recuperado). Normalmente, temos um RPO inferior a 15 minutos, embora atualmente não exista SLA em quanto tempo demora a replicação geográfica.

   Objetivo de tempo de recuperação (RTO): Esta é uma medida de quanto tempo ele levamos toodo Olá failover e voltar conta de armazenamento Olá online se tivermos toodo um failover. Olá tempo toodo Olá failover inclui o seguinte hello:
    * tempo de saudação ele levamos tooinvestigate e determinar se podemos recuperar dados Olá no local primário hello ou se é preciso toodo um failover.
    * Conta de saudação failover alterando Olá primário DNS entradas toopoint toohello local secundário.

   Vamos assumir a responsabilidade de saudação de preservar os dados muito sério, se houver qualquer chance de recuperação de dados Olá, podemos será adiar a realizar failover hello e se concentrar na recuperação de dados de Olá no local principal hello. Em Olá futuro, planejamos tooprovide uma API tooallow você tootrigger um failover em um nível de conta, que, em seguida, permitirá que você toocontrol Olá RTO por conta própria, mas isso ainda não está disponível.
   
## <a name="next-steps"></a>Próximas etapas
* [Criando aplicativos altamente disponíveis usando o armazenamento de RA-GRS](../storage-designing-ha-apps-with-ragrs.md)
* [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Sobre as contas de armazenamento do Azure](../storage-create-storage-account.md)
* [Metas de desempenho e escalabilidade do Armazenamento do Azure](storage-scalability-targets.md)
* [Armazenamento com redundância geográfica com acesso de leitura e opções de redundância do Armazenamento do Microsoft Azure ](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP Paper – Armazenamento do Azure: um serviço de armazenamento em nuvem altamente disponível com coerência forte](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

