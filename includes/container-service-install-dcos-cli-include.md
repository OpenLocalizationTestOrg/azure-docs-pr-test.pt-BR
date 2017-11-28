---
title: Instalar a CLI do DC/OS | Microsoft Docs
description: Instale a CLI do DC/OS.
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Microsserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="fd94b-104">Isso é para trabalhar com clusters ACS baseados no DC/OS.</span><span class="sxs-lookup"><span data-stu-id="fd94b-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="fd94b-105">Não é necessário fazer isso para clusters ACS baseados no Swarm.</span><span class="sxs-lookup"><span data-stu-id="fd94b-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="fd94b-106">Primeiro, [conectar-se ao cluster ACS baseado no DC/OS](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="fd94b-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="fd94b-107">Depois de fazer isso, você poderá instalar a CLI do DC/OS em seu computador cliente com os comandos abaixo:</span><span class="sxs-lookup"><span data-stu-id="fd94b-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="fd94b-108">Se estiver usando uma versão antiga do Python, talvez você observe algumas “InsecurePlatformWarnings”.</span><span class="sxs-lookup"><span data-stu-id="fd94b-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="fd94b-109">Você pode ignorá-los com segurança.</span><span class="sxs-lookup"><span data-stu-id="fd94b-109">You can safely ignore these.</span></span>

<span data-ttu-id="fd94b-110">Para começar a usar sem reiniciar o shell, execute:</span><span class="sxs-lookup"><span data-stu-id="fd94b-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="fd94b-111">Esta etapa não será necessária quando você iniciar novos shells.</span><span class="sxs-lookup"><span data-stu-id="fd94b-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="fd94b-112">Agora você pode confirmar se a CLI está instalada:</span><span class="sxs-lookup"><span data-stu-id="fd94b-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```