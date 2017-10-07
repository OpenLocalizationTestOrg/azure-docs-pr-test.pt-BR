---
title: "aaaBack o portal clássico do DPM cargas de trabalho tooAzure | Microsoft Docs"
description: "Toobacking uma introdução a servidores DPM usando o serviço de Backup do Azure Olá"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
keywords: "Gerenciador de proteção de dados do System Center, gerenciador de proteção de dados, backup do dpm"
ms.assetid: 8f23972b-d167-4231-b331-e198db3b18b4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;giridham;markgal
ms.openlocfilehash: f408957db69d45f745d5e89bd97030a341405b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparando tooback backup tooAzure de cargas de trabalho com o DPM
> [!div class="op_single_selector"]
> * [Servidor de Backup do Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Servidor de Backup do Azure (clássico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clássico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artigo fornece uma tooprotect de Backup do Microsoft Azure Introdução toousing suas cargas de trabalho e servidores do System Center Data Protection Manager (DPM). Lendo-o, você entenderá:

* Como funciona o backup do servidor DPM do Azure
* Olá pré-requisitos tooachieve uma experiência positiva de backup
* Olá erros comuns e como toodeal com eles
* Cenários com suporte

O System Center DPM faz backup dos dados de arquivos e aplicativos. Dados de backup tooDPM podem ser armazenados em fita, disco ou backup tooAzure com o Microsoft Azure Backup. O DPM interage com o Backup do Azure da seguinte maneira:

* **DPM implantado como uma máquina de virtual do servidor ou local física** — se o DPM é implantado como um servidor físico ou como uma máquina virtual de Hyper-V de local você pode fazer backup de dados tooan Backup do Azure além de cofre toodisk e backup em fita.
* **DPM implantado como máquina virtual do Azure** — No System Center 2012 R2 com atualização 3, o DPM pode ser implantado como máquina virtual do Azure. Se o DPM é implantado como uma máquina virtual do Azure, que você pode fazer backup de discos de dados de tooAzure anexado máquina de virtual do Azure do DPM toohello ou você pode descarregar o armazenamento de dados Olá fazendo backup tooan Cofre de Backup do Azure.

## <a name="why-backup-your-dpm-servers"></a>Por que fazer backup de seus servidores DPM?
benefícios de negócios de saudação do usando o Backup do Azure para fazer backup de servidores DPM incluem:

* Para implantação do DPM local, você pode usar o backup do Azure como um tootape de implantação alternativo toolong-termo.
* Para implantações do DPM no Azure, o Backup do Azure permite armazenamento toooffload de saudação do disco do Azure, que você tooscale backup armazenando dados mais antigos no Backup do Azure e novos dados no disco.

## <a name="how-does-dpm-server-backup-work"></a>Como funciona o backup do servidor DPM?
tooback uma máquina virtual, primeiro é necessário um instantâneo point-in-time de dados de saudação. Hello Azure Backup service inicia Olá trabalho de backup em hello agendado e gatilhos Olá extensão backup tootake um instantâneo. Olá coordenadas de extensão de backup com hello VSS no convidado tooachieve consistência de serviço e invoca a API de instantâneo de blob de saudação de saudação serviço de armazenamento do Azure depois de consistência foi atingida. Isso é feito tooget um instantâneo consistente de discos de saudação da máquina virtual de hello, sem ter que tooshut-o.

Depois que o instantâneo de saudação tiver sido realizado, dados de saudação são transferidos por hello Azure Backup service toohello Cofre de backup. serviço de saudação cuida da identificação e a transferência apenas os blocos de saudação que foram alterados desde o último backup de saudação tornar a rede e armazenamento de backups Olá eficiente. Quando a transferência de dados de saudação é concluída, Olá é removido e um ponto de recuperação é criado. Esse ponto de recuperação pode ser visto no hello portal clássico do Azure.

> [!NOTE]
> Para máquinas virtuais do Linux, é possível apenas o backup consistente com arquivos.
>
>

## <a name="prerequisites"></a>Pré-requisitos
Prepare o Azure Backup tooback backup de dados do DPM da seguinte maneira:

1. **Criar um Cofre de backup**. Se você ainda não criou um cofre de Backup na sua assinatura, consulte hello Azure portal versão deste artigo - [preparar tooback backup tooAzure de cargas de trabalho com o DPM](backup-azure-dpm-introduction.md).

  > [!IMPORTANT]
  > A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.
  > Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup. Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.<br/> Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup. **Em 1º de novembro de 2017**:
  >- Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.
  >- Você não será capaz de tooaccess os dados de backup no portal clássico do hello. Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.
  >

2. **Baixe as credenciais do cofre** — no Backup do Azure, carregar certificado de gerenciamento de saudação criado toohello cofre.
3. **Instalar hello Azure Backup Agent e registrar o servidor de saudação** — do Backup do Azure, instale o agente de saudação em cada servidor DPM e registrar servidor DPM Olá no cofre de backup hello.

[!INCLUDE [backup-download-credentials](../../includes/backup-download-credentials.md)]

[!INCLUDE [backup-install-agent](../../includes/backup-install-agent.md)]

## <a name="requirements-and-limitations"></a>Requisitos (e limitações)
* O DPM pode ser executado como servidor físico ou máquina virtual Hyper-V instalado no System Center 2012 SP1 ou System Center 2012 R2. Também pode ser executado como máquina virtual do Azure em execução no System Center 2012 R2 com pelo menos Pacote cumulativo de atualizações 3 do DPM 2012 R2 ou máquina virtual do Windows em VMWare em execução no System Center 2012 R2 com pelo menos Pacote cumulativo de atualizações 5.
* Se você estiver executando o DPM com o System Center 2012 SP1, instale o Rollup de atualização 2 do System Center Data Protection Manager SP1. Isso é necessário antes de instalar o hello Azure Backup Agent.
* servidor DPM Olá deve ter o Windows PowerShell e .net Framework 4.5 instalado.
* O DPM pode fazer a maioria das cargas de trabalho tooAzure Backup. Para obter uma lista completa do que é compatível, consulte hello Azure Backup oferece suporte a itens abaixo.
* Os dados armazenados no Azure Backup não podem ser recuperados com a opção de "Copiar tootape" hello.
* Você precisará de uma conta do Azure com recurso de Backup do Azure Olá habilitado. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Leia sobre os [preços do Backup do Azure](https://azure.microsoft.com/pricing/details/backup/).
* Usando o Backup do Azure requer toobe do hello Azure Backup Agent instalado nos servidores de saudação que desejar tooback. Cada servidor deve ter pelo menos 10% do tamanho de saudação do dados Olá que está sendo feitos, disponível como livre de armazenamento local. Por exemplo, fazendo backup de 100 GB de dados requer um mínimo de 10 GB de espaço livre no local de rascunho hello. Embora Olá mínimo é 10%, 15% do toobe de espaço livre de armazenamento local usado para o local do cache de saudação é recomendável.
* Os dados serão armazenados no hello armazenamento de cofre do Azure. Há um valor de toohello de limite de dados, que você pode fazer backup de Cofre de Backup do Azure tooan mas o tamanho de saudação de uma fonte de dados (por exemplo uma máquina virtual ou um banco de dados) não deve exceder 54,400 GB.

Esses tipos de arquivo têm suporte para backup tooAzure:

* Criptografados (apenas backups completos)
* Compactados (suporte para backups incrementais)
* Esparsos (suporte para backups incrementais)
* Compactados e esparsos (tratados como esparsos)

E os seguintes não têm suporte:

* Não há suporte para servidores em sistemas de arquivo que diferenciam maiúsculas de minúsculas.
* Links físicos (ignorados)
* Pontos de nova análise (ignorados)
* Criptografados e compactados (ignorados)
* Criptografados e esparsos (ignorados)
* Fluxo compactado
* Fluxo esparso

> [!NOTE]
> No System Center 2012 DPM com SP1 em diante, você pode fazer backup de cargas de trabalho protegidos pelo DPM tooAzure usando o Microsoft Azure Backup.
>
>
