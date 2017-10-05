---
title: Gateway de dados local | Microsoft Docs
description: "Um gateway local será necessário se o servidor do Analysis Services no Azure for se conectar a fontes de dados locais."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: 514b5404e8cbfa0baa657eb41736e20cad502638
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connecting-to-on-premises-data-sources-with-azure-on-premises-data-gateway"></a><span data-ttu-id="e76cb-103">Conectar-se a fontes de dados locais com o Gateway de Dados Local do Azure</span><span class="sxs-lookup"><span data-stu-id="e76cb-103">Connecting to on-premises data sources with Azure On-premises Data Gateway</span></span>
<span data-ttu-id="e76cb-104">O gateway de dados local atua como uma ponte, fornecendo transferência de dados segura entre fontes de dados locais e seus servidores do Azure Analysis Services na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e76cb-104">The on-premises data gateway acts as a bridge, providing secure data transfer between on-premises data sources and your Azure Analysis Services servers in the cloud.</span></span> <span data-ttu-id="e76cb-105">Além de trabalhar com diversos servidores do Azure Analysis Services na mesma região, a versão mais recente do gateway também funciona com os Aplicativos Lógicos do Azure, o Power BI, o Power Apps e o Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="e76cb-105">In addition to working with multiple Azure Analysis Services servers in the same region, the latest version of the gateway also works with Azure Logic Apps, Power BI, Power Apps, and Microsoft Flow.</span></span> <span data-ttu-id="e76cb-106">Você pode associar vários serviços na mesma região a um único gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-106">You can associate multiple services in the same region with a single gateway.</span></span> 

 <span data-ttu-id="e76cb-107">O Azure Analysis Services exige um recurso de gateway na mesma região.</span><span class="sxs-lookup"><span data-stu-id="e76cb-107">Azure Analysis Services requires a gateway resource in the same region.</span></span> <span data-ttu-id="e76cb-108">Por exemplo, se você tiver servidores do Azure Analysis Services na região Leste dos EUA 2, será necessário um recurso de gateway na região Leste dos EUA 2.</span><span class="sxs-lookup"><span data-stu-id="e76cb-108">For example, if you have Azure Analysis Services servers in the East US 2 region, you need a gateway resource in the East US 2 region.</span></span> <span data-ttu-id="e76cb-109">Vários servidores no Leste dos EUA 2 podem usar o mesmo gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-109">Multiple servers in East US 2 can use the same gateway.</span></span>

<span data-ttu-id="e76cb-110">Instalar o gateway pela primeira vez é um processo de quatro partes:</span><span class="sxs-lookup"><span data-stu-id="e76cb-110">Getting setup with the gateway the first time is a four-part process:</span></span>

- <span data-ttu-id="e76cb-111">**Baixar e executar a instalação** – esta etapa instala um serviço de gateway em um computador em sua organização.</span><span class="sxs-lookup"><span data-stu-id="e76cb-111">**Download and run setup** - This step installs a gateway service on a computer in your organization.</span></span>

- <span data-ttu-id="e76cb-112">**Registrar seu gateway** – nesta etapa, você especifica um nome e uma chave de recuperação para o gateway e seleciona uma região, registrando o gateway no Serviço de Nuvem do Gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-112">**Register your gateway** - In this step, you specify a name and recovery key for your gateway, and select a region, registering your gateway with the Gateway Cloud Service.</span></span>

- <span data-ttu-id="e76cb-113">**Criar um recurso de gateway no Azure** – nesta etapa, você cria um recurso de gateway em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-113">**Create a gateway resource in Azure** - In this step, you create a gateway resource in your Azure subscription.</span></span>

- <span data-ttu-id="e76cb-114">**Conectar os servidores ao recurso de gateway** – assim que tiver um recurso de gateway em sua assinatura, você pode começar a conectar seus servidores a ele.</span><span class="sxs-lookup"><span data-stu-id="e76cb-114">**Connect your servers to your gateway resource** - Once you have a gateway resource in your subscription, you can begin connecting your servers to it.</span></span>

<span data-ttu-id="e76cb-115">Quando seu recurso de gateway estiver configurado para sua assinatura, você poderá conectar vários servidores e outros serviços a ele.</span><span class="sxs-lookup"><span data-stu-id="e76cb-115">Once you have a gateway resource configured for your subscription, you can connect multiple servers, and other services to it.</span></span> <span data-ttu-id="e76cb-116">Você só precisará instalar um gateway diferente e criar recursos de gateway adicionais se tiver servidores ou outros serviços em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="e76cb-116">You only need to install a different gateway and create additional gateway resources if you have servers or other services in a different region.</span></span>

<span data-ttu-id="e76cb-117">Para começar imediatamente, consulte [Instalar e configurar gateway de dados local](analysis-services-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="e76cb-117">To get started right away, see [Install and configure on-premises data gateway](analysis-services-gateway-install.md).</span></span>

## <span data-ttu-id="e76cb-118"><a name="how-it-works"> </a>Como funciona</span><span class="sxs-lookup"><span data-stu-id="e76cb-118"><a name="how-it-works"> </a>How it works</span></span>
<span data-ttu-id="e76cb-119">O gateway que você instala em um computador de sua organização é executado como um serviço Windows, o **Gateway de dados local**.</span><span class="sxs-lookup"><span data-stu-id="e76cb-119">The gateway you install on a computer in your organization runs as a Windows service, **On-premises data gateway**.</span></span> <span data-ttu-id="e76cb-120">Esse serviço local é registrado no Serviço de Nuvem do Gateway por meio do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-120">This local service is registered with the Gateway Cloud Service through Azure Service Bus.</span></span> <span data-ttu-id="e76cb-121">Em seguida, você cria um Serviço de Nuvem do Gateway do recurso de gateway para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-121">You then create a gateway resource Gateway Cloud Service for your Azure subscription.</span></span> <span data-ttu-id="e76cb-122">Seus servidores do Azure Analysis Services são, então, conectados ao recurso de gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-122">Your Azure Analysis Services servers are then connected to your gateway resource.</span></span> <span data-ttu-id="e76cb-123">Quando modelos em seu servidor precisarem se conectar às fontes de dados locais para consultas ou processamento, um fluxo de dados e consultas atravessará o recurso de gateway, o Barramento de Serviço do Azure, o serviço de gateway de dados local e suas fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="e76cb-123">When models on your server need to connect to your on-premises data sources for queries or processing, a query and data flow traverses the gateway resource, Azure Service Bus, the local on-premises data gateway service, and your data sources.</span></span> 

![Como ele funciona](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

<span data-ttu-id="e76cb-125">Fluxo de dados e consultas:</span><span class="sxs-lookup"><span data-stu-id="e76cb-125">Queries and data flow:</span></span>

1. <span data-ttu-id="e76cb-126">Uma consulta é criada pelo serviço de nuvem com as credenciais criptografadas para a fonte de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-126">A query is created by the cloud service with the encrypted credentials for the on-premises data source.</span></span> <span data-ttu-id="e76cb-127">Ela é enviada para uma fila de processamento do gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-127">It's then sent to a queue for the gateway to process.</span></span>
2. <span data-ttu-id="e76cb-128">O serviço de nuvem do gateway analisa a consulta e envia a solicitação para o [Barramento de Serviço do Azure](https://azure.microsoft.com/documentation/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="e76cb-128">The gateway cloud service analyzes the query and pushes the request to the [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).</span></span>
3. <span data-ttu-id="e76cb-129">O gateway de dados local sonda o Barramento de Serviço do Azure para verificar solicitações pendentes.</span><span class="sxs-lookup"><span data-stu-id="e76cb-129">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>
4. <span data-ttu-id="e76cb-130">O gateway obtém a consulta, descriptografa as credenciais e conecta-se às fontes de dados com essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="e76cb-130">The gateway gets the query, decrypts the credentials, and connects to the data sources with those credentials.</span></span>
5. <span data-ttu-id="e76cb-131">O gateway envia a consulta à fonte de dados para execução.</span><span class="sxs-lookup"><span data-stu-id="e76cb-131">The gateway sends the query to the data source for execution.</span></span>
6. <span data-ttu-id="e76cb-132">Os resultados são enviados da fonte de dados de volta para o gateway e, em seguida, para o serviço de nuvem e seu servidor.</span><span class="sxs-lookup"><span data-stu-id="e76cb-132">The results are sent from the data source, back to the gateway, and then onto the cloud service and your server.</span></span>

## <span data-ttu-id="e76cb-133"><a name="windows-service-account"> </a>Conta de Serviço Windows</span><span class="sxs-lookup"><span data-stu-id="e76cb-133"><a name="windows-service-account"> </a>Windows Service account</span></span>
<span data-ttu-id="e76cb-134">O gateway de dados local é configurado para usar *NT SERVICE\PBIEgwService* para as credenciais de logon de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="e76cb-134">The on-premises data gateway is configured to use *NT SERVICE\PBIEgwService* for the Windows service logon credential.</span></span> <span data-ttu-id="e76cb-135">Por padrão, ele tem o direito de Fazer logon como um serviço; no contexto da máquina na qual você está instalando o gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-135">By default, it has the right of Logon as a service; in the context of the machine that you are installing the gateway on.</span></span> <span data-ttu-id="e76cb-136">Essa credencial não é da mesma conta usada para se conectar às fontes de dados locais ou da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-136">This credential is not the same account used to connect to on-premises data sources or your Azure account.</span></span>  

<span data-ttu-id="e76cb-137">Se você encontrar problemas com o servidor proxy devido à autenticação, convém alterar a conta de serviço do Windows para um usuário de domínio ou conta de serviço gerenciado.</span><span class="sxs-lookup"><span data-stu-id="e76cb-137">If you encounter issues with your proxy server due to authentication, you may want to change the Windows service account to a domain user or managed service account.</span></span>

## <span data-ttu-id="e76cb-138"><a name="ports"> </a>Portas</span><span class="sxs-lookup"><span data-stu-id="e76cb-138"><a name="ports"> </a>Ports</span></span>
<span data-ttu-id="e76cb-139">O gateway cria uma conexão de saída para o Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-139">The gateway creates an outbound connection to Azure Service Bus.</span></span> <span data-ttu-id="e76cb-140">Ele se comunica nas portas de saída: TCP 443 (padrão), 5671, 5672, 9350 a 9354.</span><span class="sxs-lookup"><span data-stu-id="e76cb-140">It communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span>  <span data-ttu-id="e76cb-141">O gateway não exige portas de entrada.</span><span class="sxs-lookup"><span data-stu-id="e76cb-141">The gateway does not require inbound ports.</span></span>

<span data-ttu-id="e76cb-142">Recomendamos a inclusão dos endereços IP em uma lista de permissões para a região de dados em seu firewall.</span><span class="sxs-lookup"><span data-stu-id="e76cb-142">We recommend you whitelist the IP addresses for your data region in your firewall.</span></span> <span data-ttu-id="e76cb-143">Baixe a [lista de IPs de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="e76cb-143">You can download the [Microsoft Azure Datacenter IP list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="e76cb-144">A lista é atualizada semanalmente.</span><span class="sxs-lookup"><span data-stu-id="e76cb-144">This list is updated weekly.</span></span>

> [!NOTE]
> <span data-ttu-id="e76cb-145">Os Endereços IP listados na lista de IP de Datacenter do Azure estão em notação CIDR.</span><span class="sxs-lookup"><span data-stu-id="e76cb-145">The IP Addresses listed in the Azure Datacenter IP list are in CIDR notation.</span></span> <span data-ttu-id="e76cb-146">Por exemplo, 10.0.0.0/24 significa 10.0.0.0 a 10.0.0.24.</span><span class="sxs-lookup"><span data-stu-id="e76cb-146">For example, 10.0.0.0/24 does not mean 10.0.0.0 through 10.0.0.24.</span></span> <span data-ttu-id="e76cb-147">Saiba mais sobre a [notação CIDR ](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="e76cb-147">Learn more about the [CIDR notation](http://whatismyipaddress.com/cidr).</span></span>
>
>

<span data-ttu-id="e76cb-148">Veja a seguir os nomes de domínio totalmente qualificados usados pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-148">The following are the fully qualified domain names used by the gateway.</span></span>

| <span data-ttu-id="e76cb-149">Nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="e76cb-149">Domain names</span></span> | <span data-ttu-id="e76cb-150">Portas de saída</span><span class="sxs-lookup"><span data-stu-id="e76cb-150">Outbound ports</span></span> | <span data-ttu-id="e76cb-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="e76cb-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e76cb-152">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="e76cb-152">*.powerbi.com</span></span> |<span data-ttu-id="e76cb-153">80</span><span class="sxs-lookup"><span data-stu-id="e76cb-153">80</span></span> |<span data-ttu-id="e76cb-154">HTTP usado para baixar o instalador.</span><span class="sxs-lookup"><span data-stu-id="e76cb-154">HTTP used to download the installer.</span></span> |
| <span data-ttu-id="e76cb-155">*.powerbi.com</span><span class="sxs-lookup"><span data-stu-id="e76cb-155">*.powerbi.com</span></span> |<span data-ttu-id="e76cb-156">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-156">443</span></span> |<span data-ttu-id="e76cb-157">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-157">HTTPS</span></span> |
| <span data-ttu-id="e76cb-158">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-158">*.analysis.windows.net</span></span> |<span data-ttu-id="e76cb-159">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-159">443</span></span> |<span data-ttu-id="e76cb-160">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-160">HTTPS</span></span> |
| <span data-ttu-id="e76cb-161">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-161">*.login.windows.net</span></span> |<span data-ttu-id="e76cb-162">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-162">443</span></span> |<span data-ttu-id="e76cb-163">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-163">HTTPS</span></span> |
| <span data-ttu-id="e76cb-164">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-164">*.servicebus.windows.net</span></span> |<span data-ttu-id="e76cb-165">5671-5672</span><span class="sxs-lookup"><span data-stu-id="e76cb-165">5671-5672</span></span> |<span data-ttu-id="e76cb-166">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="e76cb-166">Advanced Message Queuing Protocol (AMQP)</span></span> |
| <span data-ttu-id="e76cb-167">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-167">*.servicebus.windows.net</span></span> |<span data-ttu-id="e76cb-168">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="e76cb-168">443, 9350-9354</span></span> |<span data-ttu-id="e76cb-169">Ouvintes de Retransmissão do Barramento de Serviço por meio de TCP (requer 443 para aquisição de token de Controle de Acesso)</span><span class="sxs-lookup"><span data-stu-id="e76cb-169">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> |
| <span data-ttu-id="e76cb-170">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-170">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="e76cb-171">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-171">443</span></span> |<span data-ttu-id="e76cb-172">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-172">HTTPS</span></span> |
| <span data-ttu-id="e76cb-173">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e76cb-173">*.core.windows.net</span></span> |<span data-ttu-id="e76cb-174">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-174">443</span></span> |<span data-ttu-id="e76cb-175">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-175">HTTPS</span></span> |
| <span data-ttu-id="e76cb-176">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="e76cb-176">login.microsoftonline.com</span></span> |<span data-ttu-id="e76cb-177">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-177">443</span></span> |<span data-ttu-id="e76cb-178">HTTPS</span><span class="sxs-lookup"><span data-stu-id="e76cb-178">HTTPS</span></span> |
| <span data-ttu-id="e76cb-179">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="e76cb-179">*.msftncsi.com</span></span> |<span data-ttu-id="e76cb-180">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-180">443</span></span> |<span data-ttu-id="e76cb-181">Usado para testar a conectividade com a Internet se o gateway não poder ser acessado pelo serviço do Power BI.</span><span class="sxs-lookup"><span data-stu-id="e76cb-181">Used to test internet connectivity if the gateway is unreachable by the Power BI service.</span></span> |
| <span data-ttu-id="e76cb-182">*.microsoftonline p.com</span><span class="sxs-lookup"><span data-stu-id="e76cb-182">*.microsoftonline-p.com</span></span> |<span data-ttu-id="e76cb-183">443</span><span class="sxs-lookup"><span data-stu-id="e76cb-183">443</span></span> |<span data-ttu-id="e76cb-184">Usado para autenticação, dependendo da configuração.</span><span class="sxs-lookup"><span data-stu-id="e76cb-184">Used for authentication depending on configuration.</span></span> |

### <span data-ttu-id="e76cb-185"><a name="force-https"></a>Forçar comunicação HTTPS com o Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="e76cb-185"><a name="force-https"></a>Forcing HTTPS communication with Azure Service Bus</span></span>
<span data-ttu-id="e76cb-186">Você pode forçar o gateway para se comunicar com o Barramento de Serviço do Azure usando HTTPS em vez de TCP direto; no entanto, fazer isso pode reduzir consideravelmente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e76cb-186">You can force the gateway to communicate with Azure Service Bus by using HTTPS instead of direct TCP; however, doing so can greatly reduce performance.</span></span> <span data-ttu-id="e76cb-187">Você pode modificar o arquivo *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* alterando o valor de `AutoDetect` para `Https`.</span><span class="sxs-lookup"><span data-stu-id="e76cb-187">You can modify the *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* file by changing the value from `AutoDetect` to `Https`.</span></span> <span data-ttu-id="e76cb-188">Normalmente, esse arquivo fica localizado em *C:\Arquivos de Programas\Gateway de dados local*.</span><span class="sxs-lookup"><span data-stu-id="e76cb-188">This file is typically located at *C:\Program Files\On-premises data gateway*.</span></span>

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <span data-ttu-id="e76cb-189"><a name="faq"></a>Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="e76cb-189"><a name="faq"></a>Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="e76cb-190">Geral</span><span class="sxs-lookup"><span data-stu-id="e76cb-190">General</span></span>

<span data-ttu-id="e76cb-191">**P**: Preciso de um gateway para fontes de dados na nuvem, como o Banco de Dados SQL do Azure?</span><span class="sxs-lookup"><span data-stu-id="e76cb-191">**Q**: Do I need a gateway for data sources in the cloud, such as Azure SQL Database?</span></span> <br/><span data-ttu-id="e76cb-192">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="e76cb-192">
**A**: No.</span></span> <span data-ttu-id="e76cb-193">Um gateway conecta-se apenas a fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="e76cb-193">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="e76cb-194">**Pergunta**: O gateway precisa ser instalado no mesmo computador que a fonte de dados?</span><span class="sxs-lookup"><span data-stu-id="e76cb-194">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="e76cb-195">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="e76cb-195">
**A**: No.</span></span> <span data-ttu-id="e76cb-196">O gateway se conecta à fonte de dados usando as informações de conexão que foram fornecidas.</span><span class="sxs-lookup"><span data-stu-id="e76cb-196">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="e76cb-197">Considere o gateway como um aplicativo de cliente nesse sentido.</span><span class="sxs-lookup"><span data-stu-id="e76cb-197">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="e76cb-198">O gateway precisa apenas da capacidade de se conectar ao nome do servidor que foi fornecido, geralmente na mesma rede.</span><span class="sxs-lookup"><span data-stu-id="e76cb-198">The gateway just needs the capability to connect to the server name that was provided, typically on the same network.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="e76cb-199">**P**: Por que eu preciso usar uma conta corporativa ou de estudante para entrar?</span><span class="sxs-lookup"><span data-stu-id="e76cb-199">**Q**: Why do I need to use a work or school account to sign in?</span></span> <br/><span data-ttu-id="e76cb-200">
**R**: Você pode usar uma conta corporativa ou de estudante do Azure apenas ao instalar o gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-200">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="e76cb-201">Sua conta de entrada é armazenada em um locatário gerenciado pelo Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="e76cb-201">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e76cb-202">Geralmente, o nome UPN da conta do Azure AD corresponde ao endereço de email.</span><span class="sxs-lookup"><span data-stu-id="e76cb-202">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="e76cb-203">**P**: Em que local minhas credenciais são armazenadas?</span><span class="sxs-lookup"><span data-stu-id="e76cb-203">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="e76cb-204">
**R**: As credenciais inseridas para uma fonte de dados são criptografadas e armazenadas no Serviço de Nuvem do Gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-204">
**A**: The credentials that you enter for a data source are encrypted and stored in the Gateway Cloud Service.</span></span> <span data-ttu-id="e76cb-205">As credenciais são descriptografadas no gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-205">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="e76cb-206">**P**: Há algum requisito de largura de banda de rede?</span><span class="sxs-lookup"><span data-stu-id="e76cb-206">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="e76cb-207">
**R**: Recomendamos que sua conexão de rede tenha uma boa taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="e76cb-207">
**A**: It's recommend your network connection has good throughput.</span></span> <span data-ttu-id="e76cb-208">Cada ambiente é diferente, e a quantidade de dados enviados afeta os resultados.</span><span class="sxs-lookup"><span data-stu-id="e76cb-208">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="e76cb-209">Usar o ExpressRoute pode ajudar a assegurar um nível de taxa de transferência entre os datacenters locais e do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-209">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="e76cb-210">Você pode usar um aplicativo de Teste de Velocidade do Azure de terceiros para avaliar sua taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="e76cb-210">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="e76cb-211">**P**: Qual é a latência para execução de consultas para uma fonte de dados do gateway?</span><span class="sxs-lookup"><span data-stu-id="e76cb-211">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="e76cb-212">Qual é a melhor arquitetura?</span><span class="sxs-lookup"><span data-stu-id="e76cb-212">What is the best architecture?</span></span> <br/><span data-ttu-id="e76cb-213">
**R**: Para reduzir a latência de rede, instale o gateway o mais próximo possível da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e76cb-213">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="e76cb-214">Se você puder instalar o gateway na fonte de dados real, essa proximidade minimizará a latência introduzida.</span><span class="sxs-lookup"><span data-stu-id="e76cb-214">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="e76cb-215">Considere também os datacenters.</span><span class="sxs-lookup"><span data-stu-id="e76cb-215">Consider the datacenters too.</span></span> <span data-ttu-id="e76cb-216">Por exemplo, se o serviço usar o datacenter Oeste dos EUA e você tiver o SQL Server hospedado em uma VM do Azure, a VM do Azure também deverá estar no Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="e76cb-216">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="e76cb-217">Essa proximidade minimiza a latência e evita encargos de saída na VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-217">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="e76cb-218">**P**: Como os resultados são enviados para a nuvem?</span><span class="sxs-lookup"><span data-stu-id="e76cb-218">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="e76cb-219">
**R**: Os resultados são enviados por meio do Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-219">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="e76cb-220">**P**: Existem conexões de entrada para o gateway da nuvem?</span><span class="sxs-lookup"><span data-stu-id="e76cb-220">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="e76cb-221">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="e76cb-221">
**A**: No.</span></span> <span data-ttu-id="e76cb-222">O gateway usa conexões de saída para o Barramento de Serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="e76cb-222">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="e76cb-223">**P**: O que acontecerá se eu bloquear conexões de saída?</span><span class="sxs-lookup"><span data-stu-id="e76cb-223">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="e76cb-224">O que preciso abrir?</span><span class="sxs-lookup"><span data-stu-id="e76cb-224">What do I need to open?</span></span> <br/><span data-ttu-id="e76cb-225">
**R**: Verifique as portas e os hosts que o gateway usa.</span><span class="sxs-lookup"><span data-stu-id="e76cb-225">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="e76cb-226">**P**: Qual é o serviço Windows que é de fato chamado?</span><span class="sxs-lookup"><span data-stu-id="e76cb-226">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="e76cb-227">
**R**: Em Serviços, o gateway é chamado de Serviço de gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-227">
**A**: In Services, the gateway is called On-premises data gateway service.</span></span>

<span data-ttu-id="e76cb-228">**P**: O serviço Windows do gateway pode ser executado com uma conta do Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e76cb-228">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="e76cb-229">
**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="e76cb-229">
**A**: No.</span></span> <span data-ttu-id="e76cb-230">O serviço do Windows deve ter uma conta válida do Windows.</span><span class="sxs-lookup"><span data-stu-id="e76cb-230">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="e76cb-231">Por padrão, o serviço é executado com o SID de Serviço, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="e76cb-231">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <span data-ttu-id="e76cb-232"><a name="high-availability"></a>Alta disponibilidade e recuperação de desastres</span><span class="sxs-lookup"><span data-stu-id="e76cb-232"><a name="high-availability"></a>High availability and disaster recovery</span></span>

<span data-ttu-id="e76cb-233">**P**: Quais opções estão disponíveis para recuperação de desastre?</span><span class="sxs-lookup"><span data-stu-id="e76cb-233">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="e76cb-234">
**R**: Você pode usar a chave de recuperação para restaurar ou mover um gateway.</span><span class="sxs-lookup"><span data-stu-id="e76cb-234">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="e76cb-235">Ao instalar o gateway, especifique a chave de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e76cb-235">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="e76cb-236">**P**: Qual é o benefício da chave de recuperação?</span><span class="sxs-lookup"><span data-stu-id="e76cb-236">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="e76cb-237">
**R**: A chave de recuperação oferece uma maneira de migrar ou recuperar as configurações de gateway após um desastre.</span><span class="sxs-lookup"><span data-stu-id="e76cb-237">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

## <span data-ttu-id="e76cb-238"><a name="troubleshooting"> </a>Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="e76cb-238"><a name="troubleshooting"> </a>Troubleshooting</span></span>

<span data-ttu-id="e76cb-239">**P**: Como posso ver quais consultas estão sendo enviadas à fonte de dados local?</span><span class="sxs-lookup"><span data-stu-id="e76cb-239">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="e76cb-240">
**R**: Você pode habilitar o rastreamento de consulta, que inclui as consultas que são enviadas.</span><span class="sxs-lookup"><span data-stu-id="e76cb-240">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="e76cb-241">Lembre-se de alterar o rastreamento de consulta de volta para o valor original quando concluir a solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="e76cb-241">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="e76cb-242">Deixar o acompanhamento de consulta ativado cria logs maiores.</span><span class="sxs-lookup"><span data-stu-id="e76cb-242">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="e76cb-243">Você também pode examinar ferramentas de rastreamento de consultas disponibilizadas por sua fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e76cb-243">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="e76cb-244">Por exemplo, você pode usar o Extended Events ou o SQL Profiler para SQL Server e Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e76cb-244">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="e76cb-245">**P**: Em que local estão os logs do gateway?</span><span class="sxs-lookup"><span data-stu-id="e76cb-245">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="e76cb-246">
**R**: Veja Logs, mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="e76cb-246">
**A**: See Logs later in this topic.</span></span>

### <span data-ttu-id="e76cb-247"><a name="update"></a>Atualização para a versão mais recente</span><span class="sxs-lookup"><span data-stu-id="e76cb-247"><a name="update"></a>Update to the latest version</span></span>

<span data-ttu-id="e76cb-248">Muitos problemas podem surgir quando a versão do gateway fica desatualizada.</span><span class="sxs-lookup"><span data-stu-id="e76cb-248">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="e76cb-249">Como prática geral recomendada, use a última versão.</span><span class="sxs-lookup"><span data-stu-id="e76cb-249">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="e76cb-250">Se você não atualiza o gateway há um mês ou mais, convém instalar a versão mais recente do gateway e verificar se o problema pode ser reproduzido.</span><span class="sxs-lookup"><span data-stu-id="e76cb-250">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="e76cb-251">Erro: falha ao adicionar usuário ao grupo.</span><span class="sxs-lookup"><span data-stu-id="e76cb-251">Error: Failed to add user to group.</span></span> <span data-ttu-id="e76cb-252">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="e76cb-252">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="e76cb-253">Você poderá obter esse erro se tentar instalar o gateway em um controlador de domínio, o que não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="e76cb-253">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="e76cb-254">Implante o gateway em um computador que não seja um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="e76cb-254">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <span data-ttu-id="e76cb-255"><a name="logs"></a>Logs</span><span class="sxs-lookup"><span data-stu-id="e76cb-255"><a name="logs"></a>Logs</span></span>

<span data-ttu-id="e76cb-256">Arquivos de log são um recurso importante ao solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="e76cb-256">Log files are an important resource when troubleshooting.</span></span>

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="e76cb-257">Logs de serviço do gateway corporativo</span><span class="sxs-lookup"><span data-stu-id="e76cb-257">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a><span data-ttu-id="e76cb-258">Logs de configuração</span><span class="sxs-lookup"><span data-stu-id="e76cb-258">Configuration logs</span></span>

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a><span data-ttu-id="e76cb-259">Logs de eventos</span><span class="sxs-lookup"><span data-stu-id="e76cb-259">Event logs</span></span>

<span data-ttu-id="e76cb-260">Você pode encontrar os logs do Gateway de Gerenciamento de Dados e do PowerBIGateway em **Logs de Aplicativos e Serviços**.</span><span class="sxs-lookup"><span data-stu-id="e76cb-260">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>


## <span data-ttu-id="e76cb-261"><a name="telemetry"></a>Telemetria</span><span class="sxs-lookup"><span data-stu-id="e76cb-261"><a name="telemetry"></a>Telemetry</span></span>
<span data-ttu-id="e76cb-262">Telemetria pode ser usada para monitorar e solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="e76cb-262">Telemetry can be used for monitoring and troubleshooting.</span></span> <span data-ttu-id="e76cb-263">Por padrão</span><span class="sxs-lookup"><span data-stu-id="e76cb-263">By default</span></span>

<span data-ttu-id="e76cb-264">**Para ativar a telemetria**</span><span class="sxs-lookup"><span data-stu-id="e76cb-264">**To turn on telemetry**</span></span>

1.  <span data-ttu-id="e76cb-265">Verifique o diretório do cliente de gateway de dados local no computador.</span><span class="sxs-lookup"><span data-stu-id="e76cb-265">Check the On-premises data gateway client directory on the computer.</span></span> <span data-ttu-id="e76cb-266">Normalmente, é **%systemdrive%\Program Files\On-premises data gateway**.</span><span class="sxs-lookup"><span data-stu-id="e76cb-266">Typically, it is **%systemdrive%\Program Files\On-premises data gateway**.</span></span> <span data-ttu-id="e76cb-267">Ou, você pode abrir um console de Serviços e verificar o Caminho para o executável: uma propriedade do serviço do gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-267">Or, you can open a Services console and check the Path to executable: A property of the On-premises data gateway service.</span></span>
2.  <span data-ttu-id="e76cb-268">No arquivo Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config do diretório do cliente.</span><span class="sxs-lookup"><span data-stu-id="e76cb-268">In the Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config file from client directory.</span></span> <span data-ttu-id="e76cb-269">Altere a configuração SendTelemetry para true.</span><span class="sxs-lookup"><span data-stu-id="e76cb-269">Change the SendTelemetry setting to true.</span></span>
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  <span data-ttu-id="e76cb-270">Salve suas alterações e reinicie o serviço do Windows: serviço do gateway de dados local.</span><span class="sxs-lookup"><span data-stu-id="e76cb-270">Save your changes and restart the Windows service: On-premises data gateway service.</span></span>




## <a name="next-steps"></a><span data-ttu-id="e76cb-271">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e76cb-271">Next steps</span></span>
* [<span data-ttu-id="e76cb-272">Gerenciar o Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e76cb-272">Manage Analysis Services</span></span>](analysis-services-manage.md)
* [<span data-ttu-id="e76cb-273">Obter dados do Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e76cb-273">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
