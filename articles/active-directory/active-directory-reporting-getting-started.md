---
title: "Introdução aos relatórios do Azure Active Directory | Microsoft Docs"
description: "Listas Olá vários relatórios disponíveis no Active Directory do Azure reporting"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Introdução aos Relatórios do Active Directory do Azure
## <a name="what-it-is"></a>O que é
O Active Directory do Azure (Azure AD) inclui relatórios de auditoria, atividade e segurança para seu diretório. Aqui está uma lista de relatórios de saudação incluídos:

### <a name="security-reports"></a>Relatórios de segurança
* Entradas de fontes desconhecidas
* Entradas após várias falhas
* Entradas de várias geografias
* Entradas de endereços IP com atividade suspeita
* Atividades de entrada irregulares
* Entradas de dispositivos possivelmente infectados
* Usuários com atividade de entrada anômala

### <a name="activity-reports"></a>Relatórios de atividades
* Uso do aplicativo: resumo
* Uso do aplicativo: detalhado
* Painel do aplicativo
* Erros de provisionamento de conta
* Dispositivos de usuário individual
* Atividade de usuário individual
* Relatório de atividade de grupos
* Relatório de atividade de registro de redefinição de senha
* Atividade de redefinição de senha

### <a name="audit-reports"></a>Relatórios de auditoria
* Relatório de auditoria de diretório

> [!TIP]
> Para obter mais documentação sobre os Relatórios do AD do Azure, consulte [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Como ele funciona
### <a name="reporting-pipeline"></a>Pipeline de relatórios
Olá pipeline de emissão de relatórios consiste em três etapas principais. Sempre que um usuário faz logon ou uma autenticação é feita, ocorre a seguinte de saudação:

* Primeiro, autenticação saudação do usuário (com êxito ou não) e saudação de resultados é armazenada em bancos de dados do serviço Olá Active Directory do Azure.
* Em intervalos regulares, todas as entradas recentes são processadas. Neste ponto, nossos algoritmos de atividade anômala e segurança estão procurando atividades suspeitas em todas as entradas recentes.
* Após o processamento, Olá relatórios são gravados, armazenado em cache e servidos em Olá portal clássico do Azure.

### <a name="report-generation-times"></a>Tempos de geração dos relatórios
Devido a toohello grande volume de autenticações e entre que ins processadas pelo Olá plataforma do AD do Azure, hello mais recentes entradas processadas são, em média, uma hora antigas. Em casos raros, pode levar até too8 horas tooprocess hello mais recentes entradas.

Você pode encontrar a entrada hello mais recentes processado examinando o texto de ajuda de saudação na parte superior de saudação de cada relatório.

![Texto de ajuda na parte superior de saudação de cada relatório](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Para obter mais documentação sobre os Relatórios do AD do Azure, consulte [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Introdução
### <a name="sign-into-hello-azure-classic-portal"></a>Entrar Olá portal clássico do Azure
Primeiro, você precisará toosign em Olá [portal clássico do Azure](https://manage.windowsazure.com) como um administrador global ou de conformidade. Você também deve ser um administrador de serviço de assinatura do Azure ou coadministrador ou usar hello "acesso tooAzure AD" assinatura do Azure.

### <a name="navigate-tooreports"></a>Navegue tooReports
tooview relatórios, navegue toohello guia de relatórios na parte superior de saudação do seu diretório.

Se for a primeira vez que exibir relatórios hello, você precisará tooagree caixa de diálogo de tooa antes de exibir relatórios de saudação. Isso é tooensure que é aceitável para que os administradores em sua organização tooview esses dados, que podem ser considerados informações particulares em alguns países.

![Caixa de diálogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Explore cada relatório
Navegue até cada relatório toosee Olá de dados sendo coletados e processados Olá entradas. Você pode encontrar um [lista de todos os relatórios de saudação](active-directory-reporting-guide.md).

![Todos os relatórios](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Baixe os relatórios de saudação como CSV
Cada relatório pode ser baixado como um arquivo CSV (valores separados por vírgula). Você pode usar esses arquivos no Excel, Power BI ou programas toofurther analisar seus dados de análise de terceiros.

toodownload qualquer relatório como um CSV, navegar toohello relatório e clique em "Download" na parte inferior da saudação.

![Botão Baixar](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Para obter mais documentação sobre os Relatórios do AD do Azure, consulte [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Próximas etapas
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Personalizar alertas para atividade de entrada anômala
Navegue toohello "Configurar" guia de seu diretório.

Seção de "Notificações" toohello de rolagem.

Habilitar ou desabilitar a seção de "Notificações de Email de entradas anômalas" hello.

![Olá seção notificações](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Integrar Olá API Reporting do AD do Azure
Consulte [guia de Introdução com hello Reporting API](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Acione Multi-Factor Authentication nos usuários
Selecione um usuário em um relatório.

Botão hello "Habilitar MFA" na parte inferior da saudação da tela hello.

![botão de autenticação multifator de Olá Olá final da tela hello](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Para obter mais documentação sobre os Relatórios do AD do Azure, consulte [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Saiba mais
### <a name="audit-events"></a>Eventos de auditoria
Saiba mais sobre quais eventos são auditados no diretório de saudação em [do Azure Active Directory relatar eventos de auditoria](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Integração da API
Consulte [guia de Introdução com hello API Reporting](active-directory-reporting-api-getting-started.md) e hello [documentação de referência de API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Entre em contato
Envie um email para [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) para qualquer dúvida, ajuda ou comentário.

> [!TIP]
> Para obter mais documentação sobre os Relatórios do AD do Azure, consulte [Exibir relatórios de acesso e uso](active-directory-view-access-usage-reports.md).
> 
> 

