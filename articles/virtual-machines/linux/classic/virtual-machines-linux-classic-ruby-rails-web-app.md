---
title: aaaHost um Ruby no site de trilhos em uma VM do Linux | Microsoft Docs
description: "Configurar e hospedar um site da Web baseado no Ruby on Rails no Azure usando uma máquina virtual do Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="6dbf4-103">Aplicativo Web Ruby on Rails Web em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="6dbf4-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="6dbf4-104">Este tutorial mostra como toohost um Ruby no site de trilhos no Azure usando uma máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="6dbf4-105">Este tutorial foi validado usando o Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="6dbf4-106">Se você usar uma distribuição de Linux diferente, talvez seja necessário toomodify Olá etapas tooinstall trilhos.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6dbf4-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6dbf4-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="6dbf4-108">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="6dbf4-109">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="6dbf4-110">Criar uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="6dbf4-110">Create an Azure VM</span></span>
<span data-ttu-id="6dbf4-111">Comece criando uma VM do Azure com uma imagem do Linux.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="6dbf4-112">toocreate Olá VM, você pode usar Olá portal do Azure ou hello Azure Interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="6dbf4-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="6dbf4-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6dbf4-113">Azure portal</span></span>
1. <span data-ttu-id="6dbf4-114">O logon no hello [portal do Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6dbf4-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="6dbf4-115">Clique em **novo**, em seguida, digite "Servidor do Ubuntu 14.04" na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="6dbf4-116">Clique em entrada hello retornada pela pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="6dbf4-117">Para o modelo de implantação hello, selecione **clássico**, em seguida, clique em "Criar".</span><span class="sxs-lookup"><span data-stu-id="6dbf4-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="6dbf4-118">Na folha de Noções básicas de Olá, forneça valores para campos de saudação necessária: nome (para Olá VM), nome de usuário, tipo de autenticação e credenciais correspondentes do hello, assinatura do Azure, grupo de recursos e local.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Criar uma nova imagem Ubuntu](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="6dbf4-120">Depois que Olá VM for provisionada, clique no nome da VM hello e clique em **pontos de extremidade** em Olá **configurações** categoria.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="6dbf4-121">Localizar o ponto de extremidade SSH de hello, listado na **autônomo**.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Ponto de extremidade padrão](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="6dbf4-123">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6dbf4-123">Azure CLI</span></span>
<span data-ttu-id="6dbf4-124">Siga as etapas de saudação em [criar uma máquina Virtual executando o Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="6dbf4-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="6dbf4-125">Depois Olá VM for provisionada, você pode obter o ponto de extremidade SSH Olá executando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="6dbf4-126">Instalar o Ruby on Rails</span><span class="sxs-lookup"><span data-stu-id="6dbf4-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="6dbf4-127">Use SSH tooconnect toohello VM.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="6dbf4-128">Da sessão SSH hello, use Olá seguindo comandos tooinstall Ruby na Olá VM:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="6dbf4-129">instalação de saudação pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="6dbf4-130">Quando for concluído, use Olá após o comando tooverify que Ruby está instalado:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="6dbf4-131">Comando a seguir de saudação do uso trilhos tooinstall:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="6dbf4-132">Use hello – não rdoc e --não ri sinalizadores tooskip instalando a documentação da saudação, que é mais rápida.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="6dbf4-133">Este comando provavelmente levará um longo tempo tooexecute, para adicionar Olá -V exibirá informações sobre o progresso da instalação hello.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="6dbf4-134">Criar e executar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="6dbf4-134">Create and run an app</span></span>
<span data-ttu-id="6dbf4-135">Ainda conectado via SSH, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="6dbf4-136">Olá [novo](http://guides.rubyonrails.org/command_line.html#rails-new) comando cria um novo aplicativo Rails.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="6dbf4-137">Olá [server](http://guides.rubyonrails.org/command_line.html#rails-server) inicia Olá servidor web WEBrick que acompanha os trilhos de comando.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="6dbf4-138">(Para uso em produção, talvez seja conveniente toouse um servidor diferente, como unicórnio ou passageiro.)</span><span class="sxs-lookup"><span data-stu-id="6dbf4-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="6dbf4-139">Você deve ver o seguinte de toohello semelhante de saída.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="6dbf4-140">Adicionar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="6dbf4-140">Add an endpoint</span></span>
1. <span data-ttu-id="6dbf4-141">Vá toohello [portal do Azure] [https://portal.azure.com] e selecione sua VM.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="6dbf4-142">Selecione **pontos de EXTREMIDADE** em Olá **configurações** ao longo da página de saudação do hello borda esquerda.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="6dbf4-143">Clique em **adicionar** na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="6dbf4-144">Em Olá **Adicionar ponto de extremidade** caixa de diálogo, insira Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="6dbf4-145">**Nome**: HTTP</span><span class="sxs-lookup"><span data-stu-id="6dbf4-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="6dbf4-146">**Protocolo**: TCP</span><span class="sxs-lookup"><span data-stu-id="6dbf4-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="6dbf4-147">**Porta pública**: 80</span><span class="sxs-lookup"><span data-stu-id="6dbf4-147">**Public port**: 80</span></span>
   * <span data-ttu-id="6dbf4-148">**Porta privada**: 3000</span><span class="sxs-lookup"><span data-stu-id="6dbf4-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="6dbf4-149">**Endereço PI flutuante**: Desabilitado</span><span class="sxs-lookup"><span data-stu-id="6dbf4-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="6dbf4-150">**Lista de controle de acesso - ordem**: 1001, ou outro valor que define a prioridade Olá desta regra de acesso.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="6dbf4-151">**Lista de controle de acesso - Nome**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="6dbf4-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="6dbf4-152">**Lista de controle de acesso - Ação**: permitir</span><span class="sxs-lookup"><span data-stu-id="6dbf4-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="6dbf4-153">**Lista de controle de acesso - Sub-rede remota**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6dbf4-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="6dbf4-154">Esse ponto de extremidade tem uma porta pública 80 que irá rotear tráfego toohello porta privada 3000, onde o servidor de trilhos de saudação está escutando.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="6dbf4-155">regra de lista de controle de acesso de saudação permite tráfego público na porta 80.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="6dbf4-157">Clique em toosave Okey Olá endpoint.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="6dbf4-158">Uma mensagem deverá aparecer indicando **Salvando o ponto de extremidade da máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="6dbf4-159">Depois que essa mensagem desaparecerá, ponto de extremidade hello está ativo.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="6dbf4-160">Agora você pode testar seu aplicativo navegando toohello nome DNS de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="6dbf4-161">site de saudação deve aparecer a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-161">hello website should appear similar toohello following:</span></span>

    ![página padrão de rails][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="6dbf4-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6dbf4-163">Next steps</span></span>
<span data-ttu-id="6dbf4-164">Neste tutorial, você já fez a maioria das etapas de saudação manualmente.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="6dbf4-165">Em um ambiente de produção, você deve gravar seu aplicativo em um computador de desenvolvimento e implantá-lo toohello VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="6dbf4-166">Além disso, a maioria dos ambientes de produção hospedam o aplicativo de trilhos de saudação em conjunto com outro processo de servidor, como Apache ou NginX, que trata solicitações roteamento instâncias de toomultiple do aplicativo de trilhos hello e atendendo a recursos estáticos.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="6dbf4-167">Para obter mais informações, consulte http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="6dbf4-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="6dbf4-168">toolearn mais sobre Ruby trilhos, visite Olá [Ruby trilhos guias][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="6dbf4-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="6dbf4-169">serviços do Azure de toouse do seu aplicativo Ruby, consulte:</span><span class="sxs-lookup"><span data-stu-id="6dbf4-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="6dbf4-170">[Armazenar dados desestruturados usando blobs][blobs]</span><span class="sxs-lookup"><span data-stu-id="6dbf4-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="6dbf4-171">[Armazenar pares de chave/valor usando tabelas][tables]</span><span class="sxs-lookup"><span data-stu-id="6dbf4-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="6dbf4-172">[Atender ao conteúdo de alta largura de banda com hello rede de fornecimento de conteúdo][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="6dbf4-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
