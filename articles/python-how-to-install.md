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
# <a name="installing-python-and-hello-sdk"></a>Instalar o Python e hello SDK
Python é fácil tooset backup no Windows e vem pré-instalado no Mac, Linux, e [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about). Este guia o orientará na instalação e na preparação de seu computador para o uso com o Azure.

## <a name="whats-in-hello-python-azure-sdk"></a>O que é no hello Python do SDK do Azure?
Hello Azure SDK para Python inclui componentes que permitem que você toodevelop, implantar e gerenciam aplicativos do Python para o Azure. Especificamente, hello Azure SDK para Python inclui o seguinte hello:

* **Bibliotecas de gerenciamento**. Essas bibliotecas de classes fornecem uma interface para gerenciar recursos do Azure, como as contas de armazenamento e as máquinas virtuais.
* **Bibliotecas de tempo de execução**. Essas bibliotecas de classes fornecem uma interface para acessar recursos do Azure, como o armazenamento e o barramento de serviço.

## <a name="which-python-and-which-version-toouse"></a>Quais Python e qual versão toouse
Existem vários tipos de interpretadores do Python disponíveis - alguns exemplos incluem:

* CPython - intérprete de saudação padrão e mais comumente usada Python
* PyPy - tooCPython rápido, compatível com implementação alternativa
* IronPython -interpretador do Python que é executado no .Net/CLR
* Jython - interpretador do Python que é executado na máquina Virtual Java de saudação

**CPython** v2.7 ou v3.3 + e PyPy 5.4.0 são testados e com suporte para Olá Python do SDK do Azure.

## <a name="where-tooget-python"></a>Onde tooget Python?
Há várias maneiras tooget CPython:

* Diretamente de [www.python.org][www.python.org]
* De um distribuidor respeitável, como [www.continuum.io][www.continuum.io], [www.enthought.com][www.enthought.com] ou [www.activestate.com][www.activestate.com]
* Criá-lo a partir do código-fonte!

A menos que você tenha uma necessidade específica, é recomendável Olá duas primeiras opções.

## <a name="sdk-installation-on-windows-linux-and-macos-client-libraries-only"></a>Instalação do SDK no Windows, Linux e MacOS (apenas bibliotecas de cliente)
Se você já tiver Python instalado, você pode usar o pip tooinstall um conjunto de todas as bibliotecas de cliente Olá no seu ambiente de Python 3.3 + ou Python 2.7 existente. Isso baixa pacotes de saudação do hello [índice de pacote do Python] [ Python Package Index] (PyPI).

Você pode precisar de direitos de administrador:

* Linux e MacOS, use Olá `sudo` comando: `sudo pip install azure-mgmt-compute`.
* Para Windows: abra o PowerShell/prompt de comando como administrador

Você pode instalar cada biblioteca individualmente para cada serviço do Azure:

```console
   $ pip install azure-batch          # Install hello latest Batch runtime library
   $ pip install azure-mgmt-scheduler # Install hello latest Storage management library
```

Pacotes de visualização podem ser instalados usando Olá `--pre` sinalizador:

```console
   $ pip install --pre azure-mgmt-compute # installs only hello latest Compute Management library
```

Você também pode instalar um conjunto de bibliotecas do Azure em uma única linha usando Olá `azure` pacote meta. Porque nem todos os pacotes neste pacote meta ainda são publicados como estável, Olá `azure` pacote meta ainda está em visualização.
No entanto, pacotes de núcleo hello, de perspectivas de qualidade/integridade de código podem ser considerados "estáveis" no momento

* Ela é oficialmente rotulada como tal em sincronia com outras linguagens assim que possível.
  Não planejamos outras alterações importantes até então.

Como é uma versão de visualização, você precisa toouse Olá `--pre` sinalizador:

```console
   $ pip install --pre azure
```

ou diretamente

```console
   $ pip install azure==2.0.0rc6
```

## <a name="getting-more-packages"></a>Obter mais paquetes
Olá [índice de pacote do Python] [ Python Package Index] (PyPI) tem uma seleção avançada de bibliotecas de Python.  Se você escolher uma distribuição tooinstall, já terá a maioria das Olá interessantes bits para vários cenários de tooTechnical de desenvolvimento de web Computing.

## <a name="python-tools-for-visual-studio"></a>Python Tools para Visual Studio
[Python Tools para Visual Studio][Ferramentas do Python Visual Studio] (PTVS) é um plug-in gratuito/OSS da Microsoft que transforma o VS em um IDE completo para Python:

![como-instalar-o-webpi-do-ptvs](./media/python-how-to-install/how-to-install-python-ptvs.png)

O uso do PTVS é opcional, mas recomendável, pois ele dá suporte a Solução/Projeto Web e Python, depuração, criação de perfil, janela interativa, edição de Modelos e Intellisense.

PTVS também torna fácil toodeploy tooMicrosoft do Azure, com suporte para implantação muito[serviços de nuvem](cloud-services/cloud-services-python-ptvs.md) e [sites](app-service-web/web-sites-python-ptvs-django-mysql.md).

O PTVS funciona com sua instalação existente do Visual Studio 2013, 2015 ou 2017.  Para documentação, downloads e discussões, consulte [Ferramentas do Python Visual Studio].  

## <a name="python-azure-scenarios-for-linux-and-macos"></a>Cenários do Python Azure para Linux e MacOS
Para Linux ou MacOS, os principais cenários do Azure têm suporte:

1. Consumindo serviços do Azure usando bibliotecas de saudação do cliente da Python
2. Executando o seu aplicativo em uma VM com Linux
3. Desenvolver e publicar tooAzure sites usando o Git

cenário primeiro Olá permite tooauthor web avançados aplicativos que aproveitam Olá recursos PaaS do Azure, como [armazenamento de blob](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [armazenamento de fila](storage/queues/storage-python-how-to-use-queue-storage.md), [armazenamento de tabela](cosmos-db/table-storage-how-to-use-python.md) etc. via Pythonic wrappers para Olá APIs REST do Azure. Eles funcionam de forma idêntica no Windows, no Mac e no Linux.  Você também pode usar essas bibliotecas cliente de sua máquina de desenvolvimento local ou em uma VM do Linux em execução no Azure.

Para o cenário VM Olá, basta iniciar uma VM do Linux de sua escolha (Ubuntu, CentOS, Suse) e executar/gerenciar o que você deseja.  Por exemplo, você pode executar [IPython] [ IPython] REPL/notebook em seu computador Mac/Windows/Linux e o ponto de seu navegador tooa Linux ou execução de VM do Windows multi-proc Olá mecanismo IPython no Azure.

Para obter informações sobre como tooset a uma VM do Linux, consulte Olá [criar uma máquina Virtual executando o Linux](virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tutorial.

Usando a implantação do Git, você pode desenvolver um aplicativo da web Python e publicá-lo tooan site do Azure de qualquer sistema operacional.  Quando você enviar por push tooAzure seu repositório, ele cria automaticamente um ambiente virtual e pip instala os pacotes necessários.

Para obter mais informações sobre o desenvolvimento e publicação de sites do Azure, consulte os tutoriais de saudação do [criar sites com Django](app-service-web/web-sites-python-create-deploy-django-app.md), [criar sites com garrafa](app-service-web/web-sites-python-create-deploy-bottle-app.md), e [Criando sites com Bulbo](app-service-web/web-sites-python-create-deploy-flask-app.md). Para obter mais informações gerais sobre como usar qualquer estrutura compatível com WSGI, consulte [Configurando Python com os Sites do Azure](app-service-web/web-sites-python-configure.md).

## <a name="additional-software-and-resources"></a>Software adicional e recursos:
* [SDK do Azure para Python no ReadTheDocs](http://azure-sdk-for-python.readthedocs.io/en/latest/)
* [SDK do Azure para Python no GitHub](https://github.com/Azure/azure-sdk-for-python)
* [Exemplos oficiais do Azure para Python](https://azure.microsoft.com/documentation/samples/?platform=python)
* [Distribuição do Python de Análise de Continuidade][Continuum Analytics Python Distribution]
* [Distribuição do Python de Enthought][Enthought Python Distribution]
* [Distribuição do Python de ActiveState][ActiveState Python Distribution]
* [SciPy – um conjunto de bibliotecas científicas para Python][SciPy - A suite of Scientific Python libraries]
* [NumPy – uma biblioteca de numéricos para o Python][NumPy - A numerics library for Python]
* [Projeto Django – uma estrutura da Web/CMS sólida][Django Project - A mature web framework/CMS]
* [IPython – um REPL/Notebook avançado para o Python][IPython - an advanced REPL/Notebook for Python]
* [Ferramentas Python para Visual Studio no GitHub][Python Tools for Visual Studio on GitHub]
* [Centro de desenvolvedores do Python](/develop/python/)

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
