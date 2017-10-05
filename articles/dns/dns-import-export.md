---
title: "Importar e exportar um arquivo de zona de domínio para o DNS do Azure usando a CLI 1.0 do Azure | Microsoft Docs"
description: Saiba como importar e exportar um arquivo de zona DNS para o DNS do Azure usando a CLI do Azure 1.0
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
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="95356-103">Importar e exportar um arquivo da zona DNS usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="95356-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="95356-104">Este artigo explica como importar e exportar arquivos da zona DNS para o DNS do Azure usando a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="95356-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="95356-105">Introdução à migração de zona DNS</span><span class="sxs-lookup"><span data-stu-id="95356-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="95356-106">Um arquivo de zona DNS é um arquivo de texto que contém detalhes de cada registro DNS (Sistema de Nomes de Domínio ) na zona.</span><span class="sxs-lookup"><span data-stu-id="95356-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="95356-107">Ele segue um formato padrão, tornando-o adequado para transferir registros DNS entre sistemas DNS.</span><span class="sxs-lookup"><span data-stu-id="95356-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="95356-108">O uso de um arquivo de zona é uma maneira rápida, confiável e conveniente de transferir uma zona DNS para dentro ou fora do DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="95356-109">O DNS do Azure oferece suporte à importação e exportação de arquivos de zona usando a interface de linha de comando (CLI) do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="95356-110">Atualmente, **não** há suporte para a importação do arquivo de zona por meio do Azure PowerShell ou do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="95356-111">A CLI do Azure 1.0 é uma ferramenta de linha de comando de plataforma cruzada empregada para gerenciar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="95356-112">Ela está disponível para as plataformas Windows, Mac e Linux por meio da [página de downloads do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="95356-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="95356-113">O a plataforma cruzada é importante para importar e exportar arquivos de zona, pois o software para servidores de nomes mais comum, o [BIND](https://www.isc.org/downloads/bind/), normalmente é executado no Linux.</span><span class="sxs-lookup"><span data-stu-id="95356-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="95356-114">Atualmente, há duas versões da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="95356-115">A CLI1.0 é baseada em Node.js e tem comandos que começam com “azure”.</span><span class="sxs-lookup"><span data-stu-id="95356-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="95356-116">A CLI2.0 é baseada em Python e tem comandos que começam com “az”.</span><span class="sxs-lookup"><span data-stu-id="95356-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="95356-117">Embora ambas as versões deem suporte à importação do arquivo de zona, é recomendável usar os comandos da CLI1.0, conforme descrito nesta página.</span><span class="sxs-lookup"><span data-stu-id="95356-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="95356-118">Obtenha seu arquivo de zona DNS existente</span><span class="sxs-lookup"><span data-stu-id="95356-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="95356-119">Antes de importar um arquivo de zona DNS para o DNS do Azure, você precisa obter uma cópia do arquivo de zona.</span><span class="sxs-lookup"><span data-stu-id="95356-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="95356-120">A origem do arquivo depende do local em que a zona DNS está hospedada no momento.</span><span class="sxs-lookup"><span data-stu-id="95356-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="95356-121">Se a zona DNS for hospedada por um serviço de parceiro (como um registrador de domínio, um provedor de host DNS dedicado ou um provedor de nuvem alternativo), esse serviço deverá fornecer a capacidade de baixar o arquivo de zona DNS.</span><span class="sxs-lookup"><span data-stu-id="95356-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="95356-122">Se a zona DNS estiver hospedada no DNS do Windows, a pasta padrão para os arquivos de zona será **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="95356-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="95356-123">O caminho completo de cada arquivo de zona também é mostrado na guia **Geral** do console de DNS.</span><span class="sxs-lookup"><span data-stu-id="95356-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="95356-124">Se a zona DNS for hospedada usando o BIND, o local do arquivo de zona para cada zona será especificado no arquivo de configuração do BIND, **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="95356-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="95356-125">Arquivos de zona baixados do GoDaddy têm um formato ligeiramente diferente do padrão.</span><span class="sxs-lookup"><span data-stu-id="95356-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="95356-126">Você precisa corrigir o problema antes de importar esses arquivos de zona DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="95356-127">Nomes DNS no RDATA de cada registro DNS são especificados como nomes totalmente qualificados, mas não têm uma terminação “.” Isso significa que eles são interpretados por outros sistemas DNS como nomes relativos.</span><span class="sxs-lookup"><span data-stu-id="95356-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="95356-128">Você precisa editar o arquivo de zona para acrescentar o '.' de terminação aos nomes antes de importá-los para o DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="95356-129">Por exemplo, o registro CNAME record “www 3600 IN CNAME contoso.com” deve ser alterado para “www 3600 IN CNAME contoso.com.”</span><span class="sxs-lookup"><span data-stu-id="95356-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="95356-130">(com uma terminação “.”).</span><span class="sxs-lookup"><span data-stu-id="95356-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="95356-131">Importar um arquivo de zona DNS para o DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="95356-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="95356-132">A importação de um arquivo de zona criará uma nova zona no DNS do Azure, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="95356-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="95356-133">Se a zona já existir, os conjuntos de registros no arquivo de zona deverão ser mesclados a conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="95356-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="95356-134">Comportamento de mesclagem</span><span class="sxs-lookup"><span data-stu-id="95356-134">Merge behavior</span></span>

* <span data-ttu-id="95356-135">Por padrão, os conjuntos de registros novos e existentes são mesclados.</span><span class="sxs-lookup"><span data-stu-id="95356-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="95356-136">Registros idênticos em um conjunto de registros mesclados têm a duplicação eliminada.</span><span class="sxs-lookup"><span data-stu-id="95356-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="95356-137">Como alternativa, ao especificar a opção `--force`, o processo de importação substitui os conjuntos de registros existentes por novos conjuntos de registros.</span><span class="sxs-lookup"><span data-stu-id="95356-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="95356-138">Os conjuntos de registros existentes que não tiverem um conjunto de registros correspondente no arquivo de zona importado não serão removidos.</span><span class="sxs-lookup"><span data-stu-id="95356-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="95356-139">Quando os conjuntos de registros são mesclados, é usado o TTL dos conjuntos de registros já existentes.</span><span class="sxs-lookup"><span data-stu-id="95356-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="95356-140">Quando `--force` é usado, o TTL do novo conjunto de registros é usado.</span><span class="sxs-lookup"><span data-stu-id="95356-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="95356-141">Parâmetros SOA (Início de Autoridade) (exceto `host`) sempre são obtidos do arquivo de zona importado, independentemente do uso de `--force`.</span><span class="sxs-lookup"><span data-stu-id="95356-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="95356-142">Da mesma forma, para o conjunto do registro de nome do servidor no ápice da zona, o TTL sempre é obtido do arquivo de zona importado.</span><span class="sxs-lookup"><span data-stu-id="95356-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="95356-143">Um registro CNAME importado não substituirá um registro CNAME existente com o mesmo nome, a menos que o parâmetro `--force` seja especificado.</span><span class="sxs-lookup"><span data-stu-id="95356-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="95356-144">Quando ocorre um conflito entre um registro CNAME e outro registro com o mesmo nome, mas com tipo diferente (independentemente de qual deles é existente ou novo), o registro existente é mantido.</span><span class="sxs-lookup"><span data-stu-id="95356-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="95356-145">Isso é independente do uso de `--force`.</span><span class="sxs-lookup"><span data-stu-id="95356-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="95356-146">Informações adicionais sobre importação</span><span class="sxs-lookup"><span data-stu-id="95356-146">Additional information about importing</span></span>

<span data-ttu-id="95356-147">As observações a seguir fornecem detalhes técnicos adicionais sobre o processo de importação de zona.</span><span class="sxs-lookup"><span data-stu-id="95356-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="95356-148">A diretiva `$TTL` é opcional e tem suporte.</span><span class="sxs-lookup"><span data-stu-id="95356-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="95356-149">Quando nenhuma diretiva `$TTL` for especificada, registros sem um TTL explícito são importados definidos com um TTL padrão de 3600 segundos.</span><span class="sxs-lookup"><span data-stu-id="95356-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="95356-150">Quando dois registros no mesmo conjunto de registros especificarem TTLs diferentes, o menor valor será usado.</span><span class="sxs-lookup"><span data-stu-id="95356-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="95356-151">A diretiva `$ORIGIN` é opcional e tem suporte.</span><span class="sxs-lookup"><span data-stu-id="95356-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="95356-152">Quando nenhuma `$ORIGIN` for definida, o valor padrão usado será o nome da zona, conforme especificado na linha de comando (além do "." de terminação).</span><span class="sxs-lookup"><span data-stu-id="95356-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="95356-153">As diretivas `$INCLUDE` e `$GENERATE` não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="95356-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="95356-154">Há suporte aos seguintes tipos de registros: A, AAAA, CNAME, MX, NS, SOA, SRV e TXT.</span><span class="sxs-lookup"><span data-stu-id="95356-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="95356-155">O registro SOA é criado automaticamente pelo DNS do Azure quando uma zona é criada.</span><span class="sxs-lookup"><span data-stu-id="95356-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="95356-156">Quando você importa um arquivo de zona, todos os parâmetros SOA são extraídos do arquivo de zona, *exceto* o parâmetro `host`.</span><span class="sxs-lookup"><span data-stu-id="95356-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="95356-157">Esse parâmetro usa o valor fornecido pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="95356-158">Isso ocorre porque esse parâmetro deve referir-se ao servidor de nomes primário fornecido pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="95356-159">O registro de nome do servidor definido no ápice da zona também é criado automaticamente pelo DNS do Azure quando a zona é criada.</span><span class="sxs-lookup"><span data-stu-id="95356-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="95356-160">Apenas o TTL desse conjunto de registros é importado.</span><span class="sxs-lookup"><span data-stu-id="95356-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="95356-161">Esses registros contêm os nomes de servidor de nome fornecidos pelo DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="95356-162">Os dados de registro não são substituídos pelos valores contidos no arquivo de zona importado.</span><span class="sxs-lookup"><span data-stu-id="95356-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="95356-163">Durante a visualização pública, o DNS do Azure suporta apenas os registros TXT de cadeia de caracteres única.</span><span class="sxs-lookup"><span data-stu-id="95356-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="95356-164">Registros TXT de cadeia de caracteres múltiplas são concatenados e truncados para 255 caracteres.</span><span class="sxs-lookup"><span data-stu-id="95356-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="95356-165">Valores e formato da CLI</span><span class="sxs-lookup"><span data-stu-id="95356-165">CLI format and values</span></span>

<span data-ttu-id="95356-166">O formato do comando da CLI do Azure para importar uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="95356-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="95356-167">Valores:</span><span class="sxs-lookup"><span data-stu-id="95356-167">Values:</span></span>

* <span data-ttu-id="95356-168">`<resource group>` é o nome do grupo de recursos para a zona no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="95356-169">`<zone name>` é o nome da zona.</span><span class="sxs-lookup"><span data-stu-id="95356-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="95356-170">`<zone file name>` é o caminho/nome do arquivo de zona a ser importado.</span><span class="sxs-lookup"><span data-stu-id="95356-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="95356-171">Se uma zona com esse nome não existir no grupo de recursos, ela será criada para você.</span><span class="sxs-lookup"><span data-stu-id="95356-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="95356-172">Se a zona já existir, os conjuntos de registros importados serão mesclados aos conjuntos de registros existentes.</span><span class="sxs-lookup"><span data-stu-id="95356-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="95356-173">Para substituir os conjuntos de registros existentes, use a opção `--force` .</span><span class="sxs-lookup"><span data-stu-id="95356-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="95356-174">Para verificar o formato de um arquivo de zona sem realmente importá-lo, use a opção `--parse-only` .</span><span class="sxs-lookup"><span data-stu-id="95356-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="95356-175">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="95356-175">Step 1.</span></span> <span data-ttu-id="95356-176">Importar um arquivo de zona</span><span class="sxs-lookup"><span data-stu-id="95356-176">Import a zone file</span></span>

<span data-ttu-id="95356-177">Para importar um arquivo de zona para a zona **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="95356-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="95356-178">Entre em sua assinatura do Azure usando a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="95356-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="95356-179">Selecione a assinatura em que você deseja criar a nova zona DNS.</span><span class="sxs-lookup"><span data-stu-id="95356-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="95356-180">O DNS do Azure é um serviço somente do Gerenciador de Recursos do Azure. A CLI do Azure deve ser alternada para o modo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="95356-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="95356-181">Antes de usar o serviço DNS do Azure, você deve registrar sua assinatura para usar o provedor de recursos Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="95356-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="95356-182">(Essa operação deve ser executa apenas uma vez para cada assinatura.)</span><span class="sxs-lookup"><span data-stu-id="95356-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="95356-183">Se ainda não o tiver, você também precisará criar um grupo de recursos do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="95356-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="95356-184">Para importar a zona **contoso.com** do arquivo **contoso.com.txt** para uma nova zona DNS no grupo de recursos **myresourcegroup**, execute o comando `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="95356-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="95356-185">Esse comando carrega o arquivo de zona e analisa-o.</span><span class="sxs-lookup"><span data-stu-id="95356-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="95356-186">O comando executa uma série de comandos no serviço DNS do Azure para criar a zona e todos os conjuntos de registro na zona.</span><span class="sxs-lookup"><span data-stu-id="95356-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="95356-187">O comando relata o progresso na janela do console, bem como erros ou avisos.</span><span class="sxs-lookup"><span data-stu-id="95356-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="95356-188">Como os conjuntos de registros são criados em série, pode levar alguns minutos para importar um arquivo de zona grande.</span><span class="sxs-lookup"><span data-stu-id="95356-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="95356-189">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="95356-189">Step 2.</span></span> <span data-ttu-id="95356-190">Verificar a zona</span><span class="sxs-lookup"><span data-stu-id="95356-190">Verify the zone</span></span>

<span data-ttu-id="95356-191">Para verificar a zona DNS após importar o arquivo, você pode usar qualquer um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="95356-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="95356-192">Você pode listar os registros usando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="95356-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="95356-193">Você pode listar os registros usando o cmdlet do PowerShell `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="95356-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="95356-194">Você pode usar `nslookup` para verificar a resolução de nomes para os registros.</span><span class="sxs-lookup"><span data-stu-id="95356-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="95356-195">Como a zona ainda não foi delegada, você precisará especificar os servidores de nomes DNS do Azure corretos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="95356-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="95356-196">O exemplo a seguir mostra como recuperar os nomes do servidor de nomes atribuídos à zona.</span><span class="sxs-lookup"><span data-stu-id="95356-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="95356-197">Também mostra como consultar o registro "www" usando `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="95356-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="95356-198">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="95356-198">Step 3.</span></span> <span data-ttu-id="95356-199">Atualizar a delegação DNS</span><span class="sxs-lookup"><span data-stu-id="95356-199">Update DNS delegation</span></span>

<span data-ttu-id="95356-200">Após verificar se a zona foi importada corretamente, você precisará atualizar a delegação DNS para apontar para os servidores de nomes DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="95356-201">Para saber mais, confira o artigo [Atualizar a delegação DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="95356-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="95356-202">Como exportar um arquivo de zona DNS do DNS do Azure</span><span class="sxs-lookup"><span data-stu-id="95356-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="95356-203">O formato do comando da CLI do Azure para importar uma zona DNS é:</span><span class="sxs-lookup"><span data-stu-id="95356-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="95356-204">Valores:</span><span class="sxs-lookup"><span data-stu-id="95356-204">Values:</span></span>

* <span data-ttu-id="95356-205">`<resource group>` é o nome do grupo de recursos para a zona no DNS do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="95356-206">`<zone name>` é o nome da zona.</span><span class="sxs-lookup"><span data-stu-id="95356-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="95356-207">`<zone file name>` é o caminho/nome do arquivo de zona a ser exportado.</span><span class="sxs-lookup"><span data-stu-id="95356-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="95356-208">Como acontece com a importação de zona, você primeiro precisa fazer logon, escolher sua assinatura e configurar a CLI do Azure para usar o modo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="95356-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="95356-209">Para exportar um arquivo de zona</span><span class="sxs-lookup"><span data-stu-id="95356-209">To export a zone file</span></span>

1. <span data-ttu-id="95356-210">Entre em sua assinatura do Azure usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="95356-211">Selecione a assinatura em que você deseja criar a zona DNS.</span><span class="sxs-lookup"><span data-stu-id="95356-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="95356-212">O Azure DNS é um serviço somente do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="95356-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="95356-213">A CLI do Azure deve ser alternada para o modo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="95356-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="95356-214">Para exportar a zona DNS do Azure **contoso.com** existente no grupo de recursos **myresourcegroup** para o arquivo **contoso.com.txt** (na pasta atual), execute `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="95356-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="95356-215">Esse comando chama o serviço DNS do Azure para enumerar os conjuntos de registros na zona e exporta os resultados para um arquivo de zona compatível com BIND.</span><span class="sxs-lookup"><span data-stu-id="95356-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
