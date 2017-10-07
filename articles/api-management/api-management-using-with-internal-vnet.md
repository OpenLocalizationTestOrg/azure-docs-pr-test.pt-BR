---
title: aaaHow toouse gerenciamento de API do Azure com rede virtual interna | Microsoft Docs
description: Saiba como toosetup e configurar o gerenciamento de API do Azure na rede virtual interna.
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: 
ms.assetid: dac28ccf-2550-45a5-89cf-192d87369bc3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8d25de14e0c0bebe7ba7b47ca432ea4e45dde312
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-api-management-service-with-internal-virtual-network"></a>Usar o serviço de Gerenciamento de API do Azure com rede virtual interna
Com redes virtuais do Azure (VNETs), gerenciamento de API pode gerenciar APIs não está acessível no hello da Internet. Um número de tecnologias de VPN é conexão de saudação toomake disponíveis e gerenciamento de API pode ser implantado em dois modos principais dentro Olá redes:
* Externo
* Interna

## <a name="overview"> </a>Visão geral
Quando o gerenciamento de API é implantado em um modo de rede interna Virtual, todos os pontos de serviço hello (gateway, portal do desenvolvedor, portal do publicador, gerenciamento direto e Git) só são visíveis dentro de uma rede Virtual que você controle o acesso ao. Nenhum dos pontos de extremidade de serviço Olá estão registrados no servidor DNS público do hello.

Usando o gerenciamento de API no modo interno, você pode obter os seguintes cenários de saudação
* Torne as APIs hospedadas em seu datacenter privado seguras e acessíveis por terceiros usando as conexões de VPN Site a Site ou ExpressRoute.
* Habilite cenários de nuvem híbrida, expondo as APIs baseadas em nuvem e as APIs locais por meio de um gateway comum.
* Gerencie suas APIs hospedadas em várias localizações geográficas usando um único ponto de extremidade de Gateway. 

## <a name="enable-vpn"> </a>Criar um Gerenciamento de API na rede virtual interna
Olá serviço de gerenciamento de API na rede interna Virtual é hospedado por trás de um Balancer(ILB) de carga interno. Olá endereço IP do hello ILB está em Olá [RFC1918](http://www.faqs.org/rfcs/rfc1918.html) intervalo.  

### <a name="enable-vnet-connection-using-azure-portal"></a>Habilitar a conexão de VNET usando o Portal do Azure
Primeiro crie o serviço de gerenciamento de API Olá seguindo as etapas de saudação [serviço de gerenciamento de API criar][Create API Management service]. Em seguida, configurar gerenciamento de API toobe implantado dentro de uma rede Virtual.

![Menu de configuração de APIM na rede virtual interna][api-management-using-internal-vnet-menu]

Após a implantação de saudação for bem-sucedida, você deve ver Olá endereço IP Virtual interno do serviço no painel de saudação.

![Painel de Gerenciamento de API com a VNET interna configurada][api-management-internal-vnet-dashboard]

### <a name="enable-vnet-connection-using-powershell-cmdlets"></a>Habilitar a conexão de VNET usando cmdlets do Powershell
Você também pode habilitar a conectividade de rede virtual usando cmdlets do PowerShell hello.

* **Criar um serviço de gerenciamento de API dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagement novo](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate um gerenciamento de API do Azure do serviço dentro de uma rede virtual e configure-o tipo de rede virtual interna Olá toouse.

* **Implantar um serviço de gerenciamento de API existente dentro de uma rede virtual**: usar o cmdlet Olá [AzureRmApiManagementDeployment atualização](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove um gerenciamento de API do Azure existente de serviço dentro de uma rede Virtual e configurá-lo toouse Tipo de rede virtual interno.

## <a name="apim-dns-configuration"></a>Configuração de DNS
Ao usar o Gerenciamento de API em modo de rede virtual externa, o DNS é gerenciado pelo Azure. Para o modo de rede Virtual interna, você tem toomanage seu próprio DNS.

> [!NOTE]
> Serviço de gerenciamento de API não escuta toorequests provenientes de endereços IP. Ele responde apenas toorequests toohello nome de host configurado em seus pontos de extremidade de serviço (que inclui o gateway, portal do desenvolvedor, Portal do publicador, ponto de extremidade de gerenciamento direto e git).

### <a name="access-on-default-host-names"></a>Acesso em nomes de host padrão:
Quando você cria um serviço de gerenciamento de API na nuvem do Azure pública, chamado "contoso" por exemplo, hello seguintes pontos de extremidade de serviço são configurados por padrão.

>   Gateway/Proxy: contoso.azure-api.net

> Portal do Editor e Portal do desenvolvedor: contoso.portal.azure-api.net

> Ponto de extremidade de gerenciamento direto: contoso.management.azure-api.net

>   GIT: contoso.scm.azure-api.net

tooaccess esses pontos de extremidade de serviço de gerenciamento de API, você pode criar uma máquina Virtual em uma rede de Virtual toohello conectado de sub-rede em que o gerenciamento de API é implantado. Supondo que Olá interno endereço IP Virtual para o serviço 10.0.0.5, você pode fazer Olá mapeamento de arquivo de hosts (% SystemDrive%\drivers\etc\hosts) da seguinte maneira:

> 10.0.0.5    contoso.azure-api.net

> 10.0.0.5    contoso.portal.azure-api.net

> 10.0.0.5    contoso.management.azure-api.net

> 10.0.0.5    contoso.scm.azure-api.net

Você pode acessar todos os pontos de extremidade de serviço de saudação do hello Máquina Virtual que você criou. Se usar um servidor DNS personalizado em uma rede virtual, você também pode criar registros A de DNS e acessar esses pontos de extremidade de qualquer lugar em sua rede virtual. 

### <a name="access-on-custom-domain-names"></a>Acessar em nomes de domínio personalizados:
Se você não quiser Olá tooaccess serviço de gerenciamento de API com nomes de host padrão hello, você pode configurar os nomes de domínio personalizados para todos os seus pontos de extremidade serviço como abaixo

![Configurar o domínio personalizado para Gerenciamento de API][api-management-custom-domain-name]

Em seguida, você pode criar registros em seu servidor DNS tooaccess esses pontos de extremidade que só podem ser acessados de dentro de sua rede Virtual.

## <a name="related-content"> </a>Conteúdo relacionado
* [Problemas comuns de configuração de rede durante a configuração de APIM na VNET][Common Network Configuration Issues]
* [Perguntas frequentes sobre rede virtual](../virtual-network/virtual-networks-faq.md)
* [Criar registro A no DNS](https://msdn.microsoft.com/en-us/library/bb727018.aspx)

[api-management-using-internal-vnet-menu]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-menu.png
[api-management-internal-vnet-dashboard]: ./media/api-management-using-with-internal-vnet/api-management-internal-vnet-dashboard.png
[api-management-custom-domain-name]: ./media/api-management-using-with-internal-vnet/api-management-custom-domain-name.png

[Create API Management service]: api-management-get-started.md#create-service-instance
[Common Network Configuration Issues]: api-management-using-with-vnet.md#network-configuration-issues
