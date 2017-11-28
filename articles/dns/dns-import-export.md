---
title: "aaaImport e uma zona de domínio de exportação de arquivo tooAzure DNS usando o Azure CLI 1.0 | Microsoft Docs"
description: Saiba como tooimport e exportar um DNS da zona tooAzure arquivo DNS usando 1.0 da CLI do Azure
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="73879-103">Importar e exportar um arquivo de zona DNS usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="73879-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="73879-104">Este artigo o orienta como tooimport e exportar arquivos de zona do DNS para usar o DNS do Azure Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="73879-105">Migração de região de tooDNS de Introdução</span><span class="sxs-lookup"><span data-stu-id="73879-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="73879-106">Um arquivo de zona DNS é um arquivo de texto que contém os detalhes de cada registro do sistema de nome de domínio (DNS) na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="73879-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="73879-107">Ele segue um formato padrão, tornando-o adequado para transferir registros DNS entre sistemas DNS.</span><span class="sxs-lookup"><span data-stu-id="73879-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="73879-108">Usar um arquivo de zona é rápida e confiável e tootransfer de forma conveniente uma zona DNS ou de DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="73879-109">DNS do Azure oferece suporte à importação e exportação de arquivos de zona usando hello Azure interface de linha de comando (CLI).</span><span class="sxs-lookup"><span data-stu-id="73879-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="73879-110">Importação de arquivo de zona é **não** atualmente com suporte por meio do PowerShell do Azure ou hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="73879-111">Olá 1.0 da CLI do Azure é uma ferramenta de linha de comando de plataforma cruzada usada para gerenciar serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="73879-112">Ele está disponível para plataformas de Windows, Mac e Linux de saudação do hello [página de downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="73879-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="73879-113">Suporte de plataforma cruzada é importante para importar e exportar arquivos de zona, porque Olá software mais comuns do servidor de nome, [ASSOCIAR](https://www.isc.org/downloads/bind/), normalmente é executado no Linux.</span><span class="sxs-lookup"><span data-stu-id="73879-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="73879-114">Atualmente, há duas versões do hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="73879-115">A CLI1.0 é baseada em Node.js e tem comandos que começam com “azure”.</span><span class="sxs-lookup"><span data-stu-id="73879-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="73879-116">A CLI2.0 é baseada em Python e tem comandos que começam com “az”.</span><span class="sxs-lookup"><span data-stu-id="73879-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="73879-117">Enquanto a importação do arquivo de zona é suportada em ambas as versões, recomendamos usar comandos CLI1.0 hello, conforme descrito nesta página.</span><span class="sxs-lookup"><span data-stu-id="73879-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="73879-118">Obtenha seu arquivo de zona DNS existente</span><span class="sxs-lookup"><span data-stu-id="73879-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="73879-119">Antes de importar um arquivo de zona do DNS no DNS do Azure, você precisa tooobtain uma cópia do arquivo de zona hello.</span><span class="sxs-lookup"><span data-stu-id="73879-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="73879-120">origem desse arquivo Hello depende de onde a zona do DNS hello está hospedada no momento.</span><span class="sxs-lookup"><span data-stu-id="73879-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="73879-121">Se a zona DNS é hospedada por um serviço de parceiro (como um registrador de domínio, provedor de hospedagem de DNS dedicado ou provedor de nuvem alternativos), esse serviço deve fornecer o arquivo de zona DNS Olá capacidade toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="73879-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="73879-122">Se a zona DNS estiver hospedada no DNS do Windows, a pasta de padrão de saudação para arquivos de zona Olá é **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="73879-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="73879-123">arquivo de zona Olá caminho completo tooeach também mostra no hello **geral** guia do console de saudação do DNS.</span><span class="sxs-lookup"><span data-stu-id="73879-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="73879-124">Se a zona DNS é hospedada por meio de associação, local de saudação do arquivo de zona Olá para cada zona é especificado no arquivo de configuração de ligação de saudação **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="73879-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="73879-125">Arquivos de zona baixados do GoDaddy têm um formato ligeiramente diferente do padrão.</span><span class="sxs-lookup"><span data-stu-id="73879-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="73879-126">Você precisa toocorrect isso antes de importar esses arquivos de zona DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="73879-127">Nomes DNS em Olá RDATA de cada registro DNS são especificados como nomes totalmente qualificados, mas eles não têm um encerramento "." Isso significa que eles são interpretados por outros sistemas DNS como nomes relativos.</span><span class="sxs-lookup"><span data-stu-id="73879-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="73879-128">Você precisa de arquivo para zona tooedit Olá tooappend Olá encerrando "." tootheir nomes antes de importá-los no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="73879-129">Por exemplo, Olá registro CNAME "www 3600 CNAME contoso.com" deve ser alterada muito "www 3600 CNAME em contoso.com."</span><span class="sxs-lookup"><span data-stu-id="73879-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="73879-130">(com uma terminação “.”).</span><span class="sxs-lookup"><span data-stu-id="73879-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="73879-131">Importar um arquivo de zona DNS para o DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="73879-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="73879-132">A importação de um arquivo de zona criará uma nova zona no DNS do Azure, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="73879-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="73879-133">Se já existir uma zona Olá, hello conjuntos de registros no arquivo de zona Olá devem ser mesclados com conjuntos de registros existentes hello.</span><span class="sxs-lookup"><span data-stu-id="73879-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="73879-134">Comportamento de mesclagem</span><span class="sxs-lookup"><span data-stu-id="73879-134">Merge behavior</span></span>

* <span data-ttu-id="73879-135">Por padrão, os conjuntos de registros novos e existentes são mesclados.</span><span class="sxs-lookup"><span data-stu-id="73879-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="73879-136">Registros idênticos em um conjunto de registros mesclados têm a duplicação eliminada.</span><span class="sxs-lookup"><span data-stu-id="73879-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="73879-137">Como alternativa, especificando Olá `--force` opção, Olá substitui o processo importar conjuntos de registros existentes com novos conjuntos de registros.</span><span class="sxs-lookup"><span data-stu-id="73879-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="73879-138">Conjuntos de registros existentes que não tem um registro correspondente definido no arquivo de zona importada Olá não serão ser removidas.</span><span class="sxs-lookup"><span data-stu-id="73879-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="73879-139">Quando os conjuntos de registros são mesclados, hello tempo toolive (TTL) preexistentes de conjuntos de registros é usado.</span><span class="sxs-lookup"><span data-stu-id="73879-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="73879-140">Quando `--force` é usado, Olá TTL do novo conjunto de registros de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="73879-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="73879-141">Início dos parâmetros de autoridade (SOA) (exceto `host`) sempre são extraídas do arquivo de zona importada hello, independentemente se `--force` é usado.</span><span class="sxs-lookup"><span data-stu-id="73879-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="73879-142">Da mesma forma, para Olá nome servidor conjunto de registros no ápice da zona de hello, hello TTL é sempre obtida do arquivo de zona importada hello.</span><span class="sxs-lookup"><span data-stu-id="73879-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="73879-143">Um registro CNAME importado não substitui um CNAME existente registrar com hello mesmo nome, a menos que Olá `--force` parâmetro for especificado.</span><span class="sxs-lookup"><span data-stu-id="73879-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="73879-144">Quando um conflito entre um registro CNAME e outro registro de mesmo nome mas diferente de saudação tipo (independentemente de qual existente ou novo), registro existente Olá é mantido.</span><span class="sxs-lookup"><span data-stu-id="73879-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="73879-145">Isso é independente do uso de saudação do `--force`.</span><span class="sxs-lookup"><span data-stu-id="73879-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="73879-146">Informações adicionais sobre importação</span><span class="sxs-lookup"><span data-stu-id="73879-146">Additional information about importing</span></span>

<span data-ttu-id="73879-147">Olá observações a seguir fornecem detalhes técnicos adicionais sobre zona Olá o processo de importação.</span><span class="sxs-lookup"><span data-stu-id="73879-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="73879-148">Olá `$TTL` diretiva é opcional e é suportado.</span><span class="sxs-lookup"><span data-stu-id="73879-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="73879-149">Quando nenhum `$TTL` diretiva for fornecida, os registros sem um tempo de vida explícito sejam importados definir tooa TTL padrão de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="73879-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="73879-150">Quando dois registros no mesmo conjunto de registros hello especificar diferentes TTLs, valor inferior Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="73879-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="73879-151">Olá `$ORIGIN` diretiva é opcional e é suportado.</span><span class="sxs-lookup"><span data-stu-id="73879-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="73879-152">Quando nenhum `$ORIGIN` for definida, o padrão de saudação valor usado é o nome da zona Olá conforme especificado na linha de comando de saudação (mais encerrando Olá ".").</span><span class="sxs-lookup"><span data-stu-id="73879-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="73879-153">Olá `$INCLUDE` e `$GENERATE` diretivas não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="73879-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="73879-154">Há suporte aos seguintes tipos de registros: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="73879-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="73879-155">Olá registro SOA é criado automaticamente pelo DNS do Azure quando uma zona é criada.</span><span class="sxs-lookup"><span data-stu-id="73879-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="73879-156">Quando você importa um arquivo de zona, todos os parâmetros SOA são extraídos do arquivo de zona Olá *exceto* Olá `host` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="73879-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="73879-157">Esse parâmetro usa o valor de saudação fornecida pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="73879-158">Isso ocorre porque esse parâmetro deve referir-se o servidor de nome principal de toohello fornecido pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="73879-159">registro de servidor de nomes de saudação definido no ápice da zona de saudação também é criado automaticamente pelo DNS do Azure quando Olá zona é criada.</span><span class="sxs-lookup"><span data-stu-id="73879-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="73879-160">Somente hello TTL deste conjunto de registros é importado.</span><span class="sxs-lookup"><span data-stu-id="73879-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="73879-161">Esses registros contêm nomes de servidor de nome hello fornecidos pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="73879-162">dados de registro de saudação não são substituídos por valores hello contidos no arquivo de zona importada hello.</span><span class="sxs-lookup"><span data-stu-id="73879-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="73879-163">Durante a visualização pública, o DNS do Azure suporta apenas os registros TXT de cadeia de caracteres única.</span><span class="sxs-lookup"><span data-stu-id="73879-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="73879-164">Os registros TXT cadeias de caracteres múltiplas ser truncado e concatenado too255 caracteres.</span><span class="sxs-lookup"><span data-stu-id="73879-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="73879-165">Valores e formato da CLI</span><span class="sxs-lookup"><span data-stu-id="73879-165">CLI format and values</span></span>

<span data-ttu-id="73879-166">formato Olá Olá CLI do Azure comando tooimport uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="73879-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="73879-167">Valores:</span><span class="sxs-lookup"><span data-stu-id="73879-167">Values:</span></span>

* <span data-ttu-id="73879-168">`<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de saudação no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="73879-169">`<zone name>`é o nome de saudação da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="73879-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="73879-170">`<zone file name>`é Olá caminho/nome do toobe de arquivo de zona Olá importado.</span><span class="sxs-lookup"><span data-stu-id="73879-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="73879-171">Se uma zona com este nome não existe no grupo de recursos hello, ele é criado para você.</span><span class="sxs-lookup"><span data-stu-id="73879-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="73879-172">Se hello zona já existir, hello conjuntos de registros importados são mesclados com conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="73879-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="73879-173">toooverwrite Olá existente conjuntos de registros, use Olá `--force` opção.</span><span class="sxs-lookup"><span data-stu-id="73879-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="73879-174">formato de saudação tooverify de um arquivo de zona sem importá-lo, use Olá realmente `--parse-only` opção.</span><span class="sxs-lookup"><span data-stu-id="73879-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="73879-175">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="73879-175">Step 1.</span></span> <span data-ttu-id="73879-176">Importar um arquivo de zona</span><span class="sxs-lookup"><span data-stu-id="73879-176">Import a zone file</span></span>

<span data-ttu-id="73879-177">tooimport um arquivo de zona para a zona de saudação **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="73879-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="73879-178">Entre no tooyour assinatura do Azure usando Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="73879-179">Selecione a assinatura de saudação onde você deseja toocreate sua nova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="73879-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="73879-180">DNS do Azure é um serviço de Gerenciador de recursos somente do Azure, Olá CLI do Azure deve ser desligados tooResource Manager modo.</span><span class="sxs-lookup"><span data-stu-id="73879-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="73879-181">Antes de usar o serviço de DNS do Azure hello, você deve registrar o provedor de recursos assinatura toouse Olá Network.</span><span class="sxs-lookup"><span data-stu-id="73879-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="73879-182">(Essa operação deve ser executa apenas uma vez para cada assinatura.)</span><span class="sxs-lookup"><span data-stu-id="73879-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="73879-183">Se você não tiver um já, você também precisará toocreate um grupo de recursos do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="73879-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="73879-184">zona de saudação tooimport **contoso.com** do arquivo hello **contoso.com.txt** em uma nova zona DNS no grupo de recursos de saudação **myresourcegroup**, execute o comando de saudação `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="73879-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="73879-185">Esse comando carrega o arquivo de zona hello e analisá-lo.</span><span class="sxs-lookup"><span data-stu-id="73879-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="73879-186">comando Olá executa uma série de comandos na zona de Olá Olá DNS do Azure serviço toocreate e conjuntos de todos os registros de saudação na zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="73879-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="73879-187">comando Olá relata o progresso na janela de console hello, juntamente com quaisquer erros ou avisos.</span><span class="sxs-lookup"><span data-stu-id="73879-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="73879-188">Como conjuntos de registros são criados em série, pode levar alguns tooimport de minutos um arquivo grande.</span><span class="sxs-lookup"><span data-stu-id="73879-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="73879-189">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="73879-189">Step 2.</span></span> <span data-ttu-id="73879-190">Verifique se a zona de saudação</span><span class="sxs-lookup"><span data-stu-id="73879-190">Verify hello zone</span></span>

<span data-ttu-id="73879-191">tooverify Olá zona DNS depois de importar o arquivo hello, você pode usar qualquer um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="73879-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="73879-192">Você pode listar os registros de saudação usando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="73879-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="73879-193">Você pode listar os registros de saudação usando o cmdlet do PowerShell Olá `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="73879-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="73879-194">Você pode usar `nslookup` tooverify a resolução de nomes para os registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="73879-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="73879-195">Como a zona de saudação não é delegada ainda, é necessário servidores de nome de DNS do Azure corretos do toospecify Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="73879-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="73879-196">Olá exemplo a seguir mostra como os nomes de servidor de nome tooretrieve Olá atribuídos toohello zona.</span><span class="sxs-lookup"><span data-stu-id="73879-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="73879-197">IT também mostra como registrar o tooquery hello "www" usando `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="73879-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="73879-198">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="73879-198">Step 3.</span></span> <span data-ttu-id="73879-199">Atualizar a delegação DNS</span><span class="sxs-lookup"><span data-stu-id="73879-199">Update DNS delegation</span></span>

<span data-ttu-id="73879-200">Depois de ter verificado que zona Olá foi importada corretamente, é necessário tooupdate Olá DNS delegação toopoint toohello Azure servidores de nome DNS.</span><span class="sxs-lookup"><span data-stu-id="73879-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="73879-201">Para obter mais informações, consulte o artigo Olá [atualizar delegação de DNS Olá](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="73879-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="73879-202">Como exportar um arquivo de zona DNS do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="73879-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="73879-203">formato Olá Olá CLI do Azure comando tooimport uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="73879-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="73879-204">Valores:</span><span class="sxs-lookup"><span data-stu-id="73879-204">Values:</span></span>

* <span data-ttu-id="73879-205">`<resource group>`é o nome de Olá Olá do grupo de recursos para a zona de saudação no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="73879-206">`<zone name>`é o nome de saudação da zona de saudação.</span><span class="sxs-lookup"><span data-stu-id="73879-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="73879-207">`<zone file name>`é Olá caminho/nome do toobe de arquivo de zona hello exportada.</span><span class="sxs-lookup"><span data-stu-id="73879-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="73879-208">Como com a importação de zona hello, primeiro é necessário toosign em, escolha sua assinatura e configurar o modo de Gerenciador de recursos de toouse Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="73879-209">tooexport um arquivo de zona</span><span class="sxs-lookup"><span data-stu-id="73879-209">tooexport a zone file</span></span>

1. <span data-ttu-id="73879-210">Entre no tooyour assinatura do Azure usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="73879-211">Selecione a assinatura Olá onde você deseja toocreate a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="73879-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="73879-212">O Azure DNS é um serviço somente do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="73879-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="73879-213">Olá CLI do Azure deve ser desligados tooResource Manager modo.</span><span class="sxs-lookup"><span data-stu-id="73879-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="73879-214">tooexport Olá zona DNS do Azure existente **contoso.com** no grupo de recursos **myresourcegroup** toohello arquivo **contoso.com.txt** (na Olá atual pasta), execute `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="73879-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="73879-215">Esse comando chamadas Olá tooenumerate de serviço DNS do Azure conjuntos de registro na zona hello e exportar o arquivo de zona do hello resultados tooa compatível com o BIND.</span><span class="sxs-lookup"><span data-stu-id="73879-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
