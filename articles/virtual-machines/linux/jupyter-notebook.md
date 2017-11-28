---
title: "aaaCreate um bloco de anotações do Jupyter/IPython | Microsoft Docs"
description: "Saiba como toodeploy Olá Notebook Jupyter/IPython em uma máquina virtual Linux criado com o modelo de implantação de Gerenciador de recursos de saudação no Azure."
services: virtual-machines-linux
documentationcenter: python
author: crwilcox
manager: wpickett
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 519f36dd-865e-4c1d-abe7-b87037796aa7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 11/10/2015
ms.author: crwilcox
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d7f2e45a8ba95163ebfb0f10babc91a2b3fd9390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-vm-installing-jupyter-and-running-a-jupyter-notebook-on-azure"></a><span data-ttu-id="d388b-103">Criando uma VM do Azure, instalando o Jupyter, e executando um Notebook do Jupyter no Azure</span><span class="sxs-lookup"><span data-stu-id="d388b-103">Creating an Azure VM, installing Jupyter, and running a Jupyter Notebook on Azure</span></span>
<span data-ttu-id="d388b-104">Olá [Jupyter projeto](http://jupyter.org), Olá anteriormente [IPython projeto](http://ipython.org), fornece um conjunto de ferramentas para computação científica usando poderosos shells interativos que combinam execução de código com a criação de saudação de um documento computacional ao vivo.</span><span class="sxs-lookup"><span data-stu-id="d388b-104">hello [Jupyter project](http://jupyter.org), formerly hello [IPython project](http://ipython.org), provides a collection of tools for scientific computing using powerful interactive shells that combine code execution with hello creation of a live computational document.</span></span> <span data-ttu-id="d388b-105">Esses arquivos de notebook podem conter textos arbitrários, fórmulas matemáticas, códigos de entrada, resultados, gráficos, vídeos e qualquer outro tipo de mídia que um navegador da Web moderno é capaz de exibir.</span><span class="sxs-lookup"><span data-stu-id="d388b-105">These notebook files can contain arbitrary text, mathematical formulas, input code, results, graphics, videos and any other kind of media that a modern web browser is capable of displaying.</span></span> <span data-ttu-id="d388b-106">Se você estiver tooPython totalmente nova e deseja toolearn-lo em divertido, ambiente interativo ou fazer algumas grave paralelo/técnico de computação, Olá Jupyter Notebook é uma ótima opção.</span><span class="sxs-lookup"><span data-stu-id="d388b-106">Whether you're absolutely new tooPython and want toolearn it in a fun, interactive environment or do some serious parallel/technical computing, hello Jupyter Notebook is a great choice.</span></span>

<span data-ttu-id="d388b-107">![Captura de tela de](./media/jupyter-notebook/ipy-notebook-spectral.png) usando SciPy e Matplotlib pacotes tooanalyze Olá a estrutura de uma gravação de som.</span><span class="sxs-lookup"><span data-stu-id="d388b-107">![Screenshot](./media/jupyter-notebook/ipy-notebook-spectral.png) Using SciPy and Matplotlib packages tooanalyze hello structure of a sound recording.</span></span>

## <a name="jupyter-two-ways-azure-notebooks-or-custom-deployment"></a><span data-ttu-id="d388b-108">Duas maneiras para o Jupyter: Blocos de nota do Azure ou implantação personalizada</span><span class="sxs-lookup"><span data-stu-id="d388b-108">Jupyter Two Ways: Azure Notebooks or Custom Deployment</span></span>
<span data-ttu-id="d388b-109">O Azure fornece um serviço que você pode usar também[iniciar rapidamente usando Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span><span class="sxs-lookup"><span data-stu-id="d388b-109">Azure provides a service that you can use too[quickly start using Jupyter ](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx).</span></span>  <span data-ttu-id="d388b-110">Usando hello Azure Notebook Service, você pode facilmente obter interface web acessível do tooJupyter acesso aos recursos computacionais escalonáveis com todo o poder de saudação do Python e suas bibliotecas de muitos.</span><span class="sxs-lookup"><span data-stu-id="d388b-110">By using hello Azure Notebook Service, you can easily gain access tooJupyter's web-accessible interface to scalable computational resources with all hello power of Python and its many libraries.</span></span>  <span data-ttu-id="d388b-111">Desde que a instalação de saudação é tratada pelo serviço Olá, os usuários podem acessar esses recursos sem necessidade de saudação de administração e configuração por usuário hello.</span><span class="sxs-lookup"><span data-stu-id="d388b-111">Since hello installation is handled by hello service, users can access these resources without hello need for administration and configuration by hello user.</span></span>

<span data-ttu-id="d388b-112">Se o serviço de bloco de anotações de saudação não funciona para seu cenário continue tooread deste artigo que será mostrará como toodeploy Olá Jupyter Notebook no Microsoft Azure, usando máquinas virtuais do Linux (VMs).</span><span class="sxs-lookup"><span data-stu-id="d388b-112">If hello notebook service does not work for your scenario please continue tooread this article which will will show you how toodeploy hello Jupyter Notebook on Microsoft Azure, using Linux virtual machines (VMs).</span></span>

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-configure-a-vm-on-azure"></a><span data-ttu-id="d388b-113">Criar e configurar uma VM no Azure</span><span class="sxs-lookup"><span data-stu-id="d388b-113">Create and configure a VM on Azure</span></span>
<span data-ttu-id="d388b-114">primeira etapa de saudação é toocreate uma máquina virtual (VM) em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="d388b-114">hello first step is toocreate a virtual machine (VM)  running on Azure.</span></span>
<span data-ttu-id="d388b-115">Essa VM é um sistema operacional completo na nuvem hello e será usado para executar Olá anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d388b-115">This VM is a complete operating system in hello cloud and will be used to run hello Jupyter Notebook.</span></span> <span data-ttu-id="d388b-116">O Azure é capaz de executar máquinas virtuais Linux e Windows, e abordaremos a instalação de saudação do Jupyter em ambos os tipos de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d388b-116">Azure is capable of running both Linux and Windows virtual machines, and we will cover hello setup of Jupyter on both types of virtual machines.</span></span>

### <a name="create-a-linux-vm-and-open-a-port-for-jupyter"></a><span data-ttu-id="d388b-117">Criar uma VM Linux e abrir uma porta para o Jupyter</span><span class="sxs-lookup"><span data-stu-id="d388b-117">Create a Linux VM and open a port for Jupyter</span></span>
<span data-ttu-id="d388b-118">Siga as instruções de saudação dadas [aqui] [ portal-vm-linux] toocreate uma máquina virtual de saudação *Ubuntu* distribuição.</span><span class="sxs-lookup"><span data-stu-id="d388b-118">Follow hello instructions given [here][portal-vm-linux] toocreate a virtual machine of hello *Ubuntu* distribution.</span></span> <span data-ttu-id="d388b-119">Este tutorial usa o Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="d388b-119">This tutorial uses Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="d388b-120">Vamos supor que o nome de usuário Olá *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="d388b-120">We'll assume hello user name *azureuser*.</span></span>

<span data-ttu-id="d388b-121">Depois de máquina virtual de saudação implanta precisamos tooopen uma regra de segurança no grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="d388b-121">After hello virtual machine deploys we need tooopen up a security rule on hello network security group.</span></span>  <span data-ttu-id="d388b-122">De Olá portal do Azure, vá muito**grupos de segurança de rede** e guia de saudação aberto para tooyour correspondente do grupo de segurança de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="d388b-122">From hello Azure portal, go too**Network Security Groups** and open hello tab for hello Security Group corresponding tooyour VM.</span></span> <span data-ttu-id="d388b-123">Você precisa tooadd uma regra de segurança de entrada com hello configurações a seguir: **TCP** para protocolo hello,  **\***  para a porta de origem (público) hello e **9999** para porta de destino (privado) Hello.</span><span class="sxs-lookup"><span data-stu-id="d388b-123">You need tooadd an Inbound Security rule with hello following settings: **TCP** for hello protocol, **\*** for hello source (public) port and **9999** for hello destination (private) port.</span></span>

![Captura de tela](./media/jupyter-notebook/azure-add-endpoint.png)

<span data-ttu-id="d388b-125">Enquanto estiver no seu grupo de segurança de rede, clique em **Interfaces de rede** e observe hello **endereço IP público** pois ela será necessária tooconnect tooyour VM na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="d388b-125">While in your Network Security Group, click on **Network Interfaces** and note hello **Public IP Address** as it will be needed tooconnect tooyour VM in hello next step.</span></span>

## <a name="install-required-software-on-hello-vm"></a><span data-ttu-id="d388b-126">Instalar o software necessário Olá VM</span><span class="sxs-lookup"><span data-stu-id="d388b-126">Install required software on hello VM</span></span>
<span data-ttu-id="d388b-127">toorun Olá Jupyter Notebook em nosso VM, é necessário primeiro instalar Jupyter e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="d388b-127">toorun hello Jupyter Notebook on our VM, we must first install Jupyter and its dependencies.</span></span> <span data-ttu-id="d388b-128">Conecte-se a vm do linux tooyour usando ssh e par de nome de usuário/senha Olá você escolheu ao criar hello vm.</span><span class="sxs-lookup"><span data-stu-id="d388b-128">Connect tooyour linux vm using ssh and hello username/password pair you chose when you created hello vm.</span></span> <span data-ttu-id="d388b-129">Neste tutorial, usaremos PuTTY e conectaremos do Windows.</span><span class="sxs-lookup"><span data-stu-id="d388b-129">In this tutorial we will use PuTTY and connect from Windows.</span></span>

### <a name="installing-jupyter-on-ubuntu"></a><span data-ttu-id="d388b-130">Instalando o Jupyter no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d388b-130">Installing Jupyter on Ubuntu</span></span>
<span data-ttu-id="d388b-131">Instalar Anaconda, uma distribuição de python de ciência de dados populares, usando um dos links de saudação fornecidos pelo [continuidade análise](https://www.continuum.io/downloads).</span><span class="sxs-lookup"><span data-stu-id="d388b-131">Install Anaconda, a popular data science python distribution, using one of hello links provided from [Continuum Analytics](https://www.continuum.io/downloads).</span></span>  <span data-ttu-id="d388b-132">A partir da gravação da saudação deste documento, Olá links a seguir são hello mais toodate versões de backup.</span><span class="sxs-lookup"><span data-stu-id="d388b-132">As of hello writing of this document, hello below links are hello most up toodate versions.</span></span>

#### <a name="anaconda-installs-for-linux"></a><span data-ttu-id="d388b-133">Instalações de Anaconda para Linux</span><span class="sxs-lookup"><span data-stu-id="d388b-133">Anaconda Installs for Linux</span></span>
<table>
  <th><span data-ttu-id="d388b-134">Python 3.4</span><span class="sxs-lookup"><span data-stu-id="d388b-134">Python 3.4</span></span></th>
  <th><span data-ttu-id="d388b-135">Python 2,7</span><span class="sxs-lookup"><span data-stu-id="d388b-135">Python 2.7</span></span></th>
  <tr>
    <td><span data-ttu-id="d388b-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="d388b-136">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
    <td><span data-ttu-id="d388b-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="d388b-137">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86_64.sh'>64 bit</href>
    </span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="d388b-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="d388b-138">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>
    <td><span data-ttu-id="d388b-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bits</href>
    </span><span class="sxs-lookup"><span data-stu-id="d388b-139">
        <a href='https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda-2.3.0-Linux-x86.sh'>32 bit</href>
    </span></span></td>  
  </tr>
</table>


#### <a name="installing-anaconda3-230-64-bit-on-ubuntu"></a><span data-ttu-id="d388b-140">Instalando o Anaconda3 2.3.0 de 64 bits no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d388b-140">Installing Anaconda3 2.3.0 64-bit on Ubuntu</span></span>
<span data-ttu-id="d388b-141">Veja um exemplo de como você pode instalar o Anaconda no Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d388b-141">As an example, this is how you can install Anaconda on Ubuntu</span></span>

    # install anaconda
    cd ~
    mkdir -p anaconda
    cd anaconda/
    curl -O https://3230d63b5fc54e62148e-c95ac804525aac4b6dba79b00b39d1d3.ssl.cf1.rackcdn.com/Anaconda3-2.3.0-Linux-x86_64.sh
    sudo bash Anaconda3-2.3.0-Linux-x86_64.sh -b -f -p /anaconda3

    # clean up home directory
    cd ..
    rm -rf anaconda/

    # Update Jupyter toohello latest install and generate its config file
    sudo /anaconda3/bin/conda install jupyter -y
    /anaconda3/bin/jupyter-notebook --generate-config


![Captura de tela](./media/jupyter-notebook/anaconda-install.png)

### <a name="configuring-jupyter-and-using-ssl"></a><span data-ttu-id="d388b-143">Configurando o Jupyter e usando SSL</span><span class="sxs-lookup"><span data-stu-id="d388b-143">Configuring Jupyter and using SSL</span></span>
<span data-ttu-id="d388b-144">Depois de instalar precisamos tootake arquivos de configuração um pouco toosetup Olá para Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d388b-144">After installing we need tootake a moment toosetup hello configuration files for Jupyter.</span></span> <span data-ttu-id="d388b-145">Se você tiver problemas com a configuração Jupyter pode ser útil toolook em Olá [Jupyter documentação para a execução de um servidor de Notebook](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span><span class="sxs-lookup"><span data-stu-id="d388b-145">If you experience troubles with configuring Jupyter it may be helpful toolook at hello [Jupyter Documentation for Running a Notebook Server](http://jupyter-notebook.readthedocs.org/en/latest/public_server.html).</span></span>

<span data-ttu-id="d388b-146">Next é `cd` toohello perfil diretório toocreate nosso certificado SSL e editar o arquivo de configuração de perfis de saudação.</span><span class="sxs-lookup"><span data-stu-id="d388b-146">Next we `cd` toohello profile directory toocreate our SSL certificate and edit hello profiles configuration file.</span></span>

<span data-ttu-id="d388b-147">No Linux, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-147">On Linux use hello following command.</span></span>

    cd ~/.jupyter

<span data-ttu-id="d388b-148">Use Olá comando toocreate Olá certificado SSL (Linux e Windows) a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-148">Use hello following command toocreate hello SSL certificate(Linux and Windows).</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="d388b-149">Observe que já que estamos criando um certificado SSL autoassinado, ao conectar-se o bloco de anotações toohello seu navegador fornecerá um aviso de segurança.</span><span class="sxs-lookup"><span data-stu-id="d388b-149">Note that since we are creating a self-signed SSL certificate, when connecting toohello notebook your browser will give you a security warning.</span></span>  <span data-ttu-id="d388b-150">Para uso em produção a longo prazo, você desejará toouse um certificado apropriadamente assinado associado à sua organização.</span><span class="sxs-lookup"><span data-stu-id="d388b-150">For long-term production use, you will want toouse a properly signed certificate associated with your organization.</span></span>  <span data-ttu-id="d388b-151">Como o gerenciamento de certificado está além do escopo de saudação desta demonstração, manteremos certificado autoassinado tooa por enquanto.</span><span class="sxs-lookup"><span data-stu-id="d388b-151">Since certificate management is beyond hello scope of this demo, we will stick tooa self-signed certificate for now.</span></span>

<span data-ttu-id="d388b-152">Além disso toousing um certificado, você deve também fornecer tooprotect uma senha anotações contra uso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="d388b-152">In addition toousing a certificate, you must also provide a password tooprotect your notebook from unauthorized use.</span></span>  <span data-ttu-id="d388b-153">Por motivos de segurança Jupyter usa senhas criptografadas em seu arquivo de configuração, por isso você terá tooencrypt sua senha pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="d388b-153">For security reasons Jupyter uses encrypted passwords in its configuration file, so you'll need tooencrypt your password first.</span></span>  <span data-ttu-id="d388b-154">IPython fornece um utilitário toodo isso; no prompt de comando, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-154">IPython provides a utility toodo so; at a command prompt run hello following command.</span></span>

    /anaconda3/bin/python -c "import IPython;print(IPython.lib.passwd())"

<span data-ttu-id="d388b-155">Isso solicitará uma senha e a confirmação e imprimirá senha hello.</span><span class="sxs-lookup"><span data-stu-id="d388b-155">This will prompt you for a password and confirmation, and will then print hello password.</span></span> <span data-ttu-id="d388b-156">Observação: isso para Olá etapa a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-156">Note this for hello following step.</span></span>

    Enter password:
    Verify password:
    sha1:b86e933199ad:a02e9592e59723da722.. (elided hello rest for security)

<span data-ttu-id="d388b-157">Em seguida, Editaremos o arquivo de configuração do perfil hello, que é o `jupyter_notebook_config.py` arquivo no diretório Olá estão em.</span><span class="sxs-lookup"><span data-stu-id="d388b-157">Next, we will edit hello profile's configuration file, which is the `jupyter_notebook_config.py` file in hello directory you are in.</span></span>  <span data-ttu-id="d388b-158">Observe que esse arquivo não pode existir – criá-la apenas se for esse caso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d388b-158">Note that this file may not exist -- just create it if that is hello case.</span></span>  <span data-ttu-id="d388b-159">Esse arquivo tem diversos campos, todos comentados por padrão.  Você pode abrir este arquivo com qualquer editor de texto de sua preferência, e você deve garantir que ele tem pelo menos Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-159">This file has a number of fields and by default all are commented out.  You can open this file with any text editor of your liking, and you should ensure that it has at least hello following content.</span></span> <span data-ttu-id="d388b-160">**Ser c.NotebookApp.password de saudação tooreplace-se na configuração de saudação com hello sha1 da etapa anterior Olá**.</span><span class="sxs-lookup"><span data-stu-id="d388b-160">**Be sure tooreplace hello c.NotebookApp.password in hello config with hello sha1 from hello previous step**.</span></span>

    c = get_config()

    # You must give hello path toohello certificate file.
    c.NotebookApp.certfile = u'/home/azureuser/.jupyter/mycert.pem'

    # Create your own password as indicated above
    c.NotebookApp.password = u'sha1:b86e933199ad:a02e9592e5 etc... '

    # Network and browser details. We use a fixed port (9999) so it matches
    # our Azure setup, where we've allowed traffic on that port
    c.NotebookApp.ip = '*'
    c.NotebookApp.port = 9999
    c.NotebookApp.open_browser = False

### <a name="run-hello-jupyter-notebook"></a><span data-ttu-id="d388b-161">Executar Olá anotações do Jupyter</span><span class="sxs-lookup"><span data-stu-id="d388b-161">Run hello Jupyter Notebook</span></span>
<span data-ttu-id="d388b-162">Neste momento, estamos toostart pronto Olá anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d388b-162">At this point we are ready toostart hello Jupyter Notebook.</span></span> <span data-ttu-id="d388b-163">toodo isso, navegue toohello directory você deseja toostore notebooks e iniciar Olá servidor de Jupyter Notebook com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="d388b-163">toodo this, navigate toohello directory you want toostore notebooks in and start hello Jupyter Notebook server with hello following command.</span></span>

    /anaconda3/bin/jupyter-notebook

<span data-ttu-id="d388b-164">Agora, você deve ser capaz de tooaccess seu Jupyter Notebook no endereço Olá `https://[PUBLIC-IP-ADDRESS]:9999`.</span><span class="sxs-lookup"><span data-stu-id="d388b-164">You should now be able tooaccess your Jupyter Notebook at hello address `https://[PUBLIC-IP-ADDRESS]:9999`.</span></span>

<span data-ttu-id="d388b-165">Quando você acessa pela primeira vez o bloco de anotações, página de logon Olá solicita sua senha.</span><span class="sxs-lookup"><span data-stu-id="d388b-165">When you first access your notebook, hello login page asks for your password.</span></span> <span data-ttu-id="d388b-166">E, depois de entrar, você verá hello "Painel de Notebook Jupyter", que é o Centro de ontrole para todas as operações de bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="d388b-166">And once you log in, you will see hello "Jupyter Notebook Dashboard", which is the ontrol center for all notebook operations.</span></span>  <span data-ttu-id="d388b-167">Nessa página, é possível criar novos notebooks e abrir os que já existem.</span><span class="sxs-lookup"><span data-stu-id="d388b-167">From this page you can create new notebooks and open existing ones.</span></span>

![Captura de tela](./media/jupyter-notebook/jupyter-tree-view.png)

### <a name="using-hello-jupyter-notebook"></a><span data-ttu-id="d388b-169">Usando Olá anotações do Jupyter</span><span class="sxs-lookup"><span data-stu-id="d388b-169">Using hello Jupyter Notebook</span></span>
<span data-ttu-id="d388b-170">Se você clicar em Olá **novo** botão, você verá Olá após a página de abertura.</span><span class="sxs-lookup"><span data-stu-id="d388b-170">If you click hello **New** button, you will see hello following opening page.</span></span>

![Captura de tela](./media/jupyter-notebook/jupyter-untitled-notebook.png)

<span data-ttu-id="d388b-172">área de saudação marcados com um `In []:` prompt é a área de entrada hello, aqui você pode digitar qualquer código Python válido e ela será executada quando você clicar em `Shift-Enter` ou clique no ícone de "Executar" hello (Olá Triângulo apontando na barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="d388b-172">hello area marked with an `In []:` prompt is hello input area, and here you can type any valid Python code and it will execute when you hit `Shift-Enter` or click on hello "Play" icon (hello right-pointing triangle in hello toolbar).</span></span>

## <a name="a-powerful-paradigm-live-computational-documents-with-rich-media"></a><span data-ttu-id="d388b-173">Um paradigma avançado: documentos computacionais dinâmicos com mídia rica</span><span class="sxs-lookup"><span data-stu-id="d388b-173">A powerful paradigm: live computational documents with rich media</span></span>
<span data-ttu-id="d388b-174">notebook Olá em si deve se sentir tooanyone muito natural que usou Python e um processador de textos, porque se trata de certa forma uma mistura de ambos: você pode executar blocos de código Python, mas você pode manter notas e outro texto, alterando o estilo de saudação de uma célula de "Código" muito "Ma rkdown"usando o menu suspenso de saudação na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="d388b-174">hello notebook itself should feel very natural tooanyone who has used Python and a word processor, because it is in some ways a mix of both: you can execute blocks of Python code, but you can also keep notes and other text by changing hello style of a cell from "Code" too"Markdown" using hello drop-down menu in the toolbar.</span></span>

<span data-ttu-id="d388b-175">O Jupyter é muito mais que um processador de texto, pois permite a combinação de computação e mídia rica (texto, gráficos, vídeos e praticamente qualquer coisa que um navegador da Web moderno pode exibir).</span><span class="sxs-lookup"><span data-stu-id="d388b-175">Jupyter is much more than a word processor as it allows the mixing of computation and rich media (text, graphics, video and virtually anything a modern web browser can display).</span></span> <span data-ttu-id="d388b-176">Você pode misturar texto, códigos, vídeos e muito mais!</span><span class="sxs-lookup"><span data-stu-id="d388b-176">You can mix, text, code, videos and more!</span></span>

![Captura de tela](./media/jupyter-notebook/jupyter-editing-experience.png)

<span data-ttu-id="d388b-178">E com capacidade de saudação do muitas bibliotecas excelentes do Python para computação científica e técnica, em Olá seguinte captura de tela, um cálculo simples pode ser executado com hello iguais facilitam como uma análise de redes complexas, tudo em um ambiente.</span><span class="sxs-lookup"><span data-stu-id="d388b-178">And with hello power of Python's many excellent libraries for scientific and technical computing, in hello following screenshot, a simple calculation can be performed with hello same ease as a complex network analysis, all in one environment.</span></span>

<span data-ttu-id="d388b-179">Esse paradigma de potência de saudação do web moderna Olá a mistura de computação ao vivo oferece muitas possibilidades e é ideal para a nuvem Olá; Olá Notebook pode ser usado:</span><span class="sxs-lookup"><span data-stu-id="d388b-179">This paradigm of mixing hello power of hello modern web with live computation offers many possibilities, and is ideally suited for hello cloud; hello Notebook can be used:</span></span>

* <span data-ttu-id="d388b-180">Como um toorecord de computação de teste exploratório funcionam em um problema.</span><span class="sxs-lookup"><span data-stu-id="d388b-180">As a computational scratchpad toorecord exploratory work on a problem.</span></span>
* <span data-ttu-id="d388b-181">tooshare resultados com colegas, no formulário computacional 'dinâmico' ou em cópia impressa formatos (HTML, PDF).</span><span class="sxs-lookup"><span data-stu-id="d388b-181">tooshare results with colleagues, either in 'live' computational form or in hardcopy formats (HTML, PDF).</span></span>
* <span data-ttu-id="d388b-182">toodistribute e presente materiais de ensino ao vivo que envolvem a computação, para que os alunos imediatamente podem testar com o código real de Olá, modificam-o e execute novamente interativamente.</span><span class="sxs-lookup"><span data-stu-id="d388b-182">toodistribute and present live teaching materials that involve computation, so students can immediately experiment with hello real code, modify it and re-execute it interactively.</span></span>
* <span data-ttu-id="d388b-183">tooprovide "papers executável" que apresentam os resultados de saudação de pesquisa de uma maneira que pode ser reproduzida imediatamente, validar e estendido por outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="d388b-183">tooprovide "executable papers" that present hello results of research in a way that can be immediately reproduced, validated and extended by others.</span></span>
* <span data-ttu-id="d388b-184">Como uma plataforma de computação colaborativa: vários usuários podem fazer logon no toothe mesmo servidor de notebook tooshare uma sessão ao vivo de computação.</span><span class="sxs-lookup"><span data-stu-id="d388b-184">As a platform for collaborative computing: multiple users can log in toothe same notebook server tooshare a live computational session.</span></span>

<span data-ttu-id="d388b-185">Se você acessar o código-fonte IPython toohello [repositório][repository], você encontrará um diretório inteiro com exemplos de bloco de anotações que você pode baixar e, em seguida, experimente na sua própria máquina virtual Jupyter do Azure.</span><span class="sxs-lookup"><span data-stu-id="d388b-185">If you go toohello IPython source code [repository][repository], you will find an entire directory with notebook examples which you can download and then experiment with on your own Azure Jupyter VM.</span></span>  <span data-ttu-id="d388b-186">Basta baixar Olá `.ipynb` arquivos de saudação do site e carregá-las no painel de saudação do bloco de anotações VM do Azure (ou baixá-los diretamente no hello VM).</span><span class="sxs-lookup"><span data-stu-id="d388b-186">Simply download hello `.ipynb` files from hello site and upload them onto hello dashboard of your notebook Azure VM (or download them directly into hello VM).</span></span>

## <a name="conclusion"></a><span data-ttu-id="d388b-187">Conclusão</span><span class="sxs-lookup"><span data-stu-id="d388b-187">Conclusion</span></span>
<span data-ttu-id="d388b-188">saudação de anotações do Jupyter fornece uma interface avançada para acessar interativamente power saudação do ecossistema de Python Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="d388b-188">hello Jupyter Notebook provides a powerful interface for accessing interactively hello power of hello Python ecosystem on Azure.</span></span>  <span data-ttu-id="d388b-189">Ela abrange diversos casos de uso, incluindo exploração simples, aprendizado do Python, análise de dados e visualização, simulação e computação paralela.</span><span class="sxs-lookup"><span data-stu-id="d388b-189">It covers a wide range of usage cases including simple exploration and learning Python, data analysis and visualization, simulation and parallel computing.</span></span> <span data-ttu-id="d388b-190">documentos de Notebook resultantes Olá contêm um registro completo de computações Olá que são executadas e pode ser compartilhada com outros usuários do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d388b-190">hello resulting Notebook documents contain a complete record of hello computations that are performed and can be shared with other Jupyter users.</span></span>  <span data-ttu-id="d388b-191">saudação de anotações do Jupyter pode ser usada como um aplicativo local, mas ele é ideal para implantações de nuvem no Azure</span><span class="sxs-lookup"><span data-stu-id="d388b-191">hello Jupyter Notebook can be used as a local application, but it is ideally suited for cloud deployments on Azure</span></span>

<span data-ttu-id="d388b-192">Olá principais recursos do Jupyter também estão disponíveis no Visual Studio por meio de [ferramentas Python para Visual Studio] [ Python Tools for Visual Studio] (PTVS).</span><span class="sxs-lookup"><span data-stu-id="d388b-192">hello core features of Jupyter are also available inside Visual Studio via the [Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS).</span></span> <span data-ttu-id="d388b-193">O PTVS é um plug-in gratuito e de código aberto da Microsoft que transforma o Visual Studio em um ambiente de implantação avançado do Python, incluindo um editor avançado com IntelliSense, depuração, criação de perfil e integração de computação paralela.</span><span class="sxs-lookup"><span data-stu-id="d388b-193">PTVS is a free and open-source plug-in from Microsoft that turns Visual Studio into an advanced Python development environment that includes an advanced editor with IntelliSense, debugging, profiling and parallel computing integration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d388b-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d388b-194">Next steps</span></span>
<span data-ttu-id="d388b-195">Para obter mais informações, consulte Olá [Central de desenvolvedores de Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="d388b-195">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[portal-vm-linux]: https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial-portal-rm/
[repository]: https://github.com/ipython/ipython
[Python Tools for Visual Studio]: http://aka.ms/ptvs
