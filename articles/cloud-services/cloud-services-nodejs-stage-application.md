---
title: "aaaStage uma implantação de serviço de nuvem (Node. js) | Microsoft Docs"
description: "Saiba como toodeploy tooa seu aplicativo do Azure que ambiente de preparo, em seguida, implantar o ambiente de produção tooa usando a troca de IP Virtual (VIP)."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Preparando um aplicativo no Azure
Um aplicativo empacotado pode ser implantado toohello preparo ambiente no Azure toobe testado antes de movê-lo toohello produção ambiente no qual Olá aplicativo está acessível na saudação da Internet. O ambiente de preparo é exatamente como o ambiente de produção de hello, exceto que você pode apenas Olá acesso preparado o aplicativo com uma URL ofuscado que é gerado pelo Azure. Após ter verificado que seu aplicativo está funcionando corretamente, pode ser implantado toohello ambiente de produção, executando uma permuta de VIP (IP Virtual).

> [!NOTE]
> Olá etapas neste artigo se aplicam somente aplicativos toonode hospedados como um serviço de nuvem do Azure.
> 
> 

## <a name="step-1-stage-an-application"></a>Etapa 1: Preparar um aplicativo
Essa tarefa aborda como um aplicativo por meio de toostage Olá **Microsoft Azure PowerShell**.

1. Ao publicar um serviço, basta passar Olá **-Slot** parâmetro à saudação **AzureServiceProject publicar** cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Faça logon no toohello [portal clássico do Azure] e selecione **serviços de nuvem**. Após o serviço de nuvem Olá é criado e Olá **preparo** status de coluna tiver sido atualizado muito**executando**, clique no nome do serviço de saudação.
   
   ![portal exibindo um serviço em execução][cloud-service]
3. Selecione Olá **painel**e, em seguida, selecione **preparo**.
   
   ![painel de serviço de nuvem][cloud-service-dashboard]
4. Observe o valor Olá Olá **URL do Site** direita de toohello de entrada. nome DNS de saudação é um identificador interno ofuscado Azure gerado.
   
    ![URL do Site][cloud-service-staging-url]

Agora você pode verificar se o aplicativo hello está funcionando corretamente no ambiente de preparo usando a URL do site de preparo de saudação do hello.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>Etapa 2: Atualizar um aplicativo em produção permutando VIPs
Após ter verificado Olá a versão atualizada de um aplicativo no ambiente de preparo, você pode torná-lo disponível em produção, trocando Olá IPs virtuais (VIPs) de ambientes de preparo e produção de hello.

> [!NOTE]
> Esta etapa pressupõe que você já ter implantado um aplicativo tooproduction e preparado Olá a versão atualizada do aplicativo.
> 
> 

1. Faça logon no hello [portal clássico do Azure], clique em **serviços de nuvem** e, em seguida, selecione o nome do serviço de saudação.
2. De saudação **painel**, selecione **preparo**e, em seguida, clique em **trocar** final Olá Olá página. Olá permuta de VIP de caixa de diálogo é aberta.
   
   ![caixa de diálogo permuta de vip][vip-swap-dialog]
3. Revise as informações de saudação e, em seguida, clique em **Okey**. duas implantações do Hello começam a atualização como Olá implantação comutadores tooproduction e hello produção implantação comutadores toostaging de preparo.

Ter uma implantação de teste e atualizado de uma implantação de produção por permuta de VIPs com a implantação de saudação em preparação com êxito.

## <a name="additional-resources"></a>Recursos adicionais
* [Como tooDeploy uma tooProduction de atualização de serviço por VIPs de permuta no Azure]

[Portal clássico do Azure]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Como tooDeploy uma tooProduction de atualização de serviço por VIPs de permuta no Azure]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
