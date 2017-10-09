---
title: "Guia de início aaaAzure rápida da Central de segurança | Microsoft Docs"
description: "Este artigo ajuda você a se familiarizar rapidamente com a Central de segurança do Azure, guiando-o em componentes de gerenciamento Olá segurança monitoramento e a política e vinculação toonext etapas."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Guia de início rápido da Central de Segurança do Azure
Este artigo ajuda você a começar rapidamente com a Central de segurança do Azure, guiando você pelas Olá segurança monitoramento e política de componentes de gerenciamento da Central de segurança.

> [!NOTE]
> A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>
>

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado com a Central de segurança, você deve ter um tooMicrosoft de assinatura do Azure. Se você não tiver uma assinatura, pode se inscrever em uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).

a camada gratuita Olá da Central de segurança é habilitada automaticamente com a sua assinatura e fornece visibilidade sobre o estado de segurança Olá seus recursos do Azure. Ela fornece gerenciamento de política de segurança básica, recomendações de segurança e integração com produtos e serviços de segurança de parceiros do Azure.

Acessar a Central de segurança do hello [portal do Azure](https://azure.microsoft.com/features/azure-portal/). toolearn mais sobre Olá portal do Azure, consulte Olá [portal documentação](https://azure.microsoft.com/documentation/services/azure-portal/).

## <a name="permissions"></a>Permissões
Na Central de segurança, verá apenas informações relacionadas tooan recursos do Azure, quando foi atribuída a função de saudação do leitor, colaborador ou proprietário para Olá assinatura ou grupo de recursos que o recurso pertence. Consulte [permissões na Central de segurança do Azure](security-center-permissions.md) toolearn mais sobre as funções e ações permitidas na Central de segurança.

## <a name="data-collection"></a>Coleta de dados
Central de segurança coleta dados de suas máquinas virtuais (VMs) tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Quando você acessa pela primeira vez a Central de Segurança, a coleta de dados é habilitada em todas as VMs em sua assinatura. Central de segurança provisiona Olá Microsoft Monitoring Agent em todas as existentes suporte para todos os novos que são criados e VMs do Azure. Consulte [habilitar coleta de dados](security-center-enable-data-collection.md) toolearn mais sobre como funciona a coleta de dados.

A coleta de dados é recomendada. Se você estiver usando a camada gratuita Olá da Central de segurança, você pode desativar a coleta de dados de máquinas virtuais ao desativar a coleta de dados na política de segurança de saudação. Coleta de dados é necessária para as assinaturas na camada de saudação padrão da Central de segurança. Consulte [Central de segurança preços](security-center-pricing.md) toolearn mais sobre Olá gratuito e camadas de preços padrão.

Olá, as etapas a seguir descreve como tooaccess e use Olá componentes da Central de segurança. Essas etapas, mostramos como tooturn desativar a coleta de dados se você escolher tooopt-out.

> [!NOTE]
> Este artigo apresenta serviço hello usando um exemplo de implantação. Ele não é um guia passo a passo.
>
>

## <a name="access-security-center"></a>Acessar a Central de Segurança
No portal de hello, siga essas etapas tooaccess Central de segurança:

1. Em Olá **Microsoft Azure** menu, selecione **Central de segurança**.

   ![Menu do Azure][1]
2. Se você estiver acessando a Central de segurança para Olá primeira vez, Olá **bem-vindo** folha é aberta. Selecione **inicie a Central de segurança** tooopen Olá **Central de segurança** folha e tooenable coleta de dados.
   ![Tela de boas-vindas][10]
3. Depois de você inicia a Central de segurança da folha de boas-vindas de saudação ou selecione Central de segurança no menu do Microsoft Azure Olá, Olá **Central de segurança** folha é aberta. Para facilitar o acesso toohello **Central de segurança** folha em Olá Olá futuras, selecione **Pin folha toodashboard** opção (superior direito).
   ![Opção de toodashboard de folha de PIN][2]

## <a name="use-security-center"></a>Usar a Central de Segurança
Você pode configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure. Vamos configurar uma política de segurança para sua assinatura:

1. Em Olá **Central de segurança** folha, selecione Olá **política** lado a lado.
2. Em Olá **política de segurança - Definir política por assinatura** folha, selecione uma assinatura.
3. Em Olá **política de segurança** folha, **coleta de dados** é habilitado tooautomatically coleta logs. saudação de extensão de monitoramento é provisionada em todas as máquinas virtuais atuais e novas na assinatura de saudação. (Na camada gratuita de saudação da Central de segurança, você pode recusar a coleta de dados definindo **coleta de dados** muito**Off**. Configuração **coleta de dados** muito**Off** impede que a Central de segurança fornecendo alertas de segurança e as recomendações.)
4. Em Olá **política de segurança** folha, selecione **política de prevenção de**. Isso abre o hello **política de prevenção de** folha.
5. Em Olá **política de prevenção de** folha, ative as recomendações de saudação que você deseja toosee como parte de sua política de segurança. Exemplos:

   * Configuração **atualizações do sistema** muito**em** todas as verificações de suporte VMs faltam atualizações do sistema operacional.
   * Configuração **vulnerabilidades do sistema operacional** muito**em** verificações todos têm o suporte de VMs tooidentify todas as configurações de sistema operacional que podem tornar Olá VM tooattack mais vulnerável.

### <a name="view-recommendations"></a>Exibir recomendações
1. Retornar toohello **Central de segurança** folha e selecione Olá **recomendações** lado a lado. Central de segurança periodicamente analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele mostra as recomendações em Olá **recomendações** folha.
   ![Recomendações na Central de Segurança do Azure][5]
2. Selecione uma recomendação sobre Olá **recomendações** tooview folha mais Olá de informações e/ou tootake de ação tooresolve emitir.

### <a name="view-hello-security-state-of-your-resources"></a>Olá estado de segurança de seus recursos de exibição
1. Retornar toohello **Central de segurança** folha. Olá **prevenção** seção do painel de saudação contém indicadores de estado de segurança Olá para máquinas virtuais, redes, aplicativos e dados.
2. Selecione **de computação** tooview obter mais informações. Olá **de computação** folha abre mostrando três guias:

  - **Visão geral** – contém recomendações de monitoramento e da VM.
  - **Máquinas virtuais** – lista todas as VMs e seu estado de segurança atual.
  - **Serviços de nuvem** - Lista as funções da Web e de trabalho monitoradas pela Central de Segurança.

    ![bloco de integridade de recursos de saudação na Central de segurança do Azure][6]

3. Em Olá **visão geral** , selecione uma recomendação em **recomendações de máquinas virtuais** tooview mais informações e/ou realizar ação tooconfigure controles necessários.
4. Em Olá **máquinas virtuais** , selecione uma VM tooview mais detalhes.

### <a name="view-security-alerts"></a>Exibir alertas de segurança
1. Retornar toohello **Central de segurança** folha e selecione Olá **alertas de segurança** lado a lado. Olá **alertas de segurança** folha é aberto e exibe uma lista de alertas. Olá análise da Central de segurança de seus logs de segurança e a atividade de rede gera esses alertas. Os alertas das soluções de parceiro integradas estão incluídos.
   ![Alertas na Central de Segurança do Azure][7]

   > [!NOTE]
   > Alertas de segurança só estarão disponíveis se a camada padrão Olá da Central de segurança está habilitada. Uma avaliação gratuita de 60 dias da camada de saudação padrão está disponível. Consulte [próximas etapas](#next-steps) para obter informações sobre como tooget Olá padrão de camada.
   >
   >
2. Selecione um alerta tooview obter informações adicionais. Neste exemplo, vamos selecionar **Binário do sistema modificado descoberto**. Isso abre blades que fornecem detalhes adicionais sobre o alerta de saudação.
   ![Detalhes de alerta de segurança na Central de Segurança do Azure][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>Exibir integridade da saudação suas soluções de parceiros
1. Retornar toohello **Central de segurança** folha. Olá **soluções de parceiros** lado a lado permite monitorar, em um relance, Olá status de integridade de suas soluções de parceiros integrados com sua assinatura do Azure.
2. Selecione Olá **soluções de parceiros** lado a lado. Uma folha é aberto e exibe uma lista de suas soluções de parceiro conectado tooSecurity Center.
   ![Soluções de parceiros][9]
3. Selecione uma solução de parceiro. Neste exemplo, vamos selecionar Olá **QualysVa1** solução.  Uma folha é aberto e mostra o status da saudação de solução de parceiro de saudação e solução de saudação associados a recursos. Selecione **console de solução** experiência de gerenciamento de parceiros de saudação tooopen para esta solução.

## <a name="next-steps"></a>Próximas etapas
Este artigo introduzido toohello segurança monitoramento e política de componentes de gerenciamento da Central de segurança. Agora que você está familiarizado com a Central de segurança, tente Olá etapas a seguir:

* Configure uma política de segurança para sua assinatura do Azure. mais, consulte toolearn [definindo políticas de segurança na Central de segurança do Azure](security-center-policies.md).
* Use as recomendações de saudação na Central de segurança toohelp você proteger seus recursos do Azure. mais, consulte toolearn [Gerenciando recomendações de segurança na Central de segurança do Azure](security-center-recommendations.md).
* Confira e gerencie os alertas de segurança atuais. mais, consulte toolearn [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md).
- [Segurança de dados da Central de Segurança do Azure](security-center-data-security.md) – saiba como os dados são gerenciados e protegidos na Central de Segurança do Azure.
* Saiba mais sobre Olá [advanced threat recursos de detecção de](security-center-detection-capabilities.md) que acompanham o hello [camada padrão](security-center-pricing.md) da Central de segurança. camada padrão Olá é oferecida gratuitamente para Olá primeiros 60 dias.
* Se você tiver dúvidas sobre como usar a Central de segurança, consulte Olá [perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md).

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
