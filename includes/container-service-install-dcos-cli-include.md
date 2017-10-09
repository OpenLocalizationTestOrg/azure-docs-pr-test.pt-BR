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
> Isso é para trabalhar com clusters ACS baseados no DC/OS. Não há nenhuma necessidade toodo isso para clusters com base por nuvem ACS.
> 
> 

Primeiro, [conecte tooyour ACS baseadas no controlador de domínio/SO cluster](../articles/container-service/container-service-connect.md). Após você ter feito isso, você pode instalar Olá CLI DC/sistema operacional do computador cliente com comandos de saudação abaixo:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Se estiver usando uma versão antiga do Python, talvez você observe algumas “InsecurePlatformWarnings”. Você pode ignorá-los com segurança.

Na tooget ordem iniciado sem reiniciar o shell, execute:

```bash
source ~/.bashrc
```

Esta etapa não será necessária quando você iniciar novos shells.

Agora você pode confirmar que Olá que CLI está instalado:

```bash
dcos --help
```