---
title: aaaDeploy seu primeiro tooCloud de aplicativo Foundry no Microsoft Azure | Microsoft Docs
description: Implantar um aplicativo tooCloud Foundry no Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="15d8a-103">Implantar seu primeiro tooCloud de aplicativo Foundry no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="15d8a-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="15d8a-104">O [Cloud Foundry](http://cloudfoundry.org) é uma plataforma de aplicativos populares de software livre disponível no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="15d8a-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="15d8a-105">Neste artigo, mostramos como toodeploy e gerenciar um aplicativo em nuvem Foundry em um ambiente do Azure.</span><span class="sxs-lookup"><span data-stu-id="15d8a-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="15d8a-106">Criar um ambiente do Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="15d8a-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="15d8a-107">Há várias opções para a criação de um ambiente do Cloud Foundry no Azure:</span><span class="sxs-lookup"><span data-stu-id="15d8a-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="15d8a-108">Saudação de uso [oferta Foundry essencial de nuvem] [ pcf-azuremarketplace] em hello Azure Marketplace toocreate um ambiente padrão que inclui PCF Ops Manager e hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="15d8a-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="15d8a-109">Você pode encontrar [concluir instruções] [ pcf-azuremarketplace-pivotaldocs] para implantar o marketplace Olá oferecem em Olá documentação crucial.</span><span class="sxs-lookup"><span data-stu-id="15d8a-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="15d8a-110">Crie um ambiente personalizado [implantando o Pivotal Cloud Foundry manualmente][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="15d8a-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="15d8a-111">[Implantar pacotes de nuvem Foundry do código-fonte aberto Olá diretamente] [ oss-cf-bosh] Configurando um [BOSH](http://bosh.io) diretor, uma VM que coordena a implantação de saudação do ambiente de nuvem Foundry hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="15d8a-112">Se você estiver implantando PCF de hello Azure Marketplace, anote Olá SYSTEMDOMAINURL e credenciais de administrador Olá necessário tooaccess Olá essencial Gerenciador de aplicativos, que são descritas no guia de implantação do marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="15d8a-113">Eles é necessário toocomplete neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="15d8a-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="15d8a-114">Para implantações do marketplace, Olá SYSTEMDOMAINURL está Olá formulário https://system. *endereço ip*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="15d8a-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="15d8a-115">Conecte-se toohello controlador da nuvem</span><span class="sxs-lookup"><span data-stu-id="15d8a-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="15d8a-116">Olá controlador da nuvem é o ambiente de nuvem Foundry de tooa de ponto de entrada primária de Olá para implantar e gerenciar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="15d8a-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="15d8a-117">núcleo de saudação API de controlador de nuvem (CCAPI) é uma API REST, mas está acessível por meio de várias ferramentas.</span><span class="sxs-lookup"><span data-stu-id="15d8a-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="15d8a-118">Nesse caso, estamos interagir com ele por meio de saudação [nuvem Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="15d8a-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="15d8a-119">Você pode instalar Olá CLI no Linux, MacOS ou Windows, mas se você preferir não tooinstall, ele está disponível pré-instalado em Olá [Shell de nuvem do Azure][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="15d8a-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="15d8a-120">toolog, preceda `api` toohello SYSTEMDOMAINURL que você obteve da implantação do marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="15d8a-121">Desde que a implantação padrão de saudação usa um certificado autoassinado, você também deve incluir Olá `skip-ssl-validation` alternar.</span><span class="sxs-lookup"><span data-stu-id="15d8a-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="15d8a-122">Você está toolog solicitada no toohello controlador da nuvem.</span><span class="sxs-lookup"><span data-stu-id="15d8a-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="15d8a-123">Use credenciais de conta de administrador de saudação que você copiou de etapas de implantação do marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="15d8a-124">Nuvem Foundry fornece *organizações* e *espaços* como equipes de saudação tooisolate namespaces e ambientes em uma implantação compartilhada.</span><span class="sxs-lookup"><span data-stu-id="15d8a-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="15d8a-125">Olá implantação do marketplace PCF inclui padrão Olá *sistema* organizacional e um conjunto de espaços toocontain Olá base componentes criados, como serviço de dimensionamento automático hello e hello Azure do service broker.</span><span class="sxs-lookup"><span data-stu-id="15d8a-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="15d8a-126">Por enquanto, escolha Olá *sistema* espaço.</span><span class="sxs-lookup"><span data-stu-id="15d8a-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="15d8a-127">Criar uma organização e um espaço</span><span class="sxs-lookup"><span data-stu-id="15d8a-127">Create an org and space</span></span>

<span data-ttu-id="15d8a-128">Se você digitar `cf apps`, verá um conjunto de aplicativos do sistema que foram implantados no espaço de sistema hello dentro Olá sistema org</span><span class="sxs-lookup"><span data-stu-id="15d8a-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="15d8a-129">Você deve manter Olá *sistema* org reservado para aplicativos do sistema, portanto, crie um toohouse org e espaço de nosso aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="15d8a-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="15d8a-130">Use Olá destino comando tooswitch toohello nova organização e espaço:</span><span class="sxs-lookup"><span data-stu-id="15d8a-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="15d8a-131">Agora, quando você implanta um aplicativo, ele é criado automaticamente no espaço e Olá org de novo.</span><span class="sxs-lookup"><span data-stu-id="15d8a-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="15d8a-132">tooconfirm atualmente, há nenhum aplicativo hello novo org/espaço, digite `cf apps` novamente.</span><span class="sxs-lookup"><span data-stu-id="15d8a-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="15d8a-133">Para obter mais informações sobre organizações e espaços, e como eles podem ser usados para controle de acesso baseado em função (RBAC), consulte Olá [documentação nuvem Foundry][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="15d8a-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="15d8a-134">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="15d8a-134">Deploy an application</span></span>

<span data-ttu-id="15d8a-135">Vamos usar um aplicativo de nuvem Foundry de exemplo chamado Hello Spring nuvem, que é escrito em Java e com base em Olá [Spring Framework](http://spring.io) e [Spring inicialização](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="15d8a-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="15d8a-136">Clonar Olá Olá Spring nuvem repositório</span><span class="sxs-lookup"><span data-stu-id="15d8a-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="15d8a-137">Olá aplicativo de exemplo Hello Spring nuvem está disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="15d8a-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="15d8a-138">Clone-tooyour ambiente e alterar para o novo diretório de saudação:</span><span class="sxs-lookup"><span data-stu-id="15d8a-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="15d8a-139">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="15d8a-139">Build hello application</span></span>

<span data-ttu-id="15d8a-140">Usando o aplicativo hello compilação [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="15d8a-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="15d8a-141">Implantar o aplicativo hello com cf envio por push</span><span class="sxs-lookup"><span data-stu-id="15d8a-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="15d8a-142">Você pode implantar a maioria dos aplicativos tooCloud Foundry usando Olá `push` comando:</span><span class="sxs-lookup"><span data-stu-id="15d8a-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="15d8a-143">Quando você *push* um aplicativo, nuvem Foundry detecta o tipo de saudação do aplicativo (neste caso, um aplicativo Java) e identifica as suas dependências (neste caso, Spring framework Olá).</span><span class="sxs-lookup"><span data-stu-id="15d8a-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="15d8a-144">Em seguida, empacota tudo necessário toorun seu código em uma imagem de contêiner autônomo, conhecida como um *droplet*.</span><span class="sxs-lookup"><span data-stu-id="15d8a-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="15d8a-145">Finalmente, agendas de nuvem Foundry Olá aplicativo em um dos computadores de Olá disponível no seu ambiente e cria uma URL em que você pode acessar, que está disponível na saída de saudação do comando hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Saída do comando cf push][cf-push-output]

<span data-ttu-id="15d8a-147">aplicativo em nuvem de spring de Olá toosee hello, abra Olá fornecido URL no navegador:</span><span class="sxs-lookup"><span data-stu-id="15d8a-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Interface do usuário padrão do Hello Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="15d8a-149">toolearn mais sobre o que acontece durante `cf push`, consulte [como os aplicativos são preparados] [ cf-push-docs] em Olá documentação Foundry de nuvem.</span><span class="sxs-lookup"><span data-stu-id="15d8a-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="15d8a-150">Exibir logs do aplicativo</span><span class="sxs-lookup"><span data-stu-id="15d8a-150">View application logs</span></span>

<span data-ttu-id="15d8a-151">Você pode usar logs de tooview Olá nuvem Foundry CLI para um aplicativo por seu nome:</span><span class="sxs-lookup"><span data-stu-id="15d8a-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="15d8a-152">Por padrão, a saudação registra o comando usa *final*, que mostra os novos logs como eles são gravados.</span><span class="sxs-lookup"><span data-stu-id="15d8a-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="15d8a-153">toosee novos logs aparecerem, atualize Olá Olá de spring de nuvem aplicativo no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="15d8a-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="15d8a-154">logs de tooview que já foram gravadas, adicionar Olá `recent` alternar:</span><span class="sxs-lookup"><span data-stu-id="15d8a-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="15d8a-155">Aplicativo hello de escala</span><span class="sxs-lookup"><span data-stu-id="15d8a-155">Scale hello application</span></span>

<span data-ttu-id="15d8a-156">Por padrão, `cf push` cria apenas uma única instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="15d8a-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="15d8a-157">tooensure alta disponibilidade e habilitar expansão para maior taxa de transferência, você geralmente deseja toorun mais de uma instância de seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="15d8a-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="15d8a-158">Você pode expandir facilmente aplicativos já implantados usando Olá `scale` comando:</span><span class="sxs-lookup"><span data-stu-id="15d8a-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="15d8a-159">Olá execução `cf app` comando no aplicativo hello mostra que a nuvem Foundry está criando outra instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="15d8a-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="15d8a-160">Após o início de aplicativo hello nuvem Foundry inicia automaticamente tooit do tráfego de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="15d8a-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="15d8a-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15d8a-161">Next steps</span></span>

- <span data-ttu-id="15d8a-162">[Saudação de leitura documentação Foundry de nuvem][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="15d8a-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="15d8a-163">[Configurar o plug-in do Visual Studio Team Services Olá para nuvem Foundry][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="15d8a-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="15d8a-164">[Configurar Olá bocal de análise de Log do Microsoft para nuvem Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="15d8a-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png