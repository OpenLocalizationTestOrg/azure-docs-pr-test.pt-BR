---
title: aaaEnabling final tooend SSL no Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral da saudação Application Gateway final tooend suporte para SSL."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Visão geral do fim tooend SSL com o Application Gateway

Gateway de aplicativo oferece suporte a terminação SSL no gateway hello, depois que o tráfego que flui geralmente descriptografados toohello servidores de back-end. Esse recurso permite toobe de servidores de web unburdened da sobrecarga de criptografia e descriptografia cara. No entanto para alguns clientes a servidores de back-end de toohello de comunicação não criptografada não é uma opção aceitável. Essa comunicação não criptografada pode ser devido a requisitos de toosecurity, requisitos de conformidade, ou o aplicativo hello só pode aceitar uma conexão segura. Para tais aplicativos, o gateway de aplicativo oferece suporte a tooend final SSL criptografia.

## <a name="overview"></a>Visão geral

Final tooend SSL permite que você toosecurely transmitir dados confidenciais toohello back-end criptografado enquanto ainda tirar proveito dos benefícios de saudação de recursos de balanceamento de carga de camada 7 qual gateway de aplicativo fornece. Alguns desses recursos são a afinidade de sessão baseada em cookie, roteamento baseado em URL, o suporte para roteamento baseado em sites ou capacidade tooinject X - encaminhado-* cabeçalhos.

Quando configurado com o modo de comunicação do end tooend SSL, o gateway de aplicativo encerra as sessões SSL Olá no gateway hello e descriptografa o tráfego do usuário. Ele aplica Olá configurado regras tooselect um back-end apropriado pool instância tooroute tráfego. Gateway de aplicativo, em seguida, inicia um novo servidor de back-end de toohello de conexão SSL e criptografa novamente dados usando o certificado de chave pública do servidor de back-end Olá antes de transmitir o back-end do hello solicitação toohello. Tooend final que SSL está habilitado, definindo a configuração de protocolo no BackendHTTPSetting tooHTTPS, que é então aplicado tooa pool de back-end. Cada servidor de back-end no pool de back-end de saudação com tooend final que SSL habilitado deve ser configurado com uma certificado tooallow uma comunicação segura.

![cenário de ssl tooend final][1]

Neste exemplo, solicitações que usam o TLS 1.2 são servidores toobackend roteadas em Pool1 usando tooend final SSL.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Encerrar tooend SSL e a lista branca de certificados

Gateway de aplicativo se comunica somente com instâncias de back-end conhecidos que têm o certificado com o gateway de aplicativo hello de na lista de permissões. tooenable lista branca de certificados, você deve carregar a chave pública de saudação do gateway de aplicativo de toohello para certificados de servidor back-end (não o certificado raiz de saudação). Somente back-ends conexões tooknown e na lista de permissões, em seguida, são permitidas. Olá restantes back-ends resulta em um erro de gateway. Os certificados autoassinados servem somente para teste e não são recomendados para cargas de trabalho de produção. Esses certificados tem toobe na lista de permissões com hello application gateway conforme descrito nas etapas anteriores para que possam ser usados de saudação.

## <a name="next-steps"></a>Próximas etapas

Depois de conhecer final tooend SSL, vá muito[habilitar final tooend SSL no gateway do aplicativo](application-gateway-end-to-end-ssl-powershell.md) toocreate um gateway de aplicativo usando finalizar tooend SSL.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
