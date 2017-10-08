---
title: aaaCreate um Application Gateway - Portal do Azure | Microsoft Docs
description: "Saiba como toocreate um Application Gateway usando Olá portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>Criar um gateway de aplicativos com o portal de saudação

O [Gateway de Aplicativo](application-gateway-introduction.md) é uma solução de virtualização dedicada que fornece o ADC (controlador de entrega de aplicativos) como serviço, oferecendo várias funcionalidades de balanceamento de carga de camada 7 para o aplicativo. Este artigo o orienta por Olá etapas toocreate um Application Gateway usando Olá portal do Azure e adicionar um servidor existente como um membro de back-end.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Faça logon no toohello portal do Azure em [http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>Criar um gateway de aplicativo

toocreate um application gateway Olá concluir as etapas a seguir. O gateway de aplicativo exige sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes. Após o gateway de aplicativo hello sub-rede tooa implantado, apenas outros application gateways podem ser adicionados tooit.

1. No painel de favoritos saudação do portal de saudação, clique em **novo**
1. Em Olá **novo** folha, clique em **rede**. Em Olá **rede** folha, clique em **Application Gateway**, conforme mostrado no Olá a imagem a seguir:

    ![Criação de um gateway de aplicativo][1]

1. Em Olá **Noções básicas de** folha que aparece, digite Olá valores a seguir, clique em **Okey**:

   | **Configuração** | **Valor** | **Detalhes**|
   |---|---|---|
   |**Nome**|AdatumAppGateway|nome de saudação do gateway de aplicativo hello|
   |**Camada**|Standard|Os valores disponíveis são Standard e WAF. Visite [firewall do aplicativo web](application-gateway-web-application-firewall-overview.md) toolearn mais sobre WAF.|
   |**Tamanho do SKU**|Média|As opções ao escolher a camada Standard são Pequeno, Médio e Grande. Ao escolher a camada do WAF, as opções são apenas Médio e Grande.|
   |**Contagem de instâncias**|2|Número de instâncias do gateway de aplicativo hello para alta disponibilidade. Contagens de instância iguais a 1 devem ser usadas apenas para fins de teste.|
   |**Assinatura**|[Sua assinatura]|Selecione um assinatura toocreate Olá aplicativo gateway.|
   |**Grupo de recursos**|**Criar novo:** AdatumAppGatewayRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

1. Em Olá **configurações** folha que aparece sob **rede Virtual**, clique em **escolha uma rede virtual**. Olá **rede virtual escolha** folha é aberta.  Clique em **criar novo** tooopen Olá **criar rede virtual** folha.

   ![escolher uma rede virtual][2]

1. Em Olá **criar folha de rede virtual** digite Olá valores a seguir, clique em **Okey**. Olá **criar rede virtual** e **rede virtual escolha** folhas fechar. Essa etapa preenche Olá **sub-rede** campo Olá **configurações** folha com sub-rede Olá escolhido.

   | **Configuração** | **Valor** | **Detalhes**|
   |---|---|---|
   |**Nome**|AdatumAppGatewayVNET|Nome do gateway de aplicativo hello|
   |**Espaço de Endereço**|10.0.0.0/16|Este é o espaço de endereço de saudação para rede virtual Olá|
   |**Nome da sub-rede**|AppGatewaySubnet|Nome da sub-rede Olá para o gateway de aplicativo hello|
   |**Intervalo de endereços da sub-rede**|10.0.0.0/28|Essa sub-rede permite mais sub-redes adicionais na rede virtual Olá para membros do pool de back-end|

1. Em Olá **configurações** folha sob **configuração de IP de Frontend**, escolha **pública** como Olá **tipo de endereço IP**

1. Em hello **configurações** folha sob **endereço IP público** clique **escolher um endereço IP público**, Olá **escolher endereço IP público** abre folha , clique em **criar novo**.

   ![escolher o IP público][3]

1. Em Olá **criar endereço IP público** folha, aceite o valor padrão de saudação e clique em **Okey**. folha de saudação fecha e preenche a saudação **endereço IP público** com endereço IP público Olá escolhido.

1. Em Olá **configurações** folha sob **configuração de ouvinte**, clique em **HTTP** em **protocolo**. Digite hello porta toouse no hello **porta** campo.

2. Clique em **Okey** em Olá **configurações** toocontinue de folha.

1. Revisar configurações Olá Olá **resumo** folha e clique em **Okey** toostart criação do gateway de aplicativo hello. Criar um gateway de aplicativos é uma tarefa demorada e leva tempo toocomplete.

## <a name="add-servers-toobackend-pools"></a>Adicionar servidores toobackend pools

Depois de criar o gateway de aplicativo hello, sistemas Olá que hospedam o balanceamento de carga do hello aplicativo toobe ainda precisam de gateway de aplicativo toobe toohello adicionado. Olá endereços IP, FQDN ou NICs desses servidores são adicionados toohello pools de endereços de back-end.

### <a name="ip-address-or-fqdn"></a>Endereço IP ou FQDN

1. Com o gateway de aplicativo hello criado, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **AdatumAppGateway** application gateway em Olá folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **AdatumAppGateway** em Olá **filtrar por nome...** gateway de caixa tooeasily acesso Olá aplicativo.

1. gateway de aplicativo Hello criado é exibido. Clique em **pools de back-end**e selecione o pool de back-end atual Olá **appGatewayBackendPool**, Olá **appGatewayBackendPool** folha é aberta.

   ![Pools de back-end do Gateway de Aplicativo][4]

1. Clique em **Adicionar destino** tooadd endereços IP de valores FQDN. Escolha **IP endereço ou FQDN** como Olá **tipo** e digite o endereço IP ou FQDN no campo de saudação. Repita esta etapa para outros membros do pool de back-end. Quando terminar, clique em **Salvar**.

### <a name="virtual-machine-and-nic"></a>Máquina virtual e NIC

Também é possível adicionar NICs de máquina virtual como membros do pool de back-end. Apenas as máquinas virtuais na mesma rede virtual Olá Application Gateway estão disponíveis por meio de saudação Olá suspenso.

1. Com o gateway de aplicativo hello criado, no portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique em Olá **AdatumAppGateway** application gateway em Olá folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir **AdatumAppGateway** em Olá **filtrar por nome...** gateway de caixa tooeasily acesso Olá aplicativo.

1. gateway de aplicativo Hello criado é exibido. Clique em **pools de back-end**e selecione o pool de back-end atual Olá **appGatewayBackendPool**, Olá **appGatewayBackendPool** folha é aberta.

   ![Pools de back-end do Gateway de Aplicativo][5]

1. Clique em **Adicionar destino** tooadd endereços IP de valores FQDN. Escolha **Máquina Virtual** como Olá **tipo** e selecione máquina virtual de saudação e toouse NIC. Quando terminar, clique em **Salvar**

   > [!NOTE]
   > Apenas as máquinas virtuais em Olá mesma rede virtual como o gateway de aplicativo hello estão disponíveis na caixa suspensa hello.

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, exclua o grupo de recursos hello, gateway do aplicativo e todos os recursos relacionados. toodo, portanto, selecione o grupo de recursos de saudação da folha de gateway do aplicativo hello e clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Nesse cenário, você implantado um application gateway e adicionou um back-end do servidor toohello. Olá próximas etapas são tooconfigure gateway de aplicativo hello pela modificação das configurações e regras de ajuste no gateway hello. Essas etapas podem ser encontradas visitando Olá artigos a seguir:

Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-portal.md)

Saiba como tooprotect seus aplicativos com [Firewall do aplicativo Web](application-gateway-webapplicationfirewall-overview.md) um recurso do application gateway.

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
