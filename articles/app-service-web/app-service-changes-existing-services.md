---
title: "aaaAzure do serviço de aplicativo e seu impacto sobre os serviços do Azure existentes"
description: "Explica como Olá novo serviço de aplicativo do Azure e seus recursos afetam os serviços existentes no Azure."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Serviço de Aplicativo do Azure e serviços existentes do Azure
Este artigo descreve Olá alterações tooexisting serviços do Azure como parte da saudação alteração toobring junto vários serviços do Azure em [do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/), uma nova oferta integrada.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Visão geral
[Serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é um serviço de nuvem novos e exclusivos que permite que os desenvolvedores toocreate aplicativos web e móveis para qualquer plataforma e de qualquer dispositivo. Serviço de aplicativo é que uma solução integrada projetada toostreamline repetido funções de codificação, integrar com o enterprise e sistemas de SaaS e automatizar processos de negócios enquanto atende suas necessidades de segurança, confiabilidade e escalabilidade.

Serviço de aplicativo reúne saudação do Azure existentes a seguir services - [sites](https://azure.microsoft.com/services/websites/), [serviços móveis](https://azure.microsoft.com/services/mobile-services/), e [serviços Biztalk](https://azure.microsoft.com/services/biztalk-services/) em um único combinado serviço, enquanto adicionando novos recursos eficientes.  Serviço de aplicativo permite que você toohost Olá seguintes tipos de aplicativo:

* Aplicativos Web
* Aplicativos Móveis
* Aplicativos de API
* Aplicativos Lógicos

Olá, tabela a seguir explica como existente do Azure services mapear tooApp serviço e hello tipos de aplicativo disponíveis dentro dele.

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
<td align="left"><li>Para sites do Azure, o serviço de aplicativo é estritamente limitada toochanging Olá nome sites tooWeb aplicativos.
<p><li>Todas as suas instâncias existentes de Sites agora são Aplicativos Web no Serviço de Aplicativo.</p>
<p><li>Você pode acessar seus sites existentes por meio de saudação <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Portal do Azure</a>, onde você encontrará todos os sites existentes em <em>aplicativos Web</em>.</p>
<p><li><em>Plano de hospedagem de Web</em> agora é <em>plano do serviço de aplicativo</em>. Um <em>Plano do Serviço de Aplicativo</em> pode hospedar qualquer tipo do Serviço de Aplicativo, como aplicativos Web, Móveis, Lógicos ou de API.</p>
<p><li>Os aplicativos Web do Serviço de Aplicativo do Azure têm Disponibilidade Geral.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Saiba mais sobre aplicativos Web</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Serviços móveis do Azure</td>
<td align="left">Aplicativos Móveis</td>
<td align="left"><p><li>Serviços móveis continuar toobe disponível como um serviço autônomo e permanecem totalmente suportados.</p>
<p><li>Aplicativos móveis é um tipo de aplicativo no serviço de aplicativo, que integra a funcionalidade de saudação de serviços móveis e muito mais.</p>
<p><li>Ele é muito fácil<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrar de serviços móveis tooMobile aplicativos</a>.</p>
<p><li>Como parte do Serviço de Aplicativo, os Aplicativos Móveis obtêm novos recursos além de Serviços Móveis, como a integração com sistemas de SaaS e locais, slots de preparação, Trabalhos Web, melhores opções de dimensionamento e muito mais.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Saiba mais sobre os aplicativos móveis</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">Aplicativos de API</td>
<td align="left">
<p><li>Aplicativos de API é um novo tipo de aplicativo no serviço de aplicativo que permite criar e consumir APIs na nuvem hello.</p>
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
<li><p>Os serviços do BizTalk continuar toobe disponível como um serviço autônomo e permanecem totalmente suportados.</p>
<li><p>Todos os recursos de saudação dos serviços do BizTalk são integrados ao serviço de aplicativo como aplicativos de API Habilitando usuários tooperform integração de aplicativos empresariais e cenários de integração B2B com nenhum dos tipos de saudação do aplicativo no serviço de aplicativo.</p>
<li><p>Com a lógica de aplicativos, agora você pode automatizar processos de negócios usando um fluxos de trabalho de toocreate de experiência de design visual.</p></td>
</tr>
</tbody>
</table>

toolearn mais, visite [documentação do serviço de aplicativo](https://azure.microsoft.com/documentation/services/app-service/).

