---
title: "Perguntas frequentes sobre as funções dos Serviços de Nuvem do Azure | Microsoft Docs"
description: "Perguntas frequentes sobre os Serviços de Nuvem do Azure. Encontre respostas para algumas perguntas comuns sobre certificados, funções da Web e funções de trabalho."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="1cdbf-104">Perguntas frequentes sobre Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="1cdbf-104">Cloud Services FAQ</span></span>
<span data-ttu-id="1cdbf-105">Este artigo responde a algumas perguntas frequentes sobre os Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="1cdbf-106">Você também pode visitar as [Perguntas frequentes de suporte do Azure](http://go.microsoft.com/fwlink/?LinkID=185083) para informações gerais sobre preços e suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="1cdbf-107">Você também pode consultar a [página de tamanho de VM de Serviços de Nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="1cdbf-108">Certificados</span><span class="sxs-lookup"><span data-stu-id="1cdbf-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="1cdbf-109">Onde devo instalar o certificado?</span><span class="sxs-lookup"><span data-stu-id="1cdbf-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="1cdbf-110">**Meu**</span><span class="sxs-lookup"><span data-stu-id="1cdbf-110">**My**</span></span>  
  <span data-ttu-id="1cdbf-111">Certificado do aplicativo com a chave privada (\*. pfx, \*. p12).</span><span class="sxs-lookup"><span data-stu-id="1cdbf-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="1cdbf-112">**AC**</span><span class="sxs-lookup"><span data-stu-id="1cdbf-112">**CA**</span></span>  
  <span data-ttu-id="1cdbf-113">Todos os certificados intermediários ficam neste repositório (política e Sub ACs).</span><span class="sxs-lookup"><span data-stu-id="1cdbf-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="1cdbf-114">**RAIZ**</span><span class="sxs-lookup"><span data-stu-id="1cdbf-114">**ROOT**</span></span>  
  <span data-ttu-id="1cdbf-115">O repositório de AC raiz, para que seu certificado de AC raiz seja inserido aqui.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="1cdbf-116">Não é possível remover o certificado expirado</span><span class="sxs-lookup"><span data-stu-id="1cdbf-116">I can't remove expired certificate</span></span>
<span data-ttu-id="1cdbf-117">Azure impede a remoção de um certificado enquanto ele está em uso.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="1cdbf-118">É necessário excluir a implantação que usa o certificado ou atualizá-la com um certificado diferente ou renovado.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="1cdbf-119">Excluir um certificado expirado</span><span class="sxs-lookup"><span data-stu-id="1cdbf-119">Delete an expired certificate</span></span>
<span data-ttu-id="1cdbf-120">Enquanto o certificado não está em uso, você pode usar o cmdlet do PowerShell [AzureCertificate remover](https://msdn.microsoft.com/library/azure/mt589145.aspx) para remover um certificado.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="1cdbf-121">Tenho certificados expirados denominados Gerenciamento de Serviço do Microsoft Azure para Extensões</span><span class="sxs-lookup"><span data-stu-id="1cdbf-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="1cdbf-122">Esses certificados são criados sempre que uma extensão é adicionada ao serviço de nuvem, como a extensão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="1cdbf-123">Esses certificados são usados apenas para criptografar e descriptografar a configuração privada da extensão.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="1cdbf-124">Não importa se esses certificados expiram.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="1cdbf-125">A data de validade não é verificada.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="1cdbf-126">Certificados que excluí continuam reaparecendo</span><span class="sxs-lookup"><span data-stu-id="1cdbf-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="1cdbf-127">Eles continuam reaparecendo muito provavelmente devido a uma ferramenta que você está usando, como o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="1cdbf-128">Sempre que você se reconectar com uma ferramenta que está usando um certificado, ele será carregado novamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="1cdbf-129">Meus certificados continuam desaparecendo</span><span class="sxs-lookup"><span data-stu-id="1cdbf-129">My certificates keep disappearing</span></span>
<span data-ttu-id="1cdbf-130">Quando a instância de máquina virtual for reciclada, todas as alterações locais serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="1cdbf-131">Use um [tarefa de inicialização](cloud-services-startup-tasks.md) para instalar certificados na máquina virtual sempre que a função for iniciada.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="1cdbf-132">Não consigo encontrar meus certificados de gerenciamento no portal</span><span class="sxs-lookup"><span data-stu-id="1cdbf-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="1cdbf-133">Os [Certificados de gerenciamento](../azure-api-management-certs.md) estão disponíveis apenas no Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="1cdbf-134">O Portal do Azure atual não usa certificados de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="1cdbf-135">Como desabilitar um certificado de gerenciamento?</span><span class="sxs-lookup"><span data-stu-id="1cdbf-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="1cdbf-136">[certificados de gerenciamento](../azure-api-management-certs.md) não podem ser desabilitados.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="1cdbf-137">Exclua-os no Portal Clássico do Azure quando você não quiser mais usá-los.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="1cdbf-138">Como criar um certificado SSL para um endereço IP específico?</span><span class="sxs-lookup"><span data-stu-id="1cdbf-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="1cdbf-139">Siga as instruções no [tutorial Criar um certificado](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1cdbf-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="1cdbf-140">Use o endereço IP como o nome DNS.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="1cdbf-141">Segurança</span><span class="sxs-lookup"><span data-stu-id="1cdbf-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="1cdbf-142">Desabilitar SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="1cdbf-142">Disable SSL 3.0</span></span>
<span data-ttu-id="1cdbf-143">Para desabilitar o SSL 3.0 e usar a segurança TLS, crie uma tarefa de inicialização que está documentada nesta postagem de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="1cdbf-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="1cdbf-144">Adicionar **nosniff** ao seu site</span><span class="sxs-lookup"><span data-stu-id="1cdbf-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="1cdbf-145">Para evitar que clientes detectem os tipos MIME, adicione uma configuração ao arquivo *web.config*.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="1cdbf-146">Ela também pode ser adicionada como uma configuração no IIS.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="1cdbf-147">Use o comando abaixo com o artigo [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="1cdbf-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="1cdbf-148">Personalizar o IIS para uma função web</span><span class="sxs-lookup"><span data-stu-id="1cdbf-148">Customize IIS for a web role</span></span>
<span data-ttu-id="1cdbf-149">Use o script de inicialização do IIS do artigo [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="1cdbf-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="1cdbf-150">Dimensionamento</span><span class="sxs-lookup"><span data-stu-id="1cdbf-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="1cdbf-151">Não consigo dimensionar além de X instâncias</span><span class="sxs-lookup"><span data-stu-id="1cdbf-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="1cdbf-152">Sua Assinatura do Azure tem um limite no número de núcleos que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="1cdbf-153">O dimensionamento não funcionará se você tiver usado todos os núcleos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="1cdbf-154">Por exemplo, se você tiver um limite de 100 núcleos, isso significa você poderia ter 100 instâncias de máquina virtual A1 dimensionadas para seu serviço de nuvem ou 50 instâncias de máquina virtual A2.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="1cdbf-155">Rede</span><span class="sxs-lookup"><span data-stu-id="1cdbf-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="1cdbf-156">Eu não consigo reservar um IP em um serviço de nuvem de vários VIPs</span><span class="sxs-lookup"><span data-stu-id="1cdbf-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="1cdbf-157">Primeiro, certifique-se de que a instância de máquina virtual que você está tentando reservar o IP esteja ativada.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="1cdbf-158">Segundo, certifique-se de que você esteja usando IPs reservados para as implantações de preparo e produção.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="1cdbf-159">**Não** altere as configurações enquanto a implantação é atualizada.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="1cdbf-160">Área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="1cdbf-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="1cdbf-161">Como acesso a área de trabalho remota quando tenho um NSG?</span><span class="sxs-lookup"><span data-stu-id="1cdbf-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="1cdbf-162">Adicione regras para o NSG que permitem o tráfego nas portas **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="1cdbf-163">A Área de Trabalho Remota usa a porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="1cdbf-164">Instâncias de serviço de nuvem têm a carga balanceada, de modo que você não pode controlar diretamente a escolha da instância à qual se conectar.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="1cdbf-165">Os agentes *RemoteForwarder* e *RemoteAccess* gerenciam o tráfego RDP e permitem que o cliente envie um cookie RDP e especifique uma instância individual à qual se conectar.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="1cdbf-166">Os agentes *RemoteForwarder* e *RemoteAccess* exigem que essa porta **20000*** esteja aberta, a qual poderá ser bloqueada se você tiver um NSG.</span><span class="sxs-lookup"><span data-stu-id="1cdbf-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
