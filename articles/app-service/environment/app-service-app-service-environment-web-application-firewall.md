---
title: "Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo"
description: "Saiba como configurar um firewall de aplicativo Web no Ambiente do Serviço de Aplicativo."
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/17/2016
ms.author: naziml
ms.custom: mvc
ms.openlocfilehash: bfe36ee5365e71db4280e8e2ccff6db8e552dd39
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configurando um WAF (Firewall do Aplicativo Web) para Ambiente do Serviço de Aplicativo
## <a name="overview"></a>Visão geral
Os firewalls do aplicativo Web, como o [Barracuda WAF para Azure](https://www.barracuda.com/programs/azure), que estão disponíveis no [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/), ajudam a proteger aplicativos Web ao inspecionar o tráfego de entrada da Web para bloquear injeções de SQL, Cross-Site Scripting (script entre sites), carregamentos de malware e DDoS de aplicativo, além de outros ataques. Ele também inspeciona as respostas dos servidores Web back-end para DLP (Prevenção contra Perda de Dados). Combinado com o isolamento e a escala adicional fornecidos pelos Ambientes do Serviço de Aplicativo, esse recurso fornece um ambiente ideal para hospedar aplicativos Web críticos que precisam resistir às solicitações mal-intencionadas e ao tráfego de alto volume.

[!INCLUDE [app-service-web-to-api-and-mobile](../../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configuração
Neste documento, configuramos nosso Ambiente do Serviço de Aplicativo por trás de várias instâncias balanceadas por carga do Barracuda WAF, de modo que somente o tráfego do WAF possa chegar ao Ambiente do Serviço de Aplicativo e que este não possa ser acessado da DMZ. Também temos o Gerenciador de Tráfego do Azure em nossas instâncias do Barracuda WAF para balancear carga entre os datacenters e regiões do Azure. Um diagrama de alto nível da configuração seria semelhante à seguinte imagem:

![Arquitetura][Architecture] 

> [!NOTE]
> Com a introdução do [suporte ILB para o Ambiente do Serviço de Aplicativo](app-service-environment-with-internal-load-balancer.md), você pode configurar o ASE para ser acessado da DMZ e estar disponível apenas para a rede privada. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configurando o Ambiente do Serviço de Aplicativo
Para configurar um Ambiente do Serviço de Aplicativo , consulte a [nossa documentação](app-service-web-how-to-create-an-app-service-environment.md) sobre o assunto. Depois que você criar um Ambiente do Serviço de Aplicativo, será possível criar Aplicativos Web, Aplicativos de API e [Aplicativos Móveis](../../app-service-mobile/app-service-mobile-value-prop.md) nesse ambiente e todos eles serão protegidos pelo WAF que configuraremos na próxima seção.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configurando o Serviço de Nuvem Barracuda WAF
O Barracuda tem um [artigo detalhado](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sobre como implantar seu WAF em uma máquina virtual no Azure. Mas como queremos redundância, e não introduzir um único ponto de falha, você quer implantar pelo menos duas VMs da instância WAF no mesmo Serviço de Nuvem ao seguir estas instruções.

### <a name="adding-endpoints-to-cloud-service"></a>Adicionando pontos de extremidade ao Serviço de Nuvem
Depois que você tiver 2 ou mais instâncias da VM WAF no seu Serviço de Nuvem, será possível usar o [portal do Azure](https://portal.azure.com/) para adicionar pontos de extremidade HTTP e HTTPS, que são usados pelo seu aplicativo conforme mostrado na seguinte imagem:

![Configurar ponto de extremidade][ConfigureEndpoint]

Se seus aplicativos usam outros pontos de extremidade, certifique-se de adicioná-los também a esta lista. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configuração do Barracuda WAF por meio do Portal de Gerenciamento
O Barracuda WAF usa a porta TCP 8000 para configuração por meio do respectivo portal de gerenciamento. Se você tiver várias instâncias de VMs de WAF, será necessário repetir as etapas para cada instância de VM. 

> [!NOTE]
> Depois que tiver finalizado a configuração do WAF, remova o ponto de extremidade TCP/8000 de todas as suas VMs de WAF para manter o WAF protegido.
> 
> 

Adicione o ponto de extremidade de gerenciamento, conforme mostrado na imagem a seguir, para configurar o seu Barracuda WAF.

![Adicionar ponto de extremidade de gerenciamento][AddManagementEndpoint]

Use um navegador para navegar até o ponto de extremidade de gerenciamento no Serviço de Nuvem. Se seu Serviço de Nuvem se chamar test.cloudapp.net, você poderá acessar esse ponto de extremidade navegando até http://test.cloudapp.net:8000. Você deve ver uma página de logon conforme a imagem a seguir em que poderá fazer logon usando as credenciais que você especificou na fase de configuração da VM do WAF.

![Página de logon de gerenciamento][ManagementLoginPage]

depois de fazer logon, você deverá visualizar um painel, conforme a imagem a seguir, que apresenta as estatísticas básicas sobre a proteção do WAF.

![Painel de gerenciamento][ManagementDashboard]

Ao clicar em **Serviços**, você poderá configurar o WAF para os serviços que estiver protegendo. Para mais detalhes sobre a configuração do seu Barracuda WAF, consulte [a respectiva documentação](https://techlib.barracuda.com/waf/getstarted1). No exemplo a seguir, foi configurado um Aplicativo Web do Azure que atende tráfego em HTTP e HTTPS.

![Adicionar de gerenciamento de serviços][ManagementAddServices]

> [!NOTE]
> Dependendo de como os aplicativos são configurados e de quais recursos estão sendo usados no Ambiente do Serviço de Aplicativo, você precisará encaminhar o tráfego para portas TCP que não sejam a 80 e a 443, por exemplo, se você tiver IP SSL configurada para um Aplicativo Web. Para obter uma lista de portas de rede usadas nos Ambientes do Serviço de Aplicativo, consulte a seção Portas de Rede da [documentação sobre como Controlar Tráfego de Entrada](app-service-app-service-environment-control-inbound-traffic.md) .
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configurando o Gerenciador de Tráfego do Microsoft Azure (OPCIONAL)
Se seu aplicativo estiver disponível em várias regiões, convém balancear a carga dele no [Gerenciador de Tráfego do Azure](../../traffic-manager/traffic-manager-overview.md). Para isso, é possível adicionar um ponto de extremidade no [Portal do Azure](https://portal.azure.com) usando o nome do Serviço de Nuvem do seu WAF no perfil do Gerenciador de Tráfego, como mostrado na imagem a seguir. 

![Ponto de extremidade do Gerenciador de Tráfego][TrafficManagerEndpoint]

Se seu aplicativo exigir autenticação, certifique-se de que você tem algum recurso que não exija autenticação para que o Gerenciador de Tráfego execute ping pela disponibilidade do seu aplicativo. Você pode configurar o URL na página **Configuração** no [Portal do Azure](https://portal.azure.com), conforme mostrado na imagem a seguir:

![Configurar o Gerenciador de Tráfego][ConfigureTrafficManager]

Para encaminhar os pings do Gerenciador de Tráfego do seu WAF para o aplicativo, é preciso configurar Website Translations no Barracuda WAF, a fim de encaminhar o tráfego para o aplicativo, conforme mostrado no exemplo a seguir:

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-to-app-service-environment-using-network-security-groups-nsg"></a>Protegendo o tráfego do Ambiente do Serviço de Aplicativo usando NSGs (grupos de segurança de rede)
Siga a [documentação sobre como controlar o tráfego de entrada](app-service-app-service-environment-control-inbound-traffic.md) para obter detalhes sobre como restringir o tráfego para o Ambiente do Serviço de Aplicativo do WAF apenas usando o endereço VIP do Serviço de Nuvem. Veja um exemplo de comando do PowerShell para executar essa tarefa para a porta TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Substitua SourceAddressPrefix pelo VIP (Endereço IP Virtual) do Serviço de Nuvem do seu WAF.

> [!NOTE]
> O VIP do Serviço de Nuvem muda quando você exclui e recria o Serviço de Nuvem. Certifique-se de atualizar o endereço IP no grupo de recursos de rede depois de fazer isso. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
