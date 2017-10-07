---
title: aaaInstall Python e hello SDK - Azure
description: Saiba como tooinstall Python e hello toouse SDK com o Azure.
services: 
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: f36294be-daeb-4caf-9129-fce18130f552
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 09/06/2016
ms.author: lmazuel
ms.openlocfilehash: c1b394770f9abd3e654a23d79ae179a9af89e2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="installing-python-and-hello-sdk"></a><span data-ttu-id="a9e1b-103">Instalar o Python e hello SDK</span><span class="sxs-lookup"><span data-stu-id="a9e1b-103">Installing Python and hello SDK</span></span>
<span data-ttu-id="a9e1b-104">Python é fácil tooset backup no Windows e vem pré-instalado no Mac, Linux, e [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="a9e1b-104">Python is easy tooset up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="a9e1b-105">Este guia o orientará na instalação e na preparação de seu computador para o uso com o Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-hello-python-azure-sdk"></a><span data-ttu-id="a9e1b-106">O que é no hello Python do SDK do Azure?</span><span class="sxs-lookup"><span data-stu-id="a9e1b-106">What's in hello Python Azure SDK?</span></span>
<span data-ttu-id="a9e1b-107">Hello Azure SDK para Python inclui componentes que permitem que você toodevelop, implantar e gerenciam aplicativos do Python para o Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-107">hello Azure SDK for Python includes components that allow you toodevelop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="a9e1b-108">Especificamente, hello Azure SDK para Python inclui o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-108">Specifically, hello Azure SDK for Python includes hello following:</span></span>

* <span data-ttu-id="a9e1b-109">**Bibliotecas de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-109">**Management libraries**.</span></span> <span data-ttu-id="a9e1b-110">Essas bibliotecas de classes fornecem uma interface para gerenciar recursos do Azure, como as contas de armazenamento e as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="a9e1b-111">**Bibliotecas de tempo de execução**.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-111">**Runtime libraries**.</span></span> <span data-ttu-id="a9e1b-112">Essas bibliotecas de classes fornecem uma interface para acessar recursos do Azure, como o armazenamento e o barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-toouse"></a><span data-ttu-id="a9e1b-113">Quais Python e qual versão toouse</span><span class="sxs-lookup"><span data-stu-id="a9e1b-113">Which Python and which version toouse</span></span>
<span data-ttu-id="a9e1b-114">Existem vários tipos de interpretadores do Python disponíveis - alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="a9e1b-115">CPython - intérprete de saudação padrão e mais comumente usada Python</span><span class="sxs-lookup"><span data-stu-id="a9e1b-115">CPython - hello standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="a9e1b-116">PyPy - tooCPython rápido, compatível com implementação alternativa</span><span class="sxs-lookup"><span data-stu-id="a9e1b-116">PyPy - fast, compliant alternative implementation tooCPython</span></span>
* <span data-ttu-id="a9e1b-117">IronPython -interpretador do Python que é executado no .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="a9e1b-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="a9e1b-118">Jython - interpretador do Python que é executado na máquina Virtual Java de saudação</span><span class="sxs-lookup"><span data-stu-id="a9e1b-118">Jython - Python interpreter that runs on hello Java Virtual Machine</span></span>

<span data-ttu-id="a9e1b-119">**CPython** v2.7 ou v3.3 + e PyPy 5.4.0 são testados e com suporte para Olá Python do SDK do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for hello Python Azure SDK.</span></span>

## <a name="where-tooget-python"></a><span data-ttu-id="a9e1b-120">Onde tooget Python?</span><span class="sxs-lookup"><span data-stu-id="a9e1b-120">Where tooget Python?</span></span>
<span data-ttu-id="a9e1b-121">Há várias maneiras tooget CPython:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-121">There are several ways tooget CPython:</span></span>

* <span data-ttu-id="a9e1b-122">Diretamente de [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="a9e1b-123">De um distribuidor respeitável, como [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="a9e1b-124">Criá-lo a partir do código-fonte!</span><span class="sxs-lookup"><span data-stu-id="a9e1b-124">Build from source!</span></span>

<span data-ttu-id="a9e1b-125">A menos que você tenha uma necessidade específica, é recomendável Olá duas primeiras opções.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-125">Unless you have a specific need, we recommend hello first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="a9e1b-126">Instalação do SDK no Windows, Linux e MacOS (apenas bibliotecas de cliente)</span><span class="sxs-lookup"><span data-stu-id="a9e1b-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="a9e1b-127">Se você já tiver Python instalado, você pode usar o pip tooinstall um conjunto de todas as bibliotecas de cliente Olá no seu ambiente de Python 3.3 + ou Python 2.7 existente.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-127">If you already have Python installed, you can use pip tooinstall a bundle of all hello client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="a9e1b-128">Isso baixa pacotes de saudação do hello [índice de pacote do Python] [ Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="a9e1b-128">This downloads hello packages from hello [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="a9e1b-129">Você pode precisar de direitos de administrador:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-129">You may need administrator rights:</span></span>

* <span data-ttu-id="a9e1b-130">Linux e MacOS, use Olá `sudo` comando: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-130">Linux and MacOS, use hello `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="a9e1b-131">Para Windows: abra o PowerShell/prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="a9e1b-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="a9e1b-132">Você pode instalar cada biblioteca individualmente para cada serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

<span data-ttu-id="a9e1b-133">Pacotes de visualização podem ser instalados usando Olá `--pre` sinalizador:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-133">Preview packages can be installed using hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

<span data-ttu-id="a9e1b-134">Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando Olá `azure` pacote meta.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-134">You can also install a set of Azure libraries in a single line using hello `azure` meta-package.</span></span> <span data-ttu-id="a9e1b-135">Porque nem todos os pacotes neste pacote meta ainda são publicados como estável, Olá `azure` pacote meta ainda está em visualização.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-135">Since not all packages in this meta-package are published as stable yet, hello `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="a9e1b-136">No entanto, pacotes de núcleo hello, de perspectivas de qualidade/integridade de código podem ser considerados "estáveis" no momento</span><span class="sxs-lookup"><span data-stu-id="a9e1b-136">However, hello core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="a9e1b-137">Ela é oficialmente rotulada como tal em sincronia com outras linguagens assim que possível.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="a9e1b-138">Não planejamos outras alterações importantes até então.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="a9e1b-139">Como é uma versão de visualização, você precisa toouse Olá `--pre` sinalizador:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-139">Since it's a preview release, you need toouse hello `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="a9e1b-140">ou diretamente</span><span class="sxs-lookup"><span data-stu-id="a9e1b-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="a9e1b-141">Obter mais paquetes</span><span class="sxs-lookup"><span data-stu-id="a9e1b-141">Getting More Packages</span></span>
<span data-ttu-id="a9e1b-142">Olá [índice de pacote do Python] [ Python Package Index] (PyPI) tem uma seleção avançada de bibliotecas de Python.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-142">hello [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="a9e1b-143">Se você escolher uma distribuição tooinstall, já terá a maioria das Olá interessantes bits para vários cenários de tooTechnical de desenvolvimento de web Computing.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-143">If you chose tooinstall a Distro, you'll already have most of hello interesting bits for various scenarios from web development tooTechnical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="a9e1b-144">Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9e1b-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="a9e1b-145">[Python Tools para Visual Studio][Ferramentas do Python Visual Studio] (PTVS) é um plug-in gratuito/OSS da Microsoft que transforma o VS em um IDE completo para Python:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![como-instalar-o-webpi-do-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="a9e1b-147">O uso do PTVS é opcional, mas recomendável, pois ele dá suporte a Solução/Projeto Web e Python, depuração, criação de perfil, janela interativa, edição de Modelos e Intellisense.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="a9e1b-148">PTVS também torna fácil toodeploy tooMicrosoft do Azure, com suporte para implantação muito[serviços de nuvem](cloud-services/cloud-services-python-ptvs.md) e [sites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="a9e1b-148">PTVS also makes it easy toodeploy tooMicrosoft Azure, with support for deployment too[Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="a9e1b-149">O PTVS funciona com sua instalação existente do Visual Studio 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="a9e1b-150">Para documentação, downloads e discussões, consulte [Ferramentas do Python Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="a9e1b-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="a9e1b-151">Cenários do Python Azure para Linux e MacOS</span><span class="sxs-lookup"><span data-stu-id="a9e1b-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="a9e1b-152">Para Linux ou MacOS, os principais cenários do Azure têm suporte:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="a9e1b-153">Consumindo serviços do Azure usando bibliotecas de saudação do cliente da Python</span><span class="sxs-lookup"><span data-stu-id="a9e1b-153">Consuming Azure Services by using hello client libraries for Python</span></span>
2. <span data-ttu-id="a9e1b-154">Executando o seu aplicativo em uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="a9e1b-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="a9e1b-155">Desenvolver e publicar tooAzure sites usando o Git</span><span class="sxs-lookup"><span data-stu-id="a9e1b-155">Developing and publishing tooAzure Websites using Git</span></span>

<span data-ttu-id="a9e1b-156">cenário primeiro Olá permite tooauthor web avançados aplicativos que aproveitam Olá recursos PaaS do Azure, como [armazenamento de blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [armazenamento de fila](storage/queues/storage-python-how-to-use-queue-storage.md), [armazenamento de tabela](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers para Olá APIs REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-156">hello first scenario enables you tooauthor rich web apps that take advantage of hello Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for hello Azure REST APIs.</span></span> <span data-ttu-id="a9e1b-157">Eles funcionam de forma idêntica no Windows, no Mac e no Linux.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="a9e1b-158">Você também pode usar essas bibliotecas cliente de sua máquina de desenvolvimento local ou em uma VM do Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="a9e1b-159">Para o cenário VM Olá, basta iniciar uma VM do Linux de sua escolha (Ubuntu, CentOS, Suse) e executar/gerenciar o que você deseja.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-159">For hello VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="a9e1b-160">Por exemplo, você pode executar [IPython] [ IPython] REPL/notebook em seu computador Mac/Windows/Linux e o ponto de seu navegador tooa Linux ou execução de VM do Windows multi-proc Olá mecanismo IPython no Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser tooa Linux or Windows multi-proc VM running hello IPython Engine on Azure.</span></span>

<span data-ttu-id="a9e1b-161">Para obter informações sobre como tooset a uma VM do Linux, consulte Olá [criar uma máquina Virtual executando o Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-161">For information on how tooset up a Linux VM, see hello [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="a9e1b-162">Usando a implantação do Git, você pode desenvolver um aplicativo da web Python e publicá-lo tooan site do Azure de qualquer sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-162">Using Git deployment, you can develop a Python web application and publish it tooan Azure Website from any operating system.</span></span>  <span data-ttu-id="a9e1b-163">Quando você enviar por push tooAzure seu repositório, ele cria automaticamente um ambiente virtual e pip instala os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="a9e1b-163">When you push your repository tooAzure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="a9e1b-164">Para obter mais informações sobre o desenvolvimento e publicação de sites do Azure, consulte os tutoriais de saudação do [criar sites com Django](app-service-web/web-sites-python-create-deploy-django-app.md), [criar sites com garrafa](app-service-web/web-sites-python-create-deploy-bottle-app.md), e [Criando sites com Bulbo](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="a9e1b-164">For more information on developing and publishing Azure Websites, see hello tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="a9e1b-165">Para obter mais informações gerais sobre como usar qualquer estrutura compatível com WSGI, consulte [Configurando Python com os Sites do Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a9e1b-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="a9e1b-166">Software adicional e recursos:</span><span class="sxs-lookup"><span data-stu-id="a9e1b-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="a9e1b-167">SDK do Azure para Python no ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="a9e1b-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="a9e1b-168">SDK do Azure para Python no GitHub</span><span class="sxs-lookup"><span data-stu-id="a9e1b-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="a9e1b-169">Exemplos oficiais do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="a9e1b-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="a9e1b-170">[Distribuição do Python de Análise de Continuidade][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="a9e1b-171">[Distribuição do Python de Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="a9e1b-172">[Distribuição do Python de ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="a9e1b-173">[SciPy – um conjunto de bibliotecas científicas para Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="a9e1b-174">[NumPy – uma biblioteca de numéricos para o Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="a9e1b-175">[Projeto Django – uma estrutura da Web/CMS sólida][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="a9e1b-176">[IPython – um REPL/Notebook avançado para o Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="a9e1b-177">[Ferramentas Python para Visual Studio no GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="a9e1b-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="a9e1b-178">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="a9e1b-178">Python Developer Center</span></span>](/develop/python/)

[Continuum Analytics Python Distribution]: http://continuum.io
[Enthought Python Distribution]: http://www.enthought.com
[ActiveState Python Distribution]: http://www.activestate.com
[www.python.org]: http://www.python.org
[www.continuum.io]: http://continuum.io
[www.enthought.com]: http://www.enthought.com
[www.activestate.com]: http://www.activestate.com
[SciPy - A suite of Scientific Python libraries]: http://www.scipy.org
[NumPy - A numerics library for Python]: http://www.numpy.org
[Django Project - A mature web framework/CMS]: http://www.djangoproject.com
[IPython - an advanced REPL/Notebook for Python]: http://ipython.org
[IPython]: http://ipython.org
[IPython Notebook on Azure]: virtual-machines-linux-jupyter-notebook.md
[Cloud Services]: cloud-services-python-ptvs.md
[Websites]: web-sites-python-ptvs-django-mysql.md
[Ferramentas do Python Visual Studio]: http://aka.ms/ptvs
[Python Tools for Visual Studio on GitHub]: https://github.com/microsoft/ptvs
[Python Package Index]: http://pypi.python.org/pypi
[Microsoft Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?LinkId=254281
[Microsoft Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?LinkID=516990
[Setting up a Linux VM via hello Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How toouse hello Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
