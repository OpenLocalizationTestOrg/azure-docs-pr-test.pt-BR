---
title: aaaCreate ou atualizar um Gateway de aplicativo do Azure com firewall do aplicativo web | Microsoft Docs
description: "Saiba como toocreate um Application Gateway com o firewall do aplicativo web usando Olá portal"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>Criar um gateway de aplicativos com o firewall do aplicativo web usando o portal de saudação

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI do Azure](application-gateway-web-application-firewall-cli.md)

Saiba como toocreate um firewall do aplicativo web habilitado gateway do aplicativo.

firewall do aplicativo web Hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão. Aplicativo Web protege contra muitos Olá OWASP top 10 web vulnerabilidades comuns.

## <a name="scenarios"></a>Cenários

Neste artigo, há dois cenários:

No primeiro cenário de saudação, você aprenderá muito[criar um gateway de aplicativos com o firewall do aplicativo web](#create-an-application-gateway-with-web-application-firewall)

No cenário de segundo hello, você aprenderá muito[adicionar web aplicativo firewall tooan existente application gateway](#add-web-application-firewall-to-an-existing-application-gateway).

![Cenário de exemplo][scenario]

> [!NOTE]
> Testes de configuração adicionais do gateway de aplicativo hello, incluindo integridade personalizado, endereços do pool de back-end e regras adicionais são configuradas após a configuração do gateway de aplicativo hello e não durante a implantação inicial.

## <a name="before-you-begin"></a>Antes de começar

O Gateway de Aplicativo do Azure requer sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implantar um aplicativo gateway tooa de sub-rede, os gateways de aplicativos adicionais só são toobe capaz de adicionar sub-rede toohello.

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Adicionar web aplicativo firewall tooan aplicativo gateway existente

Este exemplo atualiza um existente application gateway toosupport firewall do aplicativo web no modo de prevenção.

1. No portal do Azure de saudação **Favoritos** painel, clique em **todos os recursos**. Clique Olá existente do Application Gateway em Olá **todos os recursos** folha. Se a assinatura de saudação selecionado já contiver vários recursos, você pode digitar o nome de saudação em Olá **filtrar por nome...** zona DNS do hello caixa tooeasily acesso.

   ![Criação de um gateway de aplicativo][1]

1. Clique em **firewall do aplicativo Web** e atualizar as configurações de gateway de aplicativo hello. Quando concluir, clique em **Salvar**

    Olá configurações tooupdate um existente application gateway toosupport firewall do aplicativo web são:

   | **Configuração** | **Valor** | **Detalhes**
   |---|---|---|
   |**Atualizar tooWAF da camada**| Verificado | Isso define a camada de saudação da camada do hello aplicativo gateway toohello WAF.|
   |**Status do firewall**| habilitado | Essa configuração habilita o firewall do hello em Olá WAF.|
   |**Modo de firewall** | Prevenção | Essa configuração é como o firewall do aplicativo Web lida com o tráfego mal-intencionado. **Detecção de** modo somente logs de eventos hello, onde **prevenção** modo registra eventos de saudação e paradas Olá tráfego mal-intencionado.|
   |**Conjunto de regras**|3.0|Essa configuração determina Olá [principal de conjunto de regras](application-gateway-web-application-firewall-overview.md#core-rule-sets) que é usado tooprotect Olá back-end membros do pool.|
   |**Configurar regras desabilitadas**|varia|tooprevent possíveis falsos positivos, essa configuração permite que você toodisable determinados [regras e grupos de regras](application-gateway-crs-rulegroups-rules.md).|

    >[!NOTE]
    > Ao atualizar um toohello de gateway do aplicativo existente WAF SKU, Olá SKU tamanho alterações muito**médio**. Isso pode ser reconfigurado após a conclusão da configuração.

    ![folha mostrando configurações básicas][2-1]

    > [!NOTE]
    > logs de firewall de aplicativo da web tooview, diagnóstico devem ser habilitadas e ApplicationGatewayFirewallLog selecionado. É possível escolher uma contagem de instâncias de 1 para fins de teste. É importante tooknow qualquer instância de contagem em duas instâncias não é coberto por Olá SLA e, portanto, não recomendável. Os gateways pequenos não estão disponíveis ao usar o firewall do aplicativo Web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>criar um gateway de aplicativo com o firewall do aplicativo Web

Este cenário:

* Crie um gateway de aplicativo de firewall do aplicativo Web médio com duas instâncias.
* Criará uma rede virtual chamada AdatumAppGatewayVNET, com um bloco CIDR 10.0.0.0/16 reservado.
* Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.
* Configurará um certificado para descarregamento SSL.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com). Caso você ainda não tenha uma conta, poderá se inscrever para obter uma [avaliação gratuita de um mês](https://azure.microsoft.com/free)
1. No painel de favoritos saudação do portal de saudação, clique em **novo**
1. Em Olá **novo** folha, clique em **rede**. Em Olá **rede** folha, clique em **Application Gateway**, conforme mostrado no Olá a imagem a seguir:
1. Navegue toohello portal do Azure, clique em **novo** > **rede** > **Application Gateway**

    ![Criação de um gateway de aplicativo][1]

1. Em Olá **Noções básicas de** folha que aparece, digite Olá valores a seguir, clique em **Okey**:

   | **Configuração** | **Valor** | **Detalhes**
   |---|---|---|
   |**Nome**|AdatumAppGateway|nome de saudação do gateway de aplicativo hello|
   |**Camada**|WAF|Os valores disponíveis são Standard e WAF. Visite [firewall do aplicativo web](application-gateway-web-application-firewall-overview.md) toolearn mais sobre WAF.|
   |**Tamanho do SKU**|Média|As opções ao escolher a camada Standard são Pequeno, Médio e Grande. Ao escolher a camada do WAF, as opções são apenas Médio e Grande.|
   |**Contagem de instâncias**|2|Número de instâncias do gateway de aplicativo hello para alta disponibilidade. Contagens de instância iguais a 1 devem ser usadas apenas para fins de teste.|
   |**Assinatura**|[Sua assinatura]|Selecione um assinatura toocreate Olá aplicativo gateway.|
   |**Grupo de recursos**|**Criar novo:** AdatumAppGatewayRG|Crie um grupos de recursos. nome do grupo de recursos Olá deve ser exclusivo na assinatura de saudação selecionado. toolearn mais sobre grupos de recursos, leia Olá [Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) artigo de visão geral.|
   |**Localidade**|Oeste dos EUA||

   ![folha mostrando configurações básicas][2-2]

1. Em Olá **configurações** folha que aparece sob **rede Virtual**, clique em **escolha uma rede virtual**. Esta etapa abre insira Olá **rede virtual escolha** folha.  Clique em **criar novo** tooopen Olá **criar rede virtual** folha.

   ![escolher uma rede virtual][2]

1. Em Olá **criar folha de rede virtual** digite Olá valores a seguir, clique em **Okey**. Esta etapa fecha Olá **criar rede virtual** e **rede virtual escolha** folhas. Isso preenche Olá **sub-rede** campo Olá **configurações** folha com sub-rede Olá escolhido.

   |**Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Nome**|AdatumAppGatewayVNET|Nome do gateway de aplicativo hello|
   |**Espaço de Endereço**|10.0.0.0/16| Esse valor é o espaço de endereço de saudação para rede virtual Olá|
   |**Nome da sub-rede**|AppGatewaySubnet|Nome da sub-rede Olá para o gateway de aplicativo hello|
   |**Intervalo de endereços da sub-rede**|10.0.0.0/28 | Essa sub-rede permite mais sub-redes adicionais na rede virtual Olá para membros do pool de back-end|

1. Em Olá **configurações** folha sob **configuração de IP de Frontend**, escolha **pública** como Olá **tipo de endereço IP**

1. Em Olá **configurações** folha sob **endereço IP público**, clique em **escolher um endereço IP público**, essa etapa abre Olá **escolher endereço IP público**folha, clique em **criar novo**.

   ![escolher o IP público][3]

1. Em Olá **criar endereço IP público** folha, aceite o valor padrão de saudação e clique em **Okey**. Esta etapa fecha Olá **escolher endereço IP público** folha, Olá **criar endereço IP público** folha e preencher **endereço IP público** com endereço IP público Olá escolhido.

1. Em Olá **configurações** folha sob **configuração de ouvinte**, clique em **HTTP** em **protocolo**. toouse **https**, é necessário um certificado. chave privada de saudação do certificado de saudação é necessária para que uma exportação. pfx de certificado Olá precisa toobe fornecido e Olá senha para o arquivo hello.

1. Configurar Olá **WAF** configurações específicas.

   |**Configuração** | **Valor** | **Detalhes** |
   |---|---|---|
   |**Status do firewall**| habilitado| Essa configuração ativa ou desativa o WAF.|
   |**Modo de firewall** | Prevenção| Essa configuração determina as ações Olá que WAF assume tráfego mal-intencionado. Se **Detecção** for escolhido, o tráfego só será registrado em log.  Se **Prevenção** for escolhido, o tráfego será registrado em log e interrompido com uma resposta 403 Não Autorizado.|


1. Examine a página de resumo de saudação e clique em **Okey**.  Agora o gateway de aplicativo hello enfileirado e criação.

1. Depois que o gateway de aplicativo hello foi criado, navegar tooit na configuração do portal toocontinue saudação do gateway de aplicativo hello.

    ![Modo de exibição de recursos do Gateway de Aplicativo][10]

Essas etapas criam um application gateway básico com configurações padrão para o ouvinte hello, pool de back-end, configurações de http de back-end e regras. Você pode modificar essas configurações toosuit sua implantação quando Olá provisionamento é bem-sucedido

> [!NOTE]
> Gateways de aplicativo criados com a configuração de firewall de aplicativo Olá web básico são configurados com CRS 3.0 para proteção.

## <a name="next-steps"></a>Próximas etapas

Em seguida, você pode aprender como tooconfigure um alias de domínio personalizado para Olá [endereço IP público](../dns/dns-custom-domain.md#public-ip-address) usando DNS do Azure ou outro provedor DNS.

Saiba como log de diagnóstico tooconfigure, eventos de saudação toolog detectadas ou evitados com o firewall do aplicativo web visitando [diagnóstico de Gateway do aplicativo](application-gateway-diagnostics.md)

Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
