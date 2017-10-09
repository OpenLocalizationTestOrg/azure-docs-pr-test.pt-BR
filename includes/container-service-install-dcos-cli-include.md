---
title: "Olá aaaInstall CLI DC/sistema operacional | Microsoft Docs"
description: "Instale Olá CLI DC/OS."
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
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="8d65d-104">Isso é para trabalhar com clusters ACS baseados no DC/OS.</span><span class="sxs-lookup"><span data-stu-id="8d65d-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="8d65d-105">Não há nenhuma necessidade toodo isso para clusters com base por nuvem ACS.</span><span class="sxs-lookup"><span data-stu-id="8d65d-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="8d65d-106">Primeiro, [conecte tooyour ACS baseadas no controlador de domínio/SO cluster](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8d65d-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="8d65d-107">Após você ter feito isso, você pode instalar Olá CLI DC/sistema operacional do computador cliente com comandos de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="8d65d-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="8d65d-108">Se estiver usando uma versão antiga do Python, talvez você observe algumas “InsecurePlatformWarnings”.</span><span class="sxs-lookup"><span data-stu-id="8d65d-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="8d65d-109">Você pode ignorá-los com segurança.</span><span class="sxs-lookup"><span data-stu-id="8d65d-109">You can safely ignore these.</span></span>

<span data-ttu-id="8d65d-110">Na tooget ordem iniciado sem reiniciar o shell, execute:</span><span class="sxs-lookup"><span data-stu-id="8d65d-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="8d65d-111">Esta etapa não será necessária quando você iniciar novos shells.</span><span class="sxs-lookup"><span data-stu-id="8d65d-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="8d65d-112">Agora você pode confirmar que Olá que CLI está instalado:</span><span class="sxs-lookup"><span data-stu-id="8d65d-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```