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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Como imagens de VM do Linux toofind em hello Azure Marketplace com hello CLI do Azure
Este tópico descreve como toouse Olá imagens da VM Azure CLI 2.0 toofind em hello Azure Marketplace. Quando você cria uma VM do Linux, use este toospecify informações sobre uma imagem do Marketplace.

Certifique-se de que você instalou o hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e são registrados no tooan conta do Azure (`az login`).

## <a name="terminology"></a>Terminologia

Imagens do Marketplace são identificadas no hello CLI e outros tooa hierarquia de acordo com as ferramentas do Azure:

* **Publicador** -Olá organização que criou a imagem de saudação. Exemplo: Canonical
* **Oferta**: um grupo de imagens relacionadas criadas por um publicador. Exemplo: servidor Ubuntu
* **SKU**: uma instância de uma oferta, como uma versão principal de uma distribuição. Exemplo: 16.04-LTS
* **Versão** -Olá número da versão de uma imagem do SKU. Ao especificar a imagem de saudação, você pode substituir número de versão de saudação com "mais recente", que seleciona a versão mais recente de saudação da distribuição de saudação.

toospecify uma imagem do Marketplace, você normalmente usa imagem Olá *URN*. Olá URN combina esses valores, separados pelo caractere de dois-pontos (:) do hello: *publicador*:*oferecem*:*Sku*:*versão*. 


## <a name="list-popular-images"></a>Listar imagens populares

Executar Olá [lista de imagens de vm az](/cli/azure/vm/image#list) comando sem Olá `--all` opção, toosee uma lista de VM popular imagens no hello Azure Marketplace. Por exemplo, execute Olá toodisplay de comando a seguir uma lista armazenada em cache de imagens populares em formato de tabela:

```azurecli
az vm image list --output table
```

saída de Hello inclui Olá URN (Olá valor Olá *Urn* coluna), que você usar toospecify Olá imagem. Ao criar uma VM com uma dessas imagens populares do Marketplace, você poderá especificar alias URN hello, tais como *UbuntuLTS*.

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

## <a name="find-specific-images"></a>Localizar imagens específicas

toofind uma imagem VM específica no hello Marketplace, use Olá `az vm image list` com hello `--all` opção. Esta versão do comando Olá usa toocomplete algum tempo e pode retornar uma saída longa, para que você geralmente filtrar a lista de saudação por `--publisher` ou outro parâmetro. 

Por exemplo, a saudação comando a seguir exibe todas as ofertas Debian (Lembre-se de que sem Olá `--all` alternar, ele pesquisa somente o cache local de saudação de imagens comuns):

```azurecli
az vm image list --offer Debian --all --output table 

```

Resultado parcial: 
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

Aplicar filtros semelhantes com hello `--location`, `--publisher`, e `--sku` opções. Você pode até mesmo executar correspondências parciais em um filtro, como procurando `--offer Deb` toofind todas as imagens Debian.

Se você não especificar uma localização específica com hello `--location` valores de opção, Olá para `westus` são retornados por padrão. (Defina um local diferente do padrão executando `az configure --defaults location=<location>`.)

Por exemplo, Olá comando a seguir lista todos os SKUs 8 Debian em `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Resultado parcial:

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

## <a name="navigate-hello-images"></a>Navegue imagens Olá 
Outra maneira toofind uma imagem em um local é Olá toorun [editores de lista de imagem de vm de az](/cli/azure/vm/image#list-publishers), [ofertas de lista de imagem de vm de az](/cli/azure/vm/image#list-offers), e [imagem de vm az lista-skus](/cli/azure/vm/image#list-skus) comandos em sequência. Com esses comandos, você determina estes valores:

1. Editores de imagem de saudação de lista.
2. Para um determinado editor, liste suas ofertas.
3. Para uma determinada oferta, liste seus SKUs.


Por exemplo, hello comando a seguir lista os editores de imagem Olá Olá local Oeste dos EUA:

```azurecli
az vm image list-publishers --location westus --output table
```

Resultado parcial:

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
Use que este toofind informações oferece um editor específico. Por exemplo, se Canonical for um editor de imagem no hello local Oeste dos EUA, localizar suas ofertas executando `azure vm image list-offers`. Passe Olá local e o publicador hello como Olá exemplo a seguir:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Saída:

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
Você vê na região Oeste dos EUA Olá Canonical publica Olá **UbuntuServer** oferecem no Azure. Mas qual SKUs? tooget esses valores, execute `azure vm image list-skus` e definir o local de saudação, publisher e oferta que você descobriu:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Saída:

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

Por fim, use Olá `az vm image list` comando toofind uma versão específica do hello SKU desejado, por exemplo, **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Saída:

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
## <a name="next-steps"></a>Próximas etapas
Agora você pode escolher a imagem de saudação precisamente desejar toouse levando anote Olá valor URN. Passe esse valor com hello `--image` parâmetro quando você cria uma máquina virtual com hello [criar vm az](/cli/azure/vm#create) comando. Lembre-se de que você pode, opcionalmente, substituir número da versão Olá no hello URN "mais recente". Esta versão é sempre a versão mais recente Olá da distribuição de saudação. toocreate uma máquina virtual rapidamente usando as informações de URN hello, consulte [criar e gerenciar máquinas virtuais Linux com hello CLI do Azure](tutorial-manage-vm.md).
