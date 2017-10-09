---
title: "coleta de dados de aaaEnable na Central de segurança do Azure | Microsoft Docs"
description: " Saiba como coleta de dados de tooenable na Central de segurança do Azure. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 411d7bae-c9d4-4e83-be63-9f2f2312b075
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 78bbf9a3d852095e2a1387c1606ff4bbb778a0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-data-collection-in-azure-security-center"></a>Habilitar coleta de dados na Central de Segurança do Azure

> [!NOTE]
> A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. mais, consulte toolearn [migração da plataforma Azure Security Center](security-center-platform-migration.md). informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>
>

Central de segurança coleta dados de suas máquinas virtuais (VMs) tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Quando você acessa a Central de segurança pela primeira vez, você possui uma coleção de dados do hello opção tooenable para todas as VMs em sua assinatura. Se a coleta de dados não estiver habilitada, a Central de segurança recomenda que você ativar a coleta de dados na política de segurança Olá para essa assinatura.

Quando a coleta de dados é habilitada, a Central de segurança provisiona Olá Microsoft Monitoring Agent em todas as existentes suporte para máquinas virtuais do Azure e os novos que são criados. Olá Microsoft Monitoring Agent verifica várias configurações relacionadas à segurança. Além disso, o sistema de operacional de hello gera eventos de log de eventos. Exemplos desses dados são: tipo e versão do sistema operacional, logs do sistema operacional (logs de eventos do Windows), processos em execução, nome do computador, endereços IP, usuário registrado e ID do locatário. Olá Microsoft Monitoring Agent lê as configurações e entradas de log de eventos e copia o espaço de trabalho do hello dados tooyour para análise. Olá Microsoft Monitoring Agent também copia o espaço de trabalho tooyour arquivos de despejo de falha.

Se você estiver usando a camada gratuita Olá da Central de segurança, você pode desativar a coleta de dados de máquinas virtuais ao desativar a coleta de dados na política de segurança de saudação. Desabilitar a coleta de dados limita as avaliações de segurança para as VMs. mais, consulte toolearn [desabilitar a coleta de dados](#disabling-data-collection). Os instantâneos de disco da VM e a coleção de artefatos são habilitados mesmo que a coleta de dados tenha sido desabilitada. Coleta de dados é necessária para as assinaturas na camada de saudação padrão da Central de segurança.

> [!NOTE]
> Saiba mais sobre os [tipos de preço](security-center-pricing.md) Gratuito e Standard da Central de Segurança.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Este documento não é um guia passo a passo.
>
>

1. Em Olá **recomendações** folha, selecione **habilitar coleta de dados para assinaturas**.  Isso abre o hello **ativar a coleta de dados** folha.
   ![Folha de recomendações][2]
2. Em Olá **ativar a coleta de dados** folha, selecione sua assinatura. Olá **política de segurança** abre folha para essa assinatura.
3. Em Olá **política de segurança** folha, selecione **na** em **coleta de dados** tooautomatically coletar logs. Ativar saudação de provisões de coleção de dados extensão de monitoramento em todos os atual e o novo suporte para VMs na assinatura de saudação.
4. Selecione **Salvar**.
5. Selecione **OK**.

## <a name="disabling-data-collection"></a>Desabilitar a coleta de dados
Se você estiver usando a camada gratuita Olá da Central de segurança, você pode desativar a coleta de dados de máquinas virtuais a qualquer momento ao desativar a coleta de dados na política de segurança de saudação. Coleta de dados é necessária para as assinaturas na camada de saudação padrão da Central de segurança.

1. Retornar toohello **Central de segurança** folha e selecione Olá **política** lado a lado. Isso abre o hello **segurança política-Definir política por assinatura** folha.
   ![Selecione o bloco de política de saudação][5]
2. Em Olá **segurança política-Definir política por assinatura** folha, assinatura Olá selecione que você deseja toodisable a coleta de dados.
3. Olá **política de segurança** abre folha para essa assinatura.  Selecione **Desativado** em Coleta de dados.
4. Selecione **salvar** na faixa de opções hello.

## <a name="next-steps"></a>Próximas etapas
Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "Habilitar coleta de dados." toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
- [Segurança de dados da Central de Segurança do Azure](security-center-data-security.md) – saiba como os dados são gerenciados e protegidos na Central de Segurança do Azure.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[2]: ./media/security-center-enable-data-collection/recommendations.png
[3]: ./media/security-center-enable-data-collection/data-collection.png
[4]: ./media/security-center-enable-data-collection/storage-account.png
[5]: ./media/security-center-enable-data-collection/policy.png
[6]: ./media/security-center-enable-data-collection/disable-data-collection.png
