---
title: "agentes de VM do Azure aaaUse para integração contínua com Jenkins."
description: "Agentes de VM do Azure como Jenkins secundários."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="fe73b-103">Use agentes de VM do Azure para a integração contínua com Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fe73b-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="fe73b-104">Este guia de início rápido mostra como toouse Olá toocreate de plug-in de agentes de VM do Azure Jenkins um agente do Linux (Ubuntu) sob demanda no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe73b-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe73b-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fe73b-105">Prerequisites</span></span>

<span data-ttu-id="fe73b-106">toocomplete este guia de início rápido:</span><span class="sxs-lookup"><span data-stu-id="fe73b-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="fe73b-107">Se você ainda não tiver um mestre Jenkins, você pode iniciar com hello [modelo de solução](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="fe73b-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="fe73b-108">Consulte também[criar uma entidade de serviço do Azure com o Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) se você ainda não tiver uma entidade de serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe73b-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="fe73b-109">Instale o plug-in de agentes da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="fe73b-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="fe73b-110">Se você iniciar da saudação [solução modelo](install-jenkins-solution-template.md), plug-in do hello Azure VM Agent está instalado no mestre de Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="fe73b-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="fe73b-111">Caso contrário, instalar Olá **agentes de VM do Azure** plug-in de dentro do painel de controle do hello Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fe73b-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="fe73b-112">Configurar o plug-in de saudação</span><span class="sxs-lookup"><span data-stu-id="fe73b-112">Configure hello plugin</span></span>

* <span data-ttu-id="fe73b-113">No painel do Jenkins hello, clique em **Jenkins Gerenciar -> configurar o sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="fe73b-114">Role toohello inferior da página de saudação e localize a seção de Olá Olá suspensa **adicionar nova nuvem**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="fe73b-115">No menu de saudação, selecione **agentes de VM do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="fe73b-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="fe73b-116">Selecione uma conta existente na lista suspensa do hello credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe73b-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="fe73b-117">tooadd um novo **entidade de serviço do Microsoft Azure,** digite Olá valores a seguir: ID de assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="fe73b-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Credenciais do Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="fe73b-119">Clique em **Verificar configuração** toomake-se de que perfil Olá a configuração está correta.</span><span class="sxs-lookup"><span data-stu-id="fe73b-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="fe73b-120">Salvar configuração hello e continuar toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="fe73b-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="fe73b-121">Configuração do modelo</span><span class="sxs-lookup"><span data-stu-id="fe73b-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="fe73b-122">Configuração geral</span><span class="sxs-lookup"><span data-stu-id="fe73b-122">General configuration</span></span>
<span data-ttu-id="fe73b-123">Em seguida, configure um modelo para uso toodefine um agente de VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe73b-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="fe73b-124">Clique em **adicionar** tooadd um modelo.</span><span class="sxs-lookup"><span data-stu-id="fe73b-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="fe73b-125">Forneça um nome para o seu novo modelo.</span><span class="sxs-lookup"><span data-stu-id="fe73b-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="fe73b-126">Rótulo de hello, digite "ubuntu."</span><span class="sxs-lookup"><span data-stu-id="fe73b-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="fe73b-127">Esse rótulo é usado durante a configuração de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="fe73b-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="fe73b-128">Selecione região desejada Olá Olá na caixa de combinação.</span><span class="sxs-lookup"><span data-stu-id="fe73b-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="fe73b-129">Selecione Olá desejada do tamanho da VM.</span><span class="sxs-lookup"><span data-stu-id="fe73b-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="fe73b-130">Especifique o nome de conta de armazenamento do Azure hello ou deixe em branco toouse Olá padrao "jenkinsarmst".</span><span class="sxs-lookup"><span data-stu-id="fe73b-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="fe73b-131">Especifique o tempo de retenção de saudação em minutos.</span><span class="sxs-lookup"><span data-stu-id="fe73b-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="fe73b-132">Essa configuração define o número de saudação de minutos que Jenkins pode aguardar antes de excluir automaticamente um agente ocioso.</span><span class="sxs-lookup"><span data-stu-id="fe73b-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="fe73b-133">Especifique 0 se não quiser toobe agentes ocioso excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fe73b-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Configuração geral](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="fe73b-135">Configuração de imagem</span><span class="sxs-lookup"><span data-stu-id="fe73b-135">Image configuration</span></span>

<span data-ttu-id="fe73b-136">toocreate um agente do Linux (Ubuntu), selecione **referência da imagem** e use Olá seguinte configuração de exemplo.</span><span class="sxs-lookup"><span data-stu-id="fe73b-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="fe73b-137">Consulte também[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) para hello Azure mais recente com suporte a imagens.</span><span class="sxs-lookup"><span data-stu-id="fe73b-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="fe73b-138">Publicador de imagem: Canonical</span><span class="sxs-lookup"><span data-stu-id="fe73b-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="fe73b-139">Oferta de imagem: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="fe73b-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="fe73b-140">Sku de imagem: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="fe73b-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="fe73b-141">Versão da imagem: mais recente</span><span class="sxs-lookup"><span data-stu-id="fe73b-141">Image version: latest</span></span>
* <span data-ttu-id="fe73b-142">Tipo de sistema operacional: Linux</span><span class="sxs-lookup"><span data-stu-id="fe73b-142">OS Type: Linux</span></span>
* <span data-ttu-id="fe73b-143">Inicie o método: SSH</span><span class="sxs-lookup"><span data-stu-id="fe73b-143">Launch method: SSH</span></span>
* <span data-ttu-id="fe73b-144">Forneça credenciais de administrador</span><span class="sxs-lookup"><span data-stu-id="fe73b-144">Provide an admin credentials</span></span>
* <span data-ttu-id="fe73b-145">Para o script de inicialização de VM, digite:</span><span class="sxs-lookup"><span data-stu-id="fe73b-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuração de imagem](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="fe73b-147">Clique em **Verificar modelo** tooverify configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe73b-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="fe73b-148">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="fe73b-149">Crie um trabalho no Jenkins</span><span class="sxs-lookup"><span data-stu-id="fe73b-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="fe73b-150">No painel do Jenkins hello, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="fe73b-151">Insira um nome e selecione **Projeto Freestyle** e clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="fe73b-152">Em Olá **geral** , selecione "Restringir onde o projeto pode ser executado" e digite "ubuntu" na expressão de rótulo.</span><span class="sxs-lookup"><span data-stu-id="fe73b-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="fe73b-153">Agora, você verá "ubuntu" no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe73b-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="fe73b-154">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-154">Click **Save**.</span></span>

![Configure o trabalho](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="fe73b-156">Compile o seu novo projeto</span><span class="sxs-lookup"><span data-stu-id="fe73b-156">Build your new project</span></span>

* <span data-ttu-id="fe73b-157">Volte toohello Jenkins painel.</span><span class="sxs-lookup"><span data-stu-id="fe73b-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="fe73b-158">Novo trabalho de saudação de atalho que você criou, clique em **compilar agora**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="fe73b-159">Uma compilação é iniciada.</span><span class="sxs-lookup"><span data-stu-id="fe73b-159">A build is kicked off.</span></span> 
* <span data-ttu-id="fe73b-160">Após a conclusão da compilação hello, ir muito**saída de Console**.</span><span class="sxs-lookup"><span data-stu-id="fe73b-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="fe73b-161">Você verá que a compilação de saudação foi executada remotamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe73b-161">You see that hello build was performed remotely on Azure.</span></span>

![Saída do console](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="fe73b-163">Referência</span><span class="sxs-lookup"><span data-stu-id="fe73b-163">Reference</span></span>

* <span data-ttu-id="fe73b-164">Vídeo de sexta-feira do Azure: [Integração contínua com Jenkins usando agentes de VM do Azure](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span><span class="sxs-lookup"><span data-stu-id="fe73b-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="fe73b-165">Opções de configuração e as informações de suporte: [Wiki de plug-in do Jenkins de agente de VM do Azure](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="fe73b-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

