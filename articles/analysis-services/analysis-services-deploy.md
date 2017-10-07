---
title: aaaDeploy tooAzure Analysis Services usando o SSDT | Microsoft Docs
description: Saiba como toodeploy tooan um modelo de tabela do Azure Analysis Services server usando o SSDT.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Implantar um modelo a partir do SSDT
Depois de criar um servidor na sua assinatura do Azure, você está pronto toodeploy um tooit de banco de dados de modelo de tabela. Você pode usar o SQL Server Data Tools (SSDT) toobuild e implantar um projeto de modelo de tabela que você está trabalhando. 

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado, você precisa:

* **Servidor do Analysis Services** no Azure. mais, consulte toolearn [criar um servidor do Azure Analysis Services](analysis-services-create-server.md).
* **Projeto de modelo tabular** no SSDT ou um modelo tabular existente em Olá 1200 ou maior nível de compatibilidade. Nunca criou um? Tente Olá [tutorial de modelagem de tabela de vendas do Adventure Works Internet](https://msdn.microsoft.com/library/hh231691.aspx).
* **Gateway local** -se uma ou mais fontes de dados local na rede da sua organização, você precisa tooinstall um [gateway de dados no local](analysis-services-gateway.md). gateway de saudação é necessário para o servidor na nuvem Olá conectar tooyour local fontes tooprocess e a atualização de dados no modelo de saudação.

> [!TIP]
> Antes de implantar, verifique se que você pode processar dados saudação nas tabelas. No SSDT, clique em **Modelo** > **Processo** > **Processar Tudo**. Se houver falha no processamento, você não poderá implantar com êxito.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy um modelo de tabela do SSDT

1. Antes de implantar, é necessário o nome do servidor de saudação tooget. Em **portal do Azure** > servidor > **visão geral** > **nome do servidor**, nome do servidor de saudação de cópia.
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. No SSDT > **Solution Explorer**, projeto de saudação do botão direito do mouse > **propriedades**. Em seguida, em **implantação** > **Server** colar o nome do servidor de saudação.   
   
    ![Colar o nome do servidor na propriedade do servidor de implantação](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Propriedades** e clique em **Implantar**. Você pode ser solicitado toosign em tooAzure.
   
    ![Implantar tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Status da implantação é exibida na janela Saída hello e na implantação.
   
    ![Status da Implantação](./media/analysis-services-deploy/aas-deploy-status.png)

Isso é tudo que há tooit!


## <a name="troubleshooting"></a>Solucionar problemas
Se a implantação falhar durante a implantação de metadados, é provável porque SSDT não foi possível conectar o servidor tooyour. Verifique se que você pode conectar o servidor tooyour usando o SSMS. Em seguida, certifique-se de Olá propriedade de servidor de implantação de projeto hello está correto.

Se a implantação falhar em uma tabela, é provável porque o servidor não pôde se conectar à fonte de dados tooa. Se sua fonte de dados é o local na rede da sua organização, ser tooinstall se um [gateway de dados no local](analysis-services-gateway.md).

## <a name="next-steps"></a>Próximas etapas
Agora que você tem o servidor de tooyour implantado do modelo de tabela, você está pronto tooconnect tooit. Você pode [conectar tooit com SSMS](analysis-services-manage.md) toomanage-lo. E, você pode [tooit usando uma ferramenta de cliente de conectar](analysis-services-connect.md) como o Power BI, o Power BI Desktop, ou o Excel e começar a criar relatórios.

