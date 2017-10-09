---
title: cluster de aaaSubmit trabalhos tooan HPC Pack no Azure | Microsoft Docs
description: Saiba como tooset a um toosubmit do computador local trabalhos tooan cluster de HPC Pack no Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="68d5b-103">Enviar trabalhos HPC de um cluster de HPC Pack local computador tooan implantado no Azure</span><span class="sxs-lookup"><span data-stu-id="68d5b-103">Submit HPC jobs from an on-premises computer tooan HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="68d5b-104">Configurar um local cliente computador toosubmit trabalhos tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="68d5b-104">Configure an on-premises client computer toosubmit jobs tooa [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="68d5b-105">Este artigo mostra como tooset um computador local com o cliente ferramentas toosubmit trabalho sobre cluster de toohello HTTPS no Azure.</span><span class="sxs-lookup"><span data-stu-id="68d5b-105">This article shows you how tooset up a local computer with client tools toosubmit job over HTTPS toohello cluster in Azure.</span></span> <span data-ttu-id="68d5b-106">Dessa forma, vários usuários do cluster podem enviar trabalhos tooa baseado em nuvem cluster de HPC Pack, mas sem se conectar diretamente toohello VM do nó principal ou acessar uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="68d5b-106">In this way, several cluster users can submit jobs tooa cloud-based HPC Pack cluster, but without connecting directly toohello head node VM or accessing an Azure subscription.</span></span>

![Enviar um cluster de tooa de trabalho no Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="68d5b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68d5b-108">Prerequisites</span></span>
* <span data-ttu-id="68d5b-109">**Nó principal do HPC Pack implantado em uma VM do Azure** -é recomendável que você use ferramentas automatizadas, como um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) ou um [script do PowerShell do Azure](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) nó principal do toodeploy hello e cluster.</span><span class="sxs-lookup"><span data-stu-id="68d5b-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello head node and cluster.</span></span> <span data-ttu-id="68d5b-110">Você precisa nome DNS de saudação do nó principal hello e credenciais de saudação de um administrador de cluster para concluir as etapas neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-110">You need hello DNS name of hello head node and hello credentials of a cluster administrator to complete hello steps in this article.</span></span>
* <span data-ttu-id="68d5b-111">**Computador cliente** – você precisa de um computador Windows Client ou Windows Server que possa executar utilitários de cliente do Pacote HPC (consulte os [requisitos do sistema](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="68d5b-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="68d5b-112">Se você desejar somente toouse Olá HPC Pack portal web ou trabalhos de toosubmit da API REST, você pode usar qualquer computador cliente de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="68d5b-112">If you only want toouse hello HPC Pack web portal or REST API toosubmit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="68d5b-113">**Mídia de instalação HPC Pack** -tooinstall Olá utilitários de cliente do HPC Pack, o pacote de instalação gratuita Olá para a versão mais recente do HPC Pack (HPC Pack 2012 R2) está disponível a partir de [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="68d5b-113">**HPC Pack installation media** - tooinstall hello HPC Pack client utilities, hello free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="68d5b-114">Certifique-se de que você baixe Olá mesma versão do HPC Pack está instalado na VM do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-114">Make sure that you download hello same version of HPC Pack that is installed on hello head node VM.</span></span>

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a><span data-ttu-id="68d5b-115">Etapa 1: Instalar e configurar os componentes da web hello no nó de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="68d5b-115">Step 1: Install and configure hello web components on hello head node</span></span>
<span data-ttu-id="68d5b-116">tooenable um cluster REST interface toosubmit trabalhos toohello via HTTPS, verifique se os componentes de web do HPC Pack Olá estão configurados no nó principal do HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-116">tooenable a REST interface toosubmit jobs toohello cluster over HTTPS, ensure that hello HPC Pack web components are configured on hello HPC Pack head node.</span></span> <span data-ttu-id="68d5b-117">Se ainda não estiverem instalados, primeiro instale os componentes da web hello executando o arquivo de instalação HpcWebComponents.msi hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-117">If they aren't already installed, first install hello web components by running hello HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="68d5b-118">Em seguida, configure componentes Olá executando o script do HPC PowerShell Olá **Set-hpcwebcomponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-118">Then, configure hello components by running hello HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="68d5b-119">Para obter procedimentos detalhados, consulte [instalar componentes da Web do hello Microsoft HPC Pack](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d5b-119">For detailed procedures, see [Install hello Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="68d5b-120">Alguns modelos de início rápido do Azure para o HPC Pack instalar e configurar os componentes da web hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="68d5b-120">Certain Azure quickstart templates for HPC Pack install and configure hello web components automatically.</span></span> <span data-ttu-id="68d5b-121">Se você usar o hello [script de implantação IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate cluster do hello, opcionalmente, você pode instalar e configurar os componentes da web hello como parte da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="68d5b-121">If you use hello [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello cluster, you can optionally install and configure hello web components as part of hello deployment.</span></span>
> 
> 

<span data-ttu-id="68d5b-122">**componentes da web do tooinstall Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-122">**tooinstall hello web components**</span></span>

1. <span data-ttu-id="68d5b-123">Conecte-se toohello VM do nó principal usando credenciais de saudação de um administrador de cluster.</span><span class="sxs-lookup"><span data-stu-id="68d5b-123">Connect toohello head node VM by using hello credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="68d5b-124">Na pasta de instalação do HPC Pack hello, execute HpcWebComponents.msi no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-124">From hello HPC Pack Setup folder, run HpcWebComponents.msi on hello head node.</span></span>
3. <span data-ttu-id="68d5b-125">Siga as etapas de Olá Olá Assistente tooinstall Olá web de componentes</span><span class="sxs-lookup"><span data-stu-id="68d5b-125">Follow hello steps in hello wizard tooinstall hello web components</span></span>

<span data-ttu-id="68d5b-126">**componentes da web do tooconfigure Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-126">**tooconfigure hello web components**</span></span>

1. <span data-ttu-id="68d5b-127">No nó de cabeçalho hello, inicie o HPC PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="68d5b-127">On hello head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="68d5b-128">local de toohello toochange diretório saudação do script de configuração, Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="68d5b-128">toochange directory toohello location of hello configuration script, type hello following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="68d5b-129">tooconfigure Olá interface REST e iniciar Olá serviço Web do HPC, Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="68d5b-129">tooconfigure hello REST interface and start hello HPC Web Service, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="68d5b-130">Quando solicitada tooselect um certificado, escolha o certificado de saudação correspondente toohello nome DNS público do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-130">When prompted tooselect a certificate, choose hello certificate that corresponds toohello public DNS name of hello head node.</span></span> <span data-ttu-id="68d5b-131">Por exemplo, se você implantar o nó principal do hello VM usando o modelo de implantação clássico Olá, nome do certificado Olá aparência CN =&lt;*HeadNodeDnsName*&gt;. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="68d5b-131">For example, if you deploy hello head node VM using hello classic deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="68d5b-132">Se você usar o modelo de implantação do Gerenciador de recursos de Olá, nome do certificado Olá aparência CN =&lt;*HeadNodeDnsName*&gt;.&lt; *região*&gt;. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="68d5b-132">If you use hello Resource Manager deployment model, hello certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="68d5b-133">Selecione este certificado mais tarde quando você envia o nó principal do toohello de trabalhos de um computador local.</span><span class="sxs-lookup"><span data-stu-id="68d5b-133">You select this certificate later when you submit jobs toohello head node from an on-premises computer.</span></span> <span data-ttu-id="68d5b-134">Não selecione nem configure um certificado que corresponde a toohello o nome do computador do nó principal do hello no domínio do Active Directory hello (por exemplo, CN =*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="68d5b-134">Don't select or configure a certificate that corresponds toohello computer name of hello head node in hello Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="68d5b-135">portal de web tooconfigure Olá para envio de trabalho, Olá tipo comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="68d5b-135">tooconfigure hello web portal for job submission, type hello following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="68d5b-136">Após a conclusão do script hello, pare e reinicie o hello serviço de Agendador de trabalho do HPC digitando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68d5b-136">After hello script completes, stop and restart hello HPC Job Scheduler Service by typing hello following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="68d5b-137">Etapa 2: Instalar utilitários de cliente Olá HPC Pack em um computador local</span><span class="sxs-lookup"><span data-stu-id="68d5b-137">Step 2: Install hello HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="68d5b-138">Se você quiser utilitários de cliente tooinstall Olá HPC Pack em seu computador, baixe os arquivos de instalação HPC Pack (instalação completa) de saudação [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="68d5b-138">If you want tooinstall hello HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="68d5b-139">Quando você começar a instalação hello, escolha a opção de instalação de saudação para Olá **utilitários de cliente do HPC Pack**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-139">When you begin hello installation, choose hello setup option for hello **HPC Pack client utilities**.</span></span>

<span data-ttu-id="68d5b-140">ferramentas de cliente de HPC Pack Olá toouse toosubmit trabalhos toohello VM do nó principal, você também precisa tooexport um certificado de nó principal hello e instalá-lo no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="68d5b-140">toouse hello HPC Pack client tools toosubmit jobs toohello head node VM, you also need tooexport a certificate from hello head node and install it on hello client computer.</span></span> <span data-ttu-id="68d5b-141">Olá certificado deve ser no. Formato CER.</span><span class="sxs-lookup"><span data-stu-id="68d5b-141">hello certificate must be in .CER format.</span></span>

<span data-ttu-id="68d5b-142">**certificado de saudação tooexport do nó principal Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-142">**tooexport hello certificate from hello head node**</span></span>

1. <span data-ttu-id="68d5b-143">No nó de cabeçalho hello, adicione Olá certificados snap-in tooa Console de gerenciamento Microsoft para Olá conta do computador Local.</span><span class="sxs-lookup"><span data-stu-id="68d5b-143">On hello head node, add hello Certificates snap-in tooa Microsoft Management Console for hello Local Computer account.</span></span> <span data-ttu-id="68d5b-144">Para obter etapas tooadd Olá snap-in, consulte [adicionar Olá Snap-in Certificados tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d5b-144">For steps tooadd hello snap-in, see [Add hello Certificates Snap-in tooan MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="68d5b-145">Na árvore de console hello, expanda **certificados – computador Local** > **pessoal**e, em seguida, clique em **certificados**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-145">In hello console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="68d5b-146">Localize Olá certificado que você configurou para web components Olá HPC Pack em [etapa 1: instalar e configurar os componentes da web hello no nó de cabeçalho de saudação](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por exemplo, CN =&lt;*HeadNodeDnsName* &gt;. >.cloudapp.NET).</span><span class="sxs-lookup"><span data-stu-id="68d5b-146">Locate hello certificate that you configured for hello HPC Pack web components in [Step 1: Install and configure hello web components on hello head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="68d5b-147">Clique com botão direito certificado hello e, em seguida, clique em **todas as tarefas** > **exportar**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-147">Right-click hello certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="68d5b-148">No hello Assistente para exportação de certificado, clique em **próximo**e certifique-se de que **não exportar chave privada Olá** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="68d5b-148">In hello Certificate Export Wizard, click **Next**, and ensure that **No, do not export hello private key** is selected.</span></span>
6. <span data-ttu-id="68d5b-149">Olá siga restantes etapas de saudação Assistente tooexport Olá certificado DER codificada x. 509 binário (. Formato CER).</span><span class="sxs-lookup"><span data-stu-id="68d5b-149">Follow hello remaining steps of hello wizard tooexport hello certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="68d5b-150">**certificado de saudação tooimport no computador do cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-150">**tooimport hello certificate on hello client computer**</span></span>

1. <span data-ttu-id="68d5b-151">Copie o certificado de saudação que você exportou da pasta de tooa Olá nó principal no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="68d5b-151">Copy hello certificate that you exported from hello head node tooa folder on hello client computer.</span></span>
2. <span data-ttu-id="68d5b-152">No computador do cliente Olá, execute certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="68d5b-152">On hello client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="68d5b-153">No Gerenciador de Certificados, expanda **Certificados – Usuário atual** > **Autoridades de Certificação Confiáveis**, clique com o botão direito do mouse em **Certificados** e clique em **Todas as Tarefas** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="68d5b-154">No hello Assistente de importação de certificado, clique em **próximo** e siga Olá etapas tooimport Olá certificado que você exportou da saudação nó principal toohello repositório de autoridades de certificação raiz confiáveis.</span><span class="sxs-lookup"><span data-stu-id="68d5b-154">In hello Certificate Import Wizard, click **Next** and follow hello steps tooimport hello certificate that you exported from hello head node toohello Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="68d5b-155">Você pode ver um aviso de segurança, porque a autoridade de certificação Olá no nó de cabeçalho Olá não é reconhecida pelo computador cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="68d5b-155">You might see a security warning, because hello certification authority on hello head node isn't recognized by hello client computer.</span></span> <span data-ttu-id="68d5b-156">Para fins de teste, você pode ignorar este aviso e concluir importação do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-156">For testing purposes, you can ignore this warning and complete hello certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a><span data-ttu-id="68d5b-157">Etapa 3: Executar trabalhos de teste no cluster Olá</span><span class="sxs-lookup"><span data-stu-id="68d5b-157">Step 3: Run test jobs on hello cluster</span></span>
<span data-ttu-id="68d5b-158">tooverify sua configuração, tente trabalhos em execução saudação do cluster no Azure de saudação local do computador.</span><span class="sxs-lookup"><span data-stu-id="68d5b-158">tooverify your configuration, try running jobs on hello cluster in Azure from hello on-premises computer.</span></span> <span data-ttu-id="68d5b-159">Por exemplo, você pode usar ferramentas de GUI do HPC Pack ou cluster de toohello comandos de linha de comando toosubmit trabalhos.</span><span class="sxs-lookup"><span data-stu-id="68d5b-159">For example, you can use HPC Pack GUI tools or command-line commands toosubmit jobs toohello cluster.</span></span> <span data-ttu-id="68d5b-160">Você também pode usar um trabalhos toosubmit portal baseado na web.</span><span class="sxs-lookup"><span data-stu-id="68d5b-160">You can also use a web-based portal toosubmit jobs.</span></span>

<span data-ttu-id="68d5b-161">**comandos de envio de trabalho toorun no computador do cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-161">**toorun job submission commands on hello client computer**</span></span>

1. <span data-ttu-id="68d5b-162">Em um computador cliente onde os utilitários de cliente do HPC Pack Olá estão instalados, inicie um Prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="68d5b-162">On a client computer where hello HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="68d5b-163">Digite um comando de exemplo.</span><span class="sxs-lookup"><span data-stu-id="68d5b-163">Type a sample command.</span></span> <span data-ttu-id="68d5b-164">Por exemplo, toolist todos os trabalhos no cluster hello, digite um tooone semelhante do comando de hello a seguir, dependendo do nome DNS completo de saudação do nó principal hello:</span><span class="sxs-lookup"><span data-stu-id="68d5b-164">For example, toolist all jobs on hello cluster, type a command similar tooone of hello following, depending on hello full DNS name of hello head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="68d5b-165">ou o</span><span class="sxs-lookup"><span data-stu-id="68d5b-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="68d5b-166">Use o nome DNS completo de saudação do nó principal hello, não endereços IP hello, Olá Agendador URL.</span><span class="sxs-lookup"><span data-stu-id="68d5b-166">Use hello full DNS name of hello head node, not hello IP address, in hello scheduler URL.</span></span> <span data-ttu-id="68d5b-167">Se você especificar o endereço IP hello, um erro semelhante também aparecerá "certificado do servidor de saudação precisa tooeither têm uma cadeia válida de confiança ou toobe colocado no repositório de raiz confiável do hello."</span><span class="sxs-lookup"><span data-stu-id="68d5b-167">If you specify hello IP address, an error appears similar too"hello server certificate needs tooeither have a valid chain of trust or toobe placed in hello trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="68d5b-168">Quando solicitado, digite o nome de usuário da saudação (na forma de saudação &lt;DomainName&gt;\\&lt;UserName&gt;) e a senha de administrador de cluster HPC hello ou outro usuário do cluster que você configurou.</span><span class="sxs-lookup"><span data-stu-id="68d5b-168">When prompted, type hello user name (in hello form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="68d5b-169">Você pode escolher toostore credenciais Olá localmente para mais operações de trabalho.</span><span class="sxs-lookup"><span data-stu-id="68d5b-169">You can choose toostore hello credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="68d5b-170">Uma lista de trabalhos é exibida.</span><span class="sxs-lookup"><span data-stu-id="68d5b-170">A list of jobs appears.</span></span>

<span data-ttu-id="68d5b-171">**toouse Gerenciador de trabalhos HPC no computador do cliente Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-171">**toouse HPC Job Manager on hello client computer**</span></span>

1. <span data-ttu-id="68d5b-172">Se anteriormente você não armazenar credenciais de domínio para um usuário de cluster durante o envio de um trabalho, você pode adicionar credenciais Olá no Gerenciador de credenciais.</span><span class="sxs-lookup"><span data-stu-id="68d5b-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add hello credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="68d5b-173">a.</span><span class="sxs-lookup"><span data-stu-id="68d5b-173">a.</span></span> <span data-ttu-id="68d5b-174">No painel de controle no computador do cliente hello, inicie o Gerenciador de credenciais.</span><span class="sxs-lookup"><span data-stu-id="68d5b-174">In Control Panel on hello client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="68d5b-175">b.</span><span class="sxs-lookup"><span data-stu-id="68d5b-175">b.</span></span> <span data-ttu-id="68d5b-176">Clique nas **Credenciais do Windows** > **Adicionar uma credencial genérica**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="68d5b-177">c.</span><span class="sxs-lookup"><span data-stu-id="68d5b-177">c.</span></span> <span data-ttu-id="68d5b-178">Especifique o endereço de Internet da saudação (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt; região&gt;.cloudapp.azure.com/HpcScheduler) e o nome de usuário da saudação (&lt;DomainName&gt;\\&lt;UserName&gt;) e a senha de administrador de cluster hello ou outro usuário de cluster que você configurou.</span><span class="sxs-lookup"><span data-stu-id="68d5b-178">Specify hello Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and hello user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of hello cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="68d5b-179">No computador do cliente hello, inicie o Gerenciador de trabalho do HPC.</span><span class="sxs-lookup"><span data-stu-id="68d5b-179">On hello client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="68d5b-180">Em Olá **selecionar nó principal** caixa de diálogo, tipo hello URL toohello nó principal no Azure (por exemplo, https://&lt;HeadNodeDnsName&gt;. cloudapp.net ou https://&lt;HeadNodeDnsName&gt;. &lt;região&gt;. cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="68d5b-180">In hello **Select Head Node** dialog box, type hello URL toohello head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="68d5b-181">Gerenciador de trabalhos HPC é aberto e mostra uma lista de trabalhos no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-181">HPC Job Manager opens and shows a list of jobs on hello head node.</span></span>

<span data-ttu-id="68d5b-182">**portal de web hello toouse em execução no nó principal Olá**</span><span class="sxs-lookup"><span data-stu-id="68d5b-182">**toouse hello web portal running on hello head node**</span></span>

1. <span data-ttu-id="68d5b-183">Iniciar um navegador da web no computador do cliente hello e insira um Olá endereços, dependendo do nome DNS completo de saudação do nó principal Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="68d5b-183">Start a web browser on hello client computer, and enter one of hello following addresses, depending on hello full DNS name of hello head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="68d5b-184">ou o</span><span class="sxs-lookup"><span data-stu-id="68d5b-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="68d5b-185">Na Olá caixa de diálogo de segurança que aparece, digite credenciais de domínio de saudação do administrador de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-185">In hello security dialog box that appears, type hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="68d5b-186">(Você também pode adicionar outros usuários do cluster em funções diferentes.</span><span class="sxs-lookup"><span data-stu-id="68d5b-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="68d5b-187">Consulte [Gerenciando Usuários de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="68d5b-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="68d5b-188">o portal da web Hello abre o modo de exibição de lista de trabalho toohello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-188">hello web portal opens toohello job list view.</span></span>
3. <span data-ttu-id="68d5b-189">toosubmit um trabalho de exemplo que retorna a cadeia de caracteres de saudação "Olá, mundo" do cluster Olá, clique em **novo trabalho** na navegação esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-189">toosubmit a sample job that returns hello string “Hello World” from hello cluster, click **New job** in hello left-hand navigation.</span></span>
4. <span data-ttu-id="68d5b-190">Em Olá **novo trabalho** página em **das páginas de envio**, clique em **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-190">On hello **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="68d5b-191">página de envio de trabalho Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="68d5b-191">hello job submission page appears.</span></span>
5. <span data-ttu-id="68d5b-192">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="68d5b-192">Click **Submit**.</span></span> <span data-ttu-id="68d5b-193">Se solicitado, forneça credenciais de domínio de saudação do administrador de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="68d5b-193">If prompted, provide hello domain credentials of hello HPC cluster administrator.</span></span> <span data-ttu-id="68d5b-194">Olá trabalho é enviado e ID do trabalho Olá aparece no hello **Meus trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="68d5b-194">hello job is submitted, and hello job ID appears on hello **My Jobs** page.</span></span>
6. <span data-ttu-id="68d5b-195">resultados de saudação do tooview de trabalho de saudação enviado, clique em ID do trabalho Olá e, em seguida, clique em **exibir tarefas** tooview saída do comando de saudação (em **saída**).</span><span class="sxs-lookup"><span data-stu-id="68d5b-195">tooview hello results of hello job that you submitted, click hello job ID, and then click **View Tasks** tooview hello command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68d5b-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68d5b-196">Next steps</span></span>
* <span data-ttu-id="68d5b-197">Você também pode enviar trabalhos toohello cluster do Azure com hello [API REST do HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="68d5b-197">You can also submit jobs toohello Azure cluster with hello [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="68d5b-198">Se você quiser toosubmit trabalhos de cluster de um cliente Linux, consulte Olá Python exemplo no hello [SDK do HPC Pack 2012 R2 e o código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="68d5b-198">If you want toosubmit cluster jobs from a Linux client, see hello Python sample in hello [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
