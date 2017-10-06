---
title: aaaConfigure SSL descarregar - Gateway de aplicativo do Azure - Portal do Azure | Microsoft Docs
description: "Esta página fornece instruções toocreate descarregar um application gateway com SSL usando o portal de saudação"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a>Configure um gateway de aplicativo para descarregamento SSL usando o portal de saudação

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-ssl-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [CLI 2.0 do Azure](application-gateway-ssl-cli.md)

Gateway de aplicativo do Azure pode ser configurado tooterminate Olá Secure Sockets Layer (SSL) sessão Olá gateway tooavoid cara SSL descriptografia tarefas toohappen no farm de web hello. Descarregamento SSL também simplifica a configuração de servidor front-end do hello e gerenciamento de aplicativo da web hello.

## <a name="scenario"></a>Cenário

Olá cenário a seguir vai pela configuração de descarregamento de SSL em um gateway existente do aplicativo. Olá cenário pressupõe que você já seguiu as etapas de saudação muito[criar um Application Gateway](application-gateway-create-gateway-portal.md).

## <a name="before-you-begin"></a>Antes de começar

Descarregamento SSL tooconfigure com um gateway de aplicativo, é necessário um certificado. Esse certificado é carregado no gateway do aplicativo hello e usado tooencrypt e descriptografar o tráfego de saudação enviado através de SSL. certificado Olá precisa toobe no formato de troca de informações pessoais (pfx). Esse formato de arquivo permite Olá privada toobe chave exportado que é exigido pelo Olá application gateway tooperform Olá criptografia e a descriptografia de tráfego.

## <a name="add-an-https-listener"></a>Adicionar um ouvinte HTTPS

Ouvinte HTTPS Olá procura o tráfego com base em sua configuração e ajuda a pools de back-end rota Olá tráfego toohello.

### <a name="step-1"></a>Etapa 1

Navegue toohello portal do Azure e selecione um gateway existente do aplicativo

### <a name="step-2"></a>Etapa 2

Clique em ouvintes e Olá adicionar botão tooadd um ouvinte.

![folha de visão geral do gateway de aplicativo][1]

### <a name="step-3"></a>Etapa 3

Preencha Olá informações necessárias para o ouvinte de saudação e upload hello. pfx do certificado, quando concluída em Okey.

**Nome** -esse valor é um nome amigável do ouvinte de saudação.

**Configuração de IP de Frontend** -este valor é a configuração de IP de front-end Olá que é usada para o ouvinte de saudação.

**Porta de front-end (nome/porta)** -um nome amigável para a porta Olá usada no front-end do gateway de aplicativo hello e porta real de saudação usada hello.

**Protocolo** -toodetermine um comutador se http ou https é usado para o front-end hello.

**Certificado (Nome/Senha)** : se o descarregamento SSL for usado, um certificado .pfx for exigido para essa configuração, serão necessários um nome amigável e uma senha.

![folha adicionar ouvinte][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a>Criar uma regra e associá-lo toohello ouvinte

ouvinte de saudação foi criado. É hora toocreate um regra toohandle Olá o tráfego do ouvinte de saudação. As regras definem como o tráfego é roteado toohello pools de back-end com base em várias configurações, incluindo se a afinidade de sessão baseada em cookie é usada, protocolo, porta e investigações de integridade.

### <a name="step-1"></a>Etapa 1

Clique em Olá **regras** do gateway de aplicativo hello e, em seguida, clique em Adicionar.

![folha de regras do gateway de aplicativo][3]

### <a name="step-2"></a>Etapa 2

Em Olá **Adicionar regra básica** folha, digite Olá o nome amigável para a regra de saudação e escolha o ouvinte Olá criado na etapa anterior hello. Escolha o pool de back-end apropriado hello e configuração de http e clique em **Okey**

![janela de configurações de https][4]

configurações de saudação agora são salvas toohello gateway de aplicativo. Olá processo para essas configurações de gravação pode demorar um pouco antes de serem tooview disponível por meio do portal hello, ou por meio do PowerShell. Gateway de aplicativo de uma vez salvo Olá lida com criptografia hello e a descriptografia de tráfego. Todo o tráfego entre o gateway do aplicativo hello e servidores de web de back-end hello será tratado por http. Qualquer cliente de toohello back comunicação se iniciada via https será retornado toohello cliente criptografado.

## <a name="next-steps"></a>Próximas etapas

toolearn como tooconfigure uma integridade personalizado teste com o Gateway de aplicativo do Azure, consulte [criar um teste de integridade personalizado](application-gateway-create-gateway-portal.md).

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
