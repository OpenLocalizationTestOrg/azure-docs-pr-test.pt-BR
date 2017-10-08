---
title: "aaaAzure do serviço de aplicativo para web, móveis e aplicativos de API | Microsoft Docs"
description: "Saiba como o Serviço de Aplicativo do Azure ajuda você a desenvolver, implantar e gerenciar aplicativos móveis e da Web."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, custo do serviço de aplicativo, escala, dimensionável, implantação de aplicativos, implantação de aplicativo do azure, paas, plataforma como serviço, site, site da web, web, aplicativo móvel do azure"
services: app-service
documentationcenter: 
author: omarkmsft
manager: erikre
editor: cephalin
ms.assetid: 979cafa8-eeb6-4d3b-87cf-764a821c3e4f
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: 22f414c7d79092d87406a8d3538b946881fb4580
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-app-service"></a>O que é o Serviço de Aplicativo do Azure?
*Serviço de Aplicativo* é uma oferta de [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) (plataforma como serviço) do Microsoft Azure. Crie aplicativos Web e móveis para qualquer plataforma ou dispositivo. Integre seus aplicativos a soluções SaaS, conecte-se com aplicativos locais e automatize os processos de negócios. O Azure executa os aplicativos em VMs (máquinas virtuais) totalmente gerenciadas, com sua escolha de recursos compartilhados de VM ou VMs dedicadas.

Serviço de aplicativo inclui Olá web e móveis funcionalidades que anteriormente fornecemos separadamente como sites do Azure e serviços móveis do Azure. Ele também inclui novos recursos para automatizar processos empresariais e hospedagem de APIs de nuvem. Como um único serviço integrado, o Serviço de Aplicativo permite incluir vários componentes (sites, back-ends de aplicativo móvel, APIs RESTful e processos de negócios) em uma única solução.

Olá, vídeo 4 minutos a seguir fornece uma breve explicação de como o serviço de aplicativo se relaciona tooearlier Azure ofertas e quais são as novidades nele.

> [!VIDEO https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/app-service-history-lesson/player]
> 
> 

## <a name="why-use-app-service"></a>Por que usar o Serviço de Aplicativo?
Veja alguns recursos importantes do Serviço de Aplicativo:

* **Várias linguagens e estruturas** -o Serviço de Aplicativo tem suporte de primeira classe para ASP.NET, Node.js, Java, PHP e Python. Você também pode executar [o Windows PowerShell e outros scripts ou executáveis](../app-service-web/web-sites-create-web-jobs.md) nas VMs do Serviço de Aplicativo.
* **Otimização de DevOps** - configure a [implantação e integração contínua](../app-service-web/app-service-continuous-deployment.md) com o Visual Studio Team Services, o GitHub ou BitBucket. Promova atualizações por meio de [ambientes de preparo e teste](../app-service-web/web-sites-staged-publishing.md). Execute [testes A/B](../app-service-web/app-service-web-test-in-production-get-start.md). Gerenciar seus aplicativos no serviço de aplicativo usando [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [interface de linha de comando de plataforma cruzada (CLI)](../cli-install-nodejs.md).
* **Escala global com alta disponibilidade** - escale [verticalmente](../app-service-web/web-sites-scale.md) ou [horizontalmente](../monitoring-and-diagnostics/insights-how-to-scale.md) de forma manual ou automática. Hospedar seus aplicativos em qualquer lugar na infraestrutura de datacenter global da Microsoft e Olá do serviço de aplicativo [SLA](https://azure.microsoft.com/support/legal/sla/app-service/) promete alta disponibilidade.
* **Dados de plataformas e locais de conexões tooSaaS** -escolha entre mais de 50 [conectores](../connectors/apis-list.md) para sistemas corporativos (como SAP, Siebel e Oracle), serviços de SaaS (por exemplo, Salesforce e Office 365) e internet serviços (como o Facebook e Twitter). Acesse dados locais usando [Conexões Híbridas](../biztalk-services/integration-hybrid-connection-overview.md) e [Redes Virtuais do Azure](../app-service-web/web-sites-integrate-with-vnet.md).
* **Segurança e conformidade** - o Serviço de Aplicativo está em [conformidade com ISO, SOC e PCI](https://www.microsoft.com/TrustCenter/).
* **Modelos de aplicativos** -escolha em uma lista extensa de modelos em Olá [Azure Marketplace](https://azure.microsoft.com/marketplace/) que permitem que você use um software de código aberto popular do assistente tooinstall como Drupal, Joomla e WordPress.
* **Integração do Visual Studio** -dedicadas ferramentas no Visual Studio simplificar o trabalho de saudação de criar, implantar e depurar.

## <a name="app-types-in-app-service"></a>Tipos de aplicativo no Serviço de Aplicativo
Serviço de aplicativo oferece várias *tipos de aplicativo*, cada um do qual é pretendido toohost uma carga de trabalho específica:

* [**Aplicativos Web**](../app-service-web/app-service-web-overview.md) - para hospedar sites e aplicativos Web.
* [**Aplicativos Móveis**](../app-service-mobile/app-service-mobile-value-prop.md) Para hospedar os back-ends do aplicativo móvel.
* [**Aplicativos da API**](../app-service-api/app-service-api-apps-why-best-platform.md) - Para hospedar as APIs RESTful.
* [**Aplicativos Lógicos**](../logic-apps/logic-apps-what-are-logic-apps.md) - Para automatizar os processos de negócios e integrar os sistemas e dados nas nuvens sem escrever código.

Olá word *aplicativo* aqui refere-se toohello recursos dedicados toorunning uma carga de trabalho de hospedagem. Colocar "aplicativo web" como um exemplo, você provavelmente se acostumar toothinking de um aplicativo web, como navegador juntos oferecem funcionalidade tooa o código de recursos de computação hello e aplicativo. Mas, no serviço de aplicativo um *aplicativo web* é hello recursos de computação que o Azure fornece para hospedar o código do aplicativo. 

O aplicativo pode ser composto de vários aplicativos do Serviço de Aplicativo de tipos diferentes. Por exemplo, se seu aplicativo é composto de um front-end da Web e um back-end de API RESTful, você pode:

- Implantar (front-end e api) tooa única web app  
- Implante seu aplicativo de web front-end código tooa e seu aplicativo tooan API de código de back-end. 



## <a name="app-service-plans"></a>Planos do Serviço de Aplicativo
[Planos de serviço de aplicativo](azure-web-sites-web-hosting-plans-in-depth-overview.md) representar a coleção de saudação de recursos físicos usados toohost seus aplicativos.

Os Planos do Serviço de Aplicativo definem:

- **Região** (Oeste dos EUA, Leste dos EUA, etc.)
- **Contagem da escala** (uma, duas, três instâncias, etc.)
- **Tamanha da instância** (Pequena, Média, Grande)
- **SKU** (Gratuito, Compartilhado, Básico, Standard, Premium)

Todos os aplicativos atribuídos tooan **plano de serviço de aplicativo** compartilham recursos Olá definidos por ela, permitindo que você toosave custo ao hospedar vários aplicativos.

O **plano de serviço de aplicativo** pode ser dimensionada de **livre** e **compartilhado** SKUs muito**básica**, **padrão**, e **Premium** SKUs dando a você acessam os recursos de toomore e recursos ao longo de saudação maneira. Depois que o plano de serviço de aplicativo é definido muito**básica** ou superior, você pode também controlar o hello **tamanho** e dimensionar a contagem de saudação VMs.

Olá **SKU** e **escala** de saudação do serviço de aplicativo plano determina o número de custo e não hello de saudação de aplicativos hospedados nele. 

Se precisar de mais escalabilidade e isolamento da rede, execute os aplicativos em um [Ambiente do Serviço de Aplicativo](../app-service-web/app-service-app-service-environment-intro.md).

## <a name="pricing"></a>Preços
Para saber mais sobre os custos do Serviço de Aplicativo, confira [Preços do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="test-drive-app-service"></a>Serviço de Aplicativo orientado a teste
[Crie um aplicativo Web, um aplicativo móvel ou um aplicativo lógico de exemplo](https://azure.microsoft.com/try/app-service/) e use-o por 1 hora, sem nenhum cartão de crédito, comprometimento ou inconvenientes.

Ou abra uma [conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/)e experimente um de nossos tutoriais de introdução:

* [Tutorial: criar um aplicativo Web](../app-service-web/app-service-web-get-started.md)
* [Tutorial: criar um aplicativo móvel](../app-service-mobile/app-service-mobile-android-get-started.md)
* [Tutorial: criar um aplicativo de API](../app-service-api/app-service-api-dotnet-get-started.md)
* [Tutorial: criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md)

