---
title: "Obter percepções: relatórios de gerenciamento de senhas do Azure AD | Microsoft Docs"
description: "Este artigo descreve como toouse relatórios tooget percepção operações de gerenciamento de senha na sua organização."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Como o consultor tooget com gerenciamento de senhas de relatórios
> [!IMPORTANT]
> **Você está aqui por que está enfrentando problemas para iniciar sessão?** Se sim, [veja aqui como alterar e redefinir sua senha](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
>
>

Esta seção descreve como você pode usar o Azure Active Directory relatórios de gerenciamento de senhas tooview como os usuários estão usando a redefinição de senha e alteração em sua organização.

* [**Visão geral de relatórios de gerenciamento de senhas**](#overview-of-password-management-reports)
* [**Como o gerenciamento de senha tooview relatórios no novo portal do Azure de saudação**](#how-to-view-password-management-reports)
 * [Funções de diretório permitidas tooread relatórios](#directory-roles-allowed-to-read-reports)
* [**Tipos de atividades de gerenciamento de senha self-serviços no hello novo Portal do Azure**](#self-service-password-management-activity-types)
 * [Impedido de executar a redefinição de senha de autoatendimento](#activity-type-blocked-from-self-service-password-reset)
 * [Alterar senha (autoatendimento)](#activity-type-change-password-self-service)
 * [Redefinir senha (pelo administrador)](#activity-type-reset-password-by-admin)
 * [Redefinir a senha (autoatendimento)](#activity-type-reset-password-self-service)
 * [Progresso da atividade de fluxo de redefinição de senha de autoatendimento](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [Desbloquear a conta de usuário (autoatendimento)](#activity-type-unlock-user-account-self-service)
 * [Usuário registrado para redefinição de senha de autoatendimento](#activity-type-user-registered-for-self-service-password-reset)
* [**Como os eventos de gerenciamento de senha tooretrieve de Olá relatórios do AD do Azure e API de eventos**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [Limitações de recuperação de dados da API de emissão de relatórios](#reporting-api-data-retrieval-limitations)
* [**Como a redefinição de senha toodownload eventos de registro rapidamente com o PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Como o gerenciamento de senha tooview relatórios no portal clássico Olá**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**Atividade de registro em sua organização no portal clássico Olá de redefinição de senha do modo de exibição**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**Atividade em sua organização no portal clássico Olá redefinição de senha do modo de exibição**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>Visão geral dos relatórios de gerenciamento de senhas
Após a implantação da redefinição de senha, uma das próximas etapas de hello mais comuns é toosee como ele está sendo usado em sua organização.  Por exemplo, talvez você queira tooget informações em como os usuários estão se registrando para redefinição de senha ou senha quantas redefinições foram feitas nos Olá últimos dias.  Aqui estão algumas perguntas comuns de saudação que você será capaz de tooanswer com relatórios de gerenciamento de senha Olá que existem no hello [Portal de gerenciamento](https://manage.windowsazure.com) hoje:

* Quantas pessoas foram registradas para a redefinição de senhas?
* Quem se registrou para a redefinição de senhas?
* Que dados as pessoas estão registrando?
* Quantas pessoas redefiniram suas senhas na Olá últimos 7 dias?
* Quais são os usuários de métodos mais comuns hello e administradores utilizam tooreset suas senhas?
* O que são comuns problemas de usuários ou administradores enfrentam durante a tentativa de redefinição de senha toouse?
* Quais administradores estão redefinindo suas próprias senhas com frequência?
* Há qualquer atividade suspeita acontecendo na redefinição de senhas?

## <a name="how-tooview-password-management-reports"></a>Como os relatórios de gerenciamento de senha tooview
Em Olá novo [Portal do Azure](https://portal.azure.com) experiência, temos uma maneira melhor tooview senha e redefinição redefinição de atividade de registro.  Eventos de registro em Olá novo de redefinição de etapas a seguir Olá abaixo toofind Olá a redefinição de senha e a senha [Portal do Azure](https://portal.azure.com):

1. Navegue muito[**portal.azure.com**](https://portal.azure.com)
2. Clique em Olá **mais serviços** menu de navegação do hello principal Portal do Azure à esquerda
3. Procurar **Active Directory do Azure** Olá a lista de serviços e selecione-o no
4. Clique em **& grupos de usuários** no menu de navegação do Active Directory do Azure Olá
5. Clique em Olá **os Logs de auditoria** item de navegação no menu de navegação de usuários e grupos de saudação. Isso mostrará todos Olá auditoria eventos que ocorrem em relação a todos os usuários de saudação em seu diretório. Você pode filtrar essa exibição toosee todos os Olá relacionadas à senha eventos, também.
6. toofilter esse gerenciamento de senha do modo de exibição tooonly Olá relacionado eventos, clique em Olá **filtro** botão na parte superior de saudação da folha de saudação.
7. De saudação **filtro** menu, selecione Olá **categoria** suspenso e altere-toohello **gerenciamento de senha de autoatendimento** tipo de categoria.
8. Opcionalmente adicional Filtrar lista de saudação escolhendo Olá específico **atividade** você está interessado
### <a name="direct-link-toouser-audit-blade"></a>Folha de auditoria tooUser link direto
Se você tiver entrado no portal de tooyour, aqui está uma folha de auditoria de usuário do link direto toohello onde você pode ver esses eventos:

* [Vá toouser gerenciamento diretamente a exibição de auditoria](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>Funções de diretório permitido tooread relatórios
Atualmente, hello seguintes funções de diretório podem ler relatórios de gerenciamento de senha do AD do Azure no portal do Azure clássico de saudação:

* Administrador global

Antes de ser capaz de tooread esses relatórios, um administrador global na empresa Olá deve ter incluído para este toobe dados recuperado em nome da organização Olá visitando Olá reporting logs de auditoria ou o guia pelo menos uma vez. Até fazer isso, os dados não serão coletados para sua organização.

tooread mais informações sobre funções de diretório e o que eles podem fazem, consulte [atribuindo funções de administrador no Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles).

## <a name="self-service-password-management-activity-types"></a>Tipos de atividades de Gerenciamento de Senha de autoatendimento
Olá, tipos de atividades a seguir aparecem no hello **gerenciamento de senha de autoatendimento** categoria de evento de auditoria.  A seguir há uma descrição de cada um deles.

* [**Impedidos de redefinição de senha de autoatendimento** ](#activity-type-blocked-from-self-service-password-reset) -indica que um usuário tentou tooreset uma senha, use uma porta específica ou validar um número de telefone mais de 5 vezes total nas 24 horas.
* [**Alterar a senha (autoatendimento)** ](#activity-type-change-password-self-service) -indica um usuário executada um voluntário ou forçado (vencimento tooexpiry) alteração da senha.
* [**Redefinição de senha (pelo administrador)** ](#activity-type-reset-password-by-admin) -indica que um administrador realizou uma redefinição em nome de um usuário de hello Azure Portal de senha.
* [**Redefinição de senha (autoatendimento)** ](#activity-type-reset-password-self-service) -indica que um usuário com êxito redefinir a senha da saudação [Portal de redefinição de senha do AD do Azure](https://passwordreset.microsoftonline.com).
* [**Progresso de atividade de fluxo de redefinição de senha de autoatendimento sirvam** ](#activity-type-self-serve-password-reset-flow-activity-progress) -indica cada etapa específica de um usuário passa (por exemplo, passar uma senha específica para redefinir a porta de autenticação), como parte da senha Olá o processo de redefinição.
* [**Desbloquear a conta de usuário (autoatendimento)** ](#activity-type-unlock-user-account-self-service) -indica que um usuário desbloqueada com êxito sua conta do Active Directory sem redefinir sua senha de saudação [Portal de redefinição de senha do AD do Azure](https://passwordreset.microsoftonline.com) usando Olá [conta AD desbloquear sem redefinir](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) recurso.
* [**Usuário registrado para redefinição de senha de autoatendimento** ](#activity-type-user-registered-for-self-service-password-reset) -indica que um usuário tiver registrado todos Olá necessárias informações toobe capaz de tooreset sua senha de acordo com a política de redefinição de senha Olá locatário especificado no momento.

### <a name="activity-type-blocked-from-self-service-password-reset"></a>Tipo de atividade: redefinição de senha de autoatendimento bloqueada
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica que um usuário tentou tooreset uma senha, use uma porta específica ou validar um número de telefone mais de 5 vezes total nas 24 horas.
* **Atividade ator** -operações de redefinição de usuário de saudação que foi limitado de execução adicionais. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -operações de redefinição de usuário de saudação que foi limitado de execução adicionais. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ -indica que um usuário foi restringido executem qualquer redefinições adicionais, tente qualquer método de autenticação adicionais ou validar quaisquer números de telefone adicionais para Olá próximas 24 horas.
* **Razão da Falha do Status de Atividade** - não aplicável

### <a name="activity-type-change-password-self-service"></a>Tipo de atividade: alterar senha (autoatendimento)
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica um usuário executada um voluntário ou forçado (vencimento tooexpiry) alteração da senha.
* **Atividade ator** -usuário Olá que alterou sua senha. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -usuário Olá que alterou sua senha. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ - indica que um usuário alterou a senha com êxito
 * _Falha_ -indica que um usuário falha toochange sua senha. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação.
* **Razão da Falha do Status de Atividade** -
 * _FuzzyPolicyViolationInvalidPassword_ -usuário Olá selecionou uma senha que foi excluída automaticamente devido a recursos de detecção de senha proibidos do tooMicrosoft Localizando toobe muito comum ou especialmente fraca.

### <a name="activity-type-reset-password-by-admin"></a>Tipo de atividade: redefinir senha (pelo administrador)
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica que um administrador realizou uma redefinição em nome de um usuário de hello Azure Portal de senha.
* **Atividade ator** -administrador Olá que realizou a redefinição de saudação em nome de outro usuário final ou administrador. Deve ser o administrador global, o administrador de senha, o administrador de usuário ou o administrador de assistência técnica.
* **Atividade de destino** -usuário Olá cuja senha foi redefinida. Pode ser um usuário final ou um administrador diferente.
* **Status de Atividade Permitida**
 * _Sucesso_ - indica que um administrador redefine a senha de um usuário com êxito
 * _Falha_ -indica que um administrador falha toochange a senha do usuário. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação.

### <a name="activity-type-reset-password-self-service"></a>Tipo de atividade: redefinir senha (autoatendimento)
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica que um usuário com êxito redefinir a senha da saudação [Portal de redefinição de senha do AD do Azure](https://passwordreset.microsoftonline.com).
* **Atividade ator** -usuário Olá redefinir sua senha. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -usuário Olá redefinir sua senha. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ - indica que um usuário redefiniu sua própria senha com êxito
 * _Falha_ -indica que um usuário falha tooreset sua própria senha. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação.
* **Razão da Falha do Status de Atividade** -
 * _FuzzyPolicyViolationInvalidPassword_ -Olá administrador selecionou uma senha que foi excluída automaticamente devido a recursos de detecção de senha proibidos do tooMicrosoft Localizando toobe muito comum ou especialmente fraca.

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>Tipo de atividade: progresso de atividade de fluxo de redefinição de senha de autoatendimento
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica a cada etapa específica de um usuário passa (por exemplo, passar uma senha específica para redefinir a porta de autenticação) como parte da senha Olá o processo de redefinição.
* **Atividade ator** -fluxo de redefinição de usuário de saudação que realizou a parte de senha de saudação. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -fluxo de redefinição de usuário de saudação que realizou a parte de senha de saudação. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ -indica que um usuário concluída com êxito uma etapa específica de fluxo de redefinição de senha hello.
 * _Falha_ -indica falhado de fluxo de redefinição de uma etapa específica de senha hello. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação.
* **Razões de Status de Atividade Permitida**
 * Confira a tabela abaixo para ver [todas as razões de status de atividade de redefinição permitida](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>Tipo de atividade: desbloquear conta de usuário (autoatendimento)
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica que um usuário desbloqueada com êxito sua conta do Active Directory sem redefinir sua senha de saudação [Portal de redefinição de senha do AD do Azure](https://passwordreset.microsoftonline.com) usando Olá [AD desbloqueio de conta sem redefinir](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password) recurso.
* **Atividade ator** -usuário Olá desbloqueou sua conta sem redefinir sua senha. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -usuário Olá desbloqueou sua conta sem redefinir sua senha. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ - indica que um usuário desbloqueou sua própria conta com êxito
 * _Falha_ -indica que um usuário falha toounlock sua conta. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação.

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>Tipo de atividade: usuário registrado para redefinição de senha de autoatendimento
Olá lista a seguir explica a atividade em detalhes:

* **Descrição da atividade** – indica que um usuário tiver registrado todos Olá necessárias informações toobe capaz de tooreset sua senha de acordo com a política de redefinição de senha Olá locatário especificado no momento.
* **Atividade ator** -usuário Olá registrado para redefinição de senha. Pode ser um usuário final ou um administrador.
* **Atividade de destino** -usuário Olá registrado para redefinição de senha. Pode ser um usuário final ou um administrador.
* **Status de Atividade Permitida**
 * _Sucesso_ -indica um usuário registrado com êxito para redefinição de acordo com a política atual de saudação de senha.
 * _Falha_ -indica um tooregister de falha de usuário para redefinição de senha. Clicando na linha de saudação permitir Olá toosee **motivo do Status de atividade** categoria toolearn mais informações sobre por que ocorreu a falha de saudação. Observação: isso não significa que um usuário é sua própria senha, assim que ele ou ela não concluiu o processo de registro de saudação de tooreset não é possível. Se houver dados não verificados em sua conta está correta (como um número de telefone que não seja validado), mesmo que eles não verificou o número de telefone, ele podem ainda usá-lo tooreset sua senha. Para obter mais informações, confira [O que acontece quando um usuário é registrado?](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>Como os eventos de gerenciamento de senha tooretrieve de Olá relatórios do AD do Azure e API de eventos
A partir de agosto de 2015, Olá AD do Azure API de relatórios e eventos agora oferece suporte à recuperação todas as informações de saudação incluídas no hello senha e redefinição redefinir os relatórios de registro. Usando essa API, você pode baixar a redefinição de senha individuais e eventos de registro para a integração de redefinição de senha com hello tecnologia de sua choce de relatórios.

### <a name="how-tooget-started-with-hello-reporting-api"></a>Como tooget iniciada com hello API de relatório
tooaccess esses dados, você precisa toowrite um pequeno aplicativo ou script tooretrieve de nossos servidores. [Saiba como tooget iniciada com hello API do Azure AD Reporting](active-directory-reporting-api-getting-started.md).

Depois que você tiver um script de trabalho, você desejará lado tooexamine Olá senha registro e redefinição eventos que você pode recuperar toomeet seus cenários.

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent): lista as colunas de saudação disponíveis para eventos de redefinição de senha
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent): lista as colunas de saudação disponíveis para eventos de registro de redefinição de senha

### <a name="reporting-api-data-retrieval-limitations"></a>Relatando limitações de recuperação de dados de API
Olá no momento, os relatórios do AD do Azure e API de eventos recupera backup muito**75.000 eventos individuais** de saudação [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent) e [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent) tipos , abrangendo Olá **últimos 30 dias**.

Se você precisa tooretrieve ou armazena dados além desta janela, sugerimos persisti-los em um banco de dados externo e usando os deltas de saudação do hello API tooquery resultantes. Uma prática recomendada é toobegin recuperar os dados quando você inicia sua senha redefinir o processo de registro na sua organização, persisti-los externamente e continue deltas de saudação tootrack desse ponto para frente.

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>Como a redefinição de senha toodownload eventos de registro rapidamente com o PowerShell
Além disso toousing Olá relatórios do AD do Azure e API de eventos diretamente, você também pode usar o hello abaixo eventos de registro de toorecent de scripts do PowerShell em seu diretório. Isso é útil caso você deseje toosee que foi registrado recentemente ou gostaria de tooensure sua senha redefinida distribuição está ocorrendo conforme o esperado.

* [Script do PowerShell de Atividade de Registro do Azure AD SSPR](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Como o gerenciamento de senha tooview relatórios no portal clássico Olá
relatórios de gerenciamento de senha do toofind hello, siga as etapas de saudação abaixo:

1. Clique em Olá **do Active Directory** extensão no hello [portal clássico do Azure](https://manage.windowsazure.com).
2. Selecione seu diretório na lista de saudação que aparece no portal de saudação.
3. Clique em Olá **relatórios** guia.
4. Procure Olá **Logs de atividade** seção.
5. Selecione qualquer Olá **atividade de redefinição de senha** relatório ou hello **atividade de registro de redefinição de senha** relatório.

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>Atividade de registro no portal clássico Olá de redefinição de senha do modo de exibição
relatório de atividade de registro de redefinição de senha Olá mostra que redefinição de senha de todos os registros que ocorreram na sua organização.  Um registro de redefinição de senha é exibido no relatório para qualquer usuário que registrou com êxito as informações de autenticação de senha de saudação portal de registro de redefinição ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup)).

* **Intervalo de tempo máximo**: 30 dias
* **Número máximo de linhas**: 75.000
* **Baixável**: sim, por meio de arquivo CSV

### <a name="description-of-report-columns"></a>Descrição das colunas do relatório
Olá lista a seguir explica cada uma das colunas do relatório Olá detalhadamente:

* **Usuário** – operação de registro de redefinição de usuário de saudação que tentou uma senha.
* **Função** – função hello do usuário Olá no diretório de saudação.
* **Data e hora** – a data de saudação e a hora da tentativa de saudação.
* **Dados registrados** – quais autenticação dados Olá fornecida pelo usuário durante a senha de registro de redefinição.

### <a name="description-of-report-values"></a>Descrição dos valores de relatório
Olá, tabela a seguir descreve Olá diferentes valores permitidos para cada coluna:

| Coluna | Valores permitidos e seus significados |
| --- | --- |
| Dados Registrados |**Email alternativo** – alternativo do usuário usadas email ou a autenticação tooauthenticate email<p><p>**Telefone comercial**– usuário usado tooauthenticate de telefone do escritório<p>**Telefone celular** -tooauthenticate de telefone celular ou a autenticação do usuário usado<p>**Perguntas de segurança** – tooauthenticate de perguntas de segurança do usuário usado<p>**Qualquer combinação de saudação acima (por exemplo, Email alternativo + telefone celular)** – ocorre quando uma política de 2 portões é especificada e mostra quais dos dois métodos Olá tooauthentication de usuário usado solicitação de redefinição de sua senha. |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>Atividade no portal clássico Olá redefinição de senha do modo de exibição
Esse relatório mostra todas as tentativas de redefinição de senha que ocorreram na sua organização.

* **Intervalo de tempo máximo**: 30 dias
* **Número máximo de linhas**: 75.000
* **Baixável**: sim, por meio de arquivo CSV

### <a name="description-of-report-columns"></a>Descrição das colunas do relatório
Olá lista a seguir explica cada uma das colunas do relatório Olá detalhadamente:

1. **Usuário** – (com base no campo de ID de usuário de saudação fornecido quando o usuário Olá vem tooreset uma senha) de operação de redefinição de usuário de saudação que tentou uma senha.
2. **Função** – função hello do usuário Olá no diretório de saudação.
3. **Data e hora** – a data de saudação e a hora da tentativa de saudação.
4. **Método (s) usada** – quais métodos de autenticação Olá usuário usado para esta operação de redefinição.
5. **Resultado** – operação de redefinição do resultado final Olá senha hello.
6. **Detalhes** – Olá detalhes de redefinição de senha de saudação por que resultaram em valor Olá que tinha.  Também inclui as etapas de atenuação levaria tooresolve um erro inesperado.

### <a name="description-of-report-values"></a>Descrição dos valores de relatório
Olá, tabela a seguir descreve Olá diferentes valores permitidos para cada coluna:

| Coluna | Valores permitidos e seus significados |
| --- | --- |
| Métodos usados |**Email alternativo** – alternativo do usuário usadas email ou a autenticação tooauthenticate email<p>**Telefone comercial** – usuário usado tooauthenticate de telefone do escritório<p>**Telefone celular** – tooauthenticate de telefone celular ou a autenticação do usuário usado<p>**Perguntas de segurança** – tooauthenticate de perguntas de segurança do usuário usado<p>**Qualquer combinação de saudação acima (por exemplo, Email alternativo + telefone celular)** – ocorre quando uma política de 2 portões é especificada e mostra quais dos dois métodos Olá tooauthentication de usuário usado solicitação de redefinição de sua senha. |
| Result |**Abandonado** – redefinição de senha iniciada pelo usuário mas, em seguida, interrompida pela metade sem ser concluída<p>**Bloqueado** – a conta do usuário foi impedido de toouse redefinição devido a página de redefinição de senha do tooattempting toouse hello ou portal de redefinição de uma única senha muitas vezes em um período de 24 horas<p>**Cancelado** – usuário iniciou a redefinição de senha, mas clicou Olá Cancelar botão toocancel Olá sessão metade do caminho <p>**Entrar em contato com o administrador** – usuário apresentou um problema durante a sessão que não foi possível resolver, portanto Olá clicar hello "Entre em contato com seu administrador" link em vez de concluir Olá redefinição de senha do fluxo<p>**Falha ao** – usuário não foi capaz de tooreset uma senha, provavelmente porque o usuário Olá não foi configurado toouse recurso de saudação (por exemplo, nenhuma licença, sem informações de autenticação, senha gerenciada no local, mas o write-back está desativado).<p>**Bem-sucedida** – a redefinição de senha foi bem-sucedida. |
| Detalhes |Consulte a tabela abaixo. |

### <a name="allowed-values-for-details-column"></a>Valores permitidos para a coluna de detalhes
Abaixo está a lista de saudação de tipos de resultados, que você pode esperar quando usando senha Olá redefina o relatório de atividade:

| Detalhes | Tipo de resultado |
| --- | --- |
| Usuário abandonado depois de concluir a opção de verificação de email Olá |Abandoned |
| Usuário abandonado depois de concluir a opção de verificação de SMS móvel Olá |Abandoned |
| Usuário abandonado depois de concluir a opção de verificação de chamada de voz de dispositivo móvel Olá |Abandoned |
| Usuário abandonado depois de concluir a opção de verificação de chamada de voz do hello office |Abandoned |
| Usuário abandonado depois de concluir a opção de perguntas de segurança Olá |Abandoned |
| Abandonado pelo usuário depois de inserir sua ID de usuário |Abandoned |
| Usuário abandonado depois de iniciar a opção de verificação de email Olá |Abandoned |
| Usuário abandonado depois de iniciar a opção de verificação de SMS móvel Olá |Abandoned |
| Usuário abandonado depois de iniciar a opção de verificação de chamada de voz de dispositivo móvel Olá |Abandoned |
| Usuário abandonado depois de iniciar a opção de verificação de chamada de voz do hello office |Abandoned |
| Usuário abandonado depois de iniciar a opção de perguntas de segurança Olá |Abandoned |
| Abandonado pelo usuário antes de selecionar uma nova senha |Abandonado |
| Abandonado pelo usuário ao selecionar uma nova senha |Abandonado |
| O usuário inseriu muitos códigos de verificação de SMS inválidos e está bloqueado para 24 horas |Bloqueado |
| O usuário tentou muitas vezes a verificação de voz por telefone celular e está bloqueado por 24 horas |Bloqueado |
| O usuário tentou muitas vezes a verificação de voz comercial e está bloqueado por 24 horas |Bloqueado |
| O usuário tentou tooanswer perguntas de segurança muitas vezes e está bloqueado por 24 horas |Bloqueado |
| O usuário tentou tooverify um número de telefone muitas vezes e está bloqueado por 24 horas |Bloqueado |
| O usuário cancelou antes de passar os métodos de autenticação Olá necessária |Cancelado |
| O usuário fez o cancelamento antes de enviar uma nova senha |Cancelado |
| O usuário contatou um administrador depois de tentar a opção de verificação de email Olá |Administrador contatado |
| O usuário contatou um administrador depois de tentar a opção de verificação de SMS móvel Olá |Administrador contatado |
| O usuário contatou um administrador depois de tentar a opção de verificação de chamada de voz de dispositivo móvel Olá |Administrador contatado |
| O usuário contatou um administrador depois de tentar a opção de verificação de chamada de voz do hello office |Administrador contatado |
| O usuário contatou um administrador depois de tentar a opção de verificação de pergunta de segurança Olá |Administrador contatado |
| A redefinição de senha não está habilitada para este usuário. Habilitar redefinição de senha na Olá configurar guia tooresolve isso |Com falha |
| O usuário não tem uma licença. Você pode adicionar isso tooresolve de usuário de toohello uma licença |Com falha |
| Usuário tentou tooreset de um dispositivo sem cookies habilitados |Com falha |
| A conta do usuário tem métodos de autenticação insuficiente definidos. Adicione tooresolve de informações de autenticação |Com falha |
| A senha do usuário é gerenciada localmente. Você pode habilitar essa tooresolve de write-back de senha |Com falha |
| Não foi possível acessar o serviço de redefinição de senha no local. Verifique o log de eventos de seu computador de sincronização |Com falha |
| Encontramos um problema ao redefinir a senha do local do usuário Olá. Verifique o log de eventos de seu computador de sincronização |Com falha |
| Este usuário não é um membro do grupo de usuários de redefinição de senha hello. Adicione esse tooresolve de grupo do usuário toothat. |Com falha |
| A redefinição de senha foi desabilitada inteiramente para este locatário. Consulte [aqui](http://aka.ms/ssprtroubleshoot) tooresolve isso. |Com falha |
| O usuário redefiniu a senha com êxito |Bem-sucedido |

## <a name="next-steps"></a>Próximas etapas
Abaixo está tooall links de saudação páginas de documentação de redefinição de senha do AD do Azure:

* **Você está aqui por que está enfrentando problemas para iniciar sessão?** Se sim, [veja aqui como alterar e redefinir sua senha](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account).
* [**Como ele funciona** ](active-directory-passwords-how-it-works.md) -Saiba mais sobre Olá seis diferentes componentes do serviço de saudação e o que cada
* [**Guia de Introdução** ](active-directory-passwords-getting-started.md) -Saiba como tooallow tooreset do usuários e alterar suas senhas de nuvem ou local
* [**Personalizar** ](active-directory-passwords-customize.md) - Saiba como toocustomize Olá parecer & aparência e comportamento de saudação as necessidades da organização tooyour de serviço
* [**Práticas recomendadas** ](active-directory-passwords-best-practices.md) -Saiba como tooquickly implantar e gerenciar com eficácia senhas na sua organização
* [**Perguntas frequentes sobre** ](active-directory-passwords-faq.md) -Obtenha respostas toofrequently perguntas frequentes
* [**Solução de problemas** ](active-directory-passwords-troubleshoot.md) -Saiba como tooquickly solucionar os problemas com o serviço de saudação
* [**Saiba mais** ](active-directory-passwords-learn-more.md) - vá profundamente detalhes técnicos de saudação do funcionamento do serviço de saudação
