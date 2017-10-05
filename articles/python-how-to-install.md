---
title: Instalar o Python e o SDK - Azure
description: Saiba como instalar o Python e o SDK para usar com o Azure.
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
ms.openlocfilehash: c9df4e1f7677b2ed10684f6f3c981f2abf64f171
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="installing-python-and-the-sdk"></a><span data-ttu-id="5b1fb-103">Instalando o Python e o SDK</span><span class="sxs-lookup"><span data-stu-id="5b1fb-103">Installing Python and the SDK</span></span>
<span data-ttu-id="5b1fb-104">O Python é fácil de ser instalado no Windows e é fornecido pré-instalado no Mac, no Linux e no [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-104">Python is easy to set up on Windows and comes pre-installed on Mac, Linux, and [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="5b1fb-105">Este guia o orientará na instalação e na preparação de seu computador para o uso com o Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-105">This guide walks you through installation and getting your machine ready for use with Azure.</span></span>

## <a name="whats-in-the-python-azure-sdk"></a><span data-ttu-id="5b1fb-106">Novidades no SDK do Python Azure</span><span class="sxs-lookup"><span data-stu-id="5b1fb-106">What's in the Python Azure SDK?</span></span>
<span data-ttu-id="5b1fb-107">O SDK do Azure para o Python inclui componentes que permitem que você desenvolva, implante e gerencie aplicativos do Python para o Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-107">The Azure SDK for Python includes components that allow you to develop, deploy, and manage Python applications for Azure.</span></span> <span data-ttu-id="5b1fb-108">O SDK do Azure para o Python inclui especificamente o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-108">Specifically, the Azure SDK for Python includes the following:</span></span>

* <span data-ttu-id="5b1fb-109">**Bibliotecas de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-109">**Management libraries**.</span></span> <span data-ttu-id="5b1fb-110">Essas bibliotecas de classes fornecem uma interface para gerenciar recursos do Azure, como as contas de armazenamento e as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-110">These class libraries provide an interface managing Azure resources, such as storage accounts, virtual machines.</span></span>
* <span data-ttu-id="5b1fb-111">**Bibliotecas de tempo de execução**.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-111">**Runtime libraries**.</span></span> <span data-ttu-id="5b1fb-112">Essas bibliotecas de classes fornecem uma interface para acessar recursos do Azure, como o armazenamento e o barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-112">These class libraries provide an interface for accessing Azure features, such as storage and service bus.</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="5b1fb-113">Qual Python e qual versão usar</span><span class="sxs-lookup"><span data-stu-id="5b1fb-113">Which Python and which version to use</span></span>
<span data-ttu-id="5b1fb-114">Existem vários tipos de interpretadores do Python disponíveis - alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-114">There are several flavors of Python interpreters available - examples include:</span></span>

* <span data-ttu-id="5b1fb-115">CPython - o interpretador do Python padrão e mais geralmente usado</span><span class="sxs-lookup"><span data-stu-id="5b1fb-115">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="5b1fb-116">PyPy – implementação alternativa rápida e compatível para CPython</span><span class="sxs-lookup"><span data-stu-id="5b1fb-116">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="5b1fb-117">IronPython -interpretador do Python que é executado no .Net/CLR</span><span class="sxs-lookup"><span data-stu-id="5b1fb-117">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="5b1fb-118">Jython – interpretador do Python que é executado na Máquina Virtual Java</span><span class="sxs-lookup"><span data-stu-id="5b1fb-118">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="5b1fb-119">**CPython** v2.7 ou v3.3+ e o PyPy 5.4.0 são testados e dão suporte ao SDK do Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-119">**CPython** v2.7 or v3.3+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="5b1fb-120">Onde obter o Python?</span><span class="sxs-lookup"><span data-stu-id="5b1fb-120">Where to get Python?</span></span>
<span data-ttu-id="5b1fb-121">Existem várias maneiras de obter o CPython:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-121">There are several ways to get CPython:</span></span>

* <span data-ttu-id="5b1fb-122">Diretamente de [www.python.org][www.python.org]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-122">Directly from [www.python.org][www.python.org]</span></span>
* <span data-ttu-id="5b1fb-123">De um distribuidor respeitável, como [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-123">From a reputable distro such as [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] or [www.activestate.com][www.activestate.com]</span></span>
* <span data-ttu-id="5b1fb-124">Criá-lo a partir do código-fonte!</span><span class="sxs-lookup"><span data-stu-id="5b1fb-124">Build from source!</span></span>

<span data-ttu-id="5b1fb-125">A menos que você tenha uma necessidade específica, recomendamos as duas primeiras opções.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-125">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a><span data-ttu-id="5b1fb-126">Instalação do SDK no Windows, Linux e MacOS (apenas bibliotecas de cliente)</span><span class="sxs-lookup"><span data-stu-id="5b1fb-126">SDK Installation on Windows, Linux, and MacOS (client libraries only)</span></span>
<span data-ttu-id="5b1fb-127">Se já tiver o Python instalado, você poderá usar pip para instalar um pacote de todas as bibliotecas de cliente em seu ambiente Python 2.7 ou Python 3.3+ existente.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-127">If you already have Python installed, you can use pip to install a bundle of all the client libraries in your existing Python 2.7 or Python 3.3+ environment.</span></span> <span data-ttu-id="5b1fb-128">Isso baixa os pacotes do [Índice de Pacotes do Python][Python Package Index] (PyPI).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-128">This downloads the packages from the [Python Package Index][Python Package Index] (PyPI).</span></span>

<span data-ttu-id="5b1fb-129">Você pode precisar de direitos de administrador:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-129">You may need administrator rights:</span></span>

* <span data-ttu-id="5b1fb-130">Para Linux e MacOS, use o comando `sudo`: `sudo pip install azure-mgmt-compute`.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-130">Linux and MacOS, use the `sudo` command: `sudo pip install azure-mgmt-compute`.</span></span>
* <span data-ttu-id="5b1fb-131">Para Windows: abra o PowerShell/prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="5b1fb-131">Windows: open your PowerShell/Command prompt as an administrator</span></span>

<span data-ttu-id="5b1fb-132">Você pode instalar cada biblioteca individualmente para cada serviço do Azure:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-132">You can install individually each library for each Azure service:</span></span>

```console
   $ pip install azure-batch          # Install the latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="5b1fb-133">Pacotes de preview podem ser instalados usando o sinalizador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="5b1fb-133">Preview packages can be installed using the `--pre` flag:</span></span>

```console
   $ pip install --pre azure-mgmt-compute # installs only the latest Compute Management library
```

<span data-ttu-id="5b1fb-134">Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando o pacote meta `azure` .</span><span class="sxs-lookup"><span data-stu-id="5b1fb-134">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span> <span data-ttu-id="5b1fb-135">Como nem todos os pacotes neste pacote meta estão publicados como estáveis, o pacote meta `azure` ainda está em preview.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-135">Since not all packages in this meta-package are published as stable yet, the `azure` meta-package is still in preview.</span></span>
<span data-ttu-id="5b1fb-136">No entanto, os pacotes essenciais podem ser considerados "estáveis" no momento do ponto de vista da integridade e da qualidade do código.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-136">However, the core packages, from code quality/completeness perspectives can be considered "stable" at this time</span></span>

* <span data-ttu-id="5b1fb-137">Ela é oficialmente rotulada como tal em sincronia com outras linguagens assim que possível.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-137">it is officially labeled as such in sync with other languages as soon as possible.</span></span>
  <span data-ttu-id="5b1fb-138">Não planejamos outras alterações importantes até então.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-138">We are not planning on any further major changes until then.</span></span>

<span data-ttu-id="5b1fb-139">Como se trata de uma versão de preview, você precisa usar o sinalizador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="5b1fb-139">Since it's a preview release, you need to use the `--pre` flag:</span></span>

```console
   $ pip install --pre azure
```

<span data-ttu-id="5b1fb-140">ou diretamente</span><span class="sxs-lookup"><span data-stu-id="5b1fb-140">or directly</span></span>

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a><span data-ttu-id="5b1fb-141">Obter mais paquetes</span><span class="sxs-lookup"><span data-stu-id="5b1fb-141">Getting More Packages</span></span>
<span data-ttu-id="5b1fb-142">O [Índice de Pacotes do Python][Python Package Index] (PyPI) tem uma seleção completa de bibliotecas do Python.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-142">The [Python Package Index][Python Package Index] (PyPI) has a rich selection of Python libraries.</span></span>  <span data-ttu-id="5b1fb-143">Caso tenha optado por instalar uma Distribuição, você já terá a maioria das partes interessantes para vários cenários, do desenvolvimento para Web até a Computação Técnica.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-143">If you chose to install a Distro, you'll already have most of the interesting bits for various scenarios from web development to Technical Computing.</span></span>

## <a name="python-tools-for-visual-studio"></a><span data-ttu-id="5b1fb-144">Python Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b1fb-144">Python Tools for Visual Studio</span></span>
<span data-ttu-id="5b1fb-145">[Python Tools para Visual Studio][Ferramentas do Python Visual Studio] (PTVS) é um plug-in gratuito/OSS da Microsoft que transforma o VS em um IDE completo para Python:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-145">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) is a free/OSS plugin from Microsoft, which turns VS into a full-fledged Python IDE:</span></span>

![como-instalar-o-webpi-do-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

<span data-ttu-id="5b1fb-147">O uso do PTVS é opcional, mas recomendável, pois ele dá suporte a Solução/Projeto Web e Python, depuração, criação de perfil, janela interativa, edição de Modelos e Intellisense.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-147">Using PTVS is optional, but is recommended as it gives you Python and Web Project/Solution support, debugging, profiling, interactive window, Template editing, and Intellisense.</span></span>

<span data-ttu-id="5b1fb-148">O PTVS também torna fácil a implantação ao Microsoft Azure, com suporte para implementação em [Serviços de Nuvem](cloud-services/cloud-services-python-ptvs.md) e [Sites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-148">PTVS also makes it easy to deploy to Microsoft Azure, with support for deployment to [Cloud Services](cloud-services/cloud-services-python-ptvs.md) and [Websites](app-service-web/web-sites-python-ptvs-django-mysql.md).</span></span>

<span data-ttu-id="5b1fb-149">O PTVS funciona com sua instalação existente do Visual Studio 2013, 2015 ou 2017.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-149">PTVS works with your existing Visual Studio 2013, 2015, or 2017 installation.</span></span>  <span data-ttu-id="5b1fb-150">Para documentação, downloads e discussões, consulte [Ferramentas do Python Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="5b1fb-150">For documentation, downloads and discussions, see [Python Tools for Visual Studio].</span></span>  

## <a name="python-azure-scenarios-for-linux-and-macos"></a><span data-ttu-id="5b1fb-151">Cenários do Python Azure para Linux e MacOS</span><span class="sxs-lookup"><span data-stu-id="5b1fb-151">Python Azure Scenarios for Linux and MacOS</span></span>
<span data-ttu-id="5b1fb-152">Para Linux ou MacOS, os principais cenários do Azure têm suporte:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-152">For Linux or MacOS, main Azure scenarios that are supported:</span></span>

1. <span data-ttu-id="5b1fb-153">Usando os Serviços do Azure por meio das bibliotecas de cliente para Python</span><span class="sxs-lookup"><span data-stu-id="5b1fb-153">Consuming Azure Services by using the client libraries for Python</span></span>
2. <span data-ttu-id="5b1fb-154">Executando o seu aplicativo em uma VM com Linux</span><span class="sxs-lookup"><span data-stu-id="5b1fb-154">Running your app in a Linux VM</span></span>
3. <span data-ttu-id="5b1fb-155">Desenvolver e publicar sites do Azure usando Git</span><span class="sxs-lookup"><span data-stu-id="5b1fb-155">Developing and publishing to Azure Websites using Git</span></span>

<span data-ttu-id="5b1fb-156">O primeiro cenário permite que você crie aplicativos Web avançados que aproveitam recursos do Azure PaaS como [armazenamento de blobs](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [armazenamento de filas](storage/queues/storage-python-how-to-use-queue-storage.md), [armazenamento de tabelas](cosmos-db/table-storage-how-to-use-python.md), etc., por meio de wrappers do Pythonic para as APIs REST do Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-156">The first scenario enables you to author rich web apps that take advantage of the Azure PaaS capabilities such as [blob storage](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [queue storage](storage/queues/storage-python-how-to-use-queue-storage.md), [table storage](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers for the Azure REST APIs.</span></span> <span data-ttu-id="5b1fb-157">Eles funcionam de forma idêntica no Windows, no Mac e no Linux.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-157">These work identically on Windows, Mac, and Linux.</span></span>  <span data-ttu-id="5b1fb-158">Você também pode usar essas bibliotecas cliente de sua máquina de desenvolvimento local ou em uma VM do Linux em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-158">You can also use these client libraries from your local development machine or a Linux VM running on Azure.</span></span>

<span data-ttu-id="5b1fb-159">Para o cenário da VM, basta iniciar uma VM com Linux de sua escolha (Ubuntu, CentOS, Suse) e executar/gerenciar os itens desejados.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-159">For the VM scenario, you simply start a Linux VM of your choice (Ubuntu, CentOS, Suse) and run/manage what you like.</span></span>  <span data-ttu-id="5b1fb-160">Por exemplo, você pode executar [IPython][IPython] REPL/notebook no seu computador com Windows/Mac/Linux e apontar o navegador para uma VM com Linux ou Windows de proc múltiplo que esteja executando o IPython Engine no Azure.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-160">As an example, you can run [IPython][IPython] REPL/notebook on your Windows/Mac/Linux machine and point your browser to a Linux or Windows multi-proc VM running the IPython Engine on Azure.</span></span>

<span data-ttu-id="5b1fb-161">Para saber mais sobre como configurar uma VM do Linux, veja o tutorial [Criar uma Máquina Virtual Executando o Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-161">For information on how to set up a Linux VM, see the [Create a Virtual Machine Running Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.</span></span>

<span data-ttu-id="5b1fb-162">Usando a implantação do Git, você pode desenvolver um aplicativo da Web Python e publicá-lo em um site do Azure de qualquer sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-162">Using Git deployment, you can develop a Python web application and publish it to an Azure Website from any operating system.</span></span>  <span data-ttu-id="5b1fb-163">Quando você envia seu repositório para o Azure, ele cria automaticamente um ambiente virtual e o pip instalará os pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="5b1fb-163">When you push your repository to Azure, it automatically creates a virtual environment and pip installs your required packages.</span></span>

<span data-ttu-id="5b1fb-164">Para obter mais informações sobre como desenvolver e publicar Sites do Azure, consulte os tutoriais [Criando Sites com Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Criando Sites com Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md) e [Criando sites com Flash](app-service-web/web-sites-python-create-deploy-flask-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-164">For more information on developing and publishing Azure Websites, see the tutorials for [Creating Websites with Django](app-service-web/web-sites-python-create-deploy-django-app.md), [Creating Websites with Bottle](app-service-web/web-sites-python-create-deploy-bottle-app.md), and [Creating Websites with Flask](app-service-web/web-sites-python-create-deploy-flask-app.md).</span></span> <span data-ttu-id="5b1fb-165">Para obter mais informações gerais sobre como usar qualquer estrutura compatível com WSGI, consulte [Configurando Python com os Sites do Azure](app-service-web/web-sites-python-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5b1fb-165">For more general information on using any WSGI-compliant framework, see [Configuring Python with Azure Websites](app-service-web/web-sites-python-configure.md).</span></span>

## <a name="additional-software-and-resources"></a><span data-ttu-id="5b1fb-166">Software adicional e recursos:</span><span class="sxs-lookup"><span data-stu-id="5b1fb-166">Additional Software and Resources:</span></span>
* [<span data-ttu-id="5b1fb-167">SDK do Azure para Python no ReadTheDocs</span><span class="sxs-lookup"><span data-stu-id="5b1fb-167">Azure SDK for Python ReadTheDocs</span></span>](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [<span data-ttu-id="5b1fb-168">SDK do Azure para Python no GitHub</span><span class="sxs-lookup"><span data-stu-id="5b1fb-168">Azure SDK for Python GitHub</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="5b1fb-169">Exemplos oficiais do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="5b1fb-169">Official Azure samples for Python</span></span>](https://azure.microsoft.com/documentation/samples/?platform=python)
* <span data-ttu-id="5b1fb-170">[Distribuição do Python de Análise de Continuidade][Continuum Analytics Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-170">[Continuum Analytics Python Distribution][Continuum Analytics Python Distribution]</span></span>
* <span data-ttu-id="5b1fb-171">[Distribuição do Python de Enthought][Enthought Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-171">[Enthought Python Distribution][Enthought Python Distribution]</span></span>
* <span data-ttu-id="5b1fb-172">[Distribuição do Python de ActiveState][ActiveState Python Distribution]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-172">[ActiveState Python Distribution][ActiveState Python Distribution]</span></span>
* <span data-ttu-id="5b1fb-173">[SciPy – um conjunto de bibliotecas científicas para Python][SciPy - A suite of Scientific Python libraries]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-173">[SciPy - A suite of Scientific Python libraries][SciPy - A suite of Scientific Python libraries]</span></span>
* <span data-ttu-id="5b1fb-174">[NumPy – uma biblioteca de numéricos para o Python][NumPy - A numerics library for Python]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-174">[NumPy - A numerics library for Python][NumPy - A numerics library for Python]</span></span>
* <span data-ttu-id="5b1fb-175">[Projeto Django – uma estrutura da Web/CMS sólida][Django Project - A mature web framework/CMS]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-175">[Django Project - A mature web framework/CMS][Django Project - A mature web framework/CMS]</span></span>
* <span data-ttu-id="5b1fb-176">[IPython – um REPL/Notebook avançado para o Python][IPython - an advanced REPL/Notebook for Python]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-176">[IPython - an advanced REPL/Notebook for Python][IPython - an advanced REPL/Notebook for Python]</span></span>
* <span data-ttu-id="5b1fb-177">[Ferramentas Python para Visual Studio no GitHub][Python Tools for Visual Studio on GitHub]</span><span class="sxs-lookup"><span data-stu-id="5b1fb-177">[Python Tools for Visual Studio on GitHub][Python Tools for Visual Studio on GitHub]</span></span>
* [<span data-ttu-id="5b1fb-178">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="5b1fb-178">Python Developer Center</span></span>](/develop/python/)

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
[Setting up a Linux VM via the Azure portal]: create-and-configure-opensuse-vm-in-portal.md
[How to use the Azure Command-Line Interface]: crossplat-cmd-tools.md
[Create a Virtual Machine Running Linux]: virtual-machines-linux-quick-create-cli.md
[Creating Websites with Django]: web-sites-python-create-deploy-django-app.md
[Creating Websites with Bottle]: web-sites-python-create-deploy-bottle-app.md
[Creating Websites with Flask]: web-sites-python-create-deploy-flask-app.md
[Configuring Python with Azure Websites]: web-sites-python-configure.md
[table storage]: storage-python-how-to-use-table-storage.md
[queue storage]: storage-python-how-to-use-queue-storage.md
[blob storage]:storage/blobs/storage-python-how-to-use-blob-storage.md
