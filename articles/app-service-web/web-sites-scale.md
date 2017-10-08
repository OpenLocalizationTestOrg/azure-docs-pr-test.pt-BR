---
title: aaaScale backup de um aplicativo no Azure | Microsoft Docs
description: "Saiba como tooscale backup de um aplicativo no serviço de aplicativo do Azure tooadd capacidade e recursos."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Dimensionar um aplicativo no Azure
Este artigo mostra como tooscale seu aplicativo no serviço de aplicativo do Azure. Há dois fluxos de trabalho para a escala de dimensionamento, backup e expansão e este artigo explica escala Olá o fluxo de trabalho.

* [Escalar verticalmente](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): obtenha mais CPU, memória, espaço em disco e recursos adicionais como VMs (máquinas virtuais) dedicadas, domínios e certificados personalizados, slots de preparação, dimensionamento automático e muito mais. Escalar verticalmente alterando Olá preço do plano de serviço de aplicativo que seu aplicativo pertence.
* [Expansão](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): aumentar Olá número de instâncias VM que executar seu aplicativo.
  Você pode expandir tooas muitos como 20 instâncias, dependendo do tipo de preços. [Ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md) na **Premium** camada aumentarão ainda mais suas instâncias de too50 de contagem de expansão. Para saber mais sobre a escala horizontal, consulte [Escalar a contagem de instâncias manualmente ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md). Lá você encontrará fora como autoscaling toouse, que é a contagem de instâncias de tooscale automaticamente com base em regras predefinidas e agendas.

Olá escala configurações take apenas segundos tooapply e afetam todos os aplicativos em seu [plano de serviço de aplicativo](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
Eles não exigem que você toochange seu código ou reimplantar o aplicativo.

Para obter informações sobre preços de saudação e recursos de planos de serviço de aplicativo individuais, consulte [detalhes de preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).  

> [!NOTE]
> Antes de alternar um plano de serviço de aplicativo de saudação **livre** camada, você deve primeiro remover Olá [os limites de gastos](https://azure.microsoft.com/pricing/spending-limits/) em vigor para a sua assinatura do Azure. tooview ou alterar as opções para sua assinatura do serviço de aplicativo do Microsoft Azure, consulte [assinatura do Microsoft Azure][azuresubscriptions].
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>Escale verticalmente seu tipo de preço
1. No navegador, abra Olá [portal do Azure][portal].
2. Na folha do aplicativo, clique em **Todas as configurações** e em **Escalar Verticalmente**.
   
    ![Navegue tooscale backup de seu aplicativo do Azure.][ChooseWHP]
3. Escolha seu tipo e depois clique em **Selecionar**.
   
    Olá **notificações** guia pisca uma verde **êxito** após a conclusão da operação de saudação.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>Escalar recursos relacionados
Se o seu aplicativo depender de outros serviços, como o Banco de Dados SQL do Azure ou o Armazenamento do Azure, você também poderá escalar verticalmente esses recursos com base em suas necessidades. Esses recursos não são dimensionados com hello plano de serviço de aplicativo e devem ser dimensionados separadamente.

1. Em **Essentials**, clique em Olá **grupo de recursos** link.
   
    ![Escale verticalmente os recursos relacionados de seu aplicativo do Azure](./media/web-sites-scale/RGEssentialsLink.png)
2. Em Olá **resumo** parte do hello **grupo de recursos** folha, clique em um recurso que você deseja tooscale. Olá captura de tela a seguir mostra um recurso de banco de dados SQL e um recurso de armazenamento do Azure.
   
    ![Navegue tooresource grupo folha tooscale backup de seu aplicativo do Azure](./media/web-sites-scale/ResourceGroup.png)
3. Para um recurso de banco de dados SQL, clique em **configurações** > **preço** tooscale Olá preço.
   
    ![Dimensionar o hello back-end de banco de dados SQL para seu aplicativo do Azure](./media/web-sites-scale/ScaleDatabase.png)
   
    Você também pode ativar a [replicação geográfica](../sql-database/sql-database-geo-replication-overview.md) de sua instância do Banco de Dados SQL.
   
    Para um recurso de armazenamento do Azure, clique em **configurações** > **configuração** tooscale as suas opções de armazenamento.
   
    ![Dimensionar a conta de armazenamento do Azure Olá usada pelo seu aplicativo do Azure](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>Saiba mais sobre os recursos de desenvolvedor
Dependendo da saudação preço, hello seguintes recursos para desenvolvedores estão disponíveis:

### <a name="bitness"></a>Número de bits
* Olá **básica**, **padrão**, e **Premium** camadas oferecem suporte a aplicativos de 64 bits e 32 bits.
* Olá **livre** e **compartilhado** plano camadas oferecem suporte apenas a aplicativos de 32 bits.

### <a name="debugger-support"></a>Suporte ao depurador
* Suporte do depurador está disponível para Olá **livre**, **compartilhado**, e **básica** modos em uma conexão por plano do serviço de aplicativo.
* Suporte do depurador está disponível para Olá **padrão** e **Premium** modos em cinco conexões simultâneas por plano do serviço de aplicativo.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>Saiba mais sobre outros recursos
* Para obter informações detalhadas sobre todos os Olá restantes recursos saudação do serviço de aplicativo planos, inclusive de preço e recursos de interesse tooall os usuários (incluindo os desenvolvedores), consulte [detalhes de preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/web-sites/).

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de você se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/) onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido e não há compromissos.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>Próximas etapas
* tooget iniciado com o Azure, consulte [avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/).
* Para obter informações sobre preços, suporte e SLA, visite Olá links a seguir.
  
    [Detalhes de preços de transferências de dados](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Planos de suporte do Microsoft Azure](https://azure.microsoft.com/support/plans/)
  
    [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/)
  
    [Detalhes de preços do banco de dados SQL](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Tamanhos de máquina virtual e de serviço de nuvem do Microsoft Azure][vmsizes]
  
    [Detalhes de Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/)
  
    [Detalhes de Preços do Serviço de Aplicativo - Conexões SSL](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* Para obter informações sobre práticas recomendadas do Serviço de Aplicativo do Azure, incluindo a criação de uma arquitetura escalonável e flexível, consulte [Práticas recomendadas: Aplicativos Web do Serviço de Aplicativo do Azure](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx).
* Para vídeos sobre como dimensionar aplicativos de serviço de aplicativo, consulte Olá recursos a seguir:
  
  * [Quando tooScale sites do Azure - com Stefan Schackow](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Dimensionamento automático de Sites do Azure, CPU ou programado - com Stefan Schackow](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Como dimensionar sites do Azure - com Stefan Schackow](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
