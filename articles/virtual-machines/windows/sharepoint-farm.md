---
title: aaaCreate farms de servidores do SharePoint no Azure | Microsoft Docs
description: "Crie rapidamente um novo farm do SharePoint 2013 ou SharePoint 2016 no Azure usando Olá marketplace portal do Azure."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a>Criar farms de servidores do SharePoint usando Olá marketplace portal do Azure

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a>Farms do SharePoint 2013
Com a saudação Microsoft Azure portal do marketplace, você pode criar rapidamente farms do SharePoint Server 2013 pré-configurado. Isso pode economizar muito tempo quando você precisar de um farm do SharePoint básico ou de alta disponibilidade para um ambiente de desenvolvimento/teste, ou se estiver avaliando o SharePoint Server 2013 como uma solução de colaboração para a sua organização.

> [!NOTE]
> Olá **Farm do SharePoint Server** item hello Azure Marketplace de saudação portal do Azure foi removido. Ela foi substituída por hello **Farm do SharePoint 2013 não - HA** e **Farm do SharePoint 2013 HA** itens.
>
>

farm do SharePoint básico de saudação consiste em três máquinas virtuais nesta configuração.

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

É possível usar esta configuração de farm para uma configuração simplificada para o desenvolvimento do aplicativo SharePoint na sua primeira avaliação do SharePoint 2013.

toocreate Olá básica () do SharePoint farm de três servidores:

1. Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).
2. Clique em **Implantar**.
3. Em Olá **Farm do SharePoint 2013 não - HA** painel, clique em **criar**.
4. Especificar as configurações em etapas Olá Olá **criar Farm do SharePoint 2013 não - HA** painel e clique **criar**.

farm do SharePoint de alta disponibilidade Olá consiste em nove máquinas virtuais nesta configuração.

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

Você pode usar este farm configuração tootest cargas mais elevadas de cliente, a alta disponibilidade do site do SharePoint externo de saudação e grupos de disponibilidade do AlwaysOn do SQL Server para um farm do SharePoint. Também é possível usar esta configuração para a implementação do aplicativo SharePoint em um ambiente de alta disponibilidade.

farm de toocreate Olá alta disponibilidade (servidor de nove) do SharePoint:

1. Clique [aqui](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).
2. Clique em **Implantar**.
3. Em Olá **Farm do SharePoint 2013 HA** painel, clique em **criar**.
4. Especificar as configurações em etapas Olá sete Olá **criar Farm do SharePoint 2013 HA** painel e clique **criar**.

> [!NOTE]
> Não é possível criar hello **Farm do SharePoint 2013 não - HA** ou **Farm do SharePoint 2013 HA** com uma avaliação gratuita do Azure.
>
>

Olá portal do Azure cria ambos esses farms de servidores em uma rede virtual somente em nuvem com uma presença da web para a Internet. Não há nenhum site a site VPN ou rota expressa conexão back tooyour rede da organização.

> [!NOTE]
> Quando você cria Olá básica ou farms do SharePoint de alta disponibilidade usando Olá portal do Azure, você não pode especificar um grupo de recursos existente. toowork com essa limitação, crie esses farms de servidores com o Azure PowerShell. Para obter mais informações, consulte [Criar farms de desenvolvimento/teste do SharePoint 2013 com o Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).
>
>

## <a name="sharepoint-2016-farms"></a>Farms do SharePoint 2016
Consulte [neste artigo](https://technet.microsoft.com/library/mt723354.aspx) para Olá Olá de toobuild de instruções a seguir de servidor único do SharePoint Server 2016 do farm.

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a>Gerenciando farms do SharePoint Olá
Você pode administrar servidores Olá esses farms através de conexões de área de trabalho remota. Para obter mais informações, consulte [fazer logon na máquina virtual de toohello](quick-create-portal.md#connect-to-virtual-machine).

No site do SharePoint de Administração Central hello, você pode configurar meus sites, aplicativos do SharePoint e outras funcionalidades. Para saber mais, confira [Configurar o SharePoint](http://technet.microsoft.com/library/ee836142.aspx).

## <a name="next-steps"></a>Próximas etapas
* Descubra as [configurações do SharePoint](https://technet.microsoft.com/library/dn635309.aspx) adicionais nos serviços de infraestrutura do Azure.
