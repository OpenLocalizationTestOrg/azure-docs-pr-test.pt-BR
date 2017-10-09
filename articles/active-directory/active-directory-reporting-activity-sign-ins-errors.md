---
title: "códigos de erro de relatório de atividade aaaSign no portal do Azure Active Directory Olá | Microsoft Docs"
description: "Referência de códigos de erro no relatório de atividade de entrada."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Códigos de erro de relatório de atividade de entrada no portal do Azure Active Directory Olá

Com informações de saudação fornecidas pelo relatório de entradas de usuário hello, você encontrar respostas tooquestions como:

- Quem entrou usando o Azure Active Directory?
- Quais aplicativos foram conectados?
- Quais entradas apresentaram falhas e por quê?

Esse erro de saudação do tópico lista os códigos e Olá descrições relacionadas. 

## <a name="how-can-i-display-failed-sign-ins"></a>Como exibir entradas com falha? 

Seu primeiro entrada tooall de ponto de entrada atividades dados  **[entradas](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  em Olá **atividade** seção **Azure Active**.


![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins-errors/61.png "Atividade de entrada")


Em seu relatório de entradas, você pode exibir todas as falhas de entradas selecionando **Falha** como **Status de Entrada**.


![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins-errors/06.png "Atividade de entrada")

Clicar em um item na lista exibida de hello, abre Olá **detalhes da atividade: entradas** folha. Essa exibição fornece todos os detalhes de saudação do Active Directory do Azure controla sobre entradas, incluindo Olá **código de erro de conexão** e um **motivo da falha**.

![Atividade de entrada](./media/active-directory-reporting-activity-sign-ins-errors/05.png "Atividade de entrada")


Como uma alternativa toousing Olá dados de entradas de saudação tooaccess portal do Azure, você também pode usar o hello [reporting API](active-directory-reporting-api-getting-started-azure-portal.md).


Olá seção a seguir fornece uma visão geral completa de todos os possíveis erros e Olá descrições relacionadas. 

## <a name="error-codes"></a>Códigos do Erro

| Erro| Descrição |
| --- | --- |
| 50001| entidade de serviço Olá chamada X não foi encontrada no locatário Olá denominado Y. Isso pode acontecer se o aplicativo hello não foi instalado pelo administrador de saudação do locatário hello. Ou entidade de segurança do recurso não foi encontrado no diretório de saudação ou é inválida|
| 50008| Asserção SAML está ausente ou configurado incorretamente no token de saudação.|
| 50011| endereço de resposta Hello está ausente, configurado incorretamente ou não coincide com os endereços de resposta configurados para o aplicativo hello.|
| 50053| Conta está bloqueada porque o usuário tentou toosign em muitas vezes com uma ID de usuário incorreto ou a senha.|
| 50054| Uma senha antiga está sendo usada para autenticação.|
| 50055| Senha inválida; a senha inserida expirou.|
| 50057| A conta de usuário está desabilitada.|
| 50058| Nenhuma informação sobre a identidade do usuário é encontrada entre fornecido as credenciais ou o usuário não foi encontrado no locatário ou uma solicitação de entrada sem confirmação foi enviada, mas nenhum usuário está conectado ou serviço foi usuário de saudação tooauthenticate não é possível.|
| 50074| Autenticação forte (segundo fator) obrigatória|
| 50079| Usuário precisa tooenroll para autenticação de dois fatores|
| 50126| Nome de usuário ou senha inválida ou Nome de usuário ou senha local inválida.|
| 50131| Usado em vários erros de acesso condicional. Estado de dispositivo do Windows incorreta por exemplo, solicitação bloqueada devido a atividade de toosuspicious, a política de acesso e política de segurança de decisões.|
| 50133| A sessão é inválida devido tooexpiration ou alteração de senha recente.|
| 50144| A senha do Active Directory do usuário expirou.|
| 65001| Aplicativo X não tem o aplicativo de tooaccess permissão Y ou Olá permissão foi revogada. Ou hello usuário ou administrador não consentiu aplicativo hello de toouse com ID X. Send uma solicitação de autorização interativa para este usuário e recursos. Ou Olá usuário ou administrador não consentiu aplicativo hello de toouse com ID X. Send tooact de administração de locatário uma autorização solicitação tooyour em nome do aplicativo de saudação: Y para o recurso: Z.|
| 65005| aplicativo Hello necessário lista de acesso de recursos não contém aplicativos detectáveis pelo recurso de saudação ou aplicativo de cliente hello solicitou tooresource de acesso que não foi especificado na sua lista de acesso de recurso necessário ou o serviço de gráfico retornado incorreta solicitação ou o recurso não foi encontrado.|
| 70001| aplicativo Hello chamado X não foi encontrado no locatário Olá denominado Y. Isso pode acontecer se o aplicativo hello não foi instalado por Olá administrador de inquilinos hello ou tooby consentido qualquer usuário no locatário hello. Você pode ter enviado o seu locatário incorreto do toohello de solicitação de autenticação.|
| 80001| Nenhum Agente de Autenticação disponível.|
| 80002| A solicitação de validação de senha do Agente de Autenticação atingiu o tempo limite.|
| 80003| Resposta inválida recebida pelo Agente de Autenticação.|
| 80004| Nome UPN incorreto usado na solicitação de entrada.|
| 80005| Agente de Autenticação: erro.|
| 80007| Autenticação agente tooconnect não é possível tooActive Directory.|
| 80010| Senha de toodecrypt não é possível do agente de autenticação.|
| 81001| O tíquete de Kerberos do usuário é muito grande.|
| 81002| Tíquete de Kerberos do usuário toovalidate não é possível.|
| 81003| Tíquete de Kerberos do usuário toovalidate não é possível.|
| 81004| Falha na tentativa de autenticação Kerberos.|
| 81008| Tíquete de Kerberos do usuário toovalidate não é possível.|
| 81009| Tíquete de Kerberos do usuário toovalidate não é possível.|
| 81010| SSO contínuo falhou porque o tíquete de Kerberos do usuário Olá expirou ou é inválido.|
| 81011| Objeto de usuário toofind não é possível com base nas informações no tíquete de Kerberos do usuário hello.|
| 81012| usuário Olá tentar toosign em tooAzure AD é diferente do usuário de saudação conectado ao dispositivo hello.|
| 81013| Objeto de usuário toofind não é possível com base nas informações no tíquete de Kerberos do usuário hello.|
| 90014| Usado em vários casos quando um campo esperado não está presente na credencial hello.|
| 90093| Gráfico retornado código de erro proibido para solicitação de saudação.|



## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes, consulte Olá [relatórios de atividade entrar no portal do Azure Active Directory Olá](active-directory-reporting-activity-sign-ins.md).

