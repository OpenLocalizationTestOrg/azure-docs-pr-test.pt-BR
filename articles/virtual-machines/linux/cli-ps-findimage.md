---
title: imagens de VM do Linux aaaSelect com hello CLI do Azure | Microsoft Docs
description: "Saiba como toouse Olá publicador de saudação toodetermine CLI do Azure, oferta, SKU e versão para imagens de VM do Marketplace."
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
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="b48d8-103">Como imagens de VM do Linux toofind em hello Azure Marketplace com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="b48d8-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="b48d8-104">Este tópico descreve como toouse Olá imagens da VM Azure CLI 2.0 toofind em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b48d8-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="b48d8-105">Quando você cria uma VM do Linux, use este toospecify informações sobre uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b48d8-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="b48d8-106">Certifique-se de que você instalou o hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e são registrados no tooan conta do Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="b48d8-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="b48d8-107">Terminologia</span><span class="sxs-lookup"><span data-stu-id="b48d8-107">Terminology</span></span>

<span data-ttu-id="b48d8-108">Imagens do Marketplace são identificadas no hello CLI e outros tooa hierarquia de acordo com as ferramentas do Azure:</span><span class="sxs-lookup"><span data-stu-id="b48d8-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="b48d8-109">**Publicador** -Olá organização que criou a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="b48d8-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="b48d8-110">Exemplo: Canonical</span><span class="sxs-lookup"><span data-stu-id="b48d8-110">Example: Canonical</span></span>
* <span data-ttu-id="b48d8-111">**Oferta**: um grupo de imagens relacionadas criadas por um publicador.</span><span class="sxs-lookup"><span data-stu-id="b48d8-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="b48d8-112">Exemplo: servidor Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b48d8-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="b48d8-113">**SKU**: uma instância de uma oferta, como uma versão principal de uma distribuição.</span><span class="sxs-lookup"><span data-stu-id="b48d8-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="b48d8-114">Exemplo: 16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="b48d8-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="b48d8-115">**Versão** -Olá número da versão de uma imagem do SKU.</span><span class="sxs-lookup"><span data-stu-id="b48d8-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="b48d8-116">Ao especificar a imagem de saudação, você pode substituir número de versão de saudação com "mais recente", que seleciona a versão mais recente de saudação da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="b48d8-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="b48d8-117">toospecify uma imagem do Marketplace, você normalmente usa imagem Olá *URN*.</span><span class="sxs-lookup"><span data-stu-id="b48d8-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="b48d8-118">Olá URN combina esses valores, separados pelo caractere de dois-pontos (:) do hello: *publicador*:*oferecem*:*Sku*:*versão*.</span><span class="sxs-lookup"><span data-stu-id="b48d8-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="b48d8-119">Listar imagens populares</span><span class="sxs-lookup"><span data-stu-id="b48d8-119">List popular images</span></span>

<span data-ttu-id="b48d8-120">Executar Olá [lista de imagens de vm az](/cli/azure/vm/image#list) comando sem Olá `--all` opção, toosee uma lista de VM popular imagens no hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b48d8-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="b48d8-121">Por exemplo, execute Olá toodisplay de comando a seguir uma lista armazenada em cache de imagens populares em formato de tabela:</span><span class="sxs-lookup"><span data-stu-id="b48d8-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="b48d8-122">saída de Hello inclui Olá URN (Olá valor Olá *Urn* coluna), que você usar toospecify Olá imagem.</span><span class="sxs-lookup"><span data-stu-id="b48d8-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="b48d8-123">Ao criar uma VM com uma dessas imagens populares do Marketplace, você poderá especificar alias URN hello, tais como *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="b48d8-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="b48d8-124">Localizar imagens específicas</span><span class="sxs-lookup"><span data-stu-id="b48d8-124">Find specific images</span></span>

<span data-ttu-id="b48d8-125">toofind uma imagem VM específica no hello Marketplace, use Olá `az vm image list` com hello `--all` opção.</span><span class="sxs-lookup"><span data-stu-id="b48d8-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="b48d8-126">Esta versão do comando Olá usa toocomplete algum tempo e pode retornar uma saída longa, para que você geralmente filtrar a lista de saudação por `--publisher` ou outro parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b48d8-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="b48d8-127">Por exemplo, a saudação comando a seguir exibe todas as ofertas Debian (Lembre-se de que sem Olá `--all` alternar, ele pesquisa somente o cache local de saudação de imagens comuns):</span><span class="sxs-lookup"><span data-stu-id="b48d8-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="b48d8-128">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="b48d8-128">Partial output:</span></span> 
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

<span data-ttu-id="b48d8-129">Aplicar filtros semelhantes com hello `--location`, `--publisher`, e `--sku` opções.</span><span class="sxs-lookup"><span data-stu-id="b48d8-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="b48d8-130">Você pode até mesmo executar correspondências parciais em um filtro, como procurando `--offer Deb` toofind todas as imagens Debian.</span><span class="sxs-lookup"><span data-stu-id="b48d8-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="b48d8-131">Se você não especificar uma localização específica com hello `--location` valores de opção, Olá para `westus` são retornados por padrão.</span><span class="sxs-lookup"><span data-stu-id="b48d8-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="b48d8-132">(Defina um local diferente do padrão executando `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="b48d8-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="b48d8-133">Por exemplo, Olá comando a seguir lista todos os SKUs 8 Debian em `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="b48d8-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="b48d8-134">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="b48d8-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="b48d8-135">Navegue imagens Olá</span><span class="sxs-lookup"><span data-stu-id="b48d8-135">Navigate hello images</span></span> 
<span data-ttu-id="b48d8-136">Outra maneira toofind uma imagem em um local é Olá toorun [editores de lista de imagem de vm de az](/cli/azure/vm/image#list-publishers), [ofertas de lista de imagem de vm de az](/cli/azure/vm/image#list-offers), e [imagem de vm az lista-skus](/cli/azure/vm/image#list-skus) comandos em sequência.</span><span class="sxs-lookup"><span data-stu-id="b48d8-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="b48d8-137">Com esses comandos, você determina estes valores:</span><span class="sxs-lookup"><span data-stu-id="b48d8-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="b48d8-138">Editores de imagem de saudação de lista.</span><span class="sxs-lookup"><span data-stu-id="b48d8-138">List hello image publishers.</span></span>
2. <span data-ttu-id="b48d8-139">Para um determinado editor, liste suas ofertas.</span><span class="sxs-lookup"><span data-stu-id="b48d8-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="b48d8-140">Para uma determinada oferta, liste seus SKUs.</span><span class="sxs-lookup"><span data-stu-id="b48d8-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="b48d8-141">Por exemplo, hello comando a seguir lista os editores de imagem Olá Olá local Oeste dos EUA:</span><span class="sxs-lookup"><span data-stu-id="b48d8-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="b48d8-142">Resultado parcial:</span><span class="sxs-lookup"><span data-stu-id="b48d8-142">Partial output:</span></span>

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
<span data-ttu-id="b48d8-143">Use que este toofind informações oferece um editor específico.</span><span class="sxs-lookup"><span data-stu-id="b48d8-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="b48d8-144">Por exemplo, se Canonical for um editor de imagem no hello local Oeste dos EUA, localizar suas ofertas executando `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="b48d8-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="b48d8-145">Passe Olá local e o publicador hello como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b48d8-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="b48d8-146">Saída:</span><span class="sxs-lookup"><span data-stu-id="b48d8-146">Output:</span></span>

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
<span data-ttu-id="b48d8-147">Você vê na região Oeste dos EUA Olá Canonical publica Olá **UbuntuServer** oferecem no Azure.</span><span class="sxs-lookup"><span data-stu-id="b48d8-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="b48d8-148">Mas qual SKUs? tooget esses valores, execute `azure vm image list-skus` e definir o local de saudação, publisher e oferta que você descobriu:</span><span class="sxs-lookup"><span data-stu-id="b48d8-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="b48d8-149">Saída:</span><span class="sxs-lookup"><span data-stu-id="b48d8-149">Output:</span></span>

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

<span data-ttu-id="b48d8-150">Por fim, use Olá `az vm image list` comando toofind uma versão específica do hello SKU desejado, por exemplo, **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="b48d8-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="b48d8-151">Saída:</span><span class="sxs-lookup"><span data-stu-id="b48d8-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="b48d8-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b48d8-152">Next steps</span></span>
<span data-ttu-id="b48d8-153">Agora você pode escolher a imagem de saudação precisamente desejar toouse levando anote Olá valor URN.</span><span class="sxs-lookup"><span data-stu-id="b48d8-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="b48d8-154">Passe esse valor com hello `--image` parâmetro quando você cria uma máquina virtual com hello [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b48d8-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="b48d8-155">Lembre-se de que você pode, opcionalmente, substituir número da versão Olá no hello URN "mais recente".</span><span class="sxs-lookup"><span data-stu-id="b48d8-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="b48d8-156">Esta versão é sempre a versão mais recente Olá da distribuição de saudação.</span><span class="sxs-lookup"><span data-stu-id="b48d8-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="b48d8-157">toocreate uma máquina virtual rapidamente usando as informações de URN hello, consulte [criar e gerenciar máquinas virtuais Linux com hello CLI do Azure](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b48d8-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
