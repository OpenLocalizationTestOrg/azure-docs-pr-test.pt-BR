---
title: "aaaTechnical pré-requisitos para criar uma imagem de máquina virtual para hello Azure Marketplace | Microsoft Docs"
description: "Entender os requisitos para criar e implantar uma imagem de máquina virtual toohello Azure Marketplace para outros Olá toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Pré-requisitos técnicos para criar uma imagem de máquina virtual para hello Azure Marketplace
Processo Olá completamente antes de começar de ler e entender por cada etapa é executada. Tanto quanto possível, você deve preparar as informações da sua empresa e outros dados, baixe as ferramentas necessárias e/ou criar componentes técnicos antes de começar o processo de criação de oferta de saudação. Esses itens devem estar claros com a leitura deste artigo.  

## <a name="download-needed-tools--applications"></a>Baixe as ferramentas e aplicativos necessários
Você deve ter Olá prontos antes de começar o processo de saudação de itens a seguir:

* Dependendo de qual sistema operacional você está visando, Olá install [cmdlets do PowerShell do Azure](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) ou [ferramenta de interface de linha de comando do Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) de saudação [Downloads do Azure](https://azure.microsoft.com/downloads/) página.
* Instale o Gerenciador do Armazenamento do Azure no CodePlex.
* Baixe e instale Olá, ferramenta de teste de certificação para o certificado do Azure:
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Precisa de uma ferramenta de certificação do computador baseado em Windows toorun hello. Se você não tiver um computador baseado em Windows disponível, você pode executar a ferramenta de saudação usando uma VM com base em Windows no Azure.

## <a name="platforms-supported"></a>Plataformas com suporte
Você pode desenvolver VMs do Azure baseadas em Windows ou Linux. Alguns elementos da saudação publicação processo--como criar um compatível com o Azure disco rígido virtual (VHD) – use diferentes ferramentas e etapas, dependendo de qual sistema operacional você está usando:  

* Se você estiver usando o Linux, consulte a seção "Criar um VHD compatível com o Azure (com base em Linux)" toohello de saudação [guia de publicação de imagem de máquina Virtual](marketplace-publishing-vm-image-creation.md).
* Se você estiver usando o Windows, consulte a seção "Criar um VHD compatível com o Azure (baseado em Windows)" toohello de saudação [guia de publicação de imagem de máquina Virtual](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Você precisará de acesso tooa baseados em Windows máquina:
> 
> * Execute a ferramenta de validação de certificação hello.
> * Crie URL de assinatura de acesso Olá VHD compartilhado para Olá envio de certificação do VHD.
> 
> 

## <a name="develop-your-vhd"></a>Desenvolver seu VHD
Você pode desenvolver VHDs do Azure na nuvem de saudação ou no local:

* Desenvolvimento baseado em nuvem significa que todas as etapas de desenvolvimento são executadas remotamente em um VHD residente no Azure.
* O desenvolvimento local requer o download de um VHD e desenvolvê-lo usando a infraestrutura local. Embora isso seja possível, não é recomendável. Observe que o desenvolvimento do Windows ou SQL local exige você toohave as chaves de licença do hello relevantes no local. Você não pode incluir ou instalar o SQL Server depois de criar uma VM. Você também deve basear sua oferta em uma imagem do SQL aprovada de saudação portal do Azure. Se você decidir toodevelop local, você deve executar algumas etapas diferente se você estivesse desenvolvendo na nuvem hello. Você pode encontrar informações relevantes em [Criar uma imagem de VM local](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
