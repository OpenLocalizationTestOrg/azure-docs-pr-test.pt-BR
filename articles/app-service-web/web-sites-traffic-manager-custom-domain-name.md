---
title: "aaaConfigure um nome de domínio personalizado para um aplicativo web no serviço de aplicativo do Azure que usa o Gerenciador de tráfego de balanceamento de carga."
description: "Use um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure que inclua o Gerenciador de Tráfego para balanceamento de carga."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configurando um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure usando o Gerenciador de Tráfego
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

Este artigo fornece instruções genéricas sobre como usar um nome de domínio personalizado com o Serviço de Aplicativo do Azure que usa o Gerenciador de Tráfego para balanceamento de carga.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Compreendendo os registros DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configurar seus aplicativos Web para o modo Padrão
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Adicionar um registro DNS a seu domínio personalizado
> [!NOTE]
> Se você tiver adquirido por meio de aplicativos de Web do serviço de aplicativo do Azure ignorar as etapas a seguir e consulte a etapa final toohello do [comprar o domínio para aplicativos Web](custom-dns-web-site-buydomains-web-app.md) artigo.
> 
> 

tooassociate seu domínio personalizado com um aplicativo web no serviço de aplicativo do Azure, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando as ferramentas fornecidas pelo registrador Olá que você adquiriu o seu nome de domínio. Use Olá toolocate as etapas a seguir e as ferramentas do DNS hello.

1. Entrar na conta tooyour no seu registrador de domínio e procure por uma página de gerenciamento de registros DNS. Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**. Geralmente um link de página toothis pode ser encontrada ser exibindo as informações da conta e procurando um link como **Meus domínios**.
2. Após localizar página de gerenciamento de saudação para seu nome de domínio, procure um link que permite que os registros DNS Olá tooedit. Ele pode estar listado como um **Arquivo de zona**, **Registros DNS** ou como um link de configuração **Avançado**.
   
   * página de saudação provavelmente terá alguns registros já criados, como uma associação de entrada '**@**'ou'\*' com uma página 'estacionamento domínio'. Ela também pode conter registros para subdomínios comuns como **www**.
   * página Hello serão mencionar **registros CNAME**, ou forneça uma lista suspensa tooselect um tipo de registro. Ela também pode mencionar outros registros, como **registros A** e **registros MX**. Em alguns casos, os registros CNAME serão chamados por outros nomes como um **Registro de Alias**.
   * página Olá também terá campos que permitem muito**mapa** de um **nome de Host** ou **nome de domínio** tooanother nome de domínio.
3. Embora especificidades de saudação do registrador de cada variam, em geral você mapear *de* seu nome de domínio personalizado (como **contoso.com**,) *para* nome de domínio do Traffic Manager hello (**contoso.trafficmanager.net**) que é usado para seu aplicativo web.
   
   > [!NOTE]
   > Como alternativa, se um registro já está em uso e você precisar toopreemptively associar tooit seus aplicativos, você pode criar um registro CNAME adicional. Por exemplo, associação de toopreemptively **www.contoso.com** tooyour web app, crie um registro CNAME do **awverify.www** muito**contoso.trafficmanager.net**. Em seguida, você pode adicionar tooyour "www.contoso.com" aplicativo Web sem alterar o registro CNAME "www" hello. Para saber mais, confira [Criar registros DNS para um aplicativo Web em um domínio personalizado][CREATEDNS].
   > 
   > 
4. Depois de terminar de adicionar ou modificar os registros DNS no registrador, salve as alterações de saudação.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Habilitar o Gerenciador de tráfego
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte Olá [Node. js Developer Center](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
