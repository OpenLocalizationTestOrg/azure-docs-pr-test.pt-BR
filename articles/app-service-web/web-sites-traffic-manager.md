---
title: "aaaControlling tráfego de aplicativo web do Azure com o Azure Traffic Manager"
description: "Este artigo fornece informações de resumo para o Azure Traffic Manager como ele se relaciona tooAzure os aplicativos web."
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Controlando o tráfego de aplicativos Web do Azure com o Gerenciador de Tráfego do Azure
> [!NOTE]
> Este artigo fornece informações de resumo do Microsoft Azure Traffic Manager como ele se relaciona tooAzure aplicativos de Web do serviço de aplicativo. Mais informações sobre o Gerenciador de tráfego do Azure em si podem ser encontradas visitando links Olá final Olá deste artigo.
> 
> 

## <a name="introduction"></a>Introdução
Você pode usar toocontrol de Gerenciador de tráfego do Azure como solicitações de clientes da web são aplicativos distribuídos tooweb no serviço de aplicativo do Azure. Quando pontos de extremidade de aplicativo da web são adicionados tooa perfil do Gerenciador de tráfego do Azure, o Azure Traffic Manager mantém o controle de status de saudação de seus aplicativos web (em execução, parado ou excluído) para que ele possa decidir qual esses pontos de extremidade deve receber tráfego.

## <a name="load-balancing-methods"></a>Métodos de balanceamento de carga
O Gerenciador de Tráfego do Azure usa três métodos de balanceamento de carga diferentes. Elas são descritas nas Olá a seguir lista como os aplicativos web tooAzure aos quais eles pertencem.

* **Failover**: se você tiver clones de aplicativo web em regiões diferentes, pode usar esse tooservice de aplicativo web de um método tooconfigure todo o tráfego de cliente da web e configurar outro aplicativo web no tooservice região diferente que o tráfego em maiusculas Olá primeiro aplicativo de web torna-se indisponível.
* **Round Robin**: se você tiver clones de aplicativo web em regiões diferentes, você pode usar esse tráfego de toodistribute método igualmente entre os aplicativos web hello em regiões diferentes.
* **Desempenho**: Olá método desempenho distribui o tráfego com base no menor tooclients de tempo de viagem de ida e hello. Olá método desempenho pode ser usado para aplicativos web dentro de saudação mesma região ou em regiões diferentes.

## <a name="web-apps-and-traffic-manager-profiles"></a>Aplicativos Web e perfis do Gerenciador de Tráfego
tooconfigure controle de saudação do tráfego de aplicativo da web, crie um perfil no Azure Traffic Manager que usa um dos métodos descritos anteriormente de balanceamento de carga de saudação três e, em seguida, adicionar pontos de extremidade de saudação (nesse caso, os aplicativos web) para o qual você deseja toocontrol tráfego toohello perfil. Seu status de aplicativo da web (em execução, parado ou excluído) é toohello regularmente comunicado de perfil para que o Azure Traffic Manager pode direcionar o tráfego de acordo.

Ao usar o Azure Traffic Manager com o Azure, lembre-Olá mente pontos a seguir:

* Para implantações somente do aplicativo web dentro de saudação mesma região, os aplicativos Web já fornece a funcionalidade de failover e round-robin sem o modo de aplicativo tooweb levar em consideração.
* Para implantações em Olá mesma região que usam aplicativos da Web em conjunto com outro serviço de nuvem do Azure, você pode combinar os dois tipos de cenários de híbrida tooenable pontos de extremidade.
* Você só pode especificar um ponto de extremidade de aplicativo Web por região em um perfil. Quando você seleciona um aplicativo web como um ponto de extremidade para uma região, Olá restantes aplicativos web na região ficarão indisponíveis para seleção para o perfil.
* pontos de extremidade do Olá web aplicativo que você especificar em um perfil do Gerenciador de tráfego do Azure serão exibidas sob o hello **nomes de domínio** seção na página Configurar Olá Olá web app no perfil hello, mas não poderá ser configurado existe.
* Depois de adicionar um perfil de tooa de aplicativo web, Olá **URL do Site** em Olá painel da web hello página do aplicativo do portal exibirá Olá domínio personalizado URL do aplicativo web de saudação se você tiver configurado um. Caso contrário, ele exibirá a URL do perfil do Traffic Manager hello (por exemplo, `contoso.trafficmgr.com`). Ambos Olá nome de domínio direto do aplicativo de web hello e Olá URL do Gerenciador de tráfego serão visível na página Configurar de seu aplicativo da web de saudação em Olá **nomes de domínio** seção.
* Nomes de domínios personalizados funcionará como esperado, mas em adição tooadding-los tooyour os aplicativos web, você também deve configurar seu toohello de toopoint de mapa DNS URL do Gerenciador de tráfego. Para obter informações sobre como tooset um domínio personalizado para um aplicativo web do Azure, consulte [Configurando um nome de domínio personalizado para um site do Azure](app-service-web-tutorial-custom-domain.md).
* Você só pode adicionar aplicativos web que estão no modo padrão ou premium tooa perfil do Gerenciador de tráfego do Azure.

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral conceitual e técnica do Gerenciador de Tráfego do Azure, consulte [Visão geral do Gerenciador de Tráfego](../traffic-manager/traffic-manager-overview.md).

Para obter mais informações sobre como usar o Gerenciador de tráfego com aplicativos Web, consulte as postagens de blog de saudação [usando o Azure Traffic Manager com o Azure Web Sites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) e [Azure Traffic Manager agora pode integrar com o Azure Web Sites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

