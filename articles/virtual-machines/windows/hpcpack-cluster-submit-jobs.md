---
title: Enviar trabalhos para um cluster do Pacote HPC no Azure | Microsoft Docs
description: Saiba como configurar um computador local para enviar trabalhos para um cluster de Pacote HPC no Azure
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
ms.openlocfilehash: d5953f1e1dd2deb4d871bd67352a6a5b2ae13dbf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-to-an-hpc-pack-cluster-deployed-in-azure"></a><span data-ttu-id="d1e9b-103">Enviar trabalhos HPC de um computador local para um cluster de Pacote HPC implantado no Azure</span><span class="sxs-lookup"><span data-stu-id="d1e9b-103">Submit HPC jobs from an on-premises computer to an HPC Pack cluster deployed in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d1e9b-104">Configure um computador cliente local para enviar trabalhos para um cluster de [Pacote Microsoft HPC](https://technet.microsoft.com/library/cc514029) no Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-104">Configure an on-premises client computer to submit jobs to a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure.</span></span> <span data-ttu-id="d1e9b-105">Este artigo mostra como configurar um computador local com as ferramentas de cliente para enviar o trabalho por HTTPS para o cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-105">This article shows you how to set up a local computer with client tools to submit job over HTTPS to the cluster in Azure.</span></span> <span data-ttu-id="d1e9b-106">Dessa forma, vários usuários de cluster podem enviar trabalhos para um cluster de Pacote HPC baseado em nuvem, mas sem se conectar diretamente à VM do nó principal ou acessar uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-106">In this way, several cluster users can submit jobs to a cloud-based HPC Pack cluster, but without connecting directly to the head node VM or accessing an Azure subscription.</span></span>

![Enviar um trabalho para um cluster no Azure][jobsubmit]

## <a name="prerequisites"></a><span data-ttu-id="d1e9b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d1e9b-108">Prerequisites</span></span>
* <span data-ttu-id="d1e9b-109">**Nó de cabeçalho do HPC Pack implantado em uma VM do Azure** – Recomendamos o uso de ferramentas automatizadas como um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) ou um [script do Azure PowerShell](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para implantar o nó de cabeçalho e o cluster.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-109">**HPC Pack head node deployed in an Azure VM** - We recommend that you use automated tools such as an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/) or an [Azure PowerShell script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to deploy the head node and cluster.</span></span> <span data-ttu-id="d1e9b-110">Você precisa do nome DNS do nó principal e as credenciais de um administrador de cluster para concluir as etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-110">You need the DNS name of the head node and the credentials of a cluster administrator to complete the steps in this article.</span></span>
* <span data-ttu-id="d1e9b-111">**Computador cliente** – você precisa de um computador Windows Client ou Windows Server que possa executar utilitários de cliente do Pacote HPC (consulte os [requisitos do sistema](https://technet.microsoft.com/library/dn535781.aspx)).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-111">**Client computer** - You need a Windows or Windows Server client computer that can run HPC Pack client utilities (see [system requirements](https://technet.microsoft.com/library/dn535781.aspx)).</span></span> <span data-ttu-id="d1e9b-112">Se você quiser usar a API REST ou o portal da Web do Pacote HPC para enviar trabalhos, poderá usar qualquer computador cliente de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-112">If you only want to use the HPC Pack web portal or REST API to submit jobs, you can use any client computer of your choice.</span></span>
* <span data-ttu-id="d1e9b-113">**Mídia de instalação do Pacote HPC** - Para instalar os utilitários de cliente do Pacote HPC, o pacote de instalação gratuita para a versão mais recente do Pacote HPC (Pacote HPC 2012 R2) está disponível no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-113">**HPC Pack installation media** - To install the HPC Pack client utilities, the free installation package for the latest version of HPC Pack (HPC Pack 2012 R2) is available from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="d1e9b-114">Confira se você baixou a mesma versão do Pacote HPC que está instalada na VM do nó principal.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-114">Make sure that you download the same version of HPC Pack that is installed on the head node VM.</span></span>

## <a name="step-1-install-and-configure-the-web-components-on-the-head-node"></a><span data-ttu-id="d1e9b-115">Etapa 1: instalar e configurar os componentes Web no nó principal</span><span class="sxs-lookup"><span data-stu-id="d1e9b-115">Step 1: Install and configure the web components on the head node</span></span>
<span data-ttu-id="d1e9b-116">Para habilitar uma interface REST para enviar trabalhos ao cluster por HTTPS, certifique-se de que os componentes Web Pacote HPC estejam configurados no nó principal do Pacote HPC.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-116">To enable a REST interface to submit jobs to the cluster over HTTPS, ensure that the HPC Pack web components are configured on the HPC Pack head node.</span></span> <span data-ttu-id="d1e9b-117">Se eles ainda não estiverem instalados, você deverá primeiro instalar os componentes Web executando o arquivo de instalação HpcWebComponents.msi.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-117">If they aren't already installed, first install the web components by running the HpcWebComponents.msi installation file.</span></span> <span data-ttu-id="d1e9b-118">Em seguida, configure os componentes executando o script do HPC PowerShell **Set-HPCWebComponents.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-118">Then, configure the components by running the HPC PowerShell script **Set-HPCWebComponents.ps1**.</span></span>

<span data-ttu-id="d1e9b-119">Para obter procedimentos detalhados, consulte [Instalar os componentes Web do Microsoft Pacote HPC](http://technet.microsoft.com/library/hh314627.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-119">For detailed procedures, see [Install the Microsoft HPC Pack Web Components](http://technet.microsoft.com/library/hh314627.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="d1e9b-120">Alguns modelos de início rápido do Azure para o HPC Pack instalam e configuram os componentes Web automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-120">Certain Azure quickstart templates for HPC Pack install and configure the web components automatically.</span></span> <span data-ttu-id="d1e9b-121">Se você usar o [script de implantação do Pacote HPC IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) para criar o cluster, pode, opcionalmente, instalar e configurar os componentes Web como parte da implantação.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-121">If you use the [HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to create the cluster, you can optionally install and configure the web components as part of the deployment.</span></span>
> 
> 

<span data-ttu-id="d1e9b-122">**Para instalar os componentes Web**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-122">**To install the web components**</span></span>

1. <span data-ttu-id="d1e9b-123">Conecte-se à VM do nó principal usando as credenciais de um administrador de cluster.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-123">Connect to the head node VM by using the credentials of a cluster administrator.</span></span>
2. <span data-ttu-id="d1e9b-124">Na pasta de instalação do Pacote HPC, execute HpcWebcomponents.msi no nó principal.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-124">From the HPC Pack Setup folder, run HpcWebComponents.msi on the head node.</span></span>
3. <span data-ttu-id="d1e9b-125">Siga as etapas no Assistente para instalar os componentes Web</span><span class="sxs-lookup"><span data-stu-id="d1e9b-125">Follow the steps in the wizard to install the web components</span></span>

<span data-ttu-id="d1e9b-126">**Para configurar os componentes Web**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-126">**To configure the web components**</span></span>

1. <span data-ttu-id="d1e9b-127">No nó principal, inicie o PowerShell HPC como administrador.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-127">On the head node, start HPC PowerShell as an administrator.</span></span>
2. <span data-ttu-id="d1e9b-128">Para alterar o diretório para o local do script de configuração, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-128">To change directory to the location of the configuration script, type the following command:</span></span>
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. <span data-ttu-id="d1e9b-129">Para configurar a interface REST e iniciar o serviço Web HPC, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-129">To configure the REST interface and start the HPC Web Service, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. <span data-ttu-id="d1e9b-130">Quando for solicitado que você selecione um certificado, escolha o certificado que corresponde ao nome DNS público do nó principal.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-130">When prompted to select a certificate, choose the certificate that corresponds to the public DNS name of the head node.</span></span> <span data-ttu-id="d1e9b-131">Por exemplo, se você implantar a VM do nó de cabeçalho usando o modelo de implantação clássica, o nome do certificado terá a forma CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-131">For example, if you deploy the head node VM using the classic deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net.</span></span> <span data-ttu-id="d1e9b-132">Se você usar um modelo de implantação do Gerenciador de Recursos, o nome do certificado terá a forma CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-132">If you use the Resource Manager deployment model, the certificate name looks like CN=&lt;*HeadNodeDnsName*&gt;.&lt;*region*&gt;.cloudapp.azure.com.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1e9b-133">Você selecionará esse certificado posteriormente quando enviar trabalhos de um computador local para o nó principal.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-133">You select this certificate later when you submit jobs to the head node from an on-premises computer.</span></span> <span data-ttu-id="d1e9b-134">Não selecione nem configure um certificado que corresponda ao nome do computador do nó principal no domínio do Active Directory (por exemplo, CN=*MyHPCHeadNode.HpcAzure.local*).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-134">Don't select or configure a certificate that corresponds to the computer name of the head node in the Active Directory domain (for example, CN=*MyHPCHeadNode.HpcAzure.local*).</span></span>
   > 
   > 
5. <span data-ttu-id="d1e9b-135">Para configurar o portal da Web para envio de trabalho, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-135">To configure the web portal for job submission, type the following command:</span></span>
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. <span data-ttu-id="d1e9b-136">Depois que o script for concluído, pare e reinicie o serviço do Agendador de trabalho do HPC digitando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-136">After the script completes, stop and restart the HPC Job Scheduler Service by typing the following commands:</span></span>
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-the-hpc-pack-client-utilities-on-an-on-premises-computer"></a><span data-ttu-id="d1e9b-137">Etapa 2: instalar os utilitários de cliente do Pacote HPC em um computador local</span><span class="sxs-lookup"><span data-stu-id="d1e9b-137">Step 2: Install the HPC Pack client utilities on an on-premises computer</span></span>
<span data-ttu-id="d1e9b-138">Se você desejar instalar os utilitários do Pacote HPC no computador cliente, baixe os arquivos de instalação do Pacote HPC (instalação completa) pelo [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=328024).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-138">If you want to install the HPC Pack client utilities on your computer, download the HPC Pack setup files (full installation) from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=328024).</span></span> <span data-ttu-id="d1e9b-139">Quando você começar a instalação, escolha a opção de instalação dos **utilitários cliente do Pacote HPC**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-139">When you begin the installation, choose the setup option for the **HPC Pack client utilities**.</span></span>

<span data-ttu-id="d1e9b-140">Para usar as ferramentas clientes Pacote HPC para enviar trabalhos para a VM do nó principal, você também precisa exportar um certificado do nó principal e instalá-lo no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-140">To use the HPC Pack client tools to submit jobs to the head node VM, you also need to export a certificate from the head node and install it on the client computer.</span></span> <span data-ttu-id="d1e9b-141">O certificado deve estar no formato .CER.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-141">The certificate must be in .CER format.</span></span>

<span data-ttu-id="d1e9b-142">**Para exportar o certificado do nó principal**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-142">**To export the certificate from the head node**</span></span>

1. <span data-ttu-id="d1e9b-143">No nó principal, adicione o snap-in de Certificados ao Console de Gerenciamento Microsoft para a conta do computador local.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-143">On the head node, add the Certificates snap-in to a Microsoft Management Console for the Local Computer account.</span></span> <span data-ttu-id="d1e9b-144">Para obter as etapas para adicionar o snap-in, consulte [Adicionar o Snap-in de Certificados a um MMC](https://technet.microsoft.com/library/cc754431.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-144">For steps to add the snap-in, see [Add the Certificates Snap-in to an MMC](https://technet.microsoft.com/library/cc754431.aspx).</span></span>
2. <span data-ttu-id="d1e9b-145">Na árvore de console, expanda **Certificados – Computador Local** > **Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-145">In the console tree, expand **Certificates – Local Computer** > **Personal**, and then click **Certificates**.</span></span>
3. <span data-ttu-id="d1e9b-146">Localize o certificado que você configurou para os componentes Web do Pacote HPC na [Etapa 1: Instalar e configurar os componentes Web no nó principal](#step-1:-install-and-configure-the-web-components-on-the-head-node) (por exemplo, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-146">Locate the certificate that you configured for the HPC Pack web components in [Step 1: Install and configure the web components on the head node](#step-1:-install-and-configure-the-web-components-on-the-head-node) (for example, CN=&lt;*HeadNodeDnsName*&gt;.cloudapp.net).</span></span>
4. <span data-ttu-id="d1e9b-147">Clique com o botão direito do mouse no certificado e selecione **Todas as Tarefas** > **Exportar**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-147">Right-click the certificate, and click **All Tasks** > **Export**.</span></span>
5. <span data-ttu-id="d1e9b-148">No Assistente de Exportação de Certificados, clique em **Avançar** e escolha a opção **Não, não exporte a chave particular**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-148">In the Certificate Export Wizard, click **Next**, and ensure that **No, do not export the private key** is selected.</span></span>
6. <span data-ttu-id="d1e9b-149">Siga as etapas restantes do Assistente para exportar o certificado no formato DER binário X.509 codificado (.CER).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-149">Follow the remaining steps of the wizard to export the certificate in DER encoded binary X.509 (.CER) format.</span></span>

<span data-ttu-id="d1e9b-150">**Para importar o certificado no computador cliente**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-150">**To import the certificate on the client computer**</span></span>

1. <span data-ttu-id="d1e9b-151">Copie o certificado exportado do nó principal para uma pasta no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-151">Copy the certificate that you exported from the head node to a folder on the client computer.</span></span>
2. <span data-ttu-id="d1e9b-152">No computador cliente, execute o certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-152">On the client computer, run certmgr.msc.</span></span>
3. <span data-ttu-id="d1e9b-153">No Gerenciador de Certificados, expanda **Certificados – Usuário atual** > **Autoridades de Certificação Confiáveis**, clique com o botão direito do mouse em **Certificados** e clique em **Todas as Tarefas** > **Importar**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-153">In Certificate Manager, expand **Certificates – Current user** > **Trusted Root Certification Authorities**, right-click **Certificates**, and then click **All Tasks** > **Import**.</span></span>
4. <span data-ttu-id="d1e9b-154">No Assistente de Importação de Certificados, clique em **Avançar** e siga as etapas para importar o certificado exportado do nó principal para o repositório de Autoridades de Certificação Confiáveis.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-154">In the Certificate Import Wizard, click **Next** and follow the steps to import the certificate that you exported from the head node to the Trusted Root Certification Authorities store.</span></span>

> [!TIP]
> <span data-ttu-id="d1e9b-155">Você pode ver um aviso de segurança, já que a autoridade de certificação no nó principal não é reconhecida pelo computador cliente.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-155">You might see a security warning, because the certification authority on the head node isn't recognized by the client computer.</span></span> <span data-ttu-id="d1e9b-156">Para fins de teste, você pode ignorar esse aviso e concluir a importação de certificados.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-156">For testing purposes, you can ignore this warning and complete the certificate import.</span></span>
> 
> 

## <a name="step-3-run-test-jobs-on-the-cluster"></a><span data-ttu-id="d1e9b-157">Etapa 3: executar trabalhos de teste no cluster</span><span class="sxs-lookup"><span data-stu-id="d1e9b-157">Step 3: Run test jobs on the cluster</span></span>
<span data-ttu-id="d1e9b-158">Para verificar a configuração, tente executar trabalhos no cluster no Azure usando o computador local.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-158">To verify your configuration, try running jobs on the cluster in Azure from the on-premises computer.</span></span> <span data-ttu-id="d1e9b-159">Por exemplo, você pode usar ferramentas de GUI do Pacote HPC ou comandos de linha de comando para enviar trabalhos para o cluster.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-159">For example, you can use HPC Pack GUI tools or command-line commands to submit jobs to the cluster.</span></span> <span data-ttu-id="d1e9b-160">Você também pode usar um portal baseado na Web para enviar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-160">You can also use a web-based portal to submit jobs.</span></span>

<span data-ttu-id="d1e9b-161">**Para executar comandos de envio de trabalho no computador cliente**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-161">**To run job submission commands on the client computer**</span></span>

1. <span data-ttu-id="d1e9b-162">Em um computador cliente em que os utilitários de cliente do Pacote HPC estão instalados, inicie um Prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-162">On a client computer where the HPC Pack client utilities are installed, start a Command Prompt.</span></span>
2. <span data-ttu-id="d1e9b-163">Digite um comando de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-163">Type a sample command.</span></span> <span data-ttu-id="d1e9b-164">Por exemplo, para listar todos os trabalhos no cluster, digite um comando semelhante a uma das opções a seguir, dependendo do nome DNS completo do nó principal:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-164">For example, to list all jobs on the cluster, type a command similar to one of the following, depending on the full DNS name of the head node:</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    <span data-ttu-id="d1e9b-165">ou o</span><span class="sxs-lookup"><span data-stu-id="d1e9b-165">or</span></span>
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > <span data-ttu-id="d1e9b-166">Use o nome DNS completo do nó principal, não o endereço IP, na URL do Agendador.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-166">Use the full DNS name of the head node, not the IP address, in the scheduler URL.</span></span> <span data-ttu-id="d1e9b-167">Se você especificar o endereço IP, verá um erro semelhante a "O certificado do servidor precisa ter uma cadeia de confiança válida ou ser colocado no repositório raiz confiável".</span><span class="sxs-lookup"><span data-stu-id="d1e9b-167">If you specify the IP address, an error appears similar to "The server certificate needs to either have a valid chain of trust or to be placed in the trusted root store."</span></span>
   > 
   > 
3. <span data-ttu-id="d1e9b-168">Quando solicitado, digite o nome de usuário (com a forma &lt;DomainName&gt;\\&lt;UserName&gt;) e a senha do administrador do cluster HPC ou de outro usuário do cluster configurado.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-168">When prompted, type the user name (in the form &lt;DomainName&gt;\\&lt;UserName&gt;) and password of the HPC cluster administrator or another cluster user that you configured.</span></span> <span data-ttu-id="d1e9b-169">Você pode optar por armazenar as credenciais localmente para mais operações de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-169">You can choose to store the credentials locally for more job operations.</span></span>
   
    <span data-ttu-id="d1e9b-170">Uma lista de trabalhos é exibida.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-170">A list of jobs appears.</span></span>

<span data-ttu-id="d1e9b-171">**Para usar o gerenciador de trabalhos de HPC no computador cliente**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-171">**To use HPC Job Manager on the client computer**</span></span>

1. <span data-ttu-id="d1e9b-172">Se você não armazenou anteriormente credenciais de domínio para um usuário de cluster no computador cliente ao enviar o trabalho, pode adicionar as credenciais no Gerenciador de Credenciais.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-172">If you didn't previously store domain credentials for a cluster user when submitting a job, you can add the credentials in Credential Manager.</span></span>
   
    <span data-ttu-id="d1e9b-173">a.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-173">a.</span></span> <span data-ttu-id="d1e9b-174">No painel de controle no computador cliente, inicie o Gerenciador de Credenciais.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-174">In Control Panel on the client computer, start Credential Manager.</span></span>
   
    <span data-ttu-id="d1e9b-175">b.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-175">b.</span></span> <span data-ttu-id="d1e9b-176">Clique nas **Credenciais do Windows** > **Adicionar uma credencial genérica**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-176">Click **Windows Credentials** > **Add a generic credential**.</span></span>
   
    <span data-ttu-id="d1e9b-177">c.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-177">c.</span></span> <span data-ttu-id="d1e9b-178">Especifique o endereço de Internet (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler ou https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler) e o nome de usuário (&lt;DomainName&gt;\\&lt;UserName&gt;) e a senha do administrador do cluster ou outro usuário do cluster que você configurou.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-178">Specify the Internet address (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com/HpcScheduler), and the user name (&lt;DomainName&gt;\\&lt;UserName&gt;) and password of the cluster administrator or another cluster user that you configured.</span></span>
2. <span data-ttu-id="d1e9b-179">No computador cliente, inicie o gerenciador de trabalho do HPC.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-179">On the client computer, start HPC Job Manager.</span></span>
3. <span data-ttu-id="d1e9b-180">Na caixa de diálogo **Selecionar nó principal**, digite a URL do nó principal no Azure (por exemplo, https://&lt;HeadNodeDnsName&gt;.cloudapp.net ou https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.com).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-180">In the **Select Head Node** dialog box, type the URL to the head node in Azure (for example, https://&lt;HeadNodeDnsName&gt;.cloudapp.net or https://&lt;HeadNodeDnsName&gt;.&lt;region&gt;.cloudapp.azure.com).</span></span>
   
    <span data-ttu-id="d1e9b-181">O gerenciador de trabalhos do HPC abre e mostra uma lista de trabalhos no nó principal.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-181">HPC Job Manager opens and shows a list of jobs on the head node.</span></span>

<span data-ttu-id="d1e9b-182">**Para usar o portal da Web no nó de cabeçalho**</span><span class="sxs-lookup"><span data-stu-id="d1e9b-182">**To use the web portal running on the head node**</span></span>

1. <span data-ttu-id="d1e9b-183">Inicie um navegador da Web no computador cliente e digite um dos endereços a seguir, dependendo do nome DNS completo do nó principal:</span><span class="sxs-lookup"><span data-stu-id="d1e9b-183">Start a web browser on the client computer, and enter one of the following addresses, depending on the full DNS name of the head node:</span></span>
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    <span data-ttu-id="d1e9b-184">ou o</span><span class="sxs-lookup"><span data-stu-id="d1e9b-184">or</span></span>
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. <span data-ttu-id="d1e9b-185">Na caixa de diálogo de segurança, digite as credenciais de domínio do administrador de cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-185">In the security dialog box that appears, type the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="d1e9b-186">(Você também pode adicionar outros usuários do cluster em funções diferentes.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-186">(You can also add other cluster users in different roles.</span></span> <span data-ttu-id="d1e9b-187">Consulte [Gerenciando Usuários de Cluster](https://technet.microsoft.com/library/ff919335.aspx).)</span><span class="sxs-lookup"><span data-stu-id="d1e9b-187">See [Managing Cluster Users](https://technet.microsoft.com/library/ff919335.aspx).)</span></span>
   
    <span data-ttu-id="d1e9b-188">O portal da Web abre no modo de exibição de lista de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-188">The web portal opens to the job list view.</span></span>
3. <span data-ttu-id="d1e9b-189">Para enviar um trabalho de exemplo que retorna a cadeia de caracteres "Olá, Mundo" do cluster, clique em **Novo trabalho** no painel de navegação esquerdo.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-189">To submit a sample job that returns the string “Hello World” from the cluster, click **New job** in the left-hand navigation.</span></span>
4. <span data-ttu-id="d1e9b-190">Na página **Novo Trabalho**, em **Das páginas de envio**, clique em **HelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-190">On the **New Job** page, under **From submission pages**, click **HelloWorld**.</span></span> <span data-ttu-id="d1e9b-191">A página de envio de trabalho é exibida.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-191">The job submission page appears.</span></span>
5. <span data-ttu-id="d1e9b-192">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-192">Click **Submit**.</span></span> <span data-ttu-id="d1e9b-193">Se solicitado, forneça as credenciais de domínio do administrador de cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-193">If prompted, provide the domain credentials of the HPC cluster administrator.</span></span> <span data-ttu-id="d1e9b-194">O trabalho é enviado e a ID de trabalho aparece na página **Meus Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="d1e9b-194">The job is submitted, and the job ID appears on the **My Jobs** page.</span></span>
6. <span data-ttu-id="d1e9b-195">Para exibir os resultados do trabalho enviado, clique na ID do trabalho e em **Exibir Tarefas** para exibir a saída do comando (em **Saída**).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-195">To view the results of the job that you submitted, click the job ID, and then click **View Tasks** to view the command output (under **Output**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1e9b-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1e9b-196">Next steps</span></span>
* <span data-ttu-id="d1e9b-197">Você também pode enviar trabalhos para o cluster do Azure com a [API REST do Pacote HPC](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-197">You can also submit jobs to the Azure cluster with the [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span>
* <span data-ttu-id="d1e9b-198">Se você quiser enviar trabalhos do cluster de um cliente Linux, consulte o exemplo do Python no [SDK do Pacote HPC 2012 R2 e código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="d1e9b-198">If you want to submit cluster jobs from a Linux client, see the Python sample in the [HPC Pack 2012 R2 SDK and Sample Code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span>

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
