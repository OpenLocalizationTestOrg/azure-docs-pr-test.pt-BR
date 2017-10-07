---
title: "Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory | Microsoft Docs"
description: "Fornece uma lista das mensagens de erro do hello atividade do Active Directory do Azure conteúdo pack e as etapas toofix-los."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Solução de erros do pacote de conteúdo dos Logs de atividades do Azure Active Directory 


Ao trabalhar com o pacote de conteúdo do Power BI de saudação visualização do Azure Active Directory, é possível encontrar hello os erros a seguir: 

- [Falha na atualização](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Credenciais de fonte de dados tooupdate com falha](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Importação de dados muito demorada](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Este tópico fornece informações sobre as possíveis causas de saudação e como toofix esses erros.
 
## <a name="refresh-failed"></a>Falha na atualização 
 
**Como esse erro aparece**: Email do Power BI ou status de falha no histórico de atualização de saudação. 


| Causa | Como toofix |
| ---   | ---        |
| Atualize erros podem ser causados quando foram Redefinir credenciais de saudação de usuários de saudação conectando o pacote de conteúdo toohello mas não atualizadas nas configurações de conexão de saudação de saudação do pacote de conteúdo de saudação de falha. | No Power BI, localize toohello correspondente do conjunto de dados de saudação painel de logs de atividade do Active Directory do Azure (logs de atividade do Azure Active Directory), escolha o agendamento de atualização e, em seguida, insira suas credenciais do AD do Azure. |
| Uma atualização pode falhar devido a problemas toodata Olá subjacente do pacote de conteúdo. | Registre um tíquete de suporte. Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Credenciais de fonte de dados tooupdate com falha 
 
**Como esse erro aparece**: no Power BI, quando você está se conectando o pacote de conteúdo toohello atividade do Active Directory do Azure (visualização) de logs. 

| Causa | Como toofix |
| ---   | ---        |
| usuário da conexão Olá não é um administrador global nem um leitor de segurança ou um administrador de segurança. | Use uma conta que seja um administrador global ou um leitor de segurança ou uma segurança admin tooaccess Olá pacotes de conteúdo. |
| Seu locatário não é um locatário Premium ou não tem, pelo menos, um usuário com um Arquivo de licença Premium. | Registre um tíquete de suporte. Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>Importação de dados muito demorada 
 
**Como esse erro aparece**: no Power BI, depois que você se conectou seu pacote de conteúdo, Olá processo de importação de dados inicia tooprepare seu dashboard para log de atividade do Active Directory do Azure. Você vê a mensagem de saudação: "*importação de dados...* "  

| Causa | Como toofix |
| ---   | ---        |
| Dependendo do tamanho de saudação do seu locatário, esta etapa pode levar de alguns minutos too30 minutos. | Seja paciente. Se a mensagem de saudação não alterar tooshowing seu painel em uma hora, envie um tíquete de suporte. Para obter mais detalhes, consulte [como tooget dão suporte ao Active Directory do Azure](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Próximas etapas

Olá tooinstall pacote de conteúdo do Power BI visualização do Azure Active Directory, clique em [aqui](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


