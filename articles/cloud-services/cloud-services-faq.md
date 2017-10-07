---
title: "funções de serviços de nuvem aaaAzure perguntas Frequentes | Microsoft Docs"
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="73263-104">Perguntas frequentes sobre Serviços de Nuvem</span><span class="sxs-lookup"><span data-stu-id="73263-104">Cloud Services FAQ</span></span>
<span data-ttu-id="73263-105">Este artigo responde a algumas perguntas frequentes sobre os Serviços de Nuvem do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="73263-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="73263-106">Você também pode visitar Olá [perguntas frequentes sobre o Azure suporte](http://go.microsoft.com/fwlink/?LinkID=185083) para informações gerais de suporte e preços do Azure.</span><span class="sxs-lookup"><span data-stu-id="73263-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="73263-107">Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.</span><span class="sxs-lookup"><span data-stu-id="73263-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="73263-108">Certificados</span><span class="sxs-lookup"><span data-stu-id="73263-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="73263-109">Onde devo instalar o certificado?</span><span class="sxs-lookup"><span data-stu-id="73263-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="73263-110">**Meu**</span><span class="sxs-lookup"><span data-stu-id="73263-110">**My**</span></span>  
  <span data-ttu-id="73263-111">Certificado do aplicativo com a chave privada (\*. pfx, \*. p12).</span><span class="sxs-lookup"><span data-stu-id="73263-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="73263-112">**AC**</span><span class="sxs-lookup"><span data-stu-id="73263-112">**CA**</span></span>  
  <span data-ttu-id="73263-113">Todos os certificados intermediários ficam neste repositório (política e Sub ACs).</span><span class="sxs-lookup"><span data-stu-id="73263-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="73263-114">**RAIZ**</span><span class="sxs-lookup"><span data-stu-id="73263-114">**ROOT**</span></span>  
  <span data-ttu-id="73263-115">autoridade de certificação de raiz de saudação armazenar, para que seu certificado de autoridade de certificação raiz principal deve ser inserido aqui.</span><span class="sxs-lookup"><span data-stu-id="73263-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="73263-116">Não é possível remover o certificado expirado</span><span class="sxs-lookup"><span data-stu-id="73263-116">I can't remove expired certificate</span></span>
<span data-ttu-id="73263-117">Azure impede a remoção de um certificado enquanto ele está em uso.</span><span class="sxs-lookup"><span data-stu-id="73263-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="73263-118">Você precisará tooeither Olá a implantação de exclusão que usa o certificado de saudação ou implantação de atualização de saudação com um certificado diferente ou renovada.</span><span class="sxs-lookup"><span data-stu-id="73263-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="73263-119">Excluir um certificado expirado</span><span class="sxs-lookup"><span data-stu-id="73263-119">Delete an expired certificate</span></span>
<span data-ttu-id="73263-120">Como Olá certificado não estiver em uso, você pode usar o hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove de cmdlet do PowerShell um certificado.</span><span class="sxs-lookup"><span data-stu-id="73263-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="73263-121">Tenho certificados expirados denominados Gerenciamento de Serviço do Microsoft Azure para Extensões</span><span class="sxs-lookup"><span data-stu-id="73263-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="73263-122">Esses certificados são criados sempre que uma extensão é adicionada toohello serviço em nuvem como Olá extensão da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="73263-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="73263-123">Esses certificados são usados apenas para criptografar e descriptografar a configuração privada Olá da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="73263-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="73263-124">Não importa se esses certificados expiram.</span><span class="sxs-lookup"><span data-stu-id="73263-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="73263-125">Data de expiração de saudação não é verificada.</span><span class="sxs-lookup"><span data-stu-id="73263-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="73263-126">Certificados que excluí continuam reaparecendo</span><span class="sxs-lookup"><span data-stu-id="73263-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="73263-127">Eles continuam reaparecendo muito provavelmente devido a uma ferramenta que você está usando, como o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="73263-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="73263-128">Sempre que você se reconectar com uma ferramenta que está usando um certificado, ele será novamente tooAzure carregado.</span><span class="sxs-lookup"><span data-stu-id="73263-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="73263-129">Meus certificados continuam desaparecendo</span><span class="sxs-lookup"><span data-stu-id="73263-129">My certificates keep disappearing</span></span>
<span data-ttu-id="73263-130">Quando a instância de máquina virtual de saudação for reciclado, todas as alterações locais serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="73263-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="73263-131">Use um [tarefa de inicialização](cloud-services-startup-tasks.md) tooinstall certificados toohello virtual machine cada vez Olá função for iniciada.</span><span class="sxs-lookup"><span data-stu-id="73263-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="73263-132">Não consigo localizar meu certificados de gerenciamento no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="73263-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="73263-133">[Certificados de gerenciamento](../azure-api-management-certs.md) só estão disponíveis em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="73263-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="73263-134">portal do Azure atual de saudação não usa certificados de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="73263-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="73263-135">Como desabilitar um certificado de gerenciamento?</span><span class="sxs-lookup"><span data-stu-id="73263-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="73263-136">[certificados de gerenciamento](../azure-api-management-certs.md) não podem ser desabilitados.</span><span class="sxs-lookup"><span data-stu-id="73263-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="73263-137">Você excluí-los por meio de saudação Portal clássico do Azure quando você não deseja toobe mais usado.</span><span class="sxs-lookup"><span data-stu-id="73263-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="73263-138">Como criar um certificado SSL para um endereço IP específico?</span><span class="sxs-lookup"><span data-stu-id="73263-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="73263-139">Siga as instruções de Olá Olá [criar um tutorial do certificado](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="73263-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="73263-140">Use o endereço IP de saudação como Olá nome DNS.</span><span class="sxs-lookup"><span data-stu-id="73263-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="73263-141">Segurança</span><span class="sxs-lookup"><span data-stu-id="73263-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="73263-142">Desabilitar SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="73263-142">Disable SSL 3.0</span></span>
<span data-ttu-id="73263-143">toodisable SSL 3.0 e TLS de usar segurança, crie uma tarefa de inicialização que está documentada nesta postagem de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="73263-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="73263-144">Adicionar **nosniff** tooyour site</span><span class="sxs-lookup"><span data-stu-id="73263-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="73263-145">clientes tooprevent de detecção de tipos MIME hello, adicionar uma configuração em seu *Web. config* arquivo.</span><span class="sxs-lookup"><span data-stu-id="73263-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="73263-146">Ela também pode ser adicionada como uma configuração no IIS.</span><span class="sxs-lookup"><span data-stu-id="73263-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="73263-147">Comando a seguir de saudação Use com hello [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artigo.</span><span class="sxs-lookup"><span data-stu-id="73263-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="73263-148">Personalizar o IIS para uma função web</span><span class="sxs-lookup"><span data-stu-id="73263-148">Customize IIS for a web role</span></span>
<span data-ttu-id="73263-149">Usar script de inicialização IIS Olá da saudação [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artigo.</span><span class="sxs-lookup"><span data-stu-id="73263-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="73263-150">Dimensionamento</span><span class="sxs-lookup"><span data-stu-id="73263-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="73263-151">Não consigo dimensionar além de X instâncias</span><span class="sxs-lookup"><span data-stu-id="73263-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="73263-152">Sua assinatura do Azure tem um limite no número de saudação de núcleos que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="73263-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="73263-153">Dimensionamento não funcionará se você tiver usado todos os núcleos Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="73263-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="73263-154">Por exemplo, se você tiver um limite de 100 núcleos, isso significa você poderia ter 100 instâncias de máquina virtual A1 dimensionadas para seu serviço de nuvem ou 50 instâncias de máquina virtual A2.</span><span class="sxs-lookup"><span data-stu-id="73263-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="73263-155">Rede</span><span class="sxs-lookup"><span data-stu-id="73263-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="73263-156">Eu não consigo reservar um IP em um serviço de nuvem de vários VIPs</span><span class="sxs-lookup"><span data-stu-id="73263-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="73263-157">Primeiro, verifique se essa instância de máquina virtual Olá que você está tentando tooreserve Olá IP para está ativada.</span><span class="sxs-lookup"><span data-stu-id="73263-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="73263-158">Em segundo lugar, certifique-se de que você está usando IPs reservados para implantações de preparo e produção de hello incômodo.</span><span class="sxs-lookup"><span data-stu-id="73263-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="73263-159">**Não** alterar configurações de saudação enquanto implantação hello está sendo atualizado.</span><span class="sxs-lookup"><span data-stu-id="73263-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="73263-160">Área de trabalho remota</span><span class="sxs-lookup"><span data-stu-id="73263-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="73263-161">Como acesso a área de trabalho remota quando tenho um NSG?</span><span class="sxs-lookup"><span data-stu-id="73263-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="73263-162">Adicionar regras toohello NSG que permitam o tráfego em portas **3389** e **20000**.</span><span class="sxs-lookup"><span data-stu-id="73263-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="73263-163">A Área de Trabalho Remota usa a porta **3389**.</span><span class="sxs-lookup"><span data-stu-id="73263-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="73263-164">Instâncias de serviço de nuvem têm a carga balanceada, portanto diretamente, você não pode controlar quais tooconnect de instância para.</span><span class="sxs-lookup"><span data-stu-id="73263-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="73263-165">Olá *RemoteForwarder* e *RemoteAccess* agentes gerenciar o tráfego RDP e permitir Olá cliente toosend um cookie RDP e especifique um tooconnect instância individual para.</span><span class="sxs-lookup"><span data-stu-id="73263-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="73263-166">Olá *RemoteForwarder* e *RemoteAccess* agentes exigem essa porta **20000*** aberto, que pode ser bloqueado se você tiver um NSG.</span><span class="sxs-lookup"><span data-stu-id="73263-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
