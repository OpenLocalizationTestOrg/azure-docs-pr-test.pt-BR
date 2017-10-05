---
title: Desenvolver localmente com o Emulador Azure Cosmos DB | Microsoft Docs
description: "Usando o Emulador do Azure Cosmos DB, você pode desenvolver e testar seu aplicativo no local gratuitamente, sem criar uma assinatura do Azure."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="bb193-104">Usar o Emulador do Azure Cosmos DB para desenvolvimento e teste locais</span><span class="sxs-lookup"><span data-stu-id="bb193-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="bb193-105"><strong>Binários</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="bb193-106">Baixar MSI</span><span class="sxs-lookup"><span data-stu-id="bb193-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="bb193-108">Hub de Docker</span><span class="sxs-lookup"><span data-stu-id="bb193-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-109"><strong>Fonte de Docker</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="bb193-110">Github</span><span class="sxs-lookup"><span data-stu-id="bb193-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="bb193-111">O Emulador do Azure Cosmos DB fornece um ambiente local que emula o serviço Azure Cosmos DB para fins de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="bb193-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="bb193-112">Com o Emulador do Azure Cosmos DB, você pode desenvolver e testar seu aplicativo localmente sem criar uma assinatura Azure ou incorrer em custos.</span><span class="sxs-lookup"><span data-stu-id="bb193-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="bb193-113">Quando estiver satisfeito com o funcionamento de seu aplicativo no Emulador do Azure Cosmos DB, você poderá passar a usar uma conta do Azure Cosmos DB na nuvem.</span><span class="sxs-lookup"><span data-stu-id="bb193-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="bb193-114">Este artigo aborda as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="bb193-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bb193-115">Instalar o Emulador</span><span class="sxs-lookup"><span data-stu-id="bb193-115">Installing the Emulator</span></span>
> * <span data-ttu-id="bb193-116">Executar o Emulador no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="bb193-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="bb193-117">Autenticar solicitações</span><span class="sxs-lookup"><span data-stu-id="bb193-117">Authenticating requests</span></span>
> * <span data-ttu-id="bb193-118">Usar o Data Explorer no Emulador</span><span class="sxs-lookup"><span data-stu-id="bb193-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="bb193-119">Exportar certificados SSL</span><span class="sxs-lookup"><span data-stu-id="bb193-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="bb193-120">Chamar o Emulador na linha de comando</span><span class="sxs-lookup"><span data-stu-id="bb193-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="bb193-121">Coletar arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="bb193-121">Collecting trace files</span></span>

<span data-ttu-id="bb193-122">É recomendável começar assistindo ao vídeo a seguir, em que Kirill Gavrylyuk mostra como começar a usar o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="bb193-123">Observe que o se vídeo refere ao emulador como o Emulador do DocumentDB, mas a ferramenta em si foi renomeada como Emulador do Azure Cosmos DB desde a gravação do vídeo.</span><span class="sxs-lookup"><span data-stu-id="bb193-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="bb193-124">Todas as informações do vídeo ainda estão corretas para o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="bb193-125">Como o emulador funciona</span><span class="sxs-lookup"><span data-stu-id="bb193-125">How the Emulator works</span></span>
<span data-ttu-id="bb193-126">O Emulador do Azure Cosmos DB fornece uma emulação de alta fidelidade do serviço Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="bb193-127">Ele dá suporte a uma funcionalidade idêntica ao Azure Cosmos DB, incluindo suporte para criar e consultar documentos JSON, provisionar e dimensionar coleções, bem como executar procedimentos armazenados e gatilhos.</span><span class="sxs-lookup"><span data-stu-id="bb193-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="bb193-128">Desenvolva e teste aplicativos usando o Emulador do Azure Cosmos DB e implante-os no Azure em escala global, apenas fazendo uma única alteração de configuração no ponto de extremidade de conexão do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="bb193-129">Embora tenhamos criado uma emulação local de alta fidelidade do serviço Azure Cosmos DB real, a implementação do Emulador do Azure Cosmos DB é diferente da implementação do serviço.</span><span class="sxs-lookup"><span data-stu-id="bb193-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="bb193-130">Por exemplo, o Emulador do Azure Cosmos DB usa componentes padrão do sistema operacional, como sistema de arquivos local para persistência e pilha de protocolo HTTPS para conectividade.</span><span class="sxs-lookup"><span data-stu-id="bb193-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="bb193-131">Isso significa que algumas funcionalidades que dependem da infraestrutura do Azure, como replicação global, latência de único dígito em milissegundos para leituras/gravações e níveis de consistência ajustáveis, não estão disponíveis pelo Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="bb193-132">No momento o Data Explorer no emulador dá suporte apenas à criação de coleções de API do DocumentDB e de coleções do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bb193-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="bb193-133">Atualmente não há suporte para a criação de tabelas e gráficos no Data Explorer no emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="bb193-134">Requisitos do sistema</span><span class="sxs-lookup"><span data-stu-id="bb193-134">System requirements</span></span>
<span data-ttu-id="bb193-135">O Emulador do Azure Cosmos DB tem os seguintes requisitos de hardware e software:</span><span class="sxs-lookup"><span data-stu-id="bb193-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="bb193-136">Requisitos de software</span><span class="sxs-lookup"><span data-stu-id="bb193-136">Software requirements</span></span>
  * <span data-ttu-id="bb193-137">Windows Server 2012 R2, Windows Server 2016 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="bb193-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="bb193-138">Requisitos mínimos de hardware</span><span class="sxs-lookup"><span data-stu-id="bb193-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="bb193-139">2 GB de RAM</span><span class="sxs-lookup"><span data-stu-id="bb193-139">2 GB RAM</span></span>
  * <span data-ttu-id="bb193-140">Espaço disponível no disco rígido de 10 GB</span><span class="sxs-lookup"><span data-stu-id="bb193-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="bb193-141">Instalação</span><span class="sxs-lookup"><span data-stu-id="bb193-141">Installation</span></span>
<span data-ttu-id="bb193-142">Você pode baixar e instalar o Emulador do Azure Cosmos DB no [Centro de Download da Microsoft](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="bb193-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="bb193-143">Para instalar, configurar e executar o Emulador do Azure Cosmos DB, você deve ter privilégios administrativos no computador.</span><span class="sxs-lookup"><span data-stu-id="bb193-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="bb193-144">Executar no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="bb193-144">Running on Docker for Windows</span></span>

<span data-ttu-id="bb193-145">O Emulador do Azure Cosmos DB pode ser executado no Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="bb193-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="bb193-146">O emulador não funciona no Docker para Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="bb193-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="bb193-147">Depois de ter instalado o [Docker para Windows](https://www.docker.com/docker-windows) é possível, do Hub do Docker, efetuar pull da imagem do emulador executando o comando a seguir do seu shell favorito (cmd.exe, PowerShell, etc.).</span><span class="sxs-lookup"><span data-stu-id="bb193-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="bb193-148">Para iniciar a imagem, execute os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb193-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="bb193-149">A resposta tem aparência semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb193-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="bb193-150">Fechar o shell interativo depois de o emulador ter sido iniciado desligará o contêiner do emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="bb193-151">Use o ponto de extremidade e a chave mestra da resposta no seu cliente e importe o certificado SSL no seu host.</span><span class="sxs-lookup"><span data-stu-id="bb193-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="bb193-152">Para importar o certificado SSL, faça o seguinte em um prompt de comando do administrador:</span><span class="sxs-lookup"><span data-stu-id="bb193-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="bb193-153">Iniciar o emulador</span><span class="sxs-lookup"><span data-stu-id="bb193-153">Start the Emulator</span></span>

<span data-ttu-id="bb193-154">Para iniciar o Emulador do Azure Cosmos DB, selecione o botão Iniciar ou pressione a tecla Windows.</span><span class="sxs-lookup"><span data-stu-id="bb193-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="bb193-155">Comece a digitar **Emulador do Azure Cosmos DB** e selecione o emulador na lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bb193-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Selecionar o botão Iniciar ou pressionar a tecla Windows, começar a digitar **Emulador do Azure Cosmos DB** e selecionar o emulador na lista de aplicativos](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="bb193-157">Quando o emulador estiver em execução, você verá um ícone na área de notificação da barra de tarefas do Windows.</span><span class="sxs-lookup"><span data-stu-id="bb193-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Notificação na barra de tarefas do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="bb193-159">O Emulador do Azure Cosmos DB, por padrão, é executado no computador local ("localhost") escutando na porta 8081.</span><span class="sxs-lookup"><span data-stu-id="bb193-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="bb193-160">O Emulador do Azure Cosmos DB é instalado por padrão no diretório `C:\Program Files\Azure Cosmos DB Emulator`.</span><span class="sxs-lookup"><span data-stu-id="bb193-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="bb193-161">Você também pode iniciar e parar o emulador pela linha de comando.</span><span class="sxs-lookup"><span data-stu-id="bb193-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="bb193-162">Veja [Referência da ferramenta de linha de comando](#command-line) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="bb193-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="bb193-163">Iniciar o Data Explorer</span><span class="sxs-lookup"><span data-stu-id="bb193-163">Start Data Explorer</span></span>

<span data-ttu-id="bb193-164">Quando o emulador do Azure Cosmos DB é iniciado, ele abre automaticamente o Data Explorer do Azure Cosmos DB no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="bb193-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="bb193-165">O endereço aparecerá como [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="bb193-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="bb193-166">Se você fechar o Explorer e quiser reabri-lo mais tarde, é possível abrir a URL no navegador ou iniciá-lo no Emulador do Azure Cosmos DB no Ícone de Bandeja do Windows, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="bb193-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Iniciador do Data Explorer do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="bb193-168">Procurando atualizações</span><span class="sxs-lookup"><span data-stu-id="bb193-168">Checking for updates</span></span>
<span data-ttu-id="bb193-169">O Data Explorer indica se há uma nova atualização disponível para download.</span><span class="sxs-lookup"><span data-stu-id="bb193-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="bb193-170">Não há garantias de que os dados criados em uma versão do Emulador do Azure Cosmos DB possam ser acessados em outras versões.</span><span class="sxs-lookup"><span data-stu-id="bb193-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="bb193-171">Se você precisar persistir seus dados por longo prazo, é recomendável armazená-los em uma conta do Azure Cosmos DB e não no Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="bb193-172">Autenticar solicitações</span><span class="sxs-lookup"><span data-stu-id="bb193-172">Authenticating requests</span></span>
<span data-ttu-id="bb193-173">Assim como no Cosmos DB na nuvem, cada solicitação feita no Emulador do Azure Cosmos DB deve ser autenticada.</span><span class="sxs-lookup"><span data-stu-id="bb193-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="bb193-174">O Emulador do Azure Cosmos DB dá suporte a uma única conta fixa e a uma chave de autenticação conhecida para autenticação de chave mestra.</span><span class="sxs-lookup"><span data-stu-id="bb193-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="bb193-175">Essa conta e a chave são as únicas credenciais permitidas para uso com o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="bb193-176">Eles são:</span><span class="sxs-lookup"><span data-stu-id="bb193-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="bb193-177">A chave mestra com suporte do Emulador do Azure Cosmos DB destina-se ao uso somente com o emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="bb193-178">Você não pode usar sua conta do Azure Cosmos DB de produção e a chave com o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="bb193-179">Se você tiver iniciado o emulador com a opção /Key, use a chave gerada em vez de "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="bb193-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="bb193-180">Além disso, assim como o serviço Azure Cosmos DB, o Emulador do Azure Cosmos DB tem suporte apenas à comunicação segura por SSL.</span><span class="sxs-lookup"><span data-stu-id="bb193-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="bb193-181">Executar o emulador em uma rede local</span><span class="sxs-lookup"><span data-stu-id="bb193-181">Running the emulator on a local network</span></span>

<span data-ttu-id="bb193-182">Você pode executar o emulador em uma rede local.</span><span class="sxs-lookup"><span data-stu-id="bb193-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="bb193-183">Para habilitar o acesso à rede, especifique a opção /AllowNetworkAccess na [linha de comando](#command-line-syntax), o que também requer que você especifique /Key=key_string ou /KeyFile=file_name.</span><span class="sxs-lookup"><span data-stu-id="bb193-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="bb193-184">Você pode usar /GenKeyFile=file_name para gerar um arquivo com uma chave aleatória antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="bb193-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="bb193-185">Em seguida, você pode passá-la para /KeyFile=file_name ou /Key=contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="bb193-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="bb193-186">Para habilitar o acesso de rede pela primeira vez, o usuário deve desligar o emulador e excluir o diretório de dados do emulador (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="bb193-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="bb193-187">Desenvolver com o Emulador</span><span class="sxs-lookup"><span data-stu-id="bb193-187">Developing with the Emulator</span></span>
<span data-ttu-id="bb193-188">Depois que o Emulador do Azure Cosmos DB estiver em execução na área de trabalho, você poderá usar qualquer [SDK do Azure Cosmos DB](documentdb-sdk-dotnet.md) com suporte ou a [API REST do Azure Cosmos DB](/rest/api/documentdb/) para interagir com o Emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="bb193-189">O Emulador do Azure Cosmos DB também inclui um Data Explorer interno que permite criar coleções para as APIs do MongoDB e DocumentDB e exibir e editar documentos sem precisar escrever qualquer código.</span><span class="sxs-lookup"><span data-stu-id="bb193-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="bb193-190">Se você estiver usando o [suporte ao protocolo do Azure Cosmos DB para MongoDB](mongodb-introduction.md), use a seguinte cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="bb193-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="bb193-191">Você pode usar ferramentas existentes, como o [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio), para se conectar ao Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="bb193-192">Também é possível migrar dados entre o Emulador do Azure Cosmos DB e o serviço Azure Cosmos DB usando a [Ferramenta de Migração de Dados do Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="bb193-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="bb193-193">Se você tiver iniciado o emulador com a opção /Key, use a chave gerada em vez de "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span><span class="sxs-lookup"><span data-stu-id="bb193-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="bb193-194">Usando o emulador do Azure Cosmos DB, por padrão, você pode criar até 25 coleções de partição única ou uma coleção particionada.</span><span class="sxs-lookup"><span data-stu-id="bb193-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="bb193-195">Para saber mais sobre como alterar esse valor, veja [Definição do valor de PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="bb193-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="bb193-196">Exportar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="bb193-196">Export the SSL certificate</span></span>

<span data-ttu-id="bb193-197">As linguagens e o tempo de execução .NET usam o Repositório de Certificados do Windows para a conexão segura com o emulador local do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="bb193-198">Outras linguagens têm seu próprio método de gerenciar e usar certificados.</span><span class="sxs-lookup"><span data-stu-id="bb193-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="bb193-199">O Java usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) enquanto o Python usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="bb193-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="bb193-200">Para obter um certificado para uso com linguagens e tempos de execução que não se integram ao Repositório de Certificados do Windows, você precisará exportá-lo usando o Gerenciador de Certificados do Windows.</span><span class="sxs-lookup"><span data-stu-id="bb193-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="bb193-201">Você pode iniciá-lo executando certlm.msc ou seguir as instruções passo a passo em [Exportar os certificados do Emulador do Azure Cosmos DB](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="bb193-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="bb193-202">Depois que o gerenciador de certificados estiver em execução, abra os Certificados Pessoais, conforme mostrado abaixo, e exporte o certificado com o nome amigável "DocumentDBEmulatorCertificate" como um arquivo X.509 codificado em BASE-64 (.cer).</span><span class="sxs-lookup"><span data-stu-id="bb193-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificado SSL do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="bb193-204">O certificado X.509 pode ser importado no repositório de certificados Java seguindo as instruções em [Adicionando um certificado ao repositório de certificados de AC do Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="bb193-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="bb193-205">Depois que o certificado é importado para o repositório de certificados, os aplicativos Java e MongoDB podem se conectar ao Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="bb193-206">Durante a conexão do emulador de SDKs Python e Node.js, a verificação de SSL é desabilitada.</span><span class="sxs-lookup"><span data-stu-id="bb193-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="bb193-207"><a id="command-line"></a>Referência da ferramenta de linha de comando</span><span class="sxs-lookup"><span data-stu-id="bb193-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="bb193-208">No local da instalação, você pode usar a linha de comando para iniciar e interromper o emulador, configurar opções e executar outras operações.</span><span class="sxs-lookup"><span data-stu-id="bb193-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="bb193-209">Sintaxe da linha de comando</span><span class="sxs-lookup"><span data-stu-id="bb193-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="bb193-210">Para exibir a lista de opções, digite `CosmosDB.Emulator.exe /?` no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="bb193-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="bb193-211"><strong>Opção</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="bb193-212"><strong>Descrição</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="bb193-213"><strong>Comando</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="bb193-214"><strong>Argumentos</strong></span><span class="sxs-lookup"><span data-stu-id="bb193-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-215">[No arguments]</span><span class="sxs-lookup"><span data-stu-id="bb193-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="bb193-216">Inicia o Emulador do Azure Cosmos DB com as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="bb193-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="bb193-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="bb193-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-218">[Ajuda]</span><span class="sxs-lookup"><span data-stu-id="bb193-218">[Help]</span></span></td>
  <td><span data-ttu-id="bb193-219">Exibe a lista de argumentos de linha de comando com suporte.</span><span class="sxs-lookup"><span data-stu-id="bb193-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="bb193-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="bb193-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="bb193-221">Shutdown</span></span></td>
  <td><span data-ttu-id="bb193-222">Desliga o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="bb193-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="bb193-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="bb193-224">DataPath</span></span></td>
  <td><span data-ttu-id="bb193-225">Especifica o caminho no qual armazenar os arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="bb193-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="bb193-226">O padrão é %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="bb193-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="bb193-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="bb193-228">&lt;datapath&gt;: um caminho acessível</span><span class="sxs-lookup"><span data-stu-id="bb193-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-229">Porta</span><span class="sxs-lookup"><span data-stu-id="bb193-229">Port</span></span></td>
  <td><span data-ttu-id="bb193-230">Especifica o número da porta a ser usada para o emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="bb193-231">O padrão é 8081.</span><span class="sxs-lookup"><span data-stu-id="bb193-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="bb193-232">CosmosDB.Emulator.exe /Port=&lt;porta&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="bb193-233">&lt;port&gt;: único número de porta</span><span class="sxs-lookup"><span data-stu-id="bb193-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="bb193-234">MongoPort</span></span></td>
  <td><span data-ttu-id="bb193-235">Especifica o número da porta a ser usada para API de compatibilidade do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="bb193-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="bb193-236">O padrão é 10255.</span><span class="sxs-lookup"><span data-stu-id="bb193-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="bb193-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="bb193-238">&lt;mongoport&gt;: único número de porta</span><span class="sxs-lookup"><span data-stu-id="bb193-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="bb193-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="bb193-240">Especifica as portas a serem usadas para conectividade direta.</span><span class="sxs-lookup"><span data-stu-id="bb193-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="bb193-241">Os padrões são 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="bb193-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="bb193-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="bb193-243">&lt;directports&gt;: lista de 4 portas delimitadas por vírgula</span><span class="sxs-lookup"><span data-stu-id="bb193-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-244">Chave</span><span class="sxs-lookup"><span data-stu-id="bb193-244">Key</span></span></td>
  <td><span data-ttu-id="bb193-245">Chave de autorização para o emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-245">Authorization key for the emulator.</span></span> <span data-ttu-id="bb193-246">A chave deve ser a codificação de base 64 de um vetor de 64 bytes.</span><span class="sxs-lookup"><span data-stu-id="bb193-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="bb193-247">CosmosDB.Emulator.exe /Key:&lt;chave&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="bb193-248">&lt;key&gt;: a chave de ser a codificação base-64 de um vetor de 64 bytes</span><span class="sxs-lookup"><span data-stu-id="bb193-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="bb193-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="bb193-250">Especifica que o comportamento de limitação da taxa de solicitação está habilitado.</span><span class="sxs-lookup"><span data-stu-id="bb193-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="bb193-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="bb193-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="bb193-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="bb193-253">Especifica que o comportamento de limitação da taxa de solicitação está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="bb193-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="bb193-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="bb193-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="bb193-255">NoUI</span></span></td>
  <td><span data-ttu-id="bb193-256">Não mostra o emulador de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="bb193-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="bb193-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="bb193-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="bb193-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="bb193-259">Não mostra o gerenciador de documentos na inicialização.</span><span class="sxs-lookup"><span data-stu-id="bb193-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="bb193-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="bb193-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="bb193-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="bb193-262">Especifica o número máximo de coleções particionadas.</span><span class="sxs-lookup"><span data-stu-id="bb193-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="bb193-263">Veja [Alterar o número de coleções](#set-partitioncount) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="bb193-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="bb193-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="bb193-265">&lt;contagemdepartições&gt;: número máximo permitido de coleções de partição única.</span><span class="sxs-lookup"><span data-stu-id="bb193-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="bb193-266">O padrão é 25.</span><span class="sxs-lookup"><span data-stu-id="bb193-266">Default is 25.</span></span> <span data-ttu-id="bb193-267">O máximo permitido é 250.</span><span class="sxs-lookup"><span data-stu-id="bb193-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="bb193-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="bb193-269">Especifica o número padrão de partições para uma coleção particionada.</span><span class="sxs-lookup"><span data-stu-id="bb193-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="bb193-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="bb193-271">&lt;defaultpartitioncount&gt; O padrão é 25.</span><span class="sxs-lookup"><span data-stu-id="bb193-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="bb193-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="bb193-273">Permite o acesso para o emulador através de uma rede.</span><span class="sxs-lookup"><span data-stu-id="bb193-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="bb193-274">Você também deve passar /Key=&lt;key_string&gt; ou /KeyFile=&lt;file_name&gt; para habilitar o acesso à rede.</span><span class="sxs-lookup"><span data-stu-id="bb193-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="bb193-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="bb193-276">ou o</span><span class="sxs-lookup"><span data-stu-id="bb193-276">or</span></span><br><br><span data-ttu-id="bb193-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="bb193-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="bb193-279">Não ajuste as regras de firewall quando /AllowNetworkAccess for usado.</span><span class="sxs-lookup"><span data-stu-id="bb193-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="bb193-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="bb193-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="bb193-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="bb193-282">Gere uma nova chave de autorização e salve no arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="bb193-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="bb193-283">A chave gerada pode ser usada com as opções /Key ou /KeyFile.</span><span class="sxs-lookup"><span data-stu-id="bb193-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="bb193-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;caminho até o arquivo da chave&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-285">Consistência</span><span class="sxs-lookup"><span data-stu-id="bb193-285">Consistency</span></span></td>
  <td><span data-ttu-id="bb193-286">Defina o nível de consistência padrão da conta.</span><span class="sxs-lookup"><span data-stu-id="bb193-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="bb193-287">CosmosDB.Emulator.exe /Consistency=&lt;consistência&gt;</span><span class="sxs-lookup"><span data-stu-id="bb193-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="bb193-288">&lt;consistência&gt;: o valor deve ser um dos seguintes [níveis de consistência](consistency-levels.md): Sessão, Forte, Eventual ou BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="bb193-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="bb193-289">O valor padrão é Sessão.</span><span class="sxs-lookup"><span data-stu-id="bb193-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="bb193-290">?</span><span class="sxs-lookup"><span data-stu-id="bb193-290">?</span></span></td>
  <td><span data-ttu-id="bb193-291">Mostre a mensagem de ajuda.</span><span class="sxs-lookup"><span data-stu-id="bb193-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="bb193-292">Diferenças entre o Emulador do Azure Cosmos DB e o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bb193-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="bb193-293">Como o Emulador do Azure Cosmos DB fornece um ambiente emulado em execução em uma estação de trabalho do desenvolvedor local, há algumas diferenças na funcionalidade entre o emulador e a conta do Azure Cosmos DB na nuvem:</span><span class="sxs-lookup"><span data-stu-id="bb193-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="bb193-294">O Emulador do Azure Cosmos DB dá suporte apenas uma única conta fixa e uma chave mestra conhecida.</span><span class="sxs-lookup"><span data-stu-id="bb193-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="bb193-295">Não é possível regenerar uma chave no Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="bb193-296">O Emulador do Azure Cosmos DB não é um serviço escalonável e não dará suporte a um grande número de coleções.</span><span class="sxs-lookup"><span data-stu-id="bb193-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="bb193-297">O Emulador do Azure Cosmos DB não simula diferentes [níveis de consistência do Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="bb193-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="bb193-298">O Emulador do Azure Cosmos DB não simula [replicação de várias regiões](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="bb193-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="bb193-299">O Emulador do Azure Cosmos DB não dá suporte às substituições de cota de serviço que estão disponíveis no serviço Azure Cosmos DB (por exemplo, limites de tamanho de documento, aumento do armazenamento de coleção particionado).</span><span class="sxs-lookup"><span data-stu-id="bb193-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="bb193-300">Como a sua cópia do Emulador do Azure Cosmos DB pode não ser atualizada com as alterações mais recentes com o serviço Azure Cosmos DB, use o [planejador de capacidade do Azure Cosmos DB](https://www.documentdb.com/capacityplanner) para estimar precisamente as necessidades de taxa de transferência (RUs) do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb193-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="bb193-301"><a id="set-partitioncount"></a>Alterar o número de coleções</span><span class="sxs-lookup"><span data-stu-id="bb193-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="bb193-302">Por padrão, você pode criar até 25 coleções de partição única ou uma coleção particionada usando o Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="bb193-303">Modificando o valor **PartitionCount**, você pode criar até 250 coleções de partição única ou 10 coleções particionadas ou qualquer combinação dos dois que não excedam 250 partições únicas (onde 1 coleção particionada = 25 coleções de partição única).</span><span class="sxs-lookup"><span data-stu-id="bb193-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="bb193-304">Se você tentar criar uma coleção depois que a contagem de partição atual tiver sido excedida, o emulador lançará uma exceção de ServiceUnavailable, com a mensagem de erro a seguir.</span><span class="sxs-lookup"><span data-stu-id="bb193-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="bb193-305">Para alterar o número de coleções disponíveis para o Emulador do Azure Cosmos DB, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb193-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="bb193-306">Exclua todos os dados locais do Emulador do Azure Cosmos DB clicando com o botão direito do mouse no ícone **Emulador do Azure Cosmos DB** na bandeja do sistema e clicando em **Redefinir Dados…**.</span><span class="sxs-lookup"><span data-stu-id="bb193-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="bb193-307">Exclua todos os dados de emulador desta pasta C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="bb193-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="bb193-308">Saia de todas as instâncias abertas clicando com o botão direito do mouse no ícone do **Emulador do Azure Cosmos DB** na bandeja do sistema e clicando em **Sair**.</span><span class="sxs-lookup"><span data-stu-id="bb193-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="bb193-309">Pode levar um minuto para que todas as instâncias saiam.</span><span class="sxs-lookup"><span data-stu-id="bb193-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="bb193-310">Instale a versão mais recente do [Emulador Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="bb193-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="bb193-311">Inicie o emulador com o sinalizador PartitionCount definindo um valor <= 250.</span><span class="sxs-lookup"><span data-stu-id="bb193-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="bb193-312">Por exemplo: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="bb193-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bb193-313">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="bb193-313">Troubleshooting</span></span>

<span data-ttu-id="bb193-314">Use as dicas a seguir para ajudar a solucionar problemas encontrados com o Emulador do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="bb193-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="bb193-315">Se você tiver instalado uma nova versão do emulador e se houver erros, redefina os dados.</span><span class="sxs-lookup"><span data-stu-id="bb193-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="bb193-316">Você pode redefinir seus dados clicando com o botão direito do mouse no ícone do Emulador do Azure Cosmos DB na bandeja do sistema e clicando em Redefinir Dados....</span><span class="sxs-lookup"><span data-stu-id="bb193-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="bb193-317">Se isso não resolver os erros, você pode desinstalar e reinstalar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb193-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="bb193-318">Veja [Desinstalar o emulador local](#uninstall) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="bb193-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="bb193-319">Se o Emulador do Azure Cosmos DB falhar, colete os arquivos de despejo na pasta c:\Users\user_name\AppData\Local\CrashDumps, compacte-os e anexe-os a um email que deve ser enviado para [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bb193-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="bb193-320">Se você enfrentar falhas em CosmosDB.StartupEntryPoint.exe, execute o seguinte comando em um prompt de comando de administrador: `lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="bb193-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="bb193-321">Se você encontrar um problema de conectividade, [colete os arquivos de rastreamento](#trace-files), compacte-os e anexe-os a um email que deve ser enviado para [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bb193-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="bb193-322">Se você receber uma mensagem de **Serviço Indisponível**, o emulador poderá estar falhando em inicializar a pilha de rede.</span><span class="sxs-lookup"><span data-stu-id="bb193-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="bb193-323">Verifique se você tem o cliente seguro Pulse ou o cliente de redes Juniper instalado, uma vez que seus drivers de filtro de rede podem causar o problema.</span><span class="sxs-lookup"><span data-stu-id="bb193-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="bb193-324">Desinstalar os drivers de filtro de rede de terceiros geralmente corrige o problema.</span><span class="sxs-lookup"><span data-stu-id="bb193-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="bb193-325"><a id="trace-files"></a>Coletar arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="bb193-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="bb193-326">Para coletar rastreamentos de depuração, execute os seguintes comandos em um prompt de comando administrativo:</span><span class="sxs-lookup"><span data-stu-id="bb193-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="bb193-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="bb193-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="bb193-328">Confira a bandeja do sistema para ter certeza de que o programa foi desligado. Isso pode levar um minuto.</span><span class="sxs-lookup"><span data-stu-id="bb193-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="bb193-329">Você também pode simplesmente clicar em **Sair** na interface do usuário do Emulador do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb193-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="bb193-330">Reproduza o problema.</span><span class="sxs-lookup"><span data-stu-id="bb193-330">Reproduce the problem.</span></span> <span data-ttu-id="bb193-331">Se o Data Explorer não está funcionando, você só precisa aguardar que o navegador abra por alguns segundos para capturar o erro.</span><span class="sxs-lookup"><span data-stu-id="bb193-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="bb193-332">Navegue até `%ProgramFiles%\Azure Cosmos DB Emulator` e localize o arquivo docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="bb193-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="bb193-333">Envie o arquivo .etl junto com as etapas reproduzidas para [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) para fins de depuração.</span><span class="sxs-lookup"><span data-stu-id="bb193-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="bb193-334"><a id="uninstall"></a>Desinstalar o Emulador local</span><span class="sxs-lookup"><span data-stu-id="bb193-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="bb193-335">Saia de todas as instâncias abertas do Emulador local clicando com o botão direito do mouse no ícone do Emulador do Azure Cosmos DB na bandeja do sistema e clicando em Sair.</span><span class="sxs-lookup"><span data-stu-id="bb193-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="bb193-336">Pode levar um minuto para que todas as instâncias saiam.</span><span class="sxs-lookup"><span data-stu-id="bb193-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="bb193-337">Na caixa de pesquisa do Windows, digite **Aplicativos e recursos** e clique no resultado de **Aplicativos e recursos (Configurações do sistema)**.</span><span class="sxs-lookup"><span data-stu-id="bb193-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="bb193-338">Na lista de aplicativos, vá para **Emulador do Azure Cosmos DB**, selecione-o, clique em **Desinstalar** e então confirme e clique em **Desinstalar** novamente.</span><span class="sxs-lookup"><span data-stu-id="bb193-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="bb193-339">Quando o aplicativo for desinstalado, navegue até C:\Users\<usuário > \AppData\Local\CosmosDBEmulator e exclua a pasta.</span><span class="sxs-lookup"><span data-stu-id="bb193-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bb193-340">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb193-340">Next steps</span></span>

<span data-ttu-id="bb193-341">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bb193-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb193-342">Instalou o Emulador local</span><span class="sxs-lookup"><span data-stu-id="bb193-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="bb193-343">Realizou o rand do Emulador no Docker para Windows</span><span class="sxs-lookup"><span data-stu-id="bb193-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="bb193-344">Autenticou solicitações</span><span class="sxs-lookup"><span data-stu-id="bb193-344">Authenticated requests</span></span>
> * <span data-ttu-id="bb193-345">Usou o Data Explorer no Emulador</span><span class="sxs-lookup"><span data-stu-id="bb193-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="bb193-346">Exportou certificados SSL</span><span class="sxs-lookup"><span data-stu-id="bb193-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="bb193-347">Chamou o Emulador na linha de comando</span><span class="sxs-lookup"><span data-stu-id="bb193-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="bb193-348">Coletou arquivos de rastreamento</span><span class="sxs-lookup"><span data-stu-id="bb193-348">Collected trace files</span></span>

<span data-ttu-id="bb193-349">Neste tutorial, você aprendeu como usar o Emulador local para o desenvolvimento local gratuito.</span><span class="sxs-lookup"><span data-stu-id="bb193-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="bb193-350">Agora, você pode seguir para o próximo tutorial e aprender como exportar certificados SSL do Emulador.</span><span class="sxs-lookup"><span data-stu-id="bb193-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb193-351">Exportar os certificados do Emulador do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bb193-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
