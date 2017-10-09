---
title: "aaaAzure alta disponibilidade de máquinas virtuais para o SAP NetWeaver | Microsoft Docs"
description: "Guia de alta disponibilidade do SAP NetWeaver em máquinas virtuais do Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Máquinas virtuais do Azure é a solução de hello para empresas que precisam de computação, armazenamento e recursos de rede, no mínimo de tempo e sem ciclos de compra longos. Você pode usar máquinas virtuais do Azure toodeploy clássico aplicativos como ABAP baseados no SAP NetWeaver, Java e uma pilha ABAP + Java. Estenda a confiabilidade e a disponibilidade sem recursos locais adicionais. As Máquinas Virtuais do Azure dão suporte à conectividade entre locais, o que permite que você integre as Máquinas Virtuais do Azure aos seus domínios locais, a nuvens privadas e à estrutura do sistema SAP.

Neste artigo, abordaremos Olá etapas que toodeploy sistemas SAP de alta disponibilidade no Azure usando o modelo de implantação do Azure Resource Manager hello. Vamos percorrer estas tarefas principais:

* Localize Olá direita guias Observações sobre o SAP e a instalação, listados em hello [recursos] [ sap-ha-guide-2] seção. Este artigo complementa a documentação de instalação do SAP e observações sobre o SAP, que são Olá recursos principais que podem ajudá-lo a instalar e implantar o software SAP em plataformas específicas.
* Conhecer as diferenças de saudação entre o modelo de implantação do Azure Resource Manager hello e modelo de implantação clássico do Azure de saudação.
* Saiba mais sobre os modos de quorum de cluster de Failover do Windows Server, para que você pode selecionar modelo de saudação que é ideal para sua implantação do Azure.
* Aprenda sobre o armazenamento compartilhado do Windows Server Failover Clustering nos serviços Azure.
* Saiba como toohelp proteger os componentes de ponto único de falha como avançado Business aplicativo programação (ABAP) SAP Central Services (ASCS) / SAP Central Services (SCS) e sistemas de gerenciamento de banco de dados (DBMS) e componentes redundantes, como SAP Servidor de aplicativos, no Azure.
* Execute um exemplo passo a passo da instalação e configuração de um sistema SAP de alta disponibilidade em um cluster do Clustering de Failover do Windows Server no o Azure usando o Azure Resource Manager.
* Saiba mais sobre toouse necessárias etapas adicionais, Clustering de Failover do Windows Server no Azure, mas que não são necessários em uma implantação local.

toosimplify implantação e configuração, neste artigo, usamos Olá modelos do Gerenciador de recursos de alta disponibilidade do SAP de três camadas. modelos de saudação automatizam a implantação de saudação toda a infraestrutura que você precisa para um sistema SAP de alta disponibilidade. infraestrutura de saudação também dá suporte a dimensionamento do SAP aplicativo desempenho padrão (SAPS) de seu sistema SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Pré-requisitos
Antes de começar, certifique-se de que você atenda aos pré-requisitos de saudação descritos nas seções a seguir de saudação. Além disso, ser toocheck-se de que todos os recursos listados em Olá [recursos] [ sap-ha-guide-2] seção.

Neste artigo, podemos usar modelos do Azure Resource Manager para [SAP NetWeaver de três camadas usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Para uma visão geral dos modelos, confira [Modelos do Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos
Esses artigos abordam implantações SAP no Azure:

* [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide]
* [Implantação de Máquinas Virtuais do Azure para SAP NetWeaver][deployment-guide]
* [Implantação de Máquinas Virtuais do Azure do DBMS para SAP NetWeaver][dbms-guide]
* [Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver (este guia)][sap-ha-guide]

> [!NOTE]
> Sempre que possível, podemos dar uma toohello link referindo-se o guia de instalação do SAP (consulte Olá [guias de instalação do SAP][sap-installation-guides]). Pré-requisitos e informações sobre o processo de instalação Olá, ele é uma instalação de SAP NetWeaver boa ideia tooread Olá orienta cuidadosamente. Este artigo aborda apenas as tarefas específicas para sistemas baseados no SAP NetWeaver que você pode usar com as Máquinas Virtuais do Azure.
>
>

Essas observações sobre o SAP estão relacionadas toohello tópico do SAP no Azure:

| Número da observação | Title |
| --- | --- |
| [1928533] |Aplicativos SAP no Azure: dimensionamento e produtos com suporte |
| [2015553] |SAP no Microsoft Azure: pré-requisitos de suporte |
| [1999351] |Monitoramento aprimorado do Azure para SAP |
| [2178632] |Métricas-chave de monitoramento para SAP no Microsoft Azure |
| [1999351] |Virtualização no Windows: monitoramento avançado |
| [2243692] |Usar o Armazenamento SSD Premium do Azure para instância do SAP DBMS |

Saiba mais sobre Olá [limitações de assinaturas do Azure][azure-subscription-service-limits-subscription], incluindo limitações padrão gerais e limitações máximo.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidade com o Azure Resource Manager versus o modelo de implantação clássico do Azure Olá
modelos de implantação clássico do Azure e Hello Azure Resource Manager são diferentes em Olá áreas a seguir:

- Grupos de recursos
- Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure Olá
- Suporte para cenário SAP com vários SID

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos
No Gerenciador de recursos do Azure, você pode usar recursos grupos toomanage todos os recursos de aplicativo hello em sua assinatura do Azure. Uma abordagem integrada, em um grupo de recursos, todos os recursos têm Olá mesmo ciclo de vida. Por exemplo, todos os recursos são criados no hello mesmo tempo e eles são excluídos no hello simultaneamente. Saiba mais sobre [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno carregar a dependência de Balanceador no grupo de recursos do Azure Olá

No modelo de implantação clássico do Azure hello, há uma dependência entre o balanceador de carga interno do Azure hello (serviço de Balanceador de carga do Azure) e o serviço de nuvem hello. Cada balanceador de carga interno precisa de um serviço de nuvem.

No Gerenciador de recursos do Azure, todos os recursos do Azure precisa toobe colocado em um grupo de recursos do Azure, e isso também é válido para o balanceador de carga do Azure. No entanto, não há nenhum grupo de recursos do Azure uma necessidade toohave por balanceador de carga do Azure, por exemplo, um grupo de recursos do Azure pode conter vários balanceadores de carga do Azure. ambiente de saudação é mais simples e mais flexível. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Suporte para cenário SAP com vários SID

No Azure Resource Manager, você pode instalar várias instâncias ASCS/SCS do SID (identificador do sistema SAP) em um cluster. Instâncias de vários SID são possíveis devido ao suporte de vários endereços IP para cada balanceador de carga interno de carga do Azure.

toouse Olá modelo de implantação clássico do Azure, siga os procedimentos de saudação descritos em [SAP NetWeaver no Azure: instâncias de cluster SAP ASCS/SCS usando o Clustering de Failover do Windows Server no Azure com SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> É altamente recomendável que você use o modelo de implantação do Azure Resource Manager Olá para as instalações do SAP. Ele oferece vários benefícios que não estão disponíveis no modelo de implantação clássico hello. Saiba mais sobre os [modelos de implantação do Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Windows Server Failover Clustering
Clustering de Failover do Windows Server é a base de saudação de uma instalação do SAP ASCS/SCS de alta disponibilidade e DBMS no Windows.

Um cluster de failover é um grupo de 1 + n servidores independentes (nós) que funcionam em conjunto de disponibilidade de saudação tooincrease de aplicativos e serviços. Se ocorrer uma falha de nó, Clustering de Failover do Windows Server calcula o número de saudação de falhas que podem ocorrer durante a manutenção de um cluster tooprovide aplicativos e serviços. Você pode escolher de clustering de failover do tooachieve de modos de quorum diferente.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de quorum
Você pode escolher dentre quatro modos de quorum quando usa o Windows Server Failover Clustering:

* **Maioria de nós**. Cada nó do cluster Olá poderá votar. funções de cluster Olá somente com a maioria dos votos, ou seja, com mais da metade Olá votos. Recomendamos essa opção para clusters com número ímpar de nós. Por exemplo, três nós em um cluster de sete nós podem falhar e ainda é de cluster Olá alcance uma maioria e continua toorun.  
* **Maioria de nós e disco**. Cada nó e um disco designado (uma testemunha de disco) no armazenamento de cluster Olá poderá votar quando elas estiverem disponíveis e em comunicação. funções de cluster Olá somente com a maioria dos Olá votos, ou seja, com mais da metade de votos de saudação. Esse modo faz sentido em um ambiente de cluster com um número par de nós. Se nós Olá metade e disco Olá estiverem online, cluster Olá permanecerá em um estado íntegro.
* **Maioria de nós e compartilhamento de arquivos**. Cada sinal de adição de nó cria um compartilhamento de arquivo designado (um compartilhamento de arquivos) que Olá administrador poderá votar, independentemente se nós hello e compartilhamento de arquivos estão disponíveis e em comunicação. funções de cluster Olá somente com a maioria dos Olá votos, ou seja, com mais da metade de votos de saudação. Esse modo faz sentido em um ambiente de cluster com um número par de nós. É semelhante toohello nó e modo de maioria de disco, mas ele usa um compartilhamento de arquivo testemunha, em vez de um disco testemunha. Este modo é fácil tooimplement, mas se o compartilhamento de arquivo hello em si não está altamente disponível, ele pode se tornar um ponto único de falha.
* **Sem maioria: somente disco**. Olá tiver um quorum se um nó estiver disponível e na comunicação com um disco específico no armazenamento de cluster hello. Somente nós de saudação que também estiverem em comunicação com esse disco podem ingressar o cluster de saudação. Recomendamos que você não use esse modo.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Windows Server Failover Clustering no local
A Figura 1 mostra um cluster de dois nós. Se hello falha de conexão de rede entre os nós de saudação e ambos os nós continuar e em execução, um compartilhamento de arquivos ou disco de quorum determina qual nó continuará do cluster de saudação tooprovide aplicativos e serviços. nó de saudação que tem o disco de quorum toohello acesso ou compartilhamento de arquivo é o nó de Olá que assegura que os serviços continuem.

Como este exemplo usa um cluster de dois nós, usamos hello nó e o modo de quorum maioria de compartilhamento de arquivo. Olá nó e a maioria dos também é uma opção válida. Em um ambiente de produção, recomendamos que você use um disco de quorum. Você pode usar toomake de tecnologia de sistema de rede e armazenamento altamente disponível.

![Figura 1: exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure][sap-ha-guide-figure-1000]

_**Figura 1:** exemplo de uma configuração de Windows Server Failover Clustering para SAP ASCS/SCS no Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Armazenamento compartilhado
A Figura 1 também mostra um cluster de armazenamento compartilhado de dois nós. Em um cluster de armazenamento compartilhado no local, todos os nós no cluster Olá detectam armazenamento compartilhado. Um mecanismo de bloqueio protege os dados de saudação contra danos. Todos os nós podem detectar se outro nó falhar. Se um nó falhar, nó restante Olá apropria Olá dos recursos de armazenamento e garante a disponibilidade de saudação de serviços.

> [!NOTE]
> Você não precisa de discos compartilhados de alta disponibilidade com alguns aplicativos de DBMS, como o SQL Server. SQL Server Always On replica os arquivos de log e dados do DBMS de disco local de saudação do disco local de toohello do nó de um cluster de outro nó do cluster. Nesse caso, configuração de cluster do Windows hello não precisa de um disco compartilhado.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Resolução de nome e rede
Computadores cliente alcançar cluster Olá sobre um endereço IP virtual e um nome de host virtual que Olá fornece do servidor DNS. Olá nós locais e o servidor DNS Olá pode lidar com vários endereços IP.

Em uma instalação comum, você usa duas ou mais conexões de rede:

* Armazenamento de toohello uma conexão dedicada
* Uma conexão de rede interna de cluster de pulsação Olá
* Uma rede pública que os clientes usam tooconnect toohello cluster

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Windows Server Failover Clustering no Azure
Em comparação com implantações de nuvem privada ou metal toobare, máquinas virtuais do Azure requer etapas adicionais tooconfigure Clustering de Failover do Windows Server. Quando você cria um disco de cluster compartilhado, você precisa tooset nomes de vários endereços IP e o host virtual para a instância do SAP ASCS/SCS hello.

Neste artigo, vamos discutir os principais conceitos e Olá etapas adicionais necessárias toobuild um cluster de serviços de alta disponibilidade central SAP no Azure. Mostraremos como tooset ferramenta de terceiros Olá SIOS DataKeeper e como tooconfigure hello Azure interno balanceador de carga. Você pode usar essas ferramentas toocreate um cluster de failover do Windows com uma testemunha de compartilhamento de arquivo no Azure.

![Figura 2: configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado][sap-ha-guide-figure-1001]

_**Figura 2:** configuração do Windows Server Failover Clustering no Azure sem um disco compartilhado_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartilhado no Azure com SIOS DataKeeper
Você precisa de armazenamento compartilhado em cluster para uma instância do SAP ASCS/SCS de alta disponibilidade. Como de setembro de 2016, o Azure não oferece armazenamento compartilhado que você pode usar toocreate um cluster de armazenamento compartilhado. Você pode usar o software de terceiros SIOS DataKeeper Cluster Edition toocreate um armazenamento espelhado que simula o armazenamento compartilhado de cluster. Olá solução SIOS fornece replicação síncrona de dados em tempo real. É assim que você pode criar um recurso de disco compartilhado para um cluster:

1. Anexe um tooeach em disco adicional de máquinas virtuais de saudação (VMs) em uma configuração de cluster do Windows.
2. Execute o SIOS DataKeeper Cluster Edition em ambos os nós da máquina virtual.
3. Configure SIOS DataKeeper Cluster Edition para que ele reflete o conteúdo de saudação do volume de disco anexado Olá Olá máquina virtual toohello anexado adicional no disco do volume de origem Olá virtual da máquina de destino. SIOS DataKeeper abstrai Olá origem e destino local os volumes e, em seguida, apresenta tooWindows Clustering de Failover do servidor como um disco compartilhado.

Saiba mais sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Figura 3: configuração do Clustering de Failover do Windows Server no Azure com o SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 3:** configuração do Windows Server Failover Cluster no Azure com o SIOS DataKeeper_

> [!NOTE]
> Você não precisa de discos compartilhados de alta disponibilidade com alguns produtos de DBMS, como o SQL Server. SQL Server Always On replica os arquivos de log e dados do DBMS de disco local de saudação do disco local de toohello do nó de um cluster de outro nó do cluster. Nesse caso, configuração de cluster do Windows hello não precisa de um disco compartilhado.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolução de nomes no Azure
plataforma de nuvem do Azure Olá não oferece Olá opção tooconfigure endereços IP virtuais, como endereços IP flutuantes. É necessário tooset uma solução alternativa a um virtual tooreach Olá cluster recurso de endereço IP na nuvem hello.
O Azure tem um balanceador de carga interno no hello Serviço Balanceador de carga do Azure. Com o balanceador de carga interno hello, clientes alcançar cluster Olá por endereço IP virtual de cluster hello.
Você precisa de Balanceador de carga interno toodeploy Olá no grupo de recursos de saudação que contém nós de cluster de saudação. Em seguida, configure porta de necessária todas as regras de encaminhamento com investigação Olá portas Olá interno do balanceador de carga.
clientes de saudação podem se conectar por meio do nome de host virtual hello. servidor DNS de saudação resolve o endereço IP de cluster hello e saudação de carga interno balanceador identificadores porta encaminhamento toohello o nó ativo do cluster de saudação.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> SAP NetWeaver de alta disponibilidade na Azure IaaS (Infraestrutura como um serviço)
tooachieve SAP alta disponibilidade de aplicativos, como SAP para componentes de software, você precisa tooprotect Olá componentes a seguir:

* Instância do Servidor de Aplicativos SAP
* Instância ASCS/SCS SAP
* Servidor DBMS

Para obter mais informações sobre como proteger os componentes SAP em cenários de alta disponibilidade, consulte [Planejamento e implementação de Máquinas Virtuais do Azure para SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Servidor de Aplicativos SAP de Alta Disponibilidade
Geralmente você não precisa de uma solução de alta disponibilidade específica para instâncias de servidor de aplicativos SAP e a caixa de diálogo hello. Você atinge alta disponibilidade por redundância e configura várias instâncias de caixa de diálogo em diferentes Máquinas Virtuais do Azure. Você deve ter pelo menos duas instâncias do aplicativo SAP instaladas em duas Máquinas Virtuais do Azure.

![Figura 4: Servidor de Aplicativos SAP de alta disponibilidade][sap-ha-guide-figure-2000]

_**Figura 4:** Servidor de Aplicativos SAP de alta disponibilidade_

Você deve colocar todas as máquinas virtuais que instâncias de servidor de aplicativos SAP host em Olá mesmo conjunto de disponibilidade do Azure. Um conjunto de disponibilidade do Azure garante que:

* Todas as máquinas virtuais são parte da saudação mesmo domínio de atualização. Por exemplo, um domínio de atualização, torna-se de que as máquinas virtuais de saudação não são atualizadas em Olá mesmo tempo durante o tempo de inatividade de manutenção planejada.
* Todas as máquinas virtuais são parte da saudação mesmo domínio de falha. Por exemplo, um domínio de falha, torna-se de que as máquinas virtuais são implantadas para que nenhum ponto de falha afeta a disponibilidade de saudação de todas as máquinas virtuais.

Saiba mais sobre como muito[gerenciar Olá disponibilidade das máquinas virtuais][virtual-machines-manage-availability].

Somente disco não gerenciado: como Olá conta de armazenamento do Azure é um ponto único de falha potencial, é importante toohave pelo menos duas contas de armazenamento do Azure, na qual pelo menos duas máquinas virtuais é distribuído. Em uma configuração ideal, discos de saudação de cada máquina virtual que está executando uma instância de diálogo SAP seriam implantados em uma conta de armazenamento diferente.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instância do SAP ASCS/SCS de alta disponibilidade
A Figura 5 é um exemplo de instância do SAP ASCS/SCS de alta disponibilidade.

![Figura 5: instância do SAP ASCS/SCS de alta disponibilidade][sap-ha-guide-figure-2001]

_**Figura 5:** instância do SAP ASCS/SCS de alta disponibilidade_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidade da Instância do SAP ASCS/SCS com o Clustering de Failover do Windows Server no Azure
Em comparação com implantações de nuvem privada ou metal toobare, máquinas virtuais do Azure requer etapas adicionais tooconfigure Clustering de Failover do Windows Server. toobuild um cluster de failover do Windows, é necessário um disco de cluster compartilhado, vários endereços IP, vários nomes de host virtual e um balanceador de carga interno do Azure para uma instância SAP ASCS/SCS de clustering. Discutiremos isso em mais detalhes posteriormente neste artigo hello.

![Figura 6: configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure usando SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 6:** configuração do Windows Server Failover Cluster para SAP ASCS/SCS no Azure com SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Instância do DBMS de alta disponibilidade
Olá DBMS é também um ponto único de contato em um sistema SAP. Você precisa tooprotect-lo usando uma solução de alta disponibilidade. A Figura 7 mostra uma solução de alta disponibilidade do SQL Server Always On no Azure, o balanceador de carga com o Clustering de Failover do Windows Server e hello Azure interno. O AlwaysOn do SQL Server replica os arquivos de log e dados do DBMS usando sua própria replicação DBMS. Nesse caso, você não precisa de discos compartilhados de cluster, que simplifica a configuração inteira de saudação.

![Figura 7: exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server][sap-ha-guide-figure-2003]

_**Figura 7:** exemplo de um DBMS SAP de alta disponibilidade com o Always On do SQL Server_

Para obter mais informações sobre o agrupamento do SQL Server no Azure usando o modelo de implantação do Azure Resource Manager hello, consulte estes artigos:

* [Configure o grupo de disponibilidade Always On em Máquinas Virtuais do Azure manualmente usando o Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Configurar um balanceador interno de carga do Azure para um grupo de disponibilidade Always On no Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Cenários de implantação de alta disponibilidade de ponta a ponta

### <a name="deployment-scenario-using-architectural-template-1"></a>Cenário de implantação usando o Modelo Arquitetônico 1

A Figura 8 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP. Esse cenário é definido da seguinte maneira:

- Um cluster dedicado é usado para a instância do SAP ASCS/SCS hello.
- Um cluster dedicado é usado para a instância DBMS hello.
- Instâncias do Servidor de Aplicativos SAP são implantadas em suas próprias VMs dedicadas.

![Figura 8: Modelo Arquitetônico 1 de alta disponibilidade de SAP, com cluster dedicado para ASCS/SCS e DBMS][sap-ha-guide-figure-2004]

_**Figura 8:** Modelo Arquitetônico 1 de alta disponibilidade de SAP, com clusters dedicados para ASCS/SCS e DBMS_

### <a name="deployment-scenario-using-architectural-template-2"></a>Cenário de implantação usando o Modelo Arquitetônico 2

A Figura 9 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **um** sistema SAP. Esse cenário é definido da seguinte maneira:

- Um cluster dedicado é usado para **ambos** Olá SAP ASCS/SCS instância e Olá DBMS.
- Instâncias do Servidor de Aplicativos SAP são implantados em VMs próprias dedicadas.

![Figura 9: Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS][sap-ha-guide-figure-2005]

_**Figura 9:** Modelo Arquitetônico 2 de alta disponibilidade de SAP, com um cluster dedicado para ASCS/SCS e outro para DBMS_

### <a name="deployment-scenario-using-architectural-template-3"></a>Cenário de implantação usando o Modelo Arquitetônico 3

A Figura 10 mostra um exemplo de uma arquitetura de alta disponibilidade do SAP NetWeaver no Azure para **dois** sistemas SAP, com &lt;SID1&gt; e &lt;SID2&gt;. Esse cenário é definido da seguinte maneira:

- Um cluster dedicado é usado para **ambos** instância Olá SAP ASCS/SCS SID1 *e* instância Olá SAP ASCS/SCS SID2 (um cluster).
- Um cluster dedicado é usado para SID1 e outro para SID2 de DBMS (dois clusters).
- Instâncias de servidor de aplicativos do SAP para Olá sistema SAP SID1 tem suas próprias VMs dedicados.
- Instâncias de servidor de aplicativos do SAP para Olá sistema SAP SID2 tem suas próprias VMs dedicados.

![Figura 10: Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS][sap-ha-guide-figure-6003]

_**Figura 10:** Modelo Arquitetônico 3 de alta disponibilidade de SAP, com cluster dedicado para diferentes instâncias de ASCS/SCS_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar a infraestrutura de saudação

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Preparar a infraestrutura de saudação para 1 arquitetura de modelo
Os modelos do Azure Resource Manager para SAP ajudam a simplificar a implantação dos recursos necessários.

modelos de três camadas Olá no Gerenciador de recursos do Azure também oferecem suporte a cenários de alta disponibilidade, como, em 1 arquitetura de modelo, que tem dois clusters. Cada cluster é um ponto único de falha de SAP para SAP ASCS/SCS e DBMS.

Aqui é onde você pode obter os modelos do Gerenciador de recursos do Azure para o cenário de exemplo hello que descrevemos neste artigo:

* [Imagem do Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Imagem do Marketplace do Azure usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Imagem personalizada usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

infraestrutura tooprepare Olá para 1 arquitetura de modelo:

- Em Olá portal do Azure, Olá **parâmetros** folha em Olá **SYSTEMAVAILABILITY** selecione **HA**.

  ![Figura 11: definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager][sap-ha-guide-figure-3000]

_**Figura 11:** definir os parâmetros de SAP de alta disponibilidade do Azure Resource Manager_


  criam modelos de saudação:

  * **Máquinas virtuais**:
    * Máquinas virtuais do Servidor de Aplicativos SAP: <*SAPSystemSID*>-di-<*Number*>
    * Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-ascs-<*Number*>
    * Cluster DBMS: <*SAPSystemSID*>-db-<*Number*>

  * **Placas de rede para todas as máquinas virtuais, com endereços IP associados**:
    * <*SAPSystemSID*>-nic-di-<*Number*>
    * <*SAPSystemSID*>-nic-ascs-<*Number*>
    * <*SAPSystemSID*>-nic-db-<*Number*>

  * **Contas de armazenamento do Azure (apenas discos não gerenciados)**

  * **Grupos de Disponibilidade** para:
    * Máquinas virtuais do Servidor de Aplicativos do SAP: <*SAPSystemSID*>-avset-di
    * Máquinas virtuais de cluster ASCS/SCS: <*SAPSystemSID*>-avset-ascs
    * Máquinas virtuais de cluster DBMS: <*SAPSystemSID*>-avset-db

  * **Balanceador de carga interno do Azure**:
    * Com todas as portas para a instância do ASCS/SCS hello e o endereço IP <*SAPSystemSID*> - lb - ascs
    * Com todas as portas para Olá DBMS do SQL Server e o endereço IP <*SAPSystemSID*> - lb - db

  * **Grupo de segurança de rede**: <*SAPSystemSID*>-nsg-ascs-0  
    * Com um toohello de porta de protocolo de área de trabalho remota (RDP) externo abra <*SAPSystemSID*> - ascs - 0 virtual machine

> [!NOTE]
> Todos os endereços IP de placas de rede hello e balanceadores de carga interno do Azure são **dinâmico** por padrão. Alterá-los muito**estático** endereços IP. Descrevemos como toodo posteriormente neste artigo hello.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implantar máquinas virtuais com toouse de conectividade (entre locais) da rede corporativa na produção
Para sistemas SAP de produção, implante máquinas virtuais do Azure com [conectividade de rede corporativa (entre instalações)][planning-guide-2.2] usando o VPN Site a Site ou o ExpressRoute do Azure.

> [!NOTE]
> Você pode usar a instância da Rede Virtual do Azure. subrede e a rede virtual Olá já foram criados e preparados.
>
>

1.  Em Olá portal do Azure, Olá **parâmetros** folha em Olá **NEWOREXISTINGSUBNET** selecione **existente**.
2.  Em Olá **SUBNETID** caixa, adicione a cadeia de caracteres completa da rede do Azure preparada SubnetID onde você planeja toodeploy suas máquinas virtuais do Azure hello.
3.  tooget uma lista de todas as sub-redes de rede do Azure, execute este comando do PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Olá **ID** campo mostra Olá **SUBNETID**.
4. tooget uma lista de todos os **SUBNETID** valores, execute este comando do PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Olá **SUBNETID** tem esta aparência:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implantar instâncias de SAP somente na nuvem para teste e demonstração
Você pode implantar o sistema SAP de alta disponibilidade em um modelo de implantação somente na nuvem. Esse tipo de implantação é principalmente útil para casos de uso de demonstração e teste. Ele não é adequado para casos de uso de produção.

- Em Olá portal do Azure, Olá **parâmetros** folha, no hello **NEWOREXISTINGSUBNET** selecione **novo**. Deixe Olá **SUBNETID** campo vazio.

  Olá SAP do Azure Resource Manager cria automaticamente Olá sub-rede e a rede virtual do Azure.

> [!NOTE]
> Você também precisa toodeploy pelo menos uma dedicada a máquina virtual para o Active Directory e DNS no Olá a mesma instância de rede Virtual do Azure. modelo de saudação não cria essas máquinas virtuais.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Preparar a infraestrutura de saudação para 2 de modelo de arquitetura

Você pode usar este modelo do Gerenciador de recursos do Azure para SAP toohelp simplificar a implantação de recursos de infraestrutura necessária para 2 de modelo de arquitetura do SAP.

Aqui é onde você pode obter os modelos do Azure Resource Manager para esse cenário de implantação:

* [Imagem do Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Imagem do Marketplace do Azure usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Imagem personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Imagem personalizada usando Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Preparar a infraestrutura de saudação para 3 arquitetura do modelo

Você pode preparar a infraestrutura de saudação e configurar SAP para **várias SID**. Por exemplo, você pode adicionar uma instância SAP ASCS/SCS adicional em uma configuração de cluster *existente*. Para obter mais informações, consulte [configurar uma instância SAP ASCS/SCS adicional em um toocreate de configuração de cluster uma configuração de multi-SID do SAP existente no Gerenciador de recursos do Azure][sap-ha-multi-sid-guide].

Se você quiser toocreate um novo cluster de várias SID, você pode usar o multi-SID de saudação [modelos de início rápido no GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate um novo cluster de várias SID, é necessário toodeploy Olá três modelos a seguir:

* [Modelo de ASCS/SCS](#ASCS-SCS-template)
* [Modelo de banco de dados](#database-template)
* [Modelo dos servidores de aplicativo](#application-servers-template)

Olá seções a seguir têm mais detalhes sobre os modelos de saudação e parâmetros Olá necessário tooprovide em modelos de saudação.

#### <a name="ASCS-SCS-template"></a> Modelo de ASCS/SCS

modelo ASCS/SCS Olá implanta duas máquinas virtuais que você pode usar toocreate um cluster de failover do Windows Server que hospeda várias instâncias do ASCS/SCS.

tooset modelo de saudação ASCS/SCS multi-SID em Olá [modelo de várias SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] ou [modelo de várias SID ASCS/SCS usando discos gerenciados] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], insira valores para Olá parâmetros a seguir:

  - **Prefixo de Recursos**.  Defina prefixo de recurso hello, que é usado tooprefix todos os recursos que são criados durante a implantação de saudação. Como recursos de Olá não pertencer a um sistema SAP tooonly, prefixo de saudação do recurso de saudação não é Olá SID de um sistema SAP.  Olá prefixo deve estar entre **três e seis caracteres**.
  - **Tipo de Pilha**. Selecione o tipo de pilha de saudação de saudação sistema SAP. Dependendo do tipo de pilha hello, o balanceador de carga do Azure tem um (ABAP ou Java somente) ou dois (ABAP + Java) endereços IP privados por sistema SAP.
  -  **Tipo de sistema operacional**. Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.
  -  **Contagem do Sistema SAP**. Selecione o número de saudação de sistemas SAP que você deseja tooinstall neste cluster.
  -  **Disponibilidade do Sistema**. Selecione **HA**.
  -  **Nome de Usuário e Senha de Administrador**. Crie um novo usuário que pode ser usado toosign toohello máquina.
  -  **Sub-rede Nova ou Existente**. Define se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada. Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione **existente**.
  -  **ID da Sub-rede**. ID de saudação do conjunto de máquinas virtuais do hello sub-rede toowhich Olá deve estar conectado. Selecione a sub-rede de saudação da sua rede virtual privada (VPN) ou rede de rota expressa rede virtual tooconnect Olá máquina virtual tooyour local. ID de saudação geralmente tem esta aparência:

   /subscriptions/<*ID da assinatura*>/resourceGroups/<*nome do grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nome de rede virtual*>/subnets/<*nome de sub-rede*>

modelo de saudação implanta uma instância de Balanceador de carga do Azure, que dá suporte a vários sistemas SAP.

- Olá ASCS são configuradas para o número de instância 00, 10, 20...
- Olá SCS são configuradas para o número de instância 01, 11, 21...
- Olá ASCS Enqueue replicação servidor (es) (Linux) são configuradas para o número de instância 02, 12, 22...
- Olá SCS es (Linux) são configuradas para o número de instância 03, 13, 23...

Balanceador de carga Hello contém 1 (2 para Linux) VIP(s), 1 VIP x do ASCS/SCS e 1 VIP x para es (Linux).

Olá lista a seguir contém todas as regras (onde x é o número de saudação do hello sistema SAP, por exemplo, 1, 2, 3...) de balanceamento de carga:
- Portas específicas do Windows para cada o sistema SAP: 445, 5985
- Portas ASCS (número de instância x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016
- Portas SCS (número de instância x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116
- Portas ASCS ERS no Linux (número de instância x2): 33x2, 5x213, 5x214, 5x216
- Portas SCS ERS no Linux (número de instância x3): 33x3, 5x313, 5x314, 5x316

Balanceador de carga de saudação é configurado toouse Olá portas de investigação (onde x é o número de saudação do hello sistema SAP, por exemplo, 1, 2, 3...) a seguir:
- Porta de investigação do balanceador interno de carga ASCS/SCS: 620x0
- Porta de investigação do balanceador interno de carga ERS (somente Linux): 621x2

#### <a name="database-template"></a> Modelo de banco de dados

modelo de banco de dados de saudação implanta uma ou duas máquinas virtuais que você pode usar tooinstall Olá o sistema de gerenciamento de banco de dados relacional (RDBMS) para um sistema SAP. Por exemplo, se você implantar um modelo ASCS/SCS para cinco sistemas SAP, será necessário toodeploy este modelo cinco vezes.

tooset modelo de várias SID Olá banco de dados, em Olá [modelo de multi-SID de banco de dados] [ sap-templates-3-tier-multisid-db-marketplace-image] ou [modelo de multi-SID de banco de dados usando discos gerenciados] [ sap-templates-3-tier-multisid-db-marketplace-image-md], insira valores para Olá parâmetros a seguir:

  -  **ID do sistema SAP**. Insira o sistema ID SAP Olá Olá sistema SAP que você deseja tooinstall. Olá ID será usado como um prefixo para recursos de saudação que são implantados.
  -  **Tipo de sistema operacional**. Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.
  -  **Dbtype**. Selecione o tipo de saudação do banco de dados de saudação desejado tooinstall no cluster hello. Selecione **SQL** se você quiser tooinstall Microsoft SQL Server. Selecione **HANA** se você planejar tooinstall SAP HANA em máquinas virtuais de saudação. Certifique-se de tooselect Olá tipo de sistema operacional correto: selecione **Windows** para SQL e selecione uma distribuição de Linux para HANA. Olá balanceador de carga do Azure que está conectada toohello máquinas virtuais serão configurado toosupport tipo de banco de dados de saudação selecionado:
    * **SQL**. o balanceador de carga Olá será a porta 1433 do balanceamento de carga. Verifique se toouse essa porta para a sua instalação do SQL Server Always On.
    * **HANA**. Balanceador de carga Hello serão portas 35015 e 35017 de balanceamento de carga. Certifique-se de que tooinstall HANA SAP com o número de instância **50**.
    Balanceador de carga Olá usará a porta de investigação 62550.
  -  **Tamanho do Sistema SAP**. Conjunto Olá número de SAPS Olá novo sistema fornecerá. Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.
  -  **Disponibilidade do Sistema**. Selecione **HA**.
  -  **Nome de Usuário e Senha de Administrador**. Crie um novo usuário que pode ser usado toosign toohello máquina.
  -  **ID da Sub-rede**. Insira a ID de Olá da sub-rede Olá que você usou durante a implantação de saudação do modelo ASCS/SCS hello, ou Olá ID de sub-rede de saudação que foi criado como parte da implantação de modelo ASCS/SCS do hello.

#### <a name="application-servers-template"></a> Modelo dos servidores de aplicativos

modelo de servidores de aplicativo Hello implanta duas ou mais máquinas virtuais que podem ser usadas como instâncias de servidor de aplicativos do SAP para um sistema SAP. Por exemplo, se você implantar um modelo ASCS/SCS para cinco sistemas SAP, será necessário toodeploy este modelo cinco vezes.

tooset backup Olá servidores multi-SID modelo de aplicativo no hello [modelo de aplicativo de SID de vários servidores] [ sap-templates-3-tier-multisid-apps-marketplace-image] ou [modelo de SID de vários servidores de aplicativo usando discos gerenciados] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], insira valores para Olá parâmetros a seguir:

  -  **ID do sistema SAP**. Insira o sistema ID SAP Olá Olá sistema SAP que você deseja tooinstall. Olá ID será usado como um prefixo para recursos de saudação que são implantados.
  -  **Tipo de sistema operacional**. Selecione o sistema de operacional de saudação de máquinas virtuais de saudação.
  -  **Tamanho do Sistema SAP**. Olá número de SAPS Olá novo sistema fornecerá. Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema.
  -  **Disponibilidade do Sistema**. Selecione **HA**.
  -  **Nome de Usuário e Senha de Administrador**. Crie um novo usuário que pode ser usado toosign toohello máquina.
  -  **ID da Sub-rede**. Insira a ID de Olá da sub-rede Olá que você usou durante a implantação de saudação do modelo ASCS/SCS hello, ou Olá ID de sub-rede de saudação que foi criado como parte da implantação de modelo ASCS/SCS do hello.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Rede virtual do Azure
Em nosso exemplo, o espaço de endereço de saudação do hello rede virtual do Azure é 10.0.0.0/16. Há uma sub-rede chamada **Subnet**, com um intervalo de endereços de 10.0.0.0/24. Todas as máquinas virtuais e balanceadores de carga internos são implantados nessa rede virtual.

> [!IMPORTANT]
> Não faça nenhuma alteração toohello as configurações de rede no sistema de operacional convidado hello. Isso inclui endereços IP, servidores DNS e sub-rede. Configure todas as configurações de rede no Azure. Olá serviço de protocolo de configuração de Host dinâmico (DHCP) propaga as configurações.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Endereços IP de DNS

Olá tooset necessário que endereços IP de DNS, Olá etapas a seguir.

1.  Em Olá portal do Azure, Olá **servidores DNS** folha, certifique-se de que sua rede virtual **servidores DNS** opção for definida muito**DNS personalizado**.
2.  Selecione as configurações com base no tipo de saudação da rede que você tem. Para obter mais informações, consulte Olá recursos a seguir:
    * [Conectividade de rede corporativa (entre locais)][planning-guide-2.2]: adicionar endereços IP hello dos servidores DNS local hello.  
    Você pode estender no DNS servidores toohello máquinas virtuais que estão em execução no Azure. Nesse cenário, você pode adicionar endereços de IP hello hello Azure máquinas virtuais em que você executa o serviço DNS hello.
    * [Implantação somente em nuvem][planning-guide-2.1]: implantar uma máquina virtual adicional no hello mesma instância de rede Virtual que serve como um servidor DNS. Adicionar endereços de IP Olá Olá Azure máquinas virtuais que você configurou o serviço DNS toorun.

    ![Figura 12: Configurar servidores DNS da Rede Virtual do Azure][sap-ha-guide-figure-3001]

    _**Figura 12:** Configurar servidores DNS da Rede Virtual do Azure_

  > [!NOTE]
  > Se você alterar os endereços IP hello dos servidores DNS hello, você precisa toorestart Olá máquinas virtuais do Azure tooapply Olá alteração e propagar os novos servidores DNS hello.
  >
  >

Em nosso exemplo, Olá serviço DNS é instalado e configurado nessas máquinas virtuais do Windows:

| Função da máquina virtual | Nome do host de máquina virtual | Nome da placa de rede | Endereço IP estático |
| --- | --- | --- | --- |
| Primeiro servidor DNS |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| Segundo servidor DNS |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Nomes de host e endereços IP estáticos para a instância clusterizada do SAP ASCS/SCS hello e instância clusterizada do DBMS

Para implantação local, você precisa destes endereços IP e nomes de host reservados:

| Função de nome de host virtual | Nome de host virtual | Endereço IP estático virtual |
| --- | --- | --- |
| Nome de host virtual do primeiro cluster SAP ASCS/SCS (para gerenciamento de cluster) |pr1-ascs-vir |10.0.0.42 |
| Nome de host virtual da instância do SAP ASCS/SCS |pr1-ascs-sap |10.0.0.43 |
| Nome de host virtual do segundo cluster SAP DBMS (gerenciamento de cluster) |pr1-dbms-vir |10.0.0.32 |

Quando você cria o cluster hello, criar hello nomes de host virtual **pr1-ascs-vir** e **pr1 de dbms de vir** e Olá associados a endereços IP que gerenciar o próprio cluster hello. Para obter informações sobre como toodo isso, consulte [coletar nós de cluster em uma configuração de cluster][sap-ha-guide-8.12.1].

Você pode criar manualmente Olá outros dois nomes de host virtual **pr1-ascs-sap** e **pr1 de dbms de sap**, e Olá associados a endereços IP, no servidor DNS hello. Hello instância clusterizada do SAP ASCS/SCS e instância DBMS Olá clusterizado usam esses recursos. Para obter informações sobre como toodo isso, consulte [criar um nome de host virtual para uma instância clusterizada do SAP ASCS/SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de endereços IP estáticos para máquinas de virtuais Olá SAP
Depois de implantar Olá toouse de máquinas virtuais no cluster, você precisa tooset os endereços IP estáticos para todas as máquinas virtuais. Fazer isso na configuração de rede Virtual do Azure Olá e não no sistema operacional hello.

1.  No portal do Azure de Olá, selecione **grupo de recursos** > **placa de rede** > **configurações** > **endereço IP** .
2.  Em Olá **endereços IP** folha, em **atribuição**, selecione **estático**. Em Olá **endereço IP** , digite o endereço IP de saudação que você deseja toouse.

  > [!NOTE]
  > Se você alterar o endereço IP Olá Olá placa de rede, você precisa toorestart Olá máquinas virtuais do Azure tooapply Olá alteração.  
  >
  >

  ![Figura 13: Definir os endereços IP estáticos Olá placa de rede de cada máquina virtual][sap-ha-guide-figure-3002]

  _**Figura 13:** conjunto de endereços IP estáticos Olá placa de rede de cada máquina virtual_

  Repita essa etapa para todas as interfaces de rede, ou seja, todas as máquinas virtuais, incluindo máquinas virtuais que você deseja toouse para o serviço do Active Directory/DNS.

Em nosso exemplo, temos estas máquinas virtuais e endereços IP estáticos:

| Função da máquina virtual | Nome do host de máquina virtual | Nome da placa de rede | Endereço IP estático |
| --- | --- | --- | --- |
| Primeira instância do Servidor de Aplicativos SAP |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| Segunda instância do Servidor de Aplicativos SAP |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Última instância do Servidor de Aplicativos SAP |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| Primeiro nó de cluster para a instância do ASCS/SCS |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| Segundo nó de cluster para a instância do ASCS/SCS |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| Primeiro nó de cluster para a instância do DBMS |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| Segundo nó de cluster para a instância do DBMS |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Definir um endereço IP estático para o balanceador de carga interno do Azure Olá

modelo do Gerenciador de recursos do Azure SAP Olá cria um balanceador de carga interno do Azure que é usado para o cluster de instância de SAP ASCS/SCS hello e DBMS hello.

> [!IMPORTANT]
> Olá endereço IP do nome de host virtual de saudação do hello SAP ASCS/SCS é Olá mesmo como endereço IP de saudação do hello balanceador de carga interno do SAP ASCS/SCS: **pr1 de balanceamento de carga de ascs**.
> Olá endereço IP do nome virtual Olá Olá DBMS é Olá mesmo como endereço IP de saudação do hello balanceador de carga interno do DBMS: **pr1 de balanceamento de carga de dbms**.
>
>

tooset um endereço IP estático para hello Azure interno balanceador de carga:

1.  Olá implantação inicial define um endereço IP do balanceador de carga interno Olá muito**dinâmico**. Em Olá portal do Azure, Olá **endereços IP** folha, em **atribuição**, selecione **estático**.
2.  Definir endereço IP de saudação do balanceador de carga interno Olá **pr1 de balanceamento de carga de ascs** toohello endereço IP do nome de host virtual Olá da instância do SAP ASCS/SCS hello.
3.  Definir endereço IP de saudação do balanceador de carga interno Olá **pr1 de balanceamento de carga de dbms** toohello endereço IP do nome de host virtual Olá da instância DBMS hello.

  ![Figura 14: Definir os endereços IP estáticos para o balanceador de carga interno Olá para instância do SAP ASCS/SCS Olá][sap-ha-guide-figure-3003]

  _**Figura 14:** definir endereços IP estáticos para o balanceador de carga interno Olá para instância do SAP ASCS/SCS Olá_

Em nosso exemplo, temos dois balanceadores de carga internos do Azure que têm esses endereços IP estáticos:

| Função do balanceador de carga interno do Azure | Nome balanceador de carga interno do Azure | Endereço IP estático |
| --- | --- | --- |
| Balanceador de carga interno da instância SAP ASCS/SCS |pr1-lb-ascs |10.0.0.43 |
| Balanceador de carga interno de DBMS SAP |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Padrão de regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do ASCS/SCS

modelo do Gerenciador de recursos do Azure SAP Olá cria portas Olá que é necessário:
* Uma instância do ASCS ABAP, com o número de instância padrão Olá **00**
* Uma instância de Java SCS, com o número de instância padrão Olá **01**

Quando você instala sua instância SAP ASCS/SCS, você deve usar o número de instância padrão Olá **00** para seu número ABAP ASCS instância e saudação padrão instância **01** para sua instância de Java SCS.

Em seguida, crie pontos de extremidade para portas do SAP NetWeaver Olá de balanceamento de carga interna necessária.

toocreate necessário balanceamento de carga interno de pontos de extremidade, primeiro, crie esses pontos de extremidade para portas do SAP NetWeaver ABAP ASCS Olá de balanceamento de carga:

| Nome da regra do balanceamento de carga/serviço | Números de porta padrão | Portas concretas para (instância do ASCS com número de instância 00) (ERS com 10) |
| --- | --- | --- |
| Enfileirar Servidor / *lbrule3200* |32 <*InstanceNumber*> |3200 |
| Servidor de Mensagens ABAP / *lbrule3600* |36 <*InstanceNumber*> |3600 |
| Mensagem interna ABAP / *lbrule3900* |39 <*InstanceNumber*> |3900 |
| HTTP do Servidor de Mensagens / *Lbrule8100* |81 <*InstanceNumber*> |8100 |
| HTTP do SAP para Iniciar Serviço ASCS / *Lbrule50013* |5 <*InstanceNumber*> 13 |50013 |
| HTTPS do SAP para Iniciar Serviço ASCS / *Lbrule50014* |5 <*InstanceNumber*> 14 |50014 |
| Enfileirar Replicação / *Lbrule50016* |5 <*InstanceNumber*> 16 |50016 |
| HTTP do SAP para Iniciar Serviço ERS *Lbrule51013* |5 <*InstanceNumber*> 13 |51013 |
| HTTP do SAP para Iniciar Serviço ERS *Lbrule51014* |5 <*InstanceNumber*> 14 |51014 |
| RM Win *Lbrule5985* | |5985 |
| Compartilhamento de Arquivos *Lbrule445* | |445 |

_**Tabela 1:** números de instâncias do SAP NetWeaver ABAP ASCS Olá de porta_

Em seguida, crie esses pontos de extremidade para portas do SAP NetWeaver Java SCS Olá de balanceamento de carga:

| Nome da regra do balanceamento de carga/serviço | Números de porta padrão | Portas concretas para (instância do SCS com número de instância 01) (ERS com 11) |
| --- | --- | --- |
| Enfileirar Servidor / *lbrule3201* |32 <*InstanceNumber*> |3201 |
| Servidor do Gateway / *lbrule3301* |33 <*InstanceNumber*> |3301 |
| Servidor de Mensagens Java / *lbrule3900* |39 <*InstanceNumber*> |3901 |
| HTTP do Servidor de Mensagens / *Lbrule8101* |81 <*InstanceNumber*> |8101 |
| HTTP do SAP para Iniciar Serviço SCS / *Lbrule50113* |5 <*InstanceNumber*> 13 |50113 |
| HTTPS do SAP para Iniciar Serviço SCS / *Lbrule50114* |5 <*InstanceNumber*> 14 |50114 |
| Enfileirar Replicação / *Lbrule50116* |5 <*InstanceNumber*> 16 |50116 |
| HTTP do SAP para Iniciar Serviço ERS *Lbrule51113* |5 <*InstanceNumber*> 13 |51113 |
| HTTP do SAP para Iniciar Serviço ERS *Lbrule51114* |5 <*InstanceNumber*> 14 |51114 |
| RM Win *Lbrule5985* | |5985 |
| Compartilhamento de Arquivos *Lbrule445* | |445 |

_**Tabela 2:** números de instâncias do SAP NetWeaver Java SCS Olá de porta_

![Figura 15: Regras de Balanceador de carga interno do Azure Olá de balanceamento de carga de padrão ASCS/SCS][sap-ha-guide-figure-3004]

_**Figura 15:** regras de Balanceador de carga interno do Azure Olá de balanceamento de carga de padrão ASCS/SCS_

Configurar endereço IP Olá Olá do balanceador de carga **pr1 de balanceamento de carga de dbms** toohello endereço IP do nome de host virtual Olá da instância DBMS hello.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Alterar regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do hello ASCS/SCS padrão

Se você quiser toouse diferentes números de saudação SAP ASCS ou instâncias do SCS, você deve alterar nomes de saudação e valores de suas portas de valores padrão.

1.  No portal do Azure de Olá, selecione  **<* SID*> - lb - ascs carregar balanceador * * > **regras de balanceamento de carga**.
2.  Todos os balanceamento de carga regras que pertencem a toohello SAP ASCS ou instância SCS, altere esses valores:

  * Nome
  * Porta
  * Porta de back-end

  Por exemplo, se desejar que o número de instância ASCS toochange saudação padrão de 00 too31, você precisa toomake alterações de saudação para todas as portas listadas na tabela 1.

  Veja um exemplo de uma atualização para a porta *lbrule3200*.

  ![Figura 16: Alterar regras de Balanceador de carga interno do Azure Olá de balanceamento de carga do hello ASCS/SCS padrão][sap-ha-guide-figure-3005]

  _**Figura 16:** alteração Olá ASCS/SCS padrão balanceamento de carga de regras de Balanceador de carga interno do Azure Olá_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Adicionar o domínio de toohello de máquinas virtuais do Windows

Depois de atribuir um endereço IP estático, toohello máquinas da virtual, adicione o domínio de toohello de máquinas virtuais de saudação.

![Figura 17: Adicionar um domínio de tooa de máquina virtual][sap-ha-guide-figure-3006]

_**Figura 17:** adicionar um domínio de tooa de máquina virtual_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Adicionar entradas de registro em ambos os nós de cluster da instância do SAP ASCS/SCS Olá

O balanceador de carga do Azure tem um balanceador de carga interno que fecha conexões quando conexões Olá estão ociosas por um determinado período de tempo (um tempo limite de ociosidade). Processos de trabalho do SAP na caixa de diálogo instâncias conexões abertas toohello SAP enqueue processam como Olá primeiro enfileirar/remoção da fila de solicitação necessidades toobe enviado. Essas conexões geralmente permanecem estabelecidas até que o processo de trabalho hello ou reinícios do processo de enfileiramento hello. No entanto, se a conexão de saudação ficar ocioso por um período de tempo definido, Olá interno de carga do Azure balanceador fecha Olá conexões. Isso não é um problema porque Olá processo de trabalho do SAP restabelece o processo de enfileiramento Olá conexão toohello se ele não existe mais. Essas atividades são documentadas nos rastreamentos do desenvolvedor de saudação de processos do SAP, mas criam uma grande quantidade de conteúdo extra nesses rastreamentos. Saudação de toochange uma boa ideia TCP/IP é `KeepAliveTime` e `KeepAliveInterval` em ambos os nós de cluster. Combine essas alterações nos parâmetros de TCP/IP hello com parâmetros de perfil do SAP, descritos mais adiante no artigo de saudação.

entradas de registro de tooadd em ambos os nós de cluster da instância do SAP ASCS/SCS hello, primeiro, adicionam essas entradas de registro do Windows em ambos os nós de cluster do Windows para o SAP ASCS/SCS:

| Caminho | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome da variável |`KeepAliveTime` |
| Tipo de variável |REG_DWORD (Decimal) |
| Valor |120000 |
| Link toodocumentation |[https://technet.microsoft.com/pt-BR/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabela 3:** alteração Olá primeiro TCP/IP parâmetro_

Em seguida, adicione as seguintes entradas de Registro em nós de cluster do Windows para SAP ASCS/SCS:

| Caminho | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nome da variável |`KeepAliveInterval` |
| Tipo de variável |REG_DWORD (Decimal) |
| Valor |120000 |
| Link toodocumentation |[https://technet.microsoft.com/pt-BR/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabela 4:** alteração Olá TCP/IP segundo_

**as alterações de saudação do tooapply, reinicie ambos os nós de cluster**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configurar um cluster Windows Server Failover Clustering para uma instância do SAP ASCS/SCS

Configurar um cluster do Clustering de Failover do Windows Server para uma instância do SAP ASCS/SCS envolve as seguintes tarefas:

- Coletando Olá nós de cluster em uma configuração de cluster
- Configurando a testemunha de compartilhamento de arquivos do cluster

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Coletar nós de cluster de saudação em uma configuração de cluster

1.  No Assistente de recursos e Olá Adicionar função, adicione clustering tooboth nós de cluster de failover.
2.  Configure o cluster de failover hello usando o Gerenciador de Cluster de Failover. No Gerenciador de Cluster de Failover, selecione **criar Cluster**e depois adicione apenas nome de saudação do primeiro cluster hello, nó A. Não adicione o segundo nó de saudação ainda; Você adicionará o nó de segundo Olá em uma etapa posterior.

  ![Figura 18: Adicionar o servidor de saudação ou nome de máquina virtual do primeiro nó de cluster Olá][sap-ha-guide-figure-3007]

  _**Figura 18:** adicionar Olá máquina virtual nome do servidor ou do primeiro nó de cluster Olá_

3.  Digite o nome de rede de saudação (nome de host virtual) do cluster hello.

  ![Figura 19: Insira o nome do cluster Olá][sap-ha-guide-figure-3008]

  _**Figura 19:** nome do cluster Olá Enter_

4.  Depois de criar o cluster de hello, execute um teste de validação de cluster.

  ![Figura 20: Executar a verificação de validação de cluster de saudação][sap-ha-guide-figure-3009]

  _**Figura 20:** executar verificação de validação de cluster Olá_

  Você pode ignorar os avisos sobre discos neste momento no processo de saudação. Você adicionará que uma testemunha de compartilhamento de arquivo e hello SIOS discos compartilhados mais tarde. Neste estágio, você não precisa tooworry quanto a ter um quorum.

  ![Figura 21: Nenhum disco de quorum é encontrado][sap-ha-guide-figure-3010]

  _**Figura 21:** Nenhum disco de quorum é encontrado_

  ![Figura 22: Recurso de cluster principal precisa de um novo endereço IP][sap-ha-guide-figure-3011]

  _**Figura 22:** Recurso de cluster principal precisa de um novo endereço IP_

5.  Alterar o endereço IP de Olá Olá principal do serviço de cluster. cluster de saudação não pode iniciar até que você altere o endereço IP Olá Olá principal do serviço de cluster, como endereço IP de saudação do servidor de saudação aponta tooone de nós de máquina virtual de saudação. Fazer isso em Olá **propriedades** página do recurso IP do serviço de cluster Olá core.

  Por exemplo, é preciso tooassign um endereço IP (em nosso exemplo, **10.0.0.42**) para o nome de host virtual de cluster Olá **pr1-ascs-vir**.

  ![Figura 23: Na caixa de diálogo de propriedades de hello, altere o endereço IP de saudação][sap-ha-guide-figure-3012]

  _**Figura 23:** em Olá **propriedades** caixa de diálogo, o endereço IP de saudação de alteração_

  ![Figura 24: Atribuir o endereço IP de saudação que é reservado para o cluster Olá][sap-ha-guide-figure-3013]

  _**Figura 24:** atribuir Olá endereço IP que é reservado para o cluster de saudação_

6.  Colocar o nome de host virtual de cluster Olá online.

  ![Figura 25: O serviço principal de Cluster está ativo e em execução e Olá corrija o endereço IP][sap-ha-guide-figure-3014]

  _**Figura 25:** principal serviço de Cluster está ativo e em execução e com hello corrija o endereço IP_

7.  Adicione o segundo nó de cluster hello.

  Agora que o serviço de cluster Olá principal está em execução, você pode adicionar o segundo nó de cluster hello.

  ![Figura 26: Adicionar Olá segundo nó de cluster][sap-ha-guide-figure-3015]

  _**Figura 26:** adicionar Olá segundo cluster nó_

8.  Insira um nome para o segundo host do nó de cluster hello.

  ![Figura 27: Insira o nome de host de nó de cluster segundo de saudação][sap-ha-guide-figure-3016]

  _**Figura 27:** Enter Olá cluster host nome do segundo nó_

  > [!IMPORTANT]
  > Certifique-se de que Olá **adicionar todos os armazenamento qualificado ao cluster toohello** caixa de seleção é **não** selecionado.  
  >
  >

  ![Figura 28: Não marque a caixa de seleção de saudação][sap-ha-guide-figure-3017]

  _**Figura 28:** fazer **não** selecione Olá a caixa de seleção_

  Você pode ignorar os avisos sobre quorum e discos. Você definirá Olá quorum e compartilhamento Olá disco posteriormente, conforme descrito em [instalando SIOS DataKeeper Cluster Edition para o disco de compartilhamento de cluster SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Figura 29: Ignorar os avisos sobre o quorum de disco Olá][sap-ha-guide-figure-3018]

  _**Figura 29:** ignorar os avisos sobre o quorum de disco Olá_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configurar a testemunha de compartilhamento de arquivos do cluster

Configurar a testemunha de compartilhamento de arquivos do cluster envolve as seguintes tarefas:

- Criar um compartilhamento de arquivos
- Configuração de quorum de testemunha de compartilhamento de arquivos Olá no Gerenciador de Cluster de Failover

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Criar um compartilhamento de arquivos

1.  Selecione uma testemunha de compartilhamento de arquivos em vez de um disco de quorum. O SIOS DataKeeper dá suporte a essa opção.

  Exemplos de saudação neste artigo, Olá testemunha de compartilhamento de arquivos é no servidor do Active Directory/DNS Olá que está em execução no Azure. Olá testemunha de compartilhamento de arquivo é chamada **domcontr 0**. Como seria configurou um tooAzure de conexão de VPN (por meio de VPN Site a Site ou rota expressa do Azure), DNS do Active Directory/serviço é local e não é adequado toorun um arquivo de testemunha de compartilhamento.

  > [!NOTE]
  > Se o serviço do Active Directory/DNS é executado somente no local, não configure o compartilhamento de arquivos no sistema de operacional de Active Directory/DNS Windows hello que é executado no local. A latência de rede entre os nós de cluster em execução no Azure e o Active Directory/DNS local pode ser muito grande e causar problemas de conectividade. Ser se tooconfigure Olá compartilhamento de arquivos em uma máquina virtual do Azure que está executando o nó de cluster toohello fechar.  
  >
  >

  unidade de quorum Olá precisa de pelo menos 1.024 MB de espaço livre. É recomendável 2.048 MB de espaço livre para a unidade de quorum hello.

2.  Adicione objeto de nome de cluster hello.

  ![Figura 30: Atribuir permissões de saudação no compartilhamento de saudação do objeto de nome de cluster Olá][sap-ha-guide-figure-3019]

  _**Figura 30:** atribuir permissões de saudação no compartilhamento de saudação do objeto de nome de cluster Olá_

  Certifique-se de que permissões de saudação incluem dados toochange Olá no compartilhamento de saudação do objeto de nome de cluster hello (em nosso exemplo, **pr1-ascs-vir$**).

3.  tooadd Olá cluster nome toohello lista de objetos, selecione **adicionar**. Alterar Olá filtro toocheck para objetos de computador, na inclusão toothose mostrado na Figura 31.

  ![Figura 31: Computadores de tooinclude alteração Olá tipos de objeto][sap-ha-guide-figure-3020]

  _**Figura 31:** alterar Olá tipos de objeto tooinclude computadores_

  ![A Figura 32: Marque a caixa de seleção de computadores de saudação][sap-ha-guide-figure-3021]

  _**A Figura 32:** Olá selecione **computadores** caixa de seleção_

4.  Insira um objeto de nome de cluster Olá conforme mostrado na Figura 31. Porque o registro de saudação já foi criado, você pode alterar permissões hello, conforme mostrado na Figura 30.

5.  Selecione Olá **segurança** guia de compartilhamento hello e defina mais detalhados permissões para o objeto de nome de cluster hello.

  ![Figura 33: Olá conjunto de atributos de segurança para objeto de nome de cluster Olá no quorum Olá de compartilhamento de arquivos][sap-ha-guide-figure-3022]

  _**Figura 33:** definir atributos de segurança de saudação para objeto de nome de cluster Olá no quorum Olá de compartilhamento de arquivos_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Definir o quorum de testemunha de compartilhamento de arquivos Olá no Gerenciador de Cluster de Failover

1.  Abra Olá configurar Assistente de configuração de Quorum.

  ![A Figura 34: Iniciar Olá configurar Assistente de configuração de Quorum de Cluster][sap-ha-guide-figure-3023]

  _**A Figura 34:** início Olá configurar o Assistente de configuração de Quorum do Cluster_

2.  Em Olá **Selecionar configuração de Quorum** , selecione **selecionar testemunha de quorum Olá**.

  ![Figura 35: Configurações de quorum à sua escolha][sap-ha-guide-figure-3024]

  _**Figura 35:** Configurações de quorum à sua escolha_

3.  Em Olá **selecionar testemunha de Quorum** , selecione **configurar uma testemunha de compartilhamento de arquivos**.

  ![A Figura 36: Olá selecione Compartilhamento de arquivos][sap-ha-guide-figure-3025]

  _**A Figura 36:** selecionar testemunha de compartilhamento de arquivo hello_

4.  Digite o compartilhamento de arquivos toohello do caminho UNC hello (em nosso exemplo, \\domcontr 0\FSW). toosee uma lista de alterações de saudação pode fazer, selecione **próximo**.

  ![A Figura 37: Definir o local de compartilhamento de arquivo hello para compartilhamento de testemunha Olá][sap-ha-guide-figure-3026]

  _**A Figura 37:** definir o local de compartilhamento de arquivo hello para compartilhamento de testemunha Olá_

5.  Selecione as alterações de saudação desejado e, em seguida, selecione **próximo**. Você precisa toosuccessfully reconfigurar a configuração de cluster Olá conforme mostrado na Figura 38.  

  ![A Figura 38: Confirmação que você tenha reconfigurado cluster Olá][sap-ha-guide-figure-3027]

  _**A Figura 38:** confirmação que você tenha reconfigurado cluster Olá_

Depois de instalar com êxito Olá Cluster de Failover do Windows, as alterações devem toobe feita toosome limites tooadapt failover detecção tooconditions no Azure. Olá toobe parâmetros alterado são documentados neste blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Supondo que seu duas VMs que criar hello configuração de Cluster do Windows para ASCS/SCS estão em Olá mesma sub-rede, parâmetros a seguir hello necessário toobe alterado toothese valores:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Essas configurações foram testadas com clientes e fornecidas um toobe comprometimento bom flexível o suficiente no lado de uma saudação. Em Olá outro lado essas configurações foram fornecendo rápido suficiente failover em condições de erro real em falha de software ou nó de VM do SAP. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar o SIOS DataKeeper Cluster Edition para o disco de compartilhamento de cluster de SAP ASCS/SCS Olá

Agora você tem uma configuração do Clustering de Failover do Windows Server em funcionamento no Azure. Mas, tooinstall uma instância SAP ASCS/SCS, você precisa de um recurso de disco compartilhado. Você não pode criar recursos de disco Olá compartilhado que é necessário no Azure. SIOS DataKeeper Cluster Edition é uma solução de terceiros que você pode usar os recursos de disco toocreate compartilhado.

Disco de compartilhamento de cluster instalando SIOS DataKeeper Cluster Edition para Olá SAP ASCS/SCS envolve as seguintes tarefas:

- Adição de saudação do .NET Framework 3.5
- Instalando o SIOS DataKeeper
- Configurar o SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Adicionar saudação do .NET Framework 3.5
saudação do Microsoft .NET Framework 3.5 não é automaticamente ativada ou instalada no Windows Server 2012 R2. Como SIOS DataKeeper requer saudação do .NET Framework toobe em todos os nós que você instalar DataKeeper no, você deve instalar saudação do .NET Framework 3.5 no sistema de operacional convidado saudação de todas as máquinas virtuais em cluster hello.

Há Olá tooadd de duas maneiras do .NET Framework 3.5:

- Use Olá assistente Adicionar funções e recursos no Windows, conforme mostrado na figura 39.

  ![Figura 39: Instalar saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos][sap-ha-guide-figure-3028]

  _**Figura 39:** Olá de instalação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos_

  ![Figura 40: Progresso da instalação barra quando você instala a saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos][sap-ha-guide-figure-3029]

  _**A figura 40:** barra quando você instala a saudação do .NET Framework 3.5 usando Olá assistente Adicionar funções e recursos de progresso de instalação_

- Use Olá ferramenta de linha de comando dism.exe. Para este tipo de instalação, você precisa SxS diretório Olá tooaccess Olá mídia de instalação do Windows. Em um prompt de comandos com privilégios elevados, digite:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalar SIOS DataKeeper

Instale o SIOS DataKeeper Cluster Edition em cada nó no cluster hello. toocreate o armazenamento compartilhado virtual com SIOS DataKeeper, criar um espelho sincronizado e, em seguida, simule o armazenamento compartilhado de cluster.

Antes de instalar o software SIOS hello, crie o usuário de domínio de saudação **DataKeeperSvc**.

> [!NOTE]
> Adicionar Olá **DataKeeperSvc** usuário toohello **Administrador Local** grupo em ambos os nós de cluster.
>
>

tooinstall SIOS DataKeeper:

1.  Instale o software SIOS Olá em ambos os nós de cluster.

  ![Instalador do SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: Primeira página do hello SIOS DataKeeper instalação][sap-ha-guide-figure-3031]

  _**Figura 41:** primeira página do hello SIOS DataKeeper instalação_

2.  Na caixa de diálogo Olá mostrada na figura 42, selecione **Sim**.

  ![Figura 42: O DataKeeper informa a você que um serviço será desabilitado][sap-ha-guide-figure-3032]

  _**Figura 42:** O DataKeeper informa a você que um serviço será desabilitado_

3.  Na caixa de diálogo Olá mostrada na figura 43, recomendamos que você selecione **conta de domínio ou servidor**.

  ![Figura 43: Seleção do usuário para o SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Figura 43:** Seleção do usuário para o SIOS DataKeeper_

4.  Insira o nome de usuário da conta de domínio hello e senhas que você criou para SIOS DataKeeper.

  ![Figura 44: Insira Olá nome de usuário de domínio e senha para Olá SIOS DataKeeper instalação][sap-ha-guide-figure-3034]

  _**Figura 44:** digite Olá nome de usuário de domínio e senha para Olá SIOS DataKeeper instalação_

5.  Instale a chave de licença de saudação para sua instância SIOS DataKeeper, conforme mostrado na figura 45.

  ![Figura 45: insira a chave da licença do SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Figura 45:** insira a chave da licença do SIOS DataKeeper_

6.  Quando solicitado, reinicie a máquina virtual de saudação.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configurar SIOS DataKeeper

Depois de instalar o SIOS DataKeeper em ambos os nós, você precisa de configuração de saudação de toostart. meta de saudação da configuração de saudação é toohave a replicação síncrona de dados entre discos adicionais Olá anexado tooeach de máquinas virtuais de saudação.

1.  Iniciar hello DataKeeper gerenciamento e a ferramenta de configuração e, em seguida, selecione **conectar servidor**. (Na Figura 46, essa opção é marcada em vermelho.)

  ![Figura 46: Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper][sap-ha-guide-figure-3036]

  _**Figura 46:** Ferramenta de Gerenciamento e Configuração do SIOS DataKeeper_

2.  Insira o nome da saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação.

  ![Figura 47: Inserir nome de saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação][sap-ha-guide-figure-3037]

  _**Figura 47:** Inserir nome de saudação ou endereço TCP/IP hello primeiro nó Olá gerenciamento e configuração da ferramenta de deve se conectar a e, em uma segunda etapa, o segundo nó de saudação_

3.  Crie trabalho de replicação de saudação entre dois nós de saudação.

  ![Figura 48: Criar trabalho de replicação][sap-ha-guide-figure-3038]

  _**Figura 48:** Criar trabalho de replicação_

  Um assistente orienta você pelo processo de saudação de criação de um trabalho de replicação.
4.  Defina nome hello, endereço TCP/IP e o volume de disco do nó de origem hello.

  ![Figura 49: Definir nome de saudação do trabalho de replicação de saudação][sap-ha-guide-figure-3039]

  _**Figura 49:** definir nome de saudação do trabalho de replicação Olá_

  ![Figura 50: Definir dados base de saudação do nó de hello, que deve ser um nó de origem atual Olá][sap-ha-guide-figure-3040]

  _**Figura 50:** definir Olá dados base nó hello, que deve ser um nó de origem atual Olá_

5.  Defina nome hello, endereço TCP/IP e volume de disco do nó de destino de saudação.

  ![Figura 51: Definir Olá dados base nó hello, que deve ser um nó de destino atual Olá][sap-ha-guide-figure-3041]

  _**Figura 51:** definir Olá dados base nó hello, que deve ser um nó de destino atual Olá_

6.  Defina os algoritmos de compactação de saudação. Em nosso exemplo, é recomendável que você compactar o fluxo de replicação de saudação. Especialmente em situações de ressincronização, compactação de saudação do fluxo de replicação Olá reduz drasticamente o tempo de ressincronização. Observe que a compactação utiliza recursos de CPU e RAM de saudação de uma máquina virtual. À medida que aumenta a taxa de compactação hello, portanto Olá volume de recursos de CPU usados. Você também pode ajustar essa configuração mais tarde.

7.  Outra configuração necessário toocheck é se replicação Olá ocorre de forma assíncrona ou síncrona. *Quando você protege configurações SAP ASCS/SCS, deve usar a replicação síncrona*.  

  ![Figura 52: Definir detalhes de replicação][sap-ha-guide-figure-3042]

  _**Figura 52:** Definir detalhes de replicação_

8.  Defina se o volume de saudação que é replicada pelo trabalho de replicação de saudação deve ser configuração de cluster Clustering de Failover do Windows Server tooa representado como um disco compartilhado. Para a configuração do SAP ASCS/SCS hello, selecione **Sim** para que o Windows hello cluster vê Olá volume replicado como um disco compartilhado que possa ser usada como um volume de cluster.

  ![Figura 53: Selecione Sim tooset Olá replicadas volume como um volume de cluster][sap-ha-guide-figure-3043]

  _**Figura 53:** selecione **Sim** tooset Olá replicadas volume como um cluster_

  Depois de criar o volume de Olá, ferramenta de configuração e gerenciamento de DataKeeper Olá mostra que esse trabalho de replicação hello está ativo.

  ![Figura 54: Espelhamento síncrono DataKeeper para Olá SAP ASCS/SCS compartilhamento de disco está ativo][sap-ha-guide-figure-3044]

  _**Figura 54:** espelhamento síncrono DataKeeper para hello SAP ASCS/SCS de compartilhamento de disco está ativo_

  Gerenciador de Cluster de failover agora mostra o disco hello como um disco DataKeeper, conforme mostrado na Figura 55.

  ![Figura 55: O Gerenciador de Cluster de Failover mostra disco Olá DataKeeper replicado][sap-ha-guide-figure-3045]

  _**Figura 55:** Gerenciador de Cluster de Failover que DataKeeper replicada de disco Olá mostra_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar o sistema do SAP NetWeaver Olá

Não descrevemos a instalação DBMS hello como as configurações variam dependendo Olá sistema DBMS usado. No entanto, vamos supor que as questões de alta disponibilidade com hello DBMS sejam resolvidos com funcionalidades Olá Olá diferentes DBMS fornecedores oferecem suporte a para o Azure. Por exemplo, o Always On ou o Espelhamento de Banco de Dados para SQL Server e Oracle Data Guard para bancos de dados Oracle. No cenário de saudação que usamos neste artigo, não adicionamos mais proteção toohello DBMS.

Não existem considerações especiais quando diferentes serviços DBMS interagem com esse tipo de configuração de SAP ASCS/SCS clusterizada no Azure.

> [!NOTE]
> procedimentos de instalação de saudação de sistemas SAP NetWeaver ABAP, sistemas de Java e sistemas ABAP + Java são quase idênticos. diferença de Hello mais significativa é que um sistema SAP ABAP tem uma instância do ASCS. Olá sistema SAP Java tem uma instância SCS. Olá sistema SAP ABAP + Java tem uma instância do ASCS e Olá de uma instância SCS em execução no mesmo grupo de cluster de failover de Microsoft. As diferenças de instalação para cada pilha de instalação do SAP NetWeaver serão explicitamente mencionadas. Você pode presumir que todas as outras partes são Olá mesmo.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade

> [!IMPORTANT]
> Verifique se não tooplace sua página de arquivo no DataKeeper espelhado volumes. O DataKeeper não dá suporte a volumes espelhados. Você pode deixar o arquivo de página na unidade temporária Olá D de uma máquina virtual do Azure, que é o padrão de saudação. Se ele não estiver lá, mova Olá Windows página arquivo toodrive d: de sua máquina virtual do Azure.
>
>

Instalar o SAP com uma instância ASCS/SCS de alta disponibilidade envolve as seguintes tarefas:

- Criando um nome de host virtual para instância do SAP ASCS/SCS Olá clusterizado
- Instalando Olá SAP primeiro nó de cluster
- Modificando Olá SAP perfil da instância do ASCS/SCS Olá
- Adicionando uma porta de investigação
- Abrir a porta de investigação Olá Windows firewall

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Criar um nome de host virtual para instância do SAP ASCS/SCS Olá clusterizado

1.  No Gerenciador de DNS do Windows hello, crie uma entrada DNS para o nome de host virtual Olá da instância do ASCS/SCS hello.

  > [!IMPORTANT]
  > Olá endereço IP que você atribuir o nome de host virtual toohello de saudação ASCS/SCS instância deve ser Olá mesmo como endereço IP de saudação que você atribuiu tooAzure balanceador de carga (**<*SID*> - lb - ascs **).  
  >
  >

  Olá o endereço IP do nome de host do SAP ASCS/SCS virtual hello (**pr1-ascs-sap**) Olá mesmo como endereço IP de saudação do balanceador de carga do Azure (**pr1 de balanceamento de carga de ascs**).

  ![Figura 56: Definir a entrada DNS Olá para o nome virtual do cluster Olá SAP ASCS/SCS e endereço TCP/IP][sap-ha-guide-figure-3046]

  _**Figura 56:** definir Olá entrada DNS para o nome virtual do cluster Olá SAP ASCS/SCS e endereço TCP/IP_

2.  toodefine Olá IP endereço atribuído toohello nome de host virtual, selecione **Gerenciador DNS** > **domínio**.

  ![Figura 57: Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Figura 57:** Novo nome virtual e endereço TCP/IP para a configuração de cluster do SAP ASCS/SCS_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar Olá SAP primeiro nó de cluster

1.  Executar Olá primeiro cluster nó opção no nó de cluster A. Por exemplo, em Olá **pr1-ascs-0** host.
2.  portas de padrão de saudação tookeep para hello Azure interno balanceador de carga, selecione:

  * **Sistema ABAP**: número da instância **ASCS** **00**
  * **Sistema Java**: número da instância **SCS** **01**
  * **Sistema ABAP + Java**: número da instância **ASCS** **00** e número da instância **SCS** **01**

  toouse instância números diferente de 00 para Olá ABAP ASCS instância e 01 para instância de Java SCS hello, primeiro é necessário toochange Olá interno de carga do Azure balanceador padrão de balanceamento de carga regras, descritas na [carga do alteração Olá ASCS/SCS padrão balanceamento de regras de Balanceador de carga interno do Azure Olá][sap-ha-guide-8.9].

Olá Avançar algumas tarefas não são descritas na documentação de instalação do SAP padrão hello.

> [!NOTE]
> Olá documentação de instalação do SAP descreve como tooinstall Olá primeiro nó do cluster ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar Olá SAP perfil da instância do ASCS/SCS Olá

É necessário tooadd um novo parâmetro de perfil. parâmetro de perfil Hello impede que conexões entre os processos de trabalho do SAP e o servidor de enfileiramento de saudação fechar quando eles estão ociosos por muito tempo. Mencionamos cenário problema Olá [adicionar entradas de registro em ambos os nós de cluster da instância do SAP ASCS/SCS Olá][sap-ha-guide-8.11]. Essa seção também apresentamos dois parâmetros de conexão de TCP/IP básicos do alterações toosome. Na segunda etapa, você precisa tooset Olá enqueue servidor toosend um `keep_alive` sinalizar para que conexões Olá não atingem o limite de ociosidade do balanceador de carga interno do Azure hello.

Olá toomodify perfil SAP da instância do ASCS/SCS hello:

1.  Adicione este parâmetro de perfil toohello perfil de instância SAP ASCS/SCS:

  ```
  enque/encni/set_so_keepalive = true
  ```
  Em nosso exemplo, o caminho de saudação é:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Por exemplo, o perfil de instância SAP SCS toohello e caminho correspondente:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  alterações de saudação tooapply, reinicie a instância de SAP ASCS /SCS de saudação.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Adicionar uma porta de investigação

Use o trabalho de configuração do balanceador de carga interno Olá investigação funcionalidade toomake Olá todo o cluster com o balanceador de carga do Azure. Balanceador de carga interno do Azure Olá geralmente distribui a carga de trabalho de entrada de saudação igualmente entre as máquinas virtuais participantes. No entanto, isso não funcionará em algumas configurações de cluster porque apenas uma instância está ativa. Olá outra instância é passiva e não pode aceitar qualquer carga de trabalho de saudação. Uma funcionalidade de teste ajuda quando atribui de Balanceador de carga interno do Azure Olá trabalha instância ativa do tooan somente. Com a funcionalidade de investigação hello, balanceador de carga interno Olá pode detectar quais instâncias ativas e direcionar apenas a instância Olá com carga de trabalho de saudação.

tooadd uma porta de investigação:

1.  Seleção atual de saudação **ProbePort** configuração executando Olá comando PowerShell a seguir. Executá-lo de dentro de uma das máquinas virtuais de saudação na configuração de cluster de saudação.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Defina uma porta de investigação. número de porta de investigação de padrão de saudação é **0**. Em nosso exemplo, usamos a porta de investigação **62000**.

  ![Figura 58: a porta de investigação de configuração de cluster de saudação é 0 por padrão][sap-ha-guide-figure-3048]

  _**Figura 58:** porta de investigação de configuração de cluster do saudação padrão é 0_

  número de porta de saudação é definido em modelos do SAP do Azure Resource Manager. Você pode atribuir o número da porta Olá no PowerShell.

  tooset um novo valor de ProbePort para Olá  **SAP <*SID*> IP * * recurso de cluster, execute Olá script do PowerShell a seguir. Atualize as variáveis do PowerShell de saudação para seu ambiente. Após a execução do script hello, será solicitada toorestart Olá SAP grupo tooactivate Olá as alterações de cluster.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Depois de você colocar Olá  **SAP <*SID*> * * função online de cluster, verifique **ProbePort** é definir o novo valor de toohello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Porta de cluster de saudação de investigação depois de definir o novo valor de saudação][sap-ha-guide-figure-3049]

  _**Figura 59:** investigação de porta de cluster Olá depois de definir o novo valor de saudação_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra a porta de investigação Olá Windows firewall

É necessário tooopen uma porta de investigação de firewall do Windows em ambos os nós de cluster. Use Olá script tooopen uma porta de investigação de firewall do Windows a seguir. Atualize as variáveis do PowerShell de saudação para seu ambiente.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Olá **ProbePort** está definido muito**62000**. Agora você pode acessar o compartilhamento de arquivo hello  **\\\ascsha-clsap\sapmnt** de outros hosts, como **ascsha dbas**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar a instância de banco de dados de saudação

o banco de dados do tooinstall Olá instância, siga o processo de saudação descrito Olá documentação de instalação do SAP.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar o segundo nó de cluster Olá

tooinstall Olá segundo cluster, siga etapas Olá Olá guia de instalação do SAP.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Alterar tipo de inicialização de saudação da instância de serviço do Windows de ES do SAP Olá

Alterar o tipo de inicialização de saudação do hello serviço Windows de ES do SAP muito**automática (início atrasado)** em ambos os nós de cluster.

![Figura 60: Alterar o tipo de serviço de saudação para Olá SAP es instância toodelayed automática][sap-ha-guide-figure-3050]

_**Figura 60:** alterar tipo de serviço Olá para Olá SAP es instância toodelayed automática_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Olá principal servidor de aplicativos SAP

Instalar a instância de servidor de aplicativo principal (PAS) hello <*SID*> - di - 0 na máquina virtual Olá que você designou toohost Olá PAS. Não há dependências nas configurações específicas do Azure ou do DataKeeper.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Olá adicional servidor de aplicativos SAP

Instale um servidor de aplicativo adicionais SAP (AAS) em todas as máquinas virtuais de saudação que você designou toohost uma instância de servidor de aplicativos SAP. Por exemplo, em <*SID*> - di - 1 muito <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Isso conclui a instalação de saudação de um sistema SAP NetWeaver de alta disponibilidade. Em seguida, continue com o teste de failover.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Testar o failover de instância SAP ASCS/SCS hello e replicação SIOS
É fácil tootest e monitorar um failover de instância SAP ASCS/SCS e replicação de disco SIOS usando o Gerenciador de Cluster de Failover e ferramenta de saudação SIOS DataKeeper gerenciamento e configuração.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> A instância do SAP ASCS/SCS está em execução no Nó A do Cluster

Olá **PR1 SAP** grupo de cluster está em execução no nó de cluster A. Por exemplo, em **pr1-ascs-0**. Atribuir a unidade de disco de saudação compartilhada S, que faz parte da saudação **PR1 SAP** cluster grupo e a instância do ASCS/SCS Olá usa, toocluster nó A.

![Figura 61: Gerenciador de Cluster de Failover: grupo de clusters do SAP < SID > Olá está em execução em um nó de cluster][sap-ha-guide-figure-5000]

_**Figura 61:** Gerenciador de Cluster de Failover: Olá SAP <*SID*> grupo de cluster está em execução em um nó de cluster_

Olá SIOS DataKeeper gerenciamento e a ferramenta de configuração, você pode ver esse disco compartilhado Olá dados são replicados sincronicamente de unidade de volume de origem Olá S no nó de cluster de uma unidade de volume de destino S toohello no nó de cluster B. Por exemplo, ele é replicado do **pr1-ascs-0 [10.0.0.40]** muito**pr1-ascs-1 [10.0.0.41]**.

![Figura 62: Na SIOS DataKeeper replicar volume local saudação do nó de cluster de um nó de toocluster B][sap-ha-guide-figure-5001]

_**Figura 62:** na SIOS DataKeeper replicar o volume de local de saudação do nó de cluster de um nó de toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Failover de nó A toonode B

1.  Escolha um dos tooinitiate opções um failover de saudação SAP <*SID*> grupo de cluster de nó do cluster nó A toocluster b:
  - Usar o Gerenciador de Cluster de Failover  
  - Usar o PowerShell de Cluster de Failover

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Reinicie o nó de cluster A no sistema de operacional de convidado do Windows hello (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).  
3.  Reinicie o nó de cluster A partir Olá portal do Azure (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).  
4.  Reiniciar um do nó de cluster usando o PowerShell do Azure (Isso inicia um failover automático de saudação SAP <*SID*> grupo de cluster do nó A toonode B).

  Após o failover, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B. Por exemplo, ele está em execução no **pr1-ascs-1**.

  ![Figura 63: No Gerenciador de Cluster de Failover, grupo de clusters do SAP < SID > Olá está em execução no nó de cluster B][sap-ha-guide-figure-5002]

  _**Figura 63**: no Gerenciador de Cluster de Failover, Olá SAP <*SID*> grupo de cluster está em execução no nó de cluster B_

  Olá disco compartilhado é agora montado no cluster de nó B. SIOS DataKeeper é replicar dados de unidade de volume de origem S em cluster no nó B tootarget volume unidade S no nó de cluster A. Por exemplo, ele está replicando de **pr1-ascs-1 [10.0.0.41]** muito**pr1-ascs-0 [10.0.0.40]**.

  ![Figura 64: SIOS DataKeeper replica volume local Olá nó B toocluster do nó de cluster A][sap-ha-guide-figure-5003]

  _**Figura 64:** SIOS DataKeeper replica volume local Olá no nó do cluster no nó B toocluster um_
