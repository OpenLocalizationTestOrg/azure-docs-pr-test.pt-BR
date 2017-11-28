---
title: aaaDevelop localmente com hello Azure Cosmos DB emulador | Microsoft Docs
description: "Usando hello Azure Cosmos DB emulador, você pode desenvolver e testar seu aplicativo localmente para livre, sem criar uma assinatura do Azure."
services: cosmos-db
documentationcenter: 
keywords: Emulador do Azure Cosmos DB
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="d72ab-104">Use hello Azure Cosmos DB emulador para teste e desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="d72ab-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="d72ab-105"><strong>Binários</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="d72ab-106">Baixar MSI</span><span class="sxs-lookup"><span data-stu-id="d72ab-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="d72ab-108">Hub de Docker</span><span class="sxs-lookup"><span data-stu-id="d72ab-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-109"><strong>Fonte de Docker</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="d72ab-110">Github</span><span class="sxs-lookup"><span data-stu-id="d72ab-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="d72ab-111">Hello Azure Cosmos DB emulador fornece um ambiente local que emula Olá serviço de banco de dados do Azure Cosmos para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d72ab-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="d72ab-112">Usando hello Azure Cosmos DB emulador, você pode desenvolver e testar seu aplicativo localmente, sem criar uma assinatura do Azure ou incorrer em todos os custos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="d72ab-113">Quando estiver satisfeito com como seu aplicativo está funcionando no hello Azure Cosmos DB emulador, você pode alternar toousing uma conta de banco de dados do Azure Cosmos na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="d72ab-114">Este artigo aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d72ab-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d72ab-115">Instalando Olá emulador</span><span class="sxs-lookup"><span data-stu-id="d72ab-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="d72ab-116">Executando Olá emulador no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="d72ab-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="d72ab-117">Autenticar solicitações</span><span class="sxs-lookup"><span data-stu-id="d72ab-117">Authenticating requests</span></span>
> * <span data-ttu-id="d72ab-118">Usando Olá Explorador de dados em Olá emulador</span><span class="sxs-lookup"><span data-stu-id="d72ab-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="d72ab-119">Exportar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="d72ab-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="d72ab-120">Chamar hello emulador da linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="d72ab-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="d72ab-121">Coletar arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="d72ab-121">Collecting trace files</span></span>

<span data-ttu-id="d72ab-122">É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Kirill Gavrylyuk mostra como tooget iniciada com hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="d72ab-123">Observe que o vídeo Olá refere-se toohello emulador como Olá emulador de documentos, mas própria ferramenta de saudação foi renomeada hello Azure Cosmos DB emulador desde colar vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="d72ab-124">Todas as informações no hello vídeo são ainda são precisas para hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="d72ab-125">Como funciona a saudação emulador</span><span class="sxs-lookup"><span data-stu-id="d72ab-125">How hello Emulator works</span></span>
<span data-ttu-id="d72ab-126">Olá emulador do Azure Cosmos DB emula uma alta fidelidade de saudação serviço de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="d72ab-127">Ele dá suporte a uma funcionalidade idêntica ao Azure Cosmos DB, incluindo suporte para criar e consultar documentos JSON, provisionar e dimensionar coleções, bem como executar procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="d72ab-128">Você pode desenvolver e testar aplicativos usando hello Azure Cosmos DB emulador e implantá-las tooAzure em escala global fazendo apenas uma única configuração de alterar o ponto de extremidade de conexão de toohello para o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="d72ab-129">Enquanto criamos uma emulação de local de alta fidelidade do serviço de banco de dados do Azure Cosmos real hello, a implementação de saudação do hello Azure Cosmos DB emulador é diferente do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="d72ab-130">Por exemplo, hello Azure Cosmos DB emulador usa componentes de sistema operacional padrão como o sistema de arquivos local Olá para persistência e a pilha do protocolo HTTPS para conectividade.</span><span class="sxs-lookup"><span data-stu-id="d72ab-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="d72ab-131">Isso significa que algumas funcionalidades que se baseia na infraestrutura do Azure, como replicação global, latência de milissegundo dígito de leituras/gravações e níveis de consistência ajustáveis não estão disponíveis por meio de hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="d72ab-132">Neste Olá tempo Data Explorer no hello emulador só oferece suporte a criação de saudação de coleções de API de documentos e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d72ab-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="d72ab-133">Atualmente, o Hello Data Explorer no emulador de saudação não oferece suporte para a criação de saudação de tabelas e gráficos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="d72ab-134">Requisitos do sistema</span><span class="sxs-lookup"><span data-stu-id="d72ab-134">System requirements</span></span>
<span data-ttu-id="d72ab-135">Olá emulador do Azure Cosmos DB tem Olá requisitos de hardware e software a seguir:</span><span class="sxs-lookup"><span data-stu-id="d72ab-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="d72ab-136">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="d72ab-136">Software requirements</span></span>
  * <span data-ttu-id="d72ab-137">Windows Server 2012 R2, Windows Server 2016 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="d72ab-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="d72ab-138">Requisitos mínimos de hardware</span><span class="sxs-lookup"><span data-stu-id="d72ab-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="d72ab-139">2 GB de RAM</span><span class="sxs-lookup"><span data-stu-id="d72ab-139">2 GB RAM</span></span>
  * <span data-ttu-id="d72ab-140">Espaço disponível no disco rígido de 10 GB</span><span class="sxs-lookup"><span data-stu-id="d72ab-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="d72ab-141">Instalação</span><span class="sxs-lookup"><span data-stu-id="d72ab-141">Installation</span></span>
<span data-ttu-id="d72ab-142">Você pode baixar e instalar hello Azure Cosmos DB emulador da saudação [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="d72ab-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="d72ab-143">tooinstall, configurar e executar hello Azure Cosmos DB emulador, você deve ter privilégios administrativos no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="d72ab-144">Executar no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="d72ab-144">Running on Docker for Windows</span></span>

<span data-ttu-id="d72ab-145">Olá emulador do Azure Cosmos banco de dados pode ser executado no Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="d72ab-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="d72ab-146">Olá emulador não funciona no Docker para Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="d72ab-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="d72ab-147">Uma vez que [Docker para Windows](https://www.docker.com/docker-windows) instalado, você pode extrair imagem do emulador de saudação do Hub do Docker executando Olá após o comando do shell favorito (cmd.exe, PowerShell, etc.).</span><span class="sxs-lookup"><span data-stu-id="d72ab-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="d72ab-148">imagem toostart hello, executar Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d72ab-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="d72ab-149">resposta de saudação tem a aparência a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="d72ab-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="d72ab-150">Fechando interativa do shell hello quando Olá emulador foi iniciado será contêiner de desligamento Olá emulador do Windows.</span><span class="sxs-lookup"><span data-stu-id="d72ab-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="d72ab-151">Usar o ponto de extremidade de saudação e chave mestra da resposta de saudação no seu cliente e Importar certificado SSL da saudação para seu host.</span><span class="sxs-lookup"><span data-stu-id="d72ab-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="d72ab-152">Olá tooimport certificado SSL, Olá a seguir de um prompt de comando do administrador:</span><span class="sxs-lookup"><span data-stu-id="d72ab-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="d72ab-153">Iniciar o emulador de saudação</span><span class="sxs-lookup"><span data-stu-id="d72ab-153">Start hello Emulator</span></span>

<span data-ttu-id="d72ab-154">Olá toostart emulador de banco de dados do Cosmos do Azure, selecione botão de início de saudação ou pressione a tecla do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="d72ab-155">Comece digitando **emulador de banco de dados do Azure Cosmos**e selecione Olá emulador da lista de saudação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Selecione Olá início botão ou pressione Olá tecla Windows, comece a digitar * * Azure Cosmos DB emulador * * e selecione Olá emulador da lista de saudação de aplicativos](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="d72ab-157">Quando o emulador de saudação estiver em execução, você verá um ícone na Olá área de notificação de barra de tarefas do Windows.</span><span class="sxs-lookup"><span data-stu-id="d72ab-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Notificação na barra de tarefas do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="d72ab-159">Olá emulador do Azure Cosmos DB por padrão é executado saudação do computador local ("localhost") escuta na porta 8081.</span><span class="sxs-lookup"><span data-stu-id="d72ab-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="d72ab-160">Hello Azure Cosmos DB emulador é instalado por padrão toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="d72ab-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="d72ab-161">Você também pode iniciar e parar o emulador de saudação da saudação de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="d72ab-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="d72ab-162">Veja [Referência da ferramenta de linha de comando](#command-line) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d72ab-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="d72ab-163">Iniciar o Data Explorer</span><span class="sxs-lookup"><span data-stu-id="d72ab-163">Start Data Explorer</span></span>

<span data-ttu-id="d72ab-164">Quando o emulador do Azure Cosmos DB Olá inicia abrirá automaticamente hello Azure Cosmos DB Data Explorer no navegador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="d72ab-165">Olá endereço aparecerá como [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="d72ab-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="d72ab-166">Se você fechar Olá explorer e gostaria de toore-open-lo mais tarde, você pode abrir Olá URL no seu navegador ou iniciá-lo do hello Azure Cosmos DB emulador no hello ícone de bandeja do Windows, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="d72ab-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Iniciador do Data Explorer do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="d72ab-168">Procurando atualizações</span><span class="sxs-lookup"><span data-stu-id="d72ab-168">Checking for updates</span></span>
<span data-ttu-id="d72ab-169">O Data Explorer indica se há uma nova atualização disponível para download.</span><span class="sxs-lookup"><span data-stu-id="d72ab-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="d72ab-170">Os dados criados em uma versão de hello Azure Cosmos DB emulador não são garantidos toobe acessível ao usar uma versão diferente.</span><span class="sxs-lookup"><span data-stu-id="d72ab-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="d72ab-171">Se você precisar toopersist seus dados de longo prazo do hello, é recomendável que você armazene esses dados em uma conta de banco de dados do Azure Cosmos, em vez de em hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="d72ab-172">Autenticar solicitações</span><span class="sxs-lookup"><span data-stu-id="d72ab-172">Authenticating requests</span></span>
<span data-ttu-id="d72ab-173">Assim como com o banco de dados do Azure Cosmos na nuvem hello, todas as solicitações feitas em relação a saudação emulador do Azure Cosmos banco de dados devem ser autenticada.</span><span class="sxs-lookup"><span data-stu-id="d72ab-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="d72ab-174">Hello Azure Cosmos DB emulador dá suporte a uma única conta fixa e uma chave de autenticação conhecido para a autenticação de chave mestra.</span><span class="sxs-lookup"><span data-stu-id="d72ab-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="d72ab-175">A conta e a chave são credenciais de somente Olá permitidas para uso com hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="d72ab-176">Eles são:</span><span class="sxs-lookup"><span data-stu-id="d72ab-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="d72ab-177">chave mestra de saudação suportado pelo hello Azure Cosmos DB emulador destina-se a uso apenas com o emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="d72ab-178">Você não pode usar a conta de banco de dados do Azure Cosmos de produção e a chave com hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="d72ab-179">Se você iniciou o emulador de saudação com hello opção /Key, use a tecla Olá gerado em vez de "C2y6yDjf5 Relational + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="d72ab-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="d72ab-180">Além disso, apenas Olá serviço de banco de dados do Azure Cosmos, hello Azure Cosmos DB emulador oferece suporte apenas para proteger a comunicação via SSL.</span><span class="sxs-lookup"><span data-stu-id="d72ab-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="d72ab-181">Emulador de saudação em execução em uma rede local</span><span class="sxs-lookup"><span data-stu-id="d72ab-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="d72ab-182">Você pode executar o emulador de saudação em uma rede local.</span><span class="sxs-lookup"><span data-stu-id="d72ab-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="d72ab-183">tooenable acesso à rede, especifique a opção de /AllowNetworkAccess Olá Olá [linha de comando](#command-line-syntax), que também requer que você especifique /Key = key_string ou /KeyFile = file_name.</span><span class="sxs-lookup"><span data-stu-id="d72ab-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="d72ab-184">Você pode usar /GenKeyFile = file_name toogenerate um arquivo com uma chave aleatória antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="d72ab-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="d72ab-185">Em seguida, você pode passar essa muito /keyfile = file_name ou /Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="d72ab-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="d72ab-186">acesso à rede tooenable para Olá Olá usuário deve desligar emulador de saudação e excluir o diretório de dados do emulador hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="d72ab-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="d72ab-187">Desenvolvendo com hello emulador</span><span class="sxs-lookup"><span data-stu-id="d72ab-187">Developing with hello Emulator</span></span>
<span data-ttu-id="d72ab-188">Depois de você ter hello emulador Cosmos banco de dados do Azure em execução em sua área de trabalho, você pode usar qualquer suporte [banco de dados do SDK do Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API de REST do banco de dados do Azure Cosmos](/rest/api/documentdb/) toointeract com hello emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="d72ab-189">Olá emulador do Azure Cosmos DB também inclui um Gerenciador de dados interno que permite que você crie coleções para Olá documentos e MongoDB APIs e exibir e editar documentos sem gravar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="d72ab-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="d72ab-190">Se você estiver usando [o banco de dados do Azure Cosmos suporte de protocolo para o MongoDB](mongodb-introduction.md), use Olá cadeia de caracteres de conexão a seguir:</span><span class="sxs-lookup"><span data-stu-id="d72ab-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="d72ab-191">Você pode usar as ferramentas existentes como [Studio do Azure DocumentDB](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello emulador do Azure Cosmos banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d72ab-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="d72ab-192">Também é possível migrar dados entre hello Azure Cosmos DB emulador e serviço de banco de dados do Azure Cosmos hello usando Olá [ferramenta de migração de dados de banco de dados do Azure Cosmos](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="d72ab-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="d72ab-193">Se você iniciou o emulador de saudação com hello opção /Key, use a tecla Olá gerado em vez de "C2y6yDjf5 Relational + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="</span><span class="sxs-lookup"><span data-stu-id="d72ab-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="d72ab-194">Usando o emulador do Windows Azure Cosmos DB hello, por padrão, você pode criar coleções com uma partição única too25 ou 1 coleção particionada.</span><span class="sxs-lookup"><span data-stu-id="d72ab-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="d72ab-195">Para obter mais informações sobre como alterar esse valor, consulte [configuração Olá PartitionCount valor](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="d72ab-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="d72ab-196">Exportar o certificado SSL Olá</span><span class="sxs-lookup"><span data-stu-id="d72ab-196">Export hello SSL certificate</span></span>

<span data-ttu-id="d72ab-197">Linguagens .NET e o tempo de execução use Olá repositório de certificados do Windows toosecurely conectam emulador local do banco de dados do Azure Cosmos toohello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="d72ab-198">Outras linguagens têm seu próprio método de gerenciar e usar certificados.</span><span class="sxs-lookup"><span data-stu-id="d72ab-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="d72ab-199">O Java usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) enquanto o Python usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="d72ab-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="d72ab-200">Em ordem tooobtain toouse um certificado com linguagens e tempos de execução que não integram Olá repositório de certificados do Windows você precisará tooexport usando Olá Gerenciador de certificados do Windows.</span><span class="sxs-lookup"><span data-stu-id="d72ab-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="d72ab-201">Você pode iniciá-lo executando certlm.msc ou siga as instruções passo a passo de saudação em [exportar hello Azure Cosmos DB emulador certificados](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="d72ab-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="d72ab-202">Quando o Gerenciador de certificados Olá estiver em execução, abra Olá pessoal de certificados conforme mostrado abaixo e exportar Olá certificado com o nome amigável do hello "DocumentDBEmulatorCertificate" como o arquivo de x. 509 (. cer) codificado em BASE 64.</span><span class="sxs-lookup"><span data-stu-id="d72ab-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificado SSL do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="d72ab-204">certificado x. 509 de saudação pode ser importado para o repositório de certificados do Java hello, seguindo as instruções de saudação do [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="d72ab-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="d72ab-205">Depois que o certificado Olá é importado no repositório de certificados Olá, aplicativos Java e MongoDB será toohello tooconnect capaz de emulador do Azure Cosmos banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d72ab-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="d72ab-206">Ao conectar o emulador toohello de Python e Node.js SDKs, verificação de SSL está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="d72ab-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="d72ab-207"><a id="command-line"></a>Referência da ferramenta de linha de comando</span><span class="sxs-lookup"><span data-stu-id="d72ab-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="d72ab-208">Do local de instalação Olá, você pode usar Olá toostart de linha de comando e interromper o emulador de saudação, configurar opções e executar outras operações.</span><span class="sxs-lookup"><span data-stu-id="d72ab-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="d72ab-209">Sintaxe da linha de comando</span><span class="sxs-lookup"><span data-stu-id="d72ab-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="d72ab-210">lista de saudação tooview de opções, digite `CosmosDB.Emulator.exe /?` no prompt de comando hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="d72ab-211"><strong>Opção</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="d72ab-212"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="d72ab-213"><strong>Comando</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="d72ab-214"><strong>Argumentos</strong></span><span class="sxs-lookup"><span data-stu-id="d72ab-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-215">[No arguments]</span><span class="sxs-lookup"><span data-stu-id="d72ab-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="d72ab-216">Inicia hello Azure Cosmos DB emulador com as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="d72ab-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="d72ab-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="d72ab-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-218">[Ajuda]</span><span class="sxs-lookup"><span data-stu-id="d72ab-218">[Help]</span></span></td>
  <td><span data-ttu-id="d72ab-219">Exibe a lista de saudação do suporte para argumentos de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="d72ab-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="d72ab-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="d72ab-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="d72ab-221">Shutdown</span></span></td>
  <td><span data-ttu-id="d72ab-222">Olá emulador do Azure Cosmos banco de dados é desligado.</span><span class="sxs-lookup"><span data-stu-id="d72ab-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="d72ab-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="d72ab-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="d72ab-224">DataPath</span></span></td>
  <td><span data-ttu-id="d72ab-225">Especifica o caminho de saudação em quais arquivos de dados toostore.</span><span class="sxs-lookup"><span data-stu-id="d72ab-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="d72ab-226">O padrão é %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="d72ab-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="d72ab-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-228">&lt;datapath&gt;: um caminho acessível</span><span class="sxs-lookup"><span data-stu-id="d72ab-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-229">Porta</span><span class="sxs-lookup"><span data-stu-id="d72ab-229">Port</span></span></td>
  <td><span data-ttu-id="d72ab-230">Especifica o toouse de número de porta Olá emulador do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="d72ab-231">O padrão é 8081.</span><span class="sxs-lookup"><span data-stu-id="d72ab-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="d72ab-232">CosmosDB.Emulator.exe /Port=&lt;porta&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-233">&lt;port&gt;: único número de porta</span><span class="sxs-lookup"><span data-stu-id="d72ab-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="d72ab-234">MongoPort</span></span></td>
  <td><span data-ttu-id="d72ab-235">Especifica o toouse de número de porta Olá para fins de compatibilidade do MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="d72ab-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="d72ab-236">O padrão é 10255.</span><span class="sxs-lookup"><span data-stu-id="d72ab-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="d72ab-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-238">&lt;mongoport&gt;: único número de porta</span><span class="sxs-lookup"><span data-stu-id="d72ab-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="d72ab-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="d72ab-240">Especifica a saudação toouse de portas para conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="d72ab-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="d72ab-241">Os padrões são 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="d72ab-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="d72ab-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-243">&lt;directports&gt;: lista de 4 portas delimitadas por vírgula</span><span class="sxs-lookup"><span data-stu-id="d72ab-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-244">Chave</span><span class="sxs-lookup"><span data-stu-id="d72ab-244">Key</span></span></td>
  <td><span data-ttu-id="d72ab-245">Chave de autorização para o emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="d72ab-246">Chave deve ser Olá codificação de base 64 de um vetor de 64 bytes.</span><span class="sxs-lookup"><span data-stu-id="d72ab-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="d72ab-247">CosmosDB.Emulator.exe /Key:&lt;chave&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-248">&lt;chave&gt;: chave deve ser Olá codificação de base 64 de um vetor de 64 bits</span><span class="sxs-lookup"><span data-stu-id="d72ab-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="d72ab-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="d72ab-250">Especifica que o comportamento de limitação da taxa de solicitação está habilitado.</span><span class="sxs-lookup"><span data-stu-id="d72ab-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="d72ab-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="d72ab-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="d72ab-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="d72ab-253">Especifica que o comportamento de limitação da taxa de solicitação está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="d72ab-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="d72ab-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="d72ab-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="d72ab-255">NoUI</span></span></td>
  <td><span data-ttu-id="d72ab-256">Não mostre o emulador Olá interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d72ab-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="d72ab-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="d72ab-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="d72ab-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="d72ab-259">Não mostra o gerenciador de documentos na inicialização.</span><span class="sxs-lookup"><span data-stu-id="d72ab-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="d72ab-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="d72ab-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="d72ab-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="d72ab-262">Especifica o número máximo de saudação de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="d72ab-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="d72ab-263">Consulte [alterar número de saudação de coleções](#set-partitioncount) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d72ab-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="d72ab-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-265">&lt;contagemdepartições&gt;: número máximo permitido de coleções de partição única.</span><span class="sxs-lookup"><span data-stu-id="d72ab-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="d72ab-266">O padrão é 25.</span><span class="sxs-lookup"><span data-stu-id="d72ab-266">Default is 25.</span></span> <span data-ttu-id="d72ab-267">O máximo permitido é 250.</span><span class="sxs-lookup"><span data-stu-id="d72ab-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="d72ab-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="d72ab-269">Especifica o número de partições para uma coleção particionada padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="d72ab-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-271">&lt;defaultpartitioncount&gt; O padrão é 25.</span><span class="sxs-lookup"><span data-stu-id="d72ab-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="d72ab-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="d72ab-273">Permite acessar emulador toohello em uma rede.</span><span class="sxs-lookup"><span data-stu-id="d72ab-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="d72ab-274">Você também deve transmitir /Key =&lt;key_string&gt; ou /KeyFile =&lt;file_name&gt; tooenable acesso à rede.</span><span class="sxs-lookup"><span data-stu-id="d72ab-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="d72ab-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="d72ab-276">ou o</span><span class="sxs-lookup"><span data-stu-id="d72ab-276">or</span></span><br><br><span data-ttu-id="d72ab-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="d72ab-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="d72ab-279">Não ajuste as regras de firewall quando /AllowNetworkAccess for usado.</span><span class="sxs-lookup"><span data-stu-id="d72ab-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="d72ab-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="d72ab-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="d72ab-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="d72ab-282">Gere uma nova chave de autorização e salve o arquivo especificado toohello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="d72ab-283">chave de saudação gerada pode ser usada com hello /Key ou /KeyFile opções.</span><span class="sxs-lookup"><span data-stu-id="d72ab-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="d72ab-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;caminho tookey arquivo&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-285">Consistência</span><span class="sxs-lookup"><span data-stu-id="d72ab-285">Consistency</span></span></td>
  <td><span data-ttu-id="d72ab-286">Defina o nível de consistência do hello padrão para a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="d72ab-287">CosmosDB.Emulator.exe /Consistency=&lt;consistência&gt;</span><span class="sxs-lookup"><span data-stu-id="d72ab-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="d72ab-288">&lt;consistência&gt;: valor deve ser um dos seguintes Olá [níveis de consistência](consistency-levels.md): BoundedStaleness, forte, Eventual ou sessão.</span><span class="sxs-lookup"><span data-stu-id="d72ab-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="d72ab-289">valor padrão de saudação é a sessão.</span><span class="sxs-lookup"><span data-stu-id="d72ab-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="d72ab-290">?</span><span class="sxs-lookup"><span data-stu-id="d72ab-290">?</span></span></td>
  <td><span data-ttu-id="d72ab-291">Mostre mensagem de saudação do ajuda.</span><span class="sxs-lookup"><span data-stu-id="d72ab-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="d72ab-292">Diferenças entre hello Azure Cosmos DB emulador e o banco de dados do Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="d72ab-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="d72ab-293">Como hello Azure Cosmos DB emulador fornece um ambiente emulado em execução em uma estação de trabalho de desenvolvedor local, existem algumas diferenças na funcionalidade entre emulador hello e uma conta de banco de dados do Azure Cosmos na nuvem hello:</span><span class="sxs-lookup"><span data-stu-id="d72ab-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="d72ab-294">Hello Azure Cosmos DB emulador dá suporte a apenas uma única conta fixa e uma chave mestra conhecida.</span><span class="sxs-lookup"><span data-stu-id="d72ab-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="d72ab-295">Regeneração da chave não é possível em hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="d72ab-296">Hello Azure Cosmos DB emulador não é um serviço escalonável e não oferecerão suporte a um grande número de coleções.</span><span class="sxs-lookup"><span data-stu-id="d72ab-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="d72ab-297">Hello Azure Cosmos DB emulador não simular diferentes [níveis de consistência do banco de dados do Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d72ab-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="d72ab-298">Hello Azure Cosmos DB emulador não simular [várias regiões replicação](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="d72ab-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="d72ab-299">Olá emulador do Azure Cosmos banco de dados não oferece suporte a substituições de cota de serviço Olá que estão disponíveis no serviço de banco de dados do Azure Cosmos hello (por exemplo, limites de tamanho do documento, armazenamento maior coleção particionada).</span><span class="sxs-lookup"><span data-stu-id="d72ab-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="d72ab-300">Como a cópia do hello Azure Cosmos DB emulador pode não ser backup toodate com alterações mais recentes de saudação com o serviço de banco de dados do Azure Cosmos hello, por favor [Planejador de capacidade do banco de dados do Azure Cosmos](https://www.documentdb.com/capacityplanner) taxa de transferência da produção de estimativa tooaccurately (RUs) necessidades do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d72ab-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="d72ab-301"><a id="set-partitioncount"></a>Alterar o número de saudação de coleções</span><span class="sxs-lookup"><span data-stu-id="d72ab-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="d72ab-302">Por padrão, você pode criar coleções com uma partição única too25 ou 1 coleção particionada usando hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="d72ab-303">Modificando Olá **PartitionCount** valor, você pode criar coleções com uma partição única too250 ou 10 coleções particionadas, ou qualquer combinação de saudação duas que não excedam único 250 partições (onde 1 particionados coleção = 25 coleção de partição única).</span><span class="sxs-lookup"><span data-stu-id="d72ab-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="d72ab-304">Se você tentar toocreate uma coleção depois que a contagem de partição atual Olá foi excedida, o emulador Olá lança uma exceção de ServiceUnavailable, com a seguinte mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="d72ab-305">número de saudação do toochange de coleções disponíveis toohello Azure Cosmos DB Emulator, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d72ab-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="d72ab-306">Exclua todos os dados locais do emulador do Azure Cosmos DB clicando Olá **emulador de banco de dados do Azure Cosmos** ícone na bandeja do sistema hello e, em seguida, clicando em **Redefinir dados...** .</span><span class="sxs-lookup"><span data-stu-id="d72ab-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="d72ab-307">Exclua todos os dados de emulador desta pasta C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="d72ab-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="d72ab-308">Saia de todas as instâncias abertas clicando Olá **emulador de banco de dados do Azure Cosmos** ícone na bandeja do sistema hello e, em seguida, clicando em **saída**.</span><span class="sxs-lookup"><span data-stu-id="d72ab-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="d72ab-309">Pode levar um minuto para tooexit de todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="d72ab-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="d72ab-310">Instale a versão mais recente Olá de saudação [emulador de banco de dados do Azure Cosmos](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="d72ab-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="d72ab-311">Iniciar o emulador de saudação com hello sinalizador PartitionCount definindo um valor < = 250.</span><span class="sxs-lookup"><span data-stu-id="d72ab-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="d72ab-312">Por exemplo: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="d72ab-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d72ab-313">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d72ab-313">Troubleshooting</span></span>

<span data-ttu-id="d72ab-314">Use Olá dicas toohelp solucionar problemas encontrados com o emulador do Azure Cosmos DB Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d72ab-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="d72ab-315">Se você instalou uma nova versão do emulador de saudação e houver erros, certifique-se de que redefinir os dados.</span><span class="sxs-lookup"><span data-stu-id="d72ab-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="d72ab-316">Você pode redefinir os dados clicando hello Azure Cosmos DB emulador ícone na bandeja do sistema hello e, em seguida, clicando em Redefinir dados...</span><span class="sxs-lookup"><span data-stu-id="d72ab-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="d72ab-317">Se isso não resolver erros de saudação, você pode desinstalar e reinstalar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="d72ab-318">Consulte [desinstalar um emulador local Olá](#uninstall) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="d72ab-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="d72ab-319">Se o emulador do Azure Cosmos DB Olá falhar, coletar arquivos de despejo da pasta c:\Users\user_name\AppData\Local\CrashDumps, compactá-los e anexá-los tooan email muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d72ab-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="d72ab-320">Se você enfrentar falhas em CosmosDB.StartupEntryPoint.exe, execute Olá comando a seguir em um prompt de comando do administrador:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="d72ab-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="d72ab-321">Se você encontrar um problema de conectividade, [coletar arquivos de rastreamento](#trace-files), compactá-los e anexá-los email tooan muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d72ab-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="d72ab-322">Se você receber um **serviço indisponível** mensagem, hello emulador poderia estar falhando tooinitialize da pilha de rede hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="d72ab-323">Toosee de seleção se você tiver Olá Pulse secure cliente ou Juniper redes cliente instalado, como drivers de filtro de rede podem causar um problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="d72ab-324">A desinstalação de drivers de filtro de rede de terceiros geralmente corrige o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="d72ab-325"><a id="trace-files"></a>Coletar arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="d72ab-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="d72ab-326">toocollect depuração rastreamentos, executados Olá comandos a seguir em um prompt de comando administrativo:</span><span class="sxs-lookup"><span data-stu-id="d72ab-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="d72ab-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="d72ab-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="d72ab-328">Inspecionar Olá bandeja toomake se Olá programa do sistema foi desligado, pode levar um minuto.</span><span class="sxs-lookup"><span data-stu-id="d72ab-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="d72ab-329">Você também pode simplesmente clicar **Exit** na interface de usuário do hello Azure Cosmos DB emulador.</span><span class="sxs-lookup"><span data-stu-id="d72ab-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="d72ab-330">Reproduza o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-330">Reproduce hello problem.</span></span> <span data-ttu-id="d72ab-331">Se o Gerenciador de dados não está funcionando, você só precisa toowait para Olá navegador tooopen para alguns erros de saudação do toocatch segundos.</span><span class="sxs-lookup"><span data-stu-id="d72ab-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="d72ab-332">Navegue muito`%ProgramFiles%\Azure Cosmos DB Emulator` e localizar o arquivo de docdbemulator_000001.etl hello.</span><span class="sxs-lookup"><span data-stu-id="d72ab-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="d72ab-333">Envie o arquivo de ETL de saudação junto com as etapas de reprodução muito[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) para depuração.</span><span class="sxs-lookup"><span data-stu-id="d72ab-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="d72ab-334"><a id="uninstall"></a>Desinstalar Olá emulador local</span><span class="sxs-lookup"><span data-stu-id="d72ab-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="d72ab-335">Saia de todas as instâncias abertas do hello emulador local clicando duas vezes o ícone do emulador do Azure Cosmos DB Olá na bandeja do sistema Olá, e, em seguida, clicar em Sair.</span><span class="sxs-lookup"><span data-stu-id="d72ab-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="d72ab-336">Pode levar um minuto para tooexit de todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="d72ab-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="d72ab-337">Na caixa de pesquisa do Windows hello, digite **aplicativos e recursos** e clique em Olá **aplicativos e recursos (configurações do sistema)** resultados.</span><span class="sxs-lookup"><span data-stu-id="d72ab-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="d72ab-338">Na lista de saudação de aplicativos, vá muito**emulador de banco de dados do Azure Cosmos**, selecioná-la, clique em **desinstalação**, em seguida, confirme e clique em **desinstalação** novamente.</span><span class="sxs-lookup"><span data-stu-id="d72ab-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="d72ab-339">Quando o aplicativo hello é desinstalado, navegue tooC:\Users\<usuário > \AppData\Local\CosmosDBEmulator e excluir a pasta de saudação.</span><span class="sxs-lookup"><span data-stu-id="d72ab-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d72ab-340">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d72ab-340">Next steps</span></span>

<span data-ttu-id="d72ab-341">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="d72ab-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d72ab-342">Instalado Olá emulador local</span><span class="sxs-lookup"><span data-stu-id="d72ab-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="d72ab-343">Saudação de RAND emulador no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="d72ab-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="d72ab-344">Autenticou solicitações</span><span class="sxs-lookup"><span data-stu-id="d72ab-344">Authenticated requests</span></span>
> * <span data-ttu-id="d72ab-345">Usado Olá Explorador de dados em Olá emulador</span><span class="sxs-lookup"><span data-stu-id="d72ab-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="d72ab-346">Exportou certificados SSL</span><span class="sxs-lookup"><span data-stu-id="d72ab-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="d72ab-347">Chamado hello emulador da linha de comando Olá</span><span class="sxs-lookup"><span data-stu-id="d72ab-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="d72ab-348">Coletou arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="d72ab-348">Collected trace files</span></span>

<span data-ttu-id="d72ab-349">Neste tutorial, você aprendeu como toouse Olá emulador local para local de desenvolvimento gratuito.</span><span class="sxs-lookup"><span data-stu-id="d72ab-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="d72ab-350">Agora você pode continuar tutorial próxima toohello e aprender como certificados de emulador SSL tooexport.</span><span class="sxs-lookup"><span data-stu-id="d72ab-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72ab-351">Exportar certificados de emulador do Azure Cosmos DB Olá</span><span class="sxs-lookup"><span data-stu-id="d72ab-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
