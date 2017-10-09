---
title: "Configurar o ambiente de origem da saudação (tooAzure servidores físicos) | Microsoft Docs"
description: "Este artigo descreve como tooset o seu toostart do ambiente local replicando servidores físicos executando o Windows ou Linux no Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Configurar o ambiente de origem da saudação (servidor físico tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure físico](./site-recovery-set-up-physical-to-azure.md)

Este artigo descreve como tooset o seu toostart do ambiente local replicando servidores físicos executando o Windows ou Linux no Azure.

## <a name="prerequisites"></a>Pré-requisitos

artigo de saudação pressupõe que você já tem:
1. Um cofre de serviços de recuperação no hello [portal do Azure](http://portal.azure.com "portal do Azure").
3. Um computador físico no qual servidor de configuração de saudação tooinstall.

### <a name="configuration-server-minimum-requirements"></a>Requisitos mínimos do servidor de configuração
Olá a tabela a seguir lista o hardware mínimo hello, software e requisitos de rede para um servidor de configuração.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Servidores proxy baseado em HTTPS não são suportados pelo servidor de configuração de saudação.

## <a name="choose-your-protection-goals"></a>Escolher as metas de proteção

1. No portal do Azure de Olá, vá toohello **dos serviços de recuperação** cofres de folha e selecione seu cofre.
2. Em Olá **recurso** menu do cofre hello, clique em **Introdução** > **recuperação de Site** > **etapa 1: preparar Infraestrutura** > **objetivo de proteção**.

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. Em **objetivo de proteção**, selecione **tooAzure** e **não virtualizados/outros**e, em seguida, clique em **Okey**.

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

1. Em **preparar fonte**, se você não tiver um servidor de configuração, clique em **+ servidor de configuração** tooadd um.

  ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. Em Olá **Adicionar servidor** folha, verifique se **servidor de configuração** aparece na **tipo de servidor**.
4. Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.
5. Baixe a chave de registro de cofre hello. Você precisa chave de registro de hello quando você executa a instalação unificado. chave de saudação é válida por cinco dias depois que ele é gerado.

    ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. No computador de saudação estiver usando como o servidor de configuração hello, execute **instalação unificado do Azure Site Recovery** mestre de Olá, servidor de processo Olá e servidor de configuração de saudação tooinstall o servidor de destino.

#### <a name="run-azure-site-recovery-unified-setup"></a>Executar a Configuração Unificada do Azure Site Recovery

> [!TIP]
> Registro do servidor de configuração falhará se o tempo de saudação no relógio do sistema do computador é mais de cinco minutos da hora local. Sincronizar o relógio do sistema com uma [tempo server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de saudação.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> servidor de configuração de saudação pode ser instalado por meio de uma linha de comando. Para obter mais informações, confira [Instalando o servidor de configuração usando ferramentas de linhas de comando](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Problemas comuns

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Próximas etapas

A próxima etapa envolve a [configuração do ambiente de destino](./site-recovery-prepare-target-physical-to-azure.md) no Azure.
