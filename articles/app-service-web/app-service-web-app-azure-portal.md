---
title: "aaaReference para navegação Olá portal do Azure"
description: "Saiba mais sobre o hello experiências de usuário diferente para Web do serviço de aplicativo entre o portal de gerenciamento hello e hello Portal do Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Referência de navegação Olá portal do Azure
Os Sites da Web do Azure agora são chamados de [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714). Estamos atualizando todos tooreflect nossa documentação instruções de alteração e tooprovide esse nome para Olá Portal do Azure. Até que esse processo for concluído, você pode usar este documento como um guia para trabalhar com aplicativos Web no hello portal do Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>Olá futuro da saudação Portal clássico do Azure
Enquanto você observará Olá marca alterações em Olá Portal clássico do Azure, portal está no processo de saudação do que está sendo substituído por Olá Portal do Azure. Como o portal clássico do hello está sendo desativado, o foco Olá para novos desenvolvimentos está mudando toohello Portal do Azure. Todos os novos recursos futuros para aplicativos Web virão em Olá Portal do Azure. Começar a usar o hello Azure Portal tootake aproveitar Olá aplicativos Web têm toooffer a melhor e mais recente.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Diferenças de layout entre Olá Portal clássico do Azure e o Portal do Azure
No portal clássico do hello, todos os hello Azure services é listado no lado esquerdo hello. Navegação no portal clássico Olá segue uma estrutura de árvore, em que você iniciar o serviço de saudação e navegar em cada elemento. Essa estrutura funciona bem para o gerenciamento de componentes independentes. No entanto, os aplicativos criados no Azure são uma coleção de serviços interconectados, e essa estrutura de árvore não é ideal para trabalhar com coleções de serviços. 

Olá portal do Azure torna fácil toobuild aplicativos-a ponta com componentes de vários serviços. portal de saudação é organizado como *jornadas*. Um *jornada* é uma série de *folhas*, que são contêineres de saudação componentes diferentes. Por exemplo, configurando o dimensionamento automático para um aplicativo web é um *jornada* que o leva várias folhas conforme mostrado no exemplo a seguir de saudação: Olá **web site** folha (que título da folha ainda não foi atualizado toouse Olá terminologia nova), Olá **configurações** folha e hello **expansão** folha. No exemplo hello, dimensionamento automático está sendo configurado toodepend no uso da CPU, portanto, há também uma **percentual de CPU** folha. Olá componentes no hello *folhas* são chamados *partes*, que se parecer com blocos. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Exemplo de navegação: criar um aplicativo Web
A criação de novos aplicativos Web é muito fácil. Olá imagem mostra Olá clássico portal e hello portal lado a lado toodemonstrate que não há muito mudou no número de saudação de etapas a seguir necessário tooget um aplicativo web para cima e em execução. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

No portal de saudação, você pode escolher de tipos mais comuns de saudação de aplicativos web, incluindo Galeria populares aplicativos como o WordPress. Para obter uma lista completa de aplicativos disponíveis, visite Olá [Azure Marketplace].

Quando você cria um aplicativo web, você especificar a URL, o plano de serviço de aplicativo e o local no portal de saudação como faria no portal clássico do hello. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Além disso, o portal de saudação permite que você defina outras configurações comuns. Por exemplo, [grupos de recursos](../azure-resource-manager/resource-group-overview.md) torná-lo toosee simple e gerenciar recursos do Azure relacionados. 

## <a name="navigation-example-settings-and-features"></a>Exemplo de navegação: configurações e recursos
Todos os Olá configurações e recursos agora são agrupados logicamente em uma única folha, do qual você pode navegar.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Por exemplo, você pode criar domínios personalizados clicando em **domínios personalizados e SSL** em Olá **configurações** folha.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset se um alerta de monitoramento, clique em **solicitações e erros** e **adicionar alerta**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Diagnóstico de tooenable, clique em **logs de diagnóstico** em Olá **configurações** folha.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

tooconfigure configurações do aplicativo, clique em **configurações do aplicativo** em Olá **configurações** folha. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Diferente de nome de marca hello, algumas coisas no portal de saudação foram renomeadas ou agrupadas de forma diferente toomake-lo mais fácil toofind-los. Por exemplo, abaixo está uma captura de tela da página correspondente de saudação para configurações de aplicativo (**configurar**) no portal clássico do hello.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Mais Recursos
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

