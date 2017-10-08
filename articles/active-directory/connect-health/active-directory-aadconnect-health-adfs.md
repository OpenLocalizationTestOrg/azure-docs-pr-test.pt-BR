---
title: aaaUsing do Azure AD Connect Health com AD FS | Microsoft Docs
description: "Esta é a página de integridade de conexão de saudação do AD do Azure como toomonitor local infraestrutura do AD FS."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Monitorar o AD FS usando o Azure AD Connect Health
Olá documentação a seguir é específico toomonitoring sua infraestrutura do AD FS com o Azure AD Connect Health. Para saber mais sobre como monitorar o Azure AD Connect (Sincronização) com o Azure AD Connect Health, confira [Usar o Azure AD Connect Health para Sincronização](active-directory-aadconnect-health-sync.md). Além disso, para obter informações sobre como monitorar os Serviços de Domínio do Active Directory com o Azure AD Connect Health, confira [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md).

## <a name="alerts-for-ad-fs"></a>Alertas do AD FS
Olá seção alertas de integridade de conexão de AD do Azure fornece que Olá lista de alertas ativos. Cada alerta inclui informações relevantes, etapas de resolução e documentação de toorelated links.

Você pode clicar duas vezes uma tooopen alerta, ativo ou resolvido uma nova folha com informações adicionais, etapas tooresolve Olá alerta e documentação de toorelevant links. Você também pode exibir dados históricos sobre alertas que foram resolvidos no hello anterior.

![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Análises de Uso do AD FS
Análise AD do Azure conectar integridade uso analisa o tráfego de autenticação de saudação dos seus servidores de Federação. Clique duas vezes em caixa de análise de uso do hello, tooopen Olá uso folha de análise, que mostra várias métricas e os agrupamentos.

> [!NOTE]
> toouse análise de uso com o AD FS, você deve garantir que a auditoria do AD FS está habilitado. Para obter mais informações, consulte [Habilitar a auditoria do AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect de métricas adicionais, especifique um intervalo de tempo, ou o agrupamento de saudação toochange, clique no gráfico de análise de uso de saudação e selecione Editar gráfico. Você pode especificar o intervalo de tempo de saudação, selecione uma métrica diferente e alterar o agrupamento de saudação. Você pode exibir a distribuição Olá Olá de tráfego de autenticação com base em diferentes "métricas" e agrupar cada métrica usando parâmetros relevantes "Agrupar por" descritos em Olá seção a seguir:

**Métrica: Total de solicitações** – Número total de solicitações processadas por servidores AD FS.

|Agrupar Por | O que significa o agrupamento de saudação e por que é útil? |
| --- | --- |
| Todos | Mostra a contagem de saudação do número total de solicitações processadas por todos os servidores do AD FS.|
| Aplicativo | Grupos Olá total de solicitações com base na terceira parte confiável Olá direcionado. Esse agrupamento é útil toounderstand qual aplicativo está recebendo o percentual do total de tráfego hello. |
|  Servidor |Total de solicitações com base no servidor de saudação que processa a solicitação Olá Olá a grupos. Esse agrupamento é útil toounderstand distribuição de carga de saudação do tráfego total de saudação.
| Ingresso no local |Grupos Olá total de solicitações com base em se eles são provenientes de dispositivos que estão no local de trabalho (conhecido). Esse agrupamento é útil toounderstand se os recursos são acessados usando dispositivos de infraestrutura de identidade toohello desconhecido. |
|  Método de autenticação | Grupos Olá total de solicitações com base no método de autenticação Olá usado para autenticação. Esse agrupamento é útil toounderstand Olá método de autenticação comum que é usado para autenticação. Estes são os métodos de autenticação possíveis Olá <ol> <li>Autenticação Integrada do Windows (Windows)</li> <li>Autenticação Baseada em Formulários (Formulários)</li> <li>SSO (Logon único)</li> <li>Autenticação de Certificado X509 (Certificado)</li> <br>Se os servidores de Federação Olá receberem solicitação Olá com um Cookie de SSO, essa solicitação é contabilizada como SSO (logon único). Nesses casos, se Olá cookie for válido, o usuário de Olá não é solicitado credenciais tooprovide e obtém acesso contínuo toohello aplicativo. Esse comportamento é comum se você tiver várias partes confiantes protegidas pelos servidores de Federação hello. |
| Local de rede | Total de solicitações com base no local de rede de saudação do usuário Olá Olá a grupos. Pode ser qualquer intranet ou extranet. Esse agrupamento é útil tooknow a porcentagem de tráfego de saudação é proveniente de intranet hello ou extranet. |


**Métrica: Solicitação com falha Total** -número total de saudação falha solicitações processadas pelo serviço de Federação hello. (Essa métrica só está disponível no AD FS para o Windows Server 2012 R2)

|Agrupar Por | O que significa o agrupamento de saudação e por que é útil? |
| --- | --- |
| Tipo de erro | Mostra o número de saudação de erros com base nos tipos de erro predefinidos. Esse agrupamento é útil toounderstand Olá os tipos comuns de erros. <ul><li>Nome de usuário ou a senha incorreta: erros devido tooincorrect username ou password.</li> <li>"O bloqueio de extranet": falhas devido a solicitações de toohello recebidas de um usuário que foi bloqueado de extranet </li><li> "Expirado senha": falhas devido a log toousers com uma senha expirada.</li><li>"Desabilitado conta": falhas devido a log toousers com uma conta desabilitada.</li><li>"Autenticação de dispositivo": falhas devido a falha toousers tooauthenticate usando a autenticação do dispositivo.</li><li>"Autenticação de certificado de usuário": falhas devido a tooauthenticate toousers falha devido a um certificado inválido.</li><li>"MFA": falhas devido a falha toouser tooauthenticate usando a autenticação multifator.</li><li>"Outras credenciais": "Autorização de emissão": falhas devido a falhas de tooauthorization.</li><li>"Emissão delegação": falhas devido a erros de delegação tooissuance.</li><li>"Aceitação de token": falhas devido a rejeição tooADFS Olá token de um provedor de identidade de terceiros.</li><li>"Protocol": falha devido a erros de tooprotocol.</li><li>"Desconhecido": envolve tudo. Outras falhas que não cabem na Olá definido categorias.</li> |
| Servidor | Grupos Olá erros com base no servidor de saudação. Esse agrupamento é útil toounderstand distribuição de erro de saudação entre os servidores. A distribuição desigual poderia ser um indicador de um servidor em um estado com falha. |
| Local de rede | Grupos Olá erros com base no local de rede de saudação de solicitações de saudação (intranet vs extranet). Esse agrupamento é útil toounderstand tipo de saudação de solicitações com falha. |
|  Aplicativo | Grupos Olá falhas com base no aplicativo hello direcionado (terceira parte confiável). Esse agrupamento é útil toounderstand qual aplicativo de destino está vendo mais o número de erros. |

**Métrica: Contagem de usuários** – número médio de usuários exclusivos autenticando-se ativamente usando o AD FS

|Agrupar Por | O que significa o agrupamento de saudação e por que é útil? |
| --- | --- |
|Todos |Essa métrica fornece uma contagem do número médio de usuários usando o serviço de Federação Olá em fatias de tempo selecionado hello. os usuários de saudação não estão agrupados. <br>Média de saudação depende Olá fração de tempo selecionada. |
| Aplicativo |Número médio de saudação de grupos de usuários com base em Olá direcionados aplicativo (terceira parte confiável). Esse agrupamento é útil toounderstand quantos usuários estão usando o aplicativo. |

## <a name="performance-monitoring-for-ad-fs"></a>Monitoramento de desempenho do AD FS
O Monitoramento de Desempenho do Azure Active Directory Connect Health fornece informações de monitoramento nas métricas. Selecionar caixa de monitoramento hello, abre uma nova folha com informações detalhadas sobre as métricas de saudação.

![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Selecionando a opção de filtro de saudação na parte superior de saudação da folha hello, você pode filtrar por servidor toosee métricas de um servidor individual. métrica de toochange, com o botão direito no gráfico em Olá monitoramento folha de monitoramento de saudação e selecione Editar gráfico (ou botão de editar gráfico Olá select). Da saudação nova folha que é aberta, você pode selecionar métricas adicionais na lista suspensa hello e especificar um intervalo de tempo para exibir dados de desempenho de saudação.

## <a name="reports-for-ad-fs"></a>Relatórios do AD FS
O Azure AD Connect Health fornece relatórios sobre a atividade e o desempenho do AD FS. Esses relatórios ajudam os administradores a obter percepções sobre as atividades nos servidores do AD FS.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>50 principais usuários com logons com falha de nome de usuário/senha
Um dos motivos comuns de saudação para uma solicitação de autenticação com falha em um servidor do AD FS é uma solicitação com credenciais inválidas, ou seja, um nome de usuário incorreto ou a senha. Normalmente acontece toousers devido toocomplex senhas, senhas esquecidas ou erros de digitação.

Mas há outros motivos que podem resultar em um número inesperado de solicitações que está sendo tratado por seus servidores do AD FS, tais como: um aplicativo que caches credenciais de usuário e credenciais de saudação expirarem ou um usuário mal-intencionado tentar toosign em uma conta com uma série de senhas conhecidas. Esses dois exemplos são motivos que poderiam levar tooa aumento nas solicitações.

O Azure AD Connect Health para AD FS fornece um relatório sobre os primeiros 50 usuários com as tentativas de logon com falha devido tooinvalid username ou password. Este relatório é obtido com o processamento de eventos de auditoria de saudação gerados por todos os servidores de saudação do AD FS em farms de saudação

![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

Neste relatório, você tem acesso fácil toohello informações a seguir:

* N º total de solicitações com falha com o nome de usuário/senha incorreta no hello últimos 30 dias
* Número médio de usuários com falha de logon com um nome de usuário/senha inválidos por dia.

Clicar nesta parte leva toohello folha de relatório principal que fornece detalhes adicionais. Esta folha inclui um gráfico com tendência informações toohelp estabelecer uma linha de base sobre solicitações com o nome de usuário incorreto ou a senha. Além disso, ele fornece a lista de saudação dos primeiros 50 usuários com número de saudação de tentativas com falha.

gráfico de saudação fornece Olá informações a seguir:

* Olá n º total de logons com falha devido a nome de usuário/senha incorreta tooa em uma base por dia.
* Olá n º total de usuários exclusivos que logons em uma base por dia com falha.
* Endereço IP do cliente da última solicitação

![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

relatório de saudação fornece Olá informações a seguir:

| Item do relatório | Descrição |
| --- | --- |
| Id de Usuário |Mostra a ID de usuário de saudação que foi usada. Esse valor é o hello usuário digitado, que, em alguns casos, é Olá ID de usuário incorreto está sendo usado. |
| Tentativas com falha |Mostra hello n º total de tentativas com falha para essa ID de usuário específico. Olá tabela é classificada por hello número máximo de tentativas com falha em ordem decrescente. |
| Última falha |Mostra o carimbo de data / hora de saudação quando Olá última falha. |
| IP da última falha |Mostra o endereço de IP do cliente de saudação de solicitação incorreta mais recente de saudação. |

> [!NOTE]
> Este relatório é atualizado automaticamente após a cada duas horas com hello novas informações coletadas no momento. Como resultado, as tentativas de logon em Olá últimas duas horas não podem ser incluídas no relatório de saudação.
>
>

## <a name="related-links"></a>Links relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)