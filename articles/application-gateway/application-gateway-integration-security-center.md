---
title: "aaaApplication integração do Gateway com a Central de segurança do Azure | Microsoft Docs"
description: "Esta página fornece informações sobre como o Gateway de Aplicativo se integra à Central de segurança do Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Visão geral da integração entre o Gateway de Aplicativo e a Central de Segurança do Azure

Saiba como o Gateway de Aplicativo e a Central de segurança ajudam a proteger os recursos do aplicativo Web. Firewall do aplicativo web do Application gateway (WAF) integra-se com [Central de segurança](../security-center/security-center-intro.md) tooprovide tooprevent uma visualização perfeita, detectar e responder a aplicativos de web toounprotected toothreats em seu ambiente.

## <a name="overview"></a>Visão geral

O WAF do Gateway de Aplicativo é uma recomendação na Central de segurança para proteger aplicativos Web contra explorações e vulnerabilidades. Recursos da Web habilitado que não estão protegidos por WAF mostram no Centro de segurança de hello como recomendações de severidade alta. Recomendações para firewalls de aplicativo da web são mostradas em Olá **visão geral** página em **aplicativos**.

![integração com a central de segurança][1]

Clicando em todas as recomendações sobre o firewall do aplicativo da web abre uma nova folha que mostra os detalhes de saudação do recomendação hello.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Adicionar um recurso existente do web aplicativo firewall tooan

Navegue muito**mais serviços** > **segurança + identidade** > **Central de segurança** e Olá **Central de segurança - visão geral**  folha, clique em **aplicativos**. Em Olá **Central de segurança - aplicativos** folha, a tabela de saudação contém uma lista de aplicativos que a Central de segurança detectada na sua assinatura.

![aplicativos Web][3]

Ao clicar em um aplicativo web com um problema crítico, você obtém Olá **integridade da segurança do aplicativo** folha. Na imagem de saudação abaixo, Olá aplicativo web que não está protegido por um firewall do aplicativo web. 

![recursos Web não protegidos][2]

Clique em **adicionar um firewall do aplicativo web** em **recomendações** tooopen Olá **adicionar um Firewall do aplicativo Web** folha.

Se você não tiver um Gateway existente do aplicativo, ou toocreate um novo, clique em **criar novo** e Olá **criar um novo Firewall do aplicativo Web** folha e clique em **Microsoft - Application Gateway**. Isso leva você através de saudação etapas toocreate um application gateway. Neste ponto, seu aplicativo Web é adicionado como um recurso protegido, agora a Central de segurança controla o que esse recurso está protegido por um firewall do aplicativo Web. Isso não o adiciona como um membro do pool de back-end.

Se você tiver um gateway de aplicativo existente, é possível escolhê-lo em **Usar solução existente**

![folha adicionar firewall do aplicativo Web][4]

Adicionar que um gateway do aplicativo web aplicativo tooan por meio da Central de segurança não adiciona recursos hello como um membro do pool de back-end, isso deve ser feito no recurso de gateway do aplicativo hello diretamente.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Adicionar um recurso tooan web aplicativo de firewall existente

Navegue muito**mais serviços** > **segurança + identidade** > **Central de segurança** e Olá **Central de segurança - visão geral**  folha, clique em **soluções de parceiros**. Mostram gateways de aplicativo com reconhecimento de Central de segurança existentes no hello **soluções de parceiros** folha.

![soluções de parceiros][7]

Clique em **aplicativo Link** tooopen Olá **aplicativos de Link** folha, aqui você terá aplicativos existentes do tooselect Olá opções. Escolha Olá tooprotect de aplicativos e clique em **Okey**. Isso não adicionar pool de back-end de toohello de aplicativos da web do hello do gateway de aplicativo hello. Isso define recursos hello como um recurso protegido para a Central de segurança possa controlá-la. recurso de saudação tooadd como um membro do pool de back-end, isso deve ser feito no gateway do aplicativo hello, folha atual Olá você pode clicar em **console de solução** toobe tomada toohello recursos de gateway de aplicativo onde você pode adicionar Olá web pool de back-end do aplicativo toohello.

![aplicativos de soluções de parceiros][6]

## <a name="finalize-configuration"></a>Finalizar a configuração

Central de segurança monitora aplicativos adicionados tooan gateway de aplicativo como um recurso protegido.  Ele monitora a integridade de saudação deste recurso e garante que ele é protegido por um application gateway. Olá próxima etapa é IP privado de saudação tooadd, IP público ou NIC de seu pool de back-end do toohello de máquina virtual do gateway de aplicativo hello. Até que isso é feito uma recomendação adicional de **finalizar a proteção do aplicativo** é exibido até que o recurso de saudação é adicionado.

![folha adicionar firewall do aplicativo Web][5]

## <a name="security-alerts"></a>Alertas de segurança

Em Central de segurança navegue muito**detecção** > **alertas de segurança**.  Aqui você encontra alertas do WAF para seus gateways de aplicativo. Os alertas são divididos pela regra do WAF.

![alertas de segurança][8]

Clicar em uma regra fornecerá uma lista de alertas para essa regra específica do WAF. Cada alerta mostra detalhes adicionais sobre como localizar hello. detalhes de saudação oferecem um gateway de aplicativo de toohello do link.
 
![detalhes do alerta][9]

## <a name="next-steps"></a>Próximas etapas

toolearn como o firewall do aplicativo web tooenable em um gateway existente do aplicativo, visite [criar ou atualizar um Gateway de aplicativo do Azure com firewall do aplicativo web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png