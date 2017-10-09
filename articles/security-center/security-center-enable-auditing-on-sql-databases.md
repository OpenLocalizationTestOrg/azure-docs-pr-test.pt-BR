---
title: "bancos de dados de detecção de ameaças e auditoria aaaEnable no SQL na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar a detecção de ameaças e auditoria em bancos de dados SQL * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a>Habilitar a auditoria e detecção de ameaças em bancos de dados SQL na Central de Segurança do Azure
A Central de Segurança do Azure recomendará que você ative a auditoria e detecção de ameaças para todos os bancos de dados SQL se isso ainda não tiver sido habilitado. A auditoria e a detecção de ameaças podem ajudar você a manter uma conformidade regulatória, a entender a atividade do banco de dados e a obter informações sobre discrepâncias e anomalias que poderiam indicar preocupações de negócios ou suspeitas de violações de segurança.

Depois que você ativou a auditoria, você pode configurar alertas de segurança de tooreceive de configurações e emails de detecção de ameaças. Detecção de ameaças detecta atividades anormais de banco de dados indicando banco dados potencial toohello de ameaças de segurança. Isso permite que você toodetect e responde a ameaças de toopotential conforme elas ocorrem.

Essa recomendação se aplica a toohello serviço do SQL Azure. não inclui o SQL em execução em máquinas virtuais.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **detecção de ameaça e habilitar a auditoria em bancos de dados do SQL**.  Isso abre o hello **detecção de ameaça e habilitar a auditoria em bancos de dados SQL** folha.

   ![Habilitar auditoria em bancos de dados SQL][1]
2. Selecione um banco de dados tooenable a auditoria do SQL no. Isso abre o hello **auditoria e detecção de ameaças** folha.

3. Em Olá **auditoria e detecção de ameaças** folha, selecione **ON** em **auditoria**.

   ![Ativar a auditoria e detecção de ameaças][2]
4. Siga as etapas de saudação em [detecção de ameaças do banco de dados SQL no portal do Azure de saudação](../sql-database/sql-database-threat-detection-portal.md) tooturn em e configurar a detecção de ameaças e a lista de saudação tooconfigure de endereços de email que receberão alertas de segurança após a detecção de atividades anormais.

## <a name="see-also"></a>Consulte também
Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "Habilitar auditoria & ameaça detecção em bancos de dados SQL." toolearn mais sobre como proteger seu banco de dados SQL, consulte a seguir hello:

* [Protegendo o Banco de Dados SQL](../sql-database/sql-database-security-overview.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
