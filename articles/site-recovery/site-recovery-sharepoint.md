---
title: "aaaReplicate um aplicativo do SharePoint de várias camado usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooreplicate um aplicativo do SharePoint de várias camado usando recursos do Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Replicar um aplicativo do SharePoint de várias camadas para recuperação de desastre usando funcionalidades do Azure Site Recovery

Este artigo descreve detalhadamente como tooprotect um aplicativo do SharePoint usando [do Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Visão geral

O Microsoft SharePoint é um aplicativo avançado que pode ajudar um grupo ou departamento a organizar, colaborar com e compartilhar informações. O SharePoint pode fornecer portais de intranet, gerenciamento de arquivos e documentos, colaboração, redes sociais, extranets, sites, Enterprise Search e business intelligence. Ele também tem integração de sistemas, integração de processos e funcionalidades de automação de fluxo de trabalho. Normalmente, as organizações considerá-lo como uma nível 1 aplicativo confidencial toodowntime e perda de dados.

Hoje, o Microsoft SharePoint não fornece nenhuma funcionalidade integrada de recuperação de desastre. Independentemente do tipo hello e escala de um desastre, recuperação envolve o uso de saudação de um centro de dados em espera que você pode recuperar o farm de saudação. Centros de dados em espera são necessários para cenários em que local sistemas redundantes e os backups não podem se recuperar interrupção Olá Olá data center primário.

Uma solução de recuperação de desastres BOM deve permitir que a modelagem de planos de recuperação nas arquiteturas de aplicativo complexo hello como o SharePoint. Ele também deve ter Olá capacidade tooadd personalizado etapas toohandle aplicativo mapeamentos entre várias camadas e, portanto, fornecendo um failover de clique simples com um RTO inferior no evento de saudação de um desastre.

Este artigo descreve detalhadamente como tooprotect um aplicativo do SharePoint usando [do Azure Site Recovery](site-recovery-overview.md). Este artigo aborda as práticas recomendadas para replicar um tooAzure de aplicativo do SharePoint de três camadas, como você pode fazer uma simulação de recuperação de desastres e como você pode tooAzure de aplicativo de saudação do failover.

Você pode assistir Olá abaixo vídeo sobre como recuperar um tooAzure de aplicativo da camada várias.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que compreender o seguinte hello:

1. [Replicando tooAzure uma máquina virtual](site-recovery-vmware-to-azure.md)
2. Como muito[criar uma rede de recuperação](site-recovery-network-design.md)
3. [Fazer um tooAzure de failover de teste](site-recovery-test-failover-to-azure.md)
4. [Fazer um failover tooAzure](site-recovery-failover.md)
5. Como muito[replicar um controlador de domínio](site-recovery-active-directory.md)
6. Como muito[replicar do SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Arquitetura do SharePoint

O SharePoint pode ser implantado em um ou mais servidores usando topologias em camadas e funções de servidor tooimplement um design de farm que atenda a metas e objetivos específicos. Um farm grande e de alta demanda típico do SharePoint Server, que dá suporte a um grande número de usuários simultâneos e um grande número de itens de conteúdo usam o agrupamento de serviços como parte de sua estratégia de escalabilidade. Essa abordagem envolve a execução de serviços em servidores dedicados, o agrupamento desses serviços e a expansão servidores hello como um grupo. Olá topologia a seguir ilustra serviço hello e agrupamento para um farm de servidores do SharePoint de três camadas de servidores. Consulte tooSharePoint documentação e arquiteturas de linha de produto para obter orientações detalhadas sobre diferentes topologias de SharePoint. Você pode encontrar mais detalhes sobre a implantação do SharePoint 2013 [neste documento](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Padrão de Implantação 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Suporte do Site Recovery

Para criar este artigo, usamos as máquinas virtuais VMware com o Windows Server 2012 R2 Enterprise. Foram usados o SharePoint 2013 Enterprise edition e o SQL Server 2014 Enterprise edition. Como a replicação de recuperação de Site é independente do aplicativo, fornecidas recomendações Olá aqui são toohold esperado para cenários a seguir também.

### <a name="source-and-target"></a>Origem e destino

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sim | Sim
**VMware** | Sim | Sim
**Servidor físico** | Sim | Sim

### <a name="sharepoint-versions"></a>Versões do SharePoint
Olá versões de servidor do SharePoint a seguir têm suporte.

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Tookeep coisas em mente

Se você estiver usando um cluster compartilhado com base em disco em qualquer camada em seu aplicativo, você não poderá ser capaz de toouse tooreplicate de replicação de recuperação de Site essas máquinas virtuais. Você pode usar replicação nativa fornecida pelo aplicativo hello e, em seguida, usar um [plano de recuperação](site-recovery-create-recovery-plans.md) toofailover todas as camadas.

## <a name="replicating-virtual-machines"></a>Replicação de máquinas virtuais

Execute [neste guia](site-recovery-vmware-to-azure.md) toostart replicando Olá tooAzure de máquina virtual.

* Após a conclusão da replicação hello, certifique-se de ir tooeach máquina de virtual de cada camada e selecione o mesmo conjunto de disponibilidade no ' replicadas item > Configurações > Propriedades > de computação e de rede '. Por exemplo, se a camada da web tem 3 máquinas virtuais, certifique-se de saudação todos os 3 máquinas virtuais são configuradas toobe parte do mesmo conjunto de disponibilidade no Azure.

    ![Definir Conjunto de Disponibilidade](./media/site-recovery-sharepoint/select-av-set.png)

* Para obter orientação sobre como proteger o Active Directory e DNS, consulte muito[proteger o Active Directory e DNS](site-recovery-active-directory.md) documento.

* Para obter orientações sobre a proteção da camada de banco de dados em execução no SQL server, consulte muito[proteger o SQL Server](site-recovery-active-directory.md) documento.

## <a name="networking-configuration"></a>Configuração de rede

### <a name="network-properties"></a>Propriedades da rede

* Olá aplicativo e da camada de Web VMs, defina configurações de rede no portal do Azure para que VMs Olá toohello anexado à direita DR rede após o failover.

    ![Selecionar Rede](./media/site-recovery-sharepoint/select-network.png)


* Se você estiver usando um endereço IP estático, em seguida, especifique Olá IP que você deseja Olá tootake de máquina virtual em Olá **IP de destino** campo

    ![Definir o IP Estático](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>Roteamento de Tráfego e de DNS

Para sites da internet [criar um perfil do Gerenciador de tráfego do tipo 'Priority'](../traffic-manager/traffic-manager-create-profile.md) em Olá assinatura do Azure. E, em seguida, configurar seu perfil DNS e o Gerenciador de tráfego em Olá maneira a seguir.


| **Onde** | **Fonte** | **Destino**|
| --- | --- | --- |
| DNS público | DNS público para sites do SharePoint <br/><br/> Por exemplo: sharepoint.contoso.com | Gerenciador de Tráfego <br/><br/> contososharepoint.trafficmanager.net |
| DNS local | sharepointonprem.contoso.com | IP público em Olá farm local |


Em Olá perfil do Gerenciador de tráfego, [criar hello pontos de extremidade primário e de recuperação](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Use ponto de extremidade externo Olá para o ponto de extremidade local e o IP público para o ponto de extremidade do Azure. Verifique se a prioridade de saudação é definida o ponto de extremidade superior tooon-local.

Host de uma página de teste em uma porta específica (por exemplo, 800) na camada de web do SharePoint Olá para que o Traffic Manager tooautomatically detectar disponibilidade após failover. Essa é uma solução alternativa caso você não possa habilitar a autenticação anônima em nenhum dos seus sites do SharePoint.

[Configurar o perfil do Gerenciador de tráfego Olá](../traffic-manager/traffic-manager-configure-priority-routing-method.md) com hello abaixo as configurações.

* Método de roteamento – 'Prioridade'
* DNS tempo toolive (TTL) - 30 ' segundos'
* Configurações do monitor de ponto de extremidade – se você pode habilitar a autenticação anônima, pode também fornecer um ponto de extremidade de site específico. Ou então, você pode usar uma página de teste em uma porta específica (por exemplo, 800).

## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação

Um plano de recuperação permite sequenciamento Olá failover de várias camadas em um aplicativo de várias camada, assim, manter a consistência do aplicativo. Siga Olá etapas a seguir ao criar um plano de recuperação para um aplicativo web de várias camadas. [Saiba mais sobre a criação de um plano de recuperação](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>A adição de grupos de toofailover de máquinas virtuais

1. Crie um plano de recuperação adicionando Olá aplicativo e a camada da Web VMs.
2. Clique em 'Personalizar' toogroup Olá VMs. Por padrão, todas as VMs são parte do 'Grupo 1'.

    ![Personalizar RP](./media/site-recovery-sharepoint/rp-groups.png)

3. Crie outro grupo (grupo 2) e mover a camada da Web de saudação VMs para Olá novo grupo. Suas VMs de camada de aplicativo devem ser parte do 'Grupo 1' e as VMs de camada da Web devem ser parte do 'Grupo 2'. Isso é tooensure que Olá aplicativo da camada VMs inicializam primeiro, seguido por máquinas virtuais de camada da Web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar plano de recuperação de toohello de scripts

Você pode implantar scripts do Azure Site Recovery hello mais comumente usada em sua conta de automação botão Olá 'Implantar tooAzure' abaixo. Quando você estiver usando qualquer script publicado, certifique-se de que você seguir as orientações de saudação no script hello.

[![Implantar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Adicione um script de pré-ação de too'Group 1' toofailover grupo de disponibilidade SQL. Use script de 'FailoverAG de SQL ASR' hello publicada em scripts de exemplo hello. Certifique-se de seguir as orientações Olá no script hello e fazer alterações de saudação necessárias no script hello adequadamente.

    ![Add-AG-Script-Step-1](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Add-AG-Script-Step-2](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Adicione um tooattach de script de ação de postagem de um balanceador de carga Olá failover em máquinas virtuais da camada da Web (grupo 2). Use script de 'ASR AddSingleLoadBalancer' hello publicada em scripts de exemplo hello. Certifique-se de seguir as orientações Olá no script hello e fazer alterações de saudação necessárias no script hello adequadamente.

    ![Add-LB-Script-Step-1](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Add-LB-Script-Step-2](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Adicione um etapa manual tooupdate Olá DNS registros toopoint toohello novo farm no Azure.

    * Para sites voltados para a Internet, não há atualizações DNS necessárias após o failover. Execute as etapas de saudação descritas em tooconfigure de seção 'Diretrizes de rede' de saudação do Traffic Manager. Se Olá perfil do Traffic Manager foi configurado conforme descrito na seção anterior hello, adicione uma porta de fictício de tooopen (800 no exemplo hello) do script em Olá VM do Azure.

    * Para sites internos de opostas, adicione IP de Balanceador de carga de uma etapa manual tooupdate Olá DNS registro toopoint toohello novo Web da camada da VM.

4. Adicionar um aplicativo de pesquisa toorestore etapa manual de um backup ou iniciar um novo serviço de pesquisa.

5. Para restaurar o aplicativo de serviço de pesquisa de um backup, execute as etapas abaixo.

    * Esse método presume que foi feito um backup de aplicativo de serviço de pesquisa do hello antes do evento catastrófico hello e backup hello está disponível no site de saudação DR.
    * Isso pode ser obtido facilmente agendamento de backup de saudação (por exemplo, uma vez diariamente) e usando um backup de saudação de tooplace de procedimento de cópia no site Olá DR. Os procedimentos de cópia podem incluir programas em script, como o AzCopy (Cópia do Azure) ou a configuração de DFSR (Serviços de Replicação de Arquivos Distribuído).
    * Agora que saudação do SharePoint farm estiver em execução, navegue Olá Administração Central, 'Backup e restauração' e selecione restaurar. restauração Hello interroga local de backup Olá especificado (talvez seja necessário tooupdate valor de saudação). Selecione o backup de aplicativo de serviço de pesquisa de Olá você gostaria que toorestore.
    * A pesquisa é restaurada. Tenha em mente que Olá restauração espera toofind Olá mesmo topologia (mesmo número de servidores) e as mesmas rígido letras da unidade atribuídas toothose servidores. Para obter mais informações, consulte o documento ['Restaurar aplicativo de serviço de Pesquisa no SharePoint 2013'](https://technet.microsoft.com/library/ee748654.aspx).


6. Para iniciar com um novo aplicativo de serviço de Pesquisa, execute as etapas a seguir.

    * Este método assume que um backup de banco de dados de "Administração de pesquisa" hello está disponível no site de saudação DR.
    * Como hello outros bancos de dados do aplicativo de serviço de pesquisa não são replicados, eles precisam toobe criado novamente. toodo, então, navegue tooCentral administração e excluir Olá aplicativo de serviço de pesquisa. Em todos os servidores que Olá host índice de pesquisa, excluir arquivos de índice de saudação.
    * Olá crie novamente o aplicativo de serviço de pesquisa e isso cria bancos de dados Olá novamente. É recomendável toohave um script preparado que recria este aplicativo de serviço porque não é possível tooperform todas as ações via Olá GUI. Por exemplo, o local da unidade índice hello e configuração de topologia de pesquisa de saudação são possível somente usando cmdlets do PowerShell do SharePoint. Use o cmdlet do Windows PowerShell Olá SPEnterpriseSearchServiceApplication de restauração e especifique hello com envio de log e banco de dados de administração de pesquisa, Search_Service__DB replicado. Esse cmdlet oferece a configuração de pesquisa hello, esquema, propriedades gerenciadas, regras e fontes e cria um conjunto padrão de saudação outros componentes.
    * Quando Olá que aplicativo de serviço de pesquisa tem ser recriados, você deve iniciar um rastreamento completo para cada Olá toorestore de fonte de conteúdo serviço de pesquisa. Você perder algumas informações de análise do farm local hello como recomendações de pesquisa.

7. Depois que todas as etapas de saudação são concluídas, salvar o plano de recuperação de saudação e plano de recuperação final Olá será semelhante ao seguinte.

    ![RP Salvo](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Executar um failover de teste
Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de serviço.
2.  Clique no plano de recuperação de saudação criado para o aplicativo do SharePoint.
3.  Clique em 'Failover de Teste'.
4.  Selecione o ponto de recuperação e o processo de failover de teste do rede virtual do Azure toostart hello.
5.  Após ambiente secundário hello, você pode executar a validação.
6.  Depois que as validações de saudação estiverem concluídas, você pode clicar em 'Failover de teste de limpeza' no plano de recuperação hello e ambiente de failover de teste de saudação é limpo.

Para obter orientação sobre como fazer o failover de teste para o AD e DNS, consulte muito[teste considerações de failover para o AD e DNS](site-recovery-active-directory.md#test-failover-considerations) documento.

Para obter orientações sobre como fazer o failover de teste para SQL sempre em grupos de disponibilidade, consulte muito[realizando teste de failover para o SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) documento.

## <a name="doing-a-failover"></a>Executar um failover
Siga [estas diretrizes](site-recovery-failover.md) para fazer um failover.

1.  Visite o portal tooAzure e selecione seu Cofre de serviços de recuperação.
2.  Clique no plano de recuperação de saudação criado para o aplicativo do SharePoint.
3.  Clique em 'Failover'.
4.  Selecione o processo de failover de saudação de toostart de ponto de recuperação.

## <a name="next-steps"></a>Próximas etapas
Você pode saber mais sobre [replicar outros aplicativos](site-recovery-workload.md) usando o Site Recovery.
