---
title: "Configurar um Gateway de VPN: Portal Clássico : Azure | Microsoft Docs"
description: "Este artigo conduz você pela configuração do seu gateway de VPN da rede virtual e pela alteração de um tipo de roteamento de VPN de gateway. Estas etapas se aplicam a toohello implantação clássica modelo e hello portal clássico."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Configure um gateway VPN no portal clássico Olá 
Se você quiser toocreate uma conexão segura entre locais entre o Azure e sua localização no local, será necessário toocreate um gateway de rede virtual. Um gateway de VPN é um tipo específico de gateway de rede virtual. No modelo de implantação clássico hello, um gateway de VPN pode ser um dos dois tipos de roteamento de VPN: estática ou dinâmica. Olá, tipo VPN que você escolher depende no plano de design de rede e no dispositivo VPN local Olá deseja toouse. Para saber mais sobre dispositivos VPN, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).

**Sobre modelos de implantação do Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Visão geral de configuração
Hello etapas a seguir mostram como configurar seu gateway VPN no portal clássico do hello. Estas etapas se aplicam a toogateways para redes virtuais que foram criadas usando o modelo de implantação clássico hello. Atualmente, não todas as configurações de saudação para gateways estão disponíveis em Olá portal do Azure. Quando eles são, vamos criar um novo conjunto de instruções que se aplicam a toohello portal do Azure.

### <a name="before-you-begin"></a>Antes de começar
Antes de configurar o gateway, você precisa primeiro toocreate sua rede virtual. Para etapas toocreate uma rede virtual para conectividade entre locais, consulte [configurar uma rede virtual com uma conexão de VPN site a site](vpn-gateway-site-to-site-create.md), ou [configurar uma rede virtual com uma conexão de VPN ponto a site](vpn-gateway-point-to-site-create.md). Em seguida, usar Olá gateway VPN de saudação de tooconfigure as etapas a seguir e coletar informações de saudação precisar tooconfigure seu dispositivo VPN. 

Se você já tiver um gateway VPN e desejar que o tipo de roteamento toochange Olá VPN, consulte [como toochange Olá tipo de roteamento de VPN para o seu gateway](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Criar um gateway de VPN
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá **redes** , verifique se a coluna status Olá para sua rede virtual é **criado**.
2. Em Olá **nome** coluna, clique em nome de saudação da sua rede virtual.
3. Em Olá **painel** página, observe que esta rede não tem um gateway configurado ainda. Você verá esse status conforme você percorrer Olá etapas tooconfigure seu gateway.

![Gateway não criado](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Em seguida, na parte inferior de saudação da página de saudação, clique em **criar Gateway**. Você pode selecionar um *Roteamento Estático* ou um *Roteamento Dinâmico*. Olá tipo de roteamento de VPN selecionado depende de alguns fatores. Por exemplo, que seu dispositivo VPN dá suporte e se você precisa de conexões de ponto para site toosupport. Verificar [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md) tooverify Olá tipo de roteamento de VPN que você precisa. Depois que o gateway de saudação foi criado, você não pode alterar entre tipos de roteamento de VPN do gateway sem excluir e recriar o gateway de saudação. Quando o sistema de saudação solicita tooconfirm que você deseja Olá gateway criado, clique em **Sim**.

![Tipo de roteamento do VPN do gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Quando a criação do gateway, observe gráfico de gateway de saudação na página Olá alterações tooyellow e diz *criando Gateway*. Pode levar até too45 minutos para Olá gateway toocreate. Aguarde até que o gateway de saudação é concluída antes de você pode prosseguir com outras definições de configuração.

![Criação de gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Olá quando alterações de gateway muito*conectando*, você pode reunir informações de hello, você precisará para seu dispositivo VPN.

![Conexão de gateway](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Conexões site a site

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Etapa 1. Coletar informações de configuração do dispositivo VPN
Se você estiver criando uma conexão Site a Site, após a criação do gateway hello, colete informações de configuração do dispositivo VPN. Essas informações estão localizadas em Olá **painel** página para sua rede virtual:

1. **Endereço IP do gateway -** endereço IP hello pode ser encontrado no hello **painel** página. Você não será capaz de toosee até após seu gateway concluiu a criação.
2. **Chave compartilhada -** clique **gerenciar chave** na parte inferior da saudação da tela hello. Clique em Olá ícone próximo toohello chave toocopy-tooyour área de transferência e, em seguida, cole e salvar a chave de saudação. Observe que esse botão funcionará apenas quando houver um único túnel VPN S2S. Se você tiver vários túneis VPN S2S, use Olá *obter Gateway chave compartilhada rede Virtual* API ou cmdlet do PowerShell.

![Gerenciar Chave](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Etapa 2.  Configurar o dispositivo de VPN
Rede de local de tooan conexões site a Site requer um dispositivo VPN. Enquanto não fornecemos etapas de configuração para todos os dispositivos VPN, você pode encontrar informações de Olá Olá seguindo os links úteis:

- Para obter informações sobre os dispositivos VPN compatíveis, consulte [Dispositivos VPN](vpn-gateway-about-vpn-devices.md). 
- Links toodevice as definições de configuração, consulte [dispositivos de VPN validados](vpn-gateway-about-vpn-devices.md#devicetable). Esses links são fornecidos em uma base de melhor esforço. Sempre é melhor toocheck com o fabricante do dispositivo para obter informações de configuração mais recentes hello.
- Para obter informações sobre a edição dos exemplos de configuração do dispositivo, consulte [Edição de exemplos](vpn-gateway-about-vpn-devices.md#editing).
- Para obter os parâmetros IPsec/IKE, consulte [Parâmetros](vpn-gateway-about-vpn-devices.md#ipsec).
- Antes de configurar seu dispositivo VPN, verificar os [problemas de compatibilidade de dispositivo](vpn-gateway-about-vpn-devices.md#known) para dispositivo VPN Olá que você deseja toouse.

Ao configurar seu dispositivo VPN, você precisará Olá itens a seguir:

- Olá endereço IP público do seu gateway de rede virtual. Você pode localizar isso vai toohello **visão geral** folha para sua rede virtual.
- Uma chave compartilhada. Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site. Em nossos exemplos, usamos uma chave compartilhada muito básica. Você deve gerar um toouse chave mais complexa.

Depois que o dispositivo VPN Olá tiver sido configurado, você pode exibir suas informações de conexão atualizadas na página de painel Olá para sua rede virtual.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Etapa 3. Verificar seus intervalos de rede local e de endereços IP do gateway de VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Verificar o endereço IP do gateway de VPN
Para o gateway tooconnect corretamente, endereço IP de saudação para seu dispositivo VPN deve ser configurado corretamente para Olá rede Local que você especificou para a sua configuração entre locais. Normalmente, isso é configurado durante o processo de configuração de site a site hello. No entanto, se você tiver usado essa rede local com um dispositivo diferente ou endereço IP de saudação foi alterado para essa rede local, edite Olá configurações toospecify Olá correto endereço IP do Gateway.

1. tooverify seu endereço IP do gateway, clique em **redes** Olá painel esquerdo do portal e, em seguida, selecione **redes locais** na parte superior de saudação da página de saudação. Você verá Olá endereço de Gateway de VPN para cada rede local que você criou. endereço IP de saudação tooedit, selecione Olá VNet e clique em **editar** final Olá Olá página.
2. Em Olá **especificar detalhes da rede local** página Editar endereço IP de saudação e clique a seta Avançar Olá final Olá Olá página.
3. Em Olá **especificar espaço de endereço Olá** , clique em marca de seleção Olá no toosave direito inferior do hello suas configurações.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Verifique se os intervalos de endereços Olá para sua rede local
Para Olá tooflow de tráfego correto por meio de saudação gateway tooyour local, você precisa tooverify que cada intervalo de endereços IP seja especificado. Cada intervalo deve estar listado na sua configuração de **Redes Locais** do Azure. Dependendo da configuração de rede de saudação do seu local, isso pode ser uma tarefa um pouco grande. O tráfego que é vinculado a um endereço IP que está contido dentro de intervalos de saudação listado será enviado pelo gateway VPN de rede virtual hello. Olá intervalos que você não tenha intervalos privados toobe, embora você deva tooverify sua configuração local pode receber Olá o tráfego de entrada.

intervalos de saudação tooadd ou editar para uma rede Local, use Olá etapas a seguir:

1. intervalos de endereços IP tooedit Olá para uma rede local, clique em **redes** Olá painel esquerdo do portal e, em seguida, selecione **redes locais** na parte superior de saudação da página de saudação. No portal Olá, hello mais fácil maneira tooview Olá intervalos que você listou está na Olá **editar** página. toosee seus intervalos, selecione Olá VNet e clique em **editar** final Olá Olá página.
2. Em Olá **especificar detalhes da rede local** página, não faça nenhuma alteração. Clique a seta Avançar Olá final Olá Olá página.
3. Em Olá **especificar espaço de endereço Olá** página, faça as alterações de espaço de endereço de rede. Clique toosave de marca de seleção de saudação em sua configuração.

## <a name="how-tooview-gateway-traffic"></a>Como o tráfego de gateway tooview
Você pode exibir seu gateway e o tráfego do gateway da página **Painel** da Rede Virtual.

Em Olá **painel** página você pode exibir o seguinte hello:

* quantidade de saudação de dados que passam por meio do gateway, dados e dados.
* Olá nomes de saudação servidores DNS especificados para sua rede virtual.
* conexão de saudação entre o gateway e o dispositivo VPN.
* Olá chave que é usada tooconfigure compartilhada seu dispositivo VPN de tooyour de conexão de gateway.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Como toochange Olá tipo de roteamento de VPN para o gateway
Como algumas configurações de conectividade estão disponíveis apenas para certos tipos de roteamento de gateway, você pode achar que precisa toochange Olá gateway VPN tipo de roteamento de gateway VPN existente. Por exemplo, talvez você queira tooadd conectividade ponto a site tooan já existente site a site conexão que tem um gateway estático. As conexões ponto a site exigem um gateway dinâmico. Isso significa que uma conexão de P2S tooconfigure, você terá toochange o tipo de roteamento de VPN do gateway do toodynamic estático.

Se você precisar toochange um tipo de roteamento de VPN do gateway, vai excluir gateway existente hello e, em seguida, criar um novo gateway com o novo tipo de roteamento hello. Você não precisa toodelete Olá toda a rede virtual toochange Olá gateway tipo de roteamento.

Antes de alterar seu tipo de roteamento de VPN do gateway, ser tooverify-se de que seu dispositivo VPN dá suporte ao tipo de roteamento Olá que você deseja toouse. novos exemplos de configuração roteamento toodownload e verificação de requisitos de dispositivo VPN, consulte [sobre dispositivos VPN para conectividade de rede Virtual](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Quando você exclui um gateway VPN de rede virtual, Olá VIP atribuído toohello gateway é liberado. Quando você recriar o gateway hello, um novo VIP é atribuído tooit.
> 
> 

1. **Exclua gateway VPN existente de saudação.**
   
    Em Olá **painel** para sua rede virtual, navegue toohello inferior da página hello e em **excluir Gateway**. Aguarde a notificação de Olá Olá gateway foi excluído. Depois de receber a notificação de saudação na tela hello que o gateway foi excluído, você pode criar um novo gateway.
2. **Criar um gateway de VPN.**
   
    Use o procedimento a saudação na parte superior de saudação do hello página toocreate um novo gateway: [criar um gateway VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Próximas etapas
Você pode adicionar a rede virtual de tooyour de máquinas virtuais. Consulte [como toocreate uma máquina virtual personalizada](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Se desejar que a conexão de VPN tooconfigure uma ponto a site, consulte [configurar uma conexão de VPN ponto a site](vpn-gateway-point-to-site-create.md).

