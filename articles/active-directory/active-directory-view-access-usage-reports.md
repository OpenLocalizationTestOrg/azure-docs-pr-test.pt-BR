---
title: "aaaView relatórios de acesso e uso | Microsoft Docs"
description: "Explica como acesso tooview relatórios de uso e toogain percepção integridade hello e segurança do diretório da sua organização."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Exibir relatórios de acesso e uso
*Esta documentação é parte da saudação [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).*

Você pode usar o acesso do Azure Active Directory e uso relatórios toogain visibilidade Olá integridade e segurança do diretório da sua organização. Com essas informações, um administrador de diretório pode determinar melhor onde possíveis riscos de segurança pode para que possa planejar toomitigate adequadamente esses riscos.

No Portal de gerenciamento do hello, relatórios são categorizados Olá maneiras a seguir:

* Relatórios de anomalias – contém eventos de conexão que nós identificamos toobe anormal. Nosso objetivo é toomake você ciente de tais atividades e permitem que você toobe capaz de toomake uma decisão sobre se um evento é suspeito.
* Relatórios de aplicativos integrados – fornece um panorama de como os aplicativos em nuvem estão sendo usados na sua organização. O Active Directory do Azure oferece integração com milhares de aplicativos em nuvem.
* Relatórios de erros – indica os erros que podem ocorrer ao provisionar contas tooexternal aplicativos.
* Relatórios específicos do usuário – exibem dados de atividade de entrada/dispositivo de vídeo de um usuário específico.
* Logs de atividade – contêm um registro de todos os eventos auditados em Olá última 24 horas, últimos 7 dias ou últimos 30 dias, bem como alterações do grupo de atividade e atividade de registro e redefinição de senha.

> [!NOTE]
> * Alguns relatórios avançados de uso de recursos e anomalias estão disponíveis somente quando você habilita o [Azure Active Directory Premium](active-directory-get-started-premium.md). Os relatórios avançados ajudam a melhorar a segurança de acesso, responder toopotential ameaças e obter acesso tooanalytics sobre o uso de acesso e o aplicativo de dispositivo.
> * O Azure Active Directory Premium e edições Basic estão disponíveis para clientes na China usando a instância mundial de saudação do Active Directory do Azure. O Azure Active Directory Premium e edições Basic não têm suporte no momento no serviço do Microsoft Azure Olá operado pela 21Vianet na China. Para obter mais informações, entre em contato conosco em Olá [Fórum do Active Directory do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Relatórios
| Relatório | Descrição |
| --- | --- |
| **Relatórios de atividades anômalas** | |
| [Entradas de fontes desconhecidas](active-directory-reporting-sign-ins-from-unknown-sources.md) |Pode indicar um toosign tentativa sem que está sendo rastreado. |
| [Entradas após várias falhas](active-directory-reporting-sign-ins-after-multiple-failures.md) |Pode indicar um ataque de força bruta com êxito. |
| [Entradas de várias regiões geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Pode indicar que vários usuários estão entrando com hello mesma conta. |
| [Entradas de endereços IP com atividade suspeita](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Pode indicar uma conexão bem-sucedida após uma tentativa de invasão prolongada. |
| [Entradas de dispositivos possivelmente infectados](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Pode indicar um toosign tentativa de dispositivos possivelmente infectados. |
| [Atividade de conexão anômala](active-directory-reporting-irregular-sign-in-activity.md) |Pode indicar padrões de entrada dos eventos anômalos toousers. |
| [Usuários com atividade de entrada anômala](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Indica os usuários cujas contas podem ter sido comprometidas. |
| Usuários com credenciais insuficientes |Usuários com credenciais insuficientes |
| **Logs de atividade** | |
| Relatório de auditoria |Eventos auditados em seu diretório |
| Atividade de redefinição de senha |Fornece uma exibição detalhada das redefinições de senha que acontecem em sua organização. |
| Atividade de registro de redefinição de senha |Fornece uma exibição detalhada dos registros de redefinições de senha que acontecem em sua organização. |
| Atividade de grupos de autoatendimento |Fornece um tooall do log de atividade atividades de autoatendimento em seu diretório de grupo |
| **Aplicativos integrados** | |
| Uso do aplicativo |Fornece um resumo do uso de todos os aplicativos SaaS integrados ao seu diretório. |
| Atividade de provisionamento de conta |Fornece um histórico de tentativas de tooprovision aplicativos de tooexternal de contas. |
| Status de substituição de senha |Fornece uma visão geral detalhada do status de substituição automática de senha de aplicativos SaaS. |
| Erros de provisionamento de conta |Indica os aplicativos de tooexternal access dos toousers um impacto. |
| **Gerenciamento de direitos** | |
| Uso do RMS |Fornece um resumo de uso do Rights Management |
| Usuários RMS mais ativos |Lista os primeiros 1.000 usuários ativos que acessaram arquivos protegidos por RMS |
| Uso de dispositivo do RMS |Lista dispositivos usados para acessar arquivos protegidos por RMS |
| Uso de aplicativos habilitados para RMS |Fornece uso de aplicativos habilitados para RMS |

## <a name="report-editions"></a>Edições de relatório
| Relatório | Grátis | Basic | Premium |
| --- | --- | --- | --- |
| **Relatórios de atividades anômalas** | | | |
| Entradas de fontes desconhecidas |✓ |✓  |✓ |
| Entradas após várias falhas |✓ |✓  |✓ |
| Entradas de várias regiões geográficas |✓ |✓  |✓ |
| Entradas de endereços IP com atividade suspeita | | |✓ |
| Entradas de dispositivos possivelmente infectados | | |✓ |
| Atividade de conexão anômala | | |✓ |
| Usuários com atividade de entrada anômala | | |✓ |
| Usuários com credenciais insuficientes | | |✓ |
| **Logs de atividade** | | | |
| Relatório de auditoria |✓ |✓  |✓ |
| Atividade de redefinição de senha | | |✓ |
| Atividade de registro de redefinição de senha | | |✓ |
| Atividade de grupos de autoatendimento | | |✓ |
| **Aplicativos integrados** | | | |
| Uso do aplicativo | | |✓ |
| Atividade de provisionamento de conta |✓ |✓  |✓ |
| Status de substituição de senha | | |✓ |
| Erros de provisionamento de conta |✓ |✓  |✓ |
| **Gerenciamento de direitos** | | | |
| Uso do RMS | | |Somente RMS |
| Usuários RMS mais ativos | | |Somente RMS |
| Uso de dispositivo do RMS | | |Somente RMS |
| Uso de aplicativos habilitados para RMS | | |Somente RMS |

## <a name="anomalous-activity-reports"></a>Relatórios de atividades anômalas
<p>Olá anormal entrar em relatórios de atividades sinalizador suspeito entrar tooOffice365 de atividade, Portal de gerenciamento, o painel de acesso do AD do Azure, o Sharepoint Online, Dynamics CRM Online e outros serviços online da Microsoft.</p>

<p>Todos esses relatórios, exceto hello "Entradas após várias falhas" relatório, também sinalizador suspeito <i>federado</i> entrar ins toohello mencionados acima dos serviços, independentemente do provedor de Federação hello. </p>

<p>Olá relatórios a seguir está disponível: </p><ul>

<li>[Entradas de fontes desconhecidas](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Entradas após várias falhas](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Entradas de várias regiões geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Entradas de endereços IP com atividade suspeita](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Atividade de conexão anômala](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Entradas de dispositivos possivelmente infectados](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li>[Usuários com atividade de entrada anômala](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</li>

<li>Usuários com credenciais insuficientes</li></ul>

## <a name="activity-logs"></a>Logs de atividade
### <a name="audit-report"></a>Relatório de auditoria
| Descrição | Local do relatório |
|:--- |:--- |
| Mostra um registro de todos os eventos auditados em Olá últimas 24 horas, últimos 7 dias ou últimos 30 dias. <br /> Para obter mais informações, consulte [Eventos de relatório de auditoria do Active Directory do Azure](active-directory-reporting-audit-events.md) |Diretório > guia Relatórios |

![Relatório de auditoria](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Atividade de redefinição de senha
| Descrição | Local do relatório |
|:--- |:--- |
| Mostra todas as tentativas de redefinição de senha que ocorreram na organização. |Diretório > guia Relatórios |

![Atividade de redefinição de senha](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Atividade de registro de redefinição de senha
| Descrição | Local do relatório |
|:--- |:--- |
| Mostra todos os registros de redefinição de senha que ocorreram na organização |Diretório > guia Relatórios |

![Atividade de registro de redefinição de senha](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Atividade de grupos de autoatendimento
| Descrição | Local do relatório |
|:--- |:--- |
| Mostra todas as atividades de saudação de grupos de autoatendimentos em seu diretório. |Diretório > Usuários > <i>Usuário</i> > guia Dispositivos |

![Atividade de grupos de autoatendimento](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Relatórios de aplicativos integrados
### <a name="application-usage-summary"></a>Uso do aplicativo: resumo
| Descrição | Local do relatório |
|:--- |:--- |
| Use este relatório quando desejar toosee uso para todos os aplicativos de SaaS Olá em seu diretório. Este relatório está baseado no número de saudação de vezes que os usuários clicaram no aplicativo hello em Olá painel de acesso. |Diretório > guia Relatórios |

Este relatório inclui entradas muito*todos os* aplicativos que o diretório tiver acessam, incluindo aplicativos pré-integrados da Microsoft.

Aplicativos Microsoft pré-integrados incluem o Office 365, Sharepoint, Olá Portal de gerenciamento e outros.

![Resumo de uso do aplicativo](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Uso do aplicativo: detalhado
| Descrição | Local do relatório |
|:--- |:--- |
| Use este relatório quando desejar toosee quanto um aplicativo SaaS específico está sendo usado. Este relatório está baseado no número de saudação de vezes que os usuários clicaram no aplicativo hello em Olá painel de acesso. |Diretório > guia Relatórios |

### <a name="application-dashboard"></a>Painel do aplicativo
| Descrição | Local do relatório |
|:--- |:--- |
| Este relatório indica o aplicativo de toohello ins cumulativa logon por usuários em sua organização, em um intervalo de tempo selecionado. gráfico de saudação na página de painel Olá ajudará você a identificar tendências para todos os usos desse aplicativo. |Diretório > Aplicativo > guia Painel |

## <a name="error-reports"></a>Relatórios de erros
### <a name="account-provisioning-errors"></a>Erros de provisionamento de conta
| Descrição | Local do relatório |
|:--- |:--- |
| Use este toomonitor os erros que ocorrem durante a sincronização de saudação de contas do tooAzure de aplicativos SaaS do Active Directory. |Diretório > guia Relatórios |

![Erros de provisionamento de conta](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Relatórios específicos de usuário
### <a name="devices"></a>Dispositivos
| Descrição | Local do relatório |
|:--- |:--- |
| Use este relatório quando desejar que o endereço IP toosee hello e a localização geográfica de dispositivos que um usuário específico tenha utilizado tooaccess Active Directory do Azure. |Diretório > Usuários > <i>Usuário</i> > guia Dispositivos |

### <a name="activity"></a>Atividade
| Descrição | Local do relatório |
|:--- |:--- |
| Mostra o logon de saudação na atividade de um usuário. relatório de saudação inclui informações como o aplicativo hello conectado, o dispositivo usado, o endereço IP e o local. Não coletamos o histórico de saudação para usuários que entram com uma conta da Microsoft. |Diretório > Usuários > <i>Usuário</i> > guia Atividade |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Inscrever-se em eventos incluídos no hello relatório de atividade de usuário
Somente determinados tipos de eventos de entrada serão exibida no hello relatório de atividade de usuário.

| Tipo de evento | Incluso? |
| --- | --- |
| Assinar ins toohello [painel de acesso](http://myapps.microsoft.com/) |Sim |
| Assinar ins toohello [Portal de gerenciamento](https://manage.windowsazure.com/) |Sim |
| Assinar ins toohello [Portal do Microsoft Azure](https://portal.azure.com/) |Sim |
| Assinar ins toohello [portal do Office 365](http://portal.office.com/) |Sim |
| Assinar o aplicativo nativo do ins tooa, como o Outlook (consulte a exceção abaixo) |Sim |
| Assinar ins tooa federado/provisionado aplicativo por meio de saudação painel de acesso, como o Salesforce |Sim |
| Assinar ins tooa baseada em senha aplicativo por meio de saudação painel de acesso, como o Twitter |Sim |
| Entrada ins tooa aplicativo de negócios personalizada que tenha sido adicionado toohello diretório |Não (em breve) |
| Assinar ins tooan Proxy de aplicativo do Azure AD aplicativo que foi adicionado toohello diretório |Não (em breve) |

> Observação: quantidade de saudação do tooreduce de ruído neste relatório, entradas por Olá [assistente Microsoft Online Services entrar](http://community.office365.com/en-us/w/sso/534.aspx) não são mostradas.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Coisas tooconsider se você suspeitar de violação de segurança
Se você suspeitar de que uma conta de usuário pode ser comprometida ou qualquer tipo de atividade de usuário suspeitos que pode levar tooa violação de segurança de dados do diretório na nuvem Olá, talvez você queira tooconsider um ou mais de saudação ações a seguir:

* Entre em contato com a atividade de Olá Olá usuário tooverify
* Redefinir senha do usuário Olá
* [Habilitar a Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md) para segurança adicional

## <a name="view-or-download-a-report"></a>Exibir ou baixar uma fatura
1. No portal clássico do Azure do hello, clique em **do Active Directory**, clique em nome de saudação do diretório da sua organização e, em seguida, clique em **relatórios**.
2. Na página de relatórios Olá, clique em relatório Olá desejado tooview e/ou download.
   
   > [!NOTE]
   > Se esse for Olá pela primeira vez que você usou Olá reporting recurso do Active Directory do Azure, você verá um tooOpt de mensagem no. Se você concordar, clique em Olá toocontinue de ícone de marca de seleção.
   > 
   > 
3. Clique Olá menu suspenso próximo tooInterval e, em seguida, selecione uma das Olá intervalos de tempo que devem ser usados ao gerar este relatório a seguir:
   
   * Últimas 24 horas
   * Últimos 7 dias
   * Últimos 30 dias
4. Clique em relatório de Olá Olá marca de seleção ícone toorun.
   * Backup too1000 eventos serão mostrados na Olá portal clássico do Azure.
5. Se aplicável, clique em **baixar** toodownload Olá relatório tooa arquivo compactado no formato de valores separados por vírgulas (CSV) para visualização offline ou finalidades de arquivamento.
   * Backup too75, 000 eventos serão incluídos no arquivo hello baixado.
   * Para mais dados, confira Olá [API do Azure AD Reporting](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignorar um evento
Se você estiver exibindo os relatórios de anomalias, perceba que você pode ignorar vários eventos que aparecem em relatórios relacionados. tooignore um evento, basta destacar o evento Olá no relatório hello e, em seguida, clique em **ignorar**. Olá **ignorar** botão removerá permanentemente evento realçado saudação do relatório hello e só pode ser usada por administradores globais licenciados.

## <a name="automatic-email-notifications"></a>Notificações automáticas por email
Para saber mais sobre as notificações de relatórios do Azure AD, confira [Notificações de relatórios do Active Directory do Azure](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>O que vem a seguir
* [Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Adicionar identidade visual tooyour páginas entrar e painel de acesso da empresa](active-directory-add-company-branding.md)

