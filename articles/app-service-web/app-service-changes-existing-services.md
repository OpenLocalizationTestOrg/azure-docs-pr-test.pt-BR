---
title: "Serviço de Aplicativo do Azure e seu impacto sobre os serviços existentes do Azure"
description: "Explica como o novo Serviço de Aplicativo do Azure e seus recursos afetam os serviços existentes no Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Serviço de Aplicativo do Azure e serviços existentes do Azure
Este artigo descreve as alterações nos serviços existentes do Azure como parte da alteração para reunir vários serviços do Azure no [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Visão geral
[Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novo e exclusivo que habilita os desenvolvedores a criar aplicativos Web e móveis para qualquer plataforma e qualquer dispositivo. O Serviço de Aplicativo é uma solução integrada criada para simplificar funções de codificação repetidas, integrar-se a sistemas corporativos e de SaaS e automatizar processos de negócios, além de atender às suas necessidades de segurança, confiabilidade e escalabilidade.

O Serviço de Aplicativo reúne os seguintes serviços existentes do Azure - [Sites](https://azure.microsoft.com/services/websites/), [Serviços Móveis](https://azure.microsoft.com/services/mobile-services/) e [Serviços Biztalk](https://azure.microsoft.com/services/biztalk-services/) em um único serviço combinado, enquanto acrescenta novas capacidades avançadas.  O Serviço de Aplicativo permite hospedar os seguintes tipos de aplicativo:

* Aplicativos Web
* Aplicativos Móveis
* Aplicativos de API
* Aplicativos Lógicos

A tabela a seguir explica como os serviços existentes do Azure são mapeados para o Serviço de Aplicativo e os tipos de aplicativos disponíveis nele.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Serviço existente do Azure</th>
<th align="left", style="width:10%">Serviço de aplicativo do Azure</th>
<th align="left", style="width:80%">O que mudou</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Websites do Azure</td>
<td align="left">Aplicativos Web</td>
<td align="left"><li>Para os Sites do Azure, o Serviço de Aplicativo limita-se estritamente à alteração do nome Sites para Aplicativos Web.
<p><li>Todas as suas instâncias existentes de Sites agora são Aplicativos Web no Serviço de Aplicativo.</p>
<p><li>Você pode acessar os sites existentes pelo <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde encontrará todos os sites existentes em <em>Aplicativos Web</em>.</p>
<p><li><em>Plano de hospedagem de Web</em> agora é <em>plano do serviço de aplicativo</em>. Um <em>Plano do Serviço de Aplicativo</em> pode hospedar qualquer tipo do Serviço de Aplicativo, como aplicativos Web, Móveis, Lógicos ou de API.</p>
<p><li>Os aplicativos Web do Serviço de Aplicativo do Azure têm Disponibilidade Geral.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre aplicativos Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Serviços móveis do Azure</td>
<td align="left">Aplicativos Móveis</td>
<td align="left"><p><li>Os Serviços Móveis continuam disponíveis como um serviço autônomo e permanecem com suporte completo.</p>
<p><li>Os Aplicativos Móveis são um tipo de aplicativo do Serviço de Aplicativo, que integram toda a funcionalidade dos Serviços Móveis e muito mais.</p>
<p><li>É fácil <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar dos Serviços Móveis para os Aplicativos Móveis</a>.</p>
<p><li>Como parte do Serviço de Aplicativo, os Aplicativos Móveis obtêm novos recursos além de Serviços Móveis, como a integração com sistemas de SaaS e locais, slots de preparação, Trabalhos Web, melhores opções de dimensionamento e muito mais.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre os aplicativos móveis</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Aplicativos de API</td>
<td align="left">
<p><li>Os Aplicativos de API são um novo tipo de aplicativo do Serviço de Aplicativo que permitem que você compile e consuma APIs na nuvem facilmente.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">Saiba mais sobre aplicativos de API</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Aplicativos Lógicos</td>
<td align="left">
<p><li>Os Aplicativos Lógicos são um novo tipo de aplicativo do Serviço de Aplicativo que permite automatizar facilmente os processos corporativos.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Saiba mais sobre aplicativos lógicos</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Serviços BizTalk do Azure</td>
<td align="left">Aplicativos de API do BizTalk</td>
<td align="left">
<li><p>Os Serviços BizTalk continuam disponíveis como um serviço autônomo e permanecem com suporte completo.</p>
<li><p>Todos os recursos dos Serviços BizTalk são integrados ao Serviço de Aplicativo como Aplicativos de API, permitindo aos usuários realizar cenários de integração de aplicativos empresariais e integração B2B com qualquer um dos tipos de aplicativos no Serviço de Aplicativo.</p>
<li><p>Com os Aplicativos Lógicos, agora é possível automatizar processos corporativos usando uma experiência de design visual para criar fluxos de trabalho.</p></td>
</tr>
</tbody>
</table>

Para saber mais, acesse a documentação do [Serviço de Aplicativo](https://azure.microsoft.com/documentation/services/app-service/).

