---
title: aaaCreate um servidor do Analysis Services no Azure | Microsoft Docs
description: "Saiba como toocreate um servidor do Analysis Services da instância no Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Criar um servidor do Azure Analysis Services no portal do Azure
Este artigo orienta você pela criação de um recurso de servidor do Analysis Services em sua assinatura do Azure.

## <a name="before-you-begin"></a>Antes de começar
toocomplete este guia de início rápido, você precisa:

* **Assinatura do Azure**: visite [avaliação gratuita do Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate uma conta.
* **Azure Active Directory**: sua assinatura deve estar associada a um locatário do Azure Active Directory. E, então, você precisa toobe tooAzure conectado com uma conta em que o Active Directory do Azure. Não há suporte para contas da Microsoft. mais, consulte toolearn [permissões de usuário e autenticação](analysis-services-manage-users.md).
* **Grupo de recursos**: use um grupo de recursos que você já tem ou [crie um novo](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> Criar um servidor pode resultar em um novo serviço faturável. mais, consulte toolearn [preços do Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate um servidor no portal do Azure
1. Entrar toohello [portal do Azure](https://portal.azure.com).  
2. Clique em **+ Novo** > **Dados + Análise** > **Analysis Services**.
3. Em Olá **Analysis Services** folha, preencha os campos de saudação necessárias e, em seguida, pressione **criar**.
   
    ![Criar servidor](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **Nome do servidor**: digite um servidor de saudação tooreference nome exclusivo usado.
   * **Assinatura**: selecione Olá assinatura neste servidor cobra para.
   * **Grupo de recursos**: esses contêineres são projetado toohelp você gerenciar uma coleção de recursos do Azure. mais, consulte toolearn [grupos de recursos](../azure-resource-manager/resource-group-overview.md).
   * **Local**: Olá de hosts de local do datacenter do Azure neste servidor. Escolha um local mais próximo da sua maior base de usuários.
   * **Tipo de preço**: selecione um tipo de preço. Há suporte para modelos de tabela para cima too400 GB. mais, consulte toolearn [preços do Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).
4. Clique em **Criar**.

Normalmente, a criação demora menos de um minuto; com frequência, apenas alguns segundos. Se você selecionou **adicionar tooPortal**, navegar toosee portal tooyour o novo servidor. Ou, navegue muito**mais serviços** > **Analysis Services** toosee se seu servidor está pronto.

 ![Painel](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>Próximas etapas
Depois de criar seu servidor, você pode [implantar um modelo](analysis-services-deploy.md) tooit usando SSDT ou com o SSMS.

Se um modelo que você implantar o servidor tooyour se conecta a fontes de dados tooon locais, você precisa tooinstall um [gateway de dados no local](analysis-services-gateway.md) em um computador em sua rede.

