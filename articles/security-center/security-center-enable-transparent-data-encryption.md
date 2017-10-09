---
title: "aaaEnable criptografia transparente de dados na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar Transparent Data Encryption * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a>Habilitar Transparent Data Encryption na Central de Segurança do Azure
A Central de Segurança do Azure recomendará habilitar a TDE (Transparent Data Encryption) em bancos de dados SQL se já não estiver habilitada. A TDE protege seus dados e ajuda a atender aos requisitos de conformidade por meio da criptografia de banco de dados, backups associados e arquivos de log de transações em descanso, sem a necessidade de alterações tooyour aplicativo. toolearn mais ver [Transparent Data Encryption com o banco de dados do Azure SQL](https://msdn.microsoft.com/library/dn948096).

Essa recomendação se aplica a toohello serviço do SQL Azure. não inclui o SQL em execução em máquinas virtuais.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **habilitar a criptografia transparente de dados**.
   ![Habilitar Transparent Data Encryption][1]
2. Isso abre o hello **habilitar a criptografia transparente de dados em bancos de dados SQL** folha. Selecione um banco de dados SQL tooenable TDE.
   ![Selecione o banco de dados SQL tooenable TDE no][2]
3. Em Olá **criptografia transparente de dados** folha, selecione **ON** em criptografia de dados e selecione **salvar** na faixa de opções superior da folha de Olá Olá.
   ![Ativar TDE][3]

   Quando a TDE está habilitada em Olá selecionados banco de dados SQL, hello **status de criptografia** alterará muito**criptografado**.    

   ![Status de criptografia][4]

## <a name="see-also"></a>Consulte também
Este artigo lhe mostrou como tooimplement Olá recomendação da Central de segurança "Habilitar criptografia transparente de dados". toolearn mais sobre o SQL TDE, consulte a seguir hello:

* [Transparent Data Encryption com o Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/dn948096)
* [Introdução ao Transparent Data Encryption (TDE)](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
