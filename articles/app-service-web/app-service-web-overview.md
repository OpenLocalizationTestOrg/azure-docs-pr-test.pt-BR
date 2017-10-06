---
title: "Visão geral de aplicativos aaaWeb | Microsoft Docs"
description: "Saiba como o Serviço de Aplicativo do Azure o ajuda a desenvolver e hospedar aplicativos Web"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 94af2caf-a2ec-4415-a097-f60694b860b3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 01/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: ce27519bddd62a7fca6ba1fb23c763d0fc378c2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="web-apps-overview"></a>Visão geral de aplicativos Web
*Aplicativos Web do Serviço de Aplicativo* é uma plataforma de computação totalmente gerenciada que é otimizada para hospedagem de sites e aplicativos Web. Isso [plataforma como serviço](https://en.wikipedia.org/wiki/Platform_as_a_service) oferta (PaaS) do Microsoft Azure permite que você se concentre em sua lógica de negócios enquanto Azure cuida da saudação infraestrutura toorun e dimensionar seus aplicativos.

Olá vídeo de 5 minutos a seguir apresenta os aplicativos de Web do serviço de aplicativo do Azure.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-App-Service-Web-Apps-with-Yochay-Kiriaty/player]
>
>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

## <a name="what-is-a-web-app-in-app-service"></a>O que é um aplicativo Web no Serviço de Aplicativo?
No serviço de aplicativo, um *aplicativo web* é hello recursos de computação que o Azure fornece para hospedar um site ou aplicativo web.  

recursos de computação Olá podem estar em compartilhado ou dedicadas máquinas virtuais (), dependendo da saudação preço que você escolher. O código do aplicativo é executado em uma VM gerenciada que é isolada de outros clientes.

O código pode estar em qualquer linguagem ou estrutura com suporte no [Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md), como ASP.NET, Node.js, Java, PHP ou Python. Você também pode executar scripts que usam o [PowerShell e outras linguagens de script](web-sites-create-web-jobs.md#acceptablefiles) em um aplicativo Web.

Para obter exemplos de cenários típicos de aplicativos que você pode usar os aplicativos Web para o, consulte [Web cenários de aplicativos](https://azure.microsoft.com/documentation/scenarios/web-app/) e hello **cenários e recomendações** seção [do serviço de aplicativo do Azure, Virtual Comparação de máquinas do Service Fabric e serviços de nuvem](choose-web-site-cloud-service-vm.md#scenarios).

## <a name="why-use-web-apps"></a>Por que usar aplicativos Web?
Aqui estão alguns recursos principais do serviço de aplicativo que se aplicam a aplicativos tooWeb:

* **Várias linguagens e estruturas** -o Serviço de Aplicativo tem suporte de primeira classe para ASP.NET, Node.js, Java, PHP e Python. Você também pode executar [o PowerShell e outros scripts ou executáveis](web-sites-create-web-jobs.md) nas VMs do Serviço de Aplicativo.
* **Otimização de DevOps** - configure a [implantação e integração contínua](app-service-continuous-deployment.md) com o Visual Studio Team Services, o GitHub ou BitBucket. Promova atualizações por meio de [ambientes de preparo e teste](web-sites-staged-publishing.md). Execute [testes A/B](app-service-web-test-in-production-get-start.md). Gerenciar seus aplicativos no serviço de aplicativo usando [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [interface de linha de comando de plataforma cruzada (CLI)](../cli-install-nodejs.md).
* **Escala global com alta disponibilidade** - escale [verticalmente](web-sites-scale.md) ou [horizontalmente](../monitoring-and-diagnostics/insights-how-to-scale.md) de forma manual ou automática. Hospedar seus aplicativos em qualquer lugar na infraestrutura de datacenter global da Microsoft e Olá do serviço de aplicativo [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promete alta disponibilidade.
* **Dados de plataformas e locais de conexões tooSaaS** -escolha entre mais de 50 [conectores](../connectors/apis-list.md) para sistemas corporativos (como SAP, Siebel e Oracle), serviços de SaaS (por exemplo, Salesforce e Office 365) e internet serviços (como o Facebook e Twitter). Acesse dados locais usando [Conexões Híbridas](../biztalk-services/integration-hybrid-connection-overview.md) e [Redes Virtuais do Azure](web-sites-integrate-with-vnet.md).
* **Segurança e conformidade** - o Serviço de Aplicativo está em [conformidade com ISO, SOC e PCI](https://www.microsoft.com/TrustCenter/).
* **Modelos de aplicativos** -escolha em uma lista abrangente dos modelos de aplicativos no hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) que permitem que você use um software de código aberto popular do assistente tooinstall como Drupal, Joomla e WordPress.
* **Integração do Visual Studio** -dedicadas ferramentas no Visual Studio simplificar o trabalho de saudação de criar, implantar e depurar.

Além disso, um aplicativo Web pode tirar proveito dos recursos oferecidos por [Aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md) (como suporte a CORS) e [Aplicativos Móveis](../app-service-mobile/app-service-mobile-value-prop.md) (como notificações por push). Para saber mais sobre os tipos de aplicativos no Serviço de Aplicativo, confira [Visão geral do Serviço de Aplicativo do Azure](../app-service/app-service-value-prop-what-is.md).

Além dos Aplicativos Web no Serviço de Aplicativo, o Azure oferece outros serviços que podem ser usados para hospedar sites e aplicativos Web. Na maioria dos cenários, os aplicativos Web é Olá melhor opção.  Arquitetura de microsserviço, considere [Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric)e se você precisar de mais controle sobre Olá VMs que seu código é executado no, considere [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/). Para obter mais informações sobre como toochoose entre esses serviços do Azure, consulte [comparação do serviço de aplicativo do Azure, máquinas virtuais, serviço de malha e serviços de nuvem](choose-web-site-cloud-service-vm.md).

## <a name="getting-started"></a>Introdução
tooget iniciado com a implantação de exemplo código tooa novo aplicativo web no serviço de aplicativo, siga um dos tutoriais Olá Olá caixa suspensa a seguir. Você precisará de uma conta gratuita do Azure.

> [!div class="op_single_selector"]
> * [Implantar seu primeiro tooAzure de aplicativo de web do ASP.NET em 5 minutos](app-service-web-get-started-dotnet.md)
> * [Implantar seu primeiro tooAzure de aplicativo de web PHP em 5 minutos](app-service-web-get-started-php.md)
> * [Implantar seu primeiro tooAzure de aplicativo de web Node. js em 5 minutos](app-service-web-get-started-nodejs.md)
> * [Implantar seu primeiro tooAzure de aplicativo de web de Java em 5 minutos](app-service-web-get-started-java.md)
> * [Implantar seu primeiro tooAzure de aplicativo de web Python em 5 minutos](app-service-web-get-started-python.md)
> * [Implantar seu primeiro site tooAzure da HTML em 5 minutos](app-service-web-get-started-html.md)
> 
> 

> [!NOTE]
> Você pode [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) sem uma conta do Azure. Criar um aplicativo de início e explorá-la para a hora de tooan – nenhum cartão de crédito necessários, nenhum investimento.
> 
> 
