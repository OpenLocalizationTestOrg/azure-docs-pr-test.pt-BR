---
title: Selecionar imagens da VM Linux com a CLI do Azure | Microsoft Docs
description: "Saiba como usar a CLI do Azure para determinar o editor, oferta, SKU e versão de imagens de VM do Marketplace."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="331ad-103">Como localizar imagens de VMs Linux no Azure Marketplace com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="331ad-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="331ad-104">Este tópico descreve como usar a CLI do Azure 2.0 para localizar imagens de VM no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="331ad-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="331ad-105">Use essas informações para especificar uma imagem do Marketplace quando você criar uma VM Linux.</span><span class="sxs-lookup"><span data-stu-id="331ad-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="331ad-106">Verifique se você instalou a [CLI do Azure 2.0](/cli/azure/install-az-cli2) mais recente e conectou-se a uma conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="331ad-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="331ad-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="331ad-107">Terminology</span></span>

<span data-ttu-id="331ad-108">As imagens do Marketplace são identificadas na CLI e em outras ferramentas do Azure de acordo com uma hierarquia:</span><span class="sxs-lookup"><span data-stu-id="331ad-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="331ad-109">**Publicador**: a organização que criou a imagem.</span><span class="sxs-lookup"><span data-stu-id="331ad-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="331ad-110">Exemplo: Canonical</span><span class="sxs-lookup"><span data-stu-id="331ad-110">Example: Canonical</span></span>
* <span data-ttu-id="331ad-111">**Oferta**: um grupo de imagens relacionadas criadas por um publicador.</span><span class="sxs-lookup"><span data-stu-id="331ad-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="331ad-112">Exemplo: servidor Ubuntu</span><span class="sxs-lookup"><span data-stu-id="331ad-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="331ad-113">**SKU**: uma instância de uma oferta, como uma versão principal de uma distribuição.</span><span class="sxs-lookup"><span data-stu-id="331ad-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="331ad-114">Exemplo: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="331ad-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="331ad-115">**Versão**: o número de versão de uma imagem de SKU.</span><span class="sxs-lookup"><span data-stu-id="331ad-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="331ad-116">Ao especificar a imagem, substitua o número de versão por "mais recente", o que seleciona a versão mais recente da distribuição.</span><span class="sxs-lookup"><span data-stu-id="331ad-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="331ad-117">Para especificar uma imagem do Marketplace, você normalmente usa o *URN* da a imagem.</span><span class="sxs-lookup"><span data-stu-id="331ad-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="331ad-118">O URN combina esses valores, separados pelo caractere de dois pontos (:): *Publicador*:*Oferta*:*Sku*:*Versão*.</span><span class="sxs-lookup"><span data-stu-id="331ad-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="331ad-119">Listar imagens populares</span><span class="sxs-lookup"><span data-stu-id="331ad-119">List popular images</span></span>

<span data-ttu-id="331ad-120">Execute o comando [az vm image list](/cli/azure/vm/image#list) sem a opção `--all` para ver uma lista de imagens de VM populares no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="331ad-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="331ad-121">Por exemplo, execute o comando a seguir para exibir uma lista armazenada em cache de imagens populares em formato de tabela:</span><span class="sxs-lookup"><span data-stu-id="331ad-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="331ad-122">A saída inclui o URN (o valor na coluna *Urn*), que você pode usar para especificar a imagem.</span><span class="sxs-lookup"><span data-stu-id="331ad-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="331ad-123">Ao criar uma VM com uma das imagens populares do Marketplace, você poderá especificar o alias do URN, como *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="331ad-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a><span data-ttu-id="331ad-124">Localizar imagens específicas</span><span class="sxs-lookup"><span data-stu-id="331ad-124">Find specific images</span></span>

<span data-ttu-id="331ad-125">Para localizar uma imagem de VM específica no mercado, use o comando `az vm image list` com a opção `--all`.</span><span class="sxs-lookup"><span data-stu-id="331ad-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="331ad-126">Essa versão do comando leva algum tempo para concluir e pode retornar uma saída longa, portanto, você geralmente filtra a lista por `--publisher` ou outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="331ad-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="331ad-127">O exemplo a seguir exibe todas as ofertas para Debian (lembre-se de que sem a opção `--all`, ele pesquisa apenas no cache local de imagens comuns):</span><span class="sxs-lookup"><span data-stu-id="331ad-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="331ad-128">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="331ad-128">Partial output:</span></span> 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

<span data-ttu-id="331ad-129">Aplique filtros semelhantes com as opções `--location`, `--publisher` e `--sku`.</span><span class="sxs-lookup"><span data-stu-id="331ad-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="331ad-130">Você pode até mesmo executar correspondências parciais em um filtro, assim como procurar por `--offer Deb` para localizar todas as imagens do Debian.</span><span class="sxs-lookup"><span data-stu-id="331ad-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="331ad-131">Se você não especificar um local específico com a opção `--location`, os valores para `westus` serão retornados por padrão.</span><span class="sxs-lookup"><span data-stu-id="331ad-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="331ad-132">(Defina um local diferente do padrão executando `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="331ad-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="331ad-133">Por exemplo, o comando a seguir lista todos os SKUs do Debian 8 em `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="331ad-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="331ad-134">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="331ad-134">Partial output:</span></span>

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-the-images"></a><span data-ttu-id="331ad-135">Navegar pelas imagens</span><span class="sxs-lookup"><span data-stu-id="331ad-135">Navigate the images</span></span> 
<span data-ttu-id="331ad-136">Outra maneira de localizar uma imagem em um local é executar os comandos [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers) e [az vm image list-skus](/cli/azure/vm/image#list-skus) em sequência.</span><span class="sxs-lookup"><span data-stu-id="331ad-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="331ad-137">Com esses comandos, você determina estes valores:</span><span class="sxs-lookup"><span data-stu-id="331ad-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="331ad-138">Liste os editores de imagem.</span><span class="sxs-lookup"><span data-stu-id="331ad-138">List the image publishers.</span></span>
2. <span data-ttu-id="331ad-139">Para um determinado editor, liste suas ofertas.</span><span class="sxs-lookup"><span data-stu-id="331ad-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="331ad-140">Para uma determinada oferta, liste seus SKUs.</span><span class="sxs-lookup"><span data-stu-id="331ad-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="331ad-141">Por exemplo, o comando a seguir lista os editores de imagem na localização Oeste dos EUA:</span><span class="sxs-lookup"><span data-stu-id="331ad-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="331ad-142">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="331ad-142">Partial output:</span></span>

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
<span data-ttu-id="331ad-143">Use essas informações para encontrar as ofertas do editor específico.</span><span class="sxs-lookup"><span data-stu-id="331ad-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="331ad-144">Por exemplo, se Canonical for um editor de imagem na localização Oeste dos EUA, localize as ofertas dele executando `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="331ad-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="331ad-145">Passe a localização e o editor como no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="331ad-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="331ad-146">Saída:</span><span class="sxs-lookup"><span data-stu-id="331ad-146">Output:</span></span>

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
<span data-ttu-id="331ad-147">Você vê que, na região Oeste dos EUA, o Canonical publica a oferta **UbuntuServer** no Azure.</span><span class="sxs-lookup"><span data-stu-id="331ad-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="331ad-148">Mas quais SKUs?</span><span class="sxs-lookup"><span data-stu-id="331ad-148">But what SKUs?</span></span> <span data-ttu-id="331ad-149">Para obter esses valores, execute `azure vm image list-skus` e defina a localização, editor e oferta que você descobriu:</span><span class="sxs-lookup"><span data-stu-id="331ad-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="331ad-150">Saída:</span><span class="sxs-lookup"><span data-stu-id="331ad-150">Output:</span></span>

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

<span data-ttu-id="331ad-151">Por fim, use o comando `az vm image list` para encontrar uma versão específica do SKU desejado, por exemplo, **16.04-LTS**:</span><span class="sxs-lookup"><span data-stu-id="331ad-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="331ad-152">Saída:</span><span class="sxs-lookup"><span data-stu-id="331ad-152">Output:</span></span>

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a><span data-ttu-id="331ad-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="331ad-153">Next steps</span></span>
<span data-ttu-id="331ad-154">Agora você pode escolher exatamente a imagem que deseja usar anotando o valor do URN.</span><span class="sxs-lookup"><span data-stu-id="331ad-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="331ad-155">Passe esse valor com o parâmetro `--image` quando criar uma VM com o comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="331ad-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="331ad-156">Lembre-se de que é possível substituir, como opção, o número de versão no URN por "mais recente".</span><span class="sxs-lookup"><span data-stu-id="331ad-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="331ad-157">Essa versão é sempre a versão mais recente da distribuição.</span><span class="sxs-lookup"><span data-stu-id="331ad-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="331ad-158">Para criar uma máquina virtual rapidamente usando as informações de URN, confira [Criar e gerenciar VMs do Linux usando a CLI do Azure](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="331ad-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
