---
title: Proxy de aplicativo de aaaTroubleshoot | Microsoft Docs
description: Aborda como erros de tootroubleshoot no Proxy de aplicativo do Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Solucionar problemas e mensagens de erro do Proxy do Aplicativo
Se ocorrerem erros ao acessar um aplicativo publicado ou em aplicativos de publicação, verifique Olá toosee opções a seguir se o Proxy de aplicativo do Microsoft Azure AD está funcionando corretamente:

* Serviços do Windows hello abrir console e verifique se esse Olá **conector de Proxy de aplicativo Microsoft AAD** serviço está habilitado e em execução. Você também pode ser toolook na página de propriedades de serviço de Proxy de aplicativo hello, como mostrado na Olá a imagem a seguir:  
  ![Captura de tela da janela Propriedades do Conector de Proxy de Aplicativo do Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Abra o Visualizador de Eventos e procure eventos de conector do Proxy de Aplicativo em **Logs de Aplicativos e Serviços**  > **Microsoft** > **AadApplicationProxy** > **Connector** > **Admin**.
* Se necessário, logs mais detalhados estão disponíveis por [ativar Olá logs de sessão de conector de Proxy de aplicativo](application-proxy-understand-connectors.md#under-the-hood).

Para obter mais informações sobre a ferramenta de solução de problemas de saudação do AD do Azure, consulte [ferramenta toovalidate conector rede pré-requisitos de solução de problemas](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>página de saudação não será renderizada corretamente
Você pode ter problemas com a renderização do aplicativo ou de funcionamento incorreto sem receber mensagens específicas de erro. Isso pode ocorrer se você publicou o caminho de artigo hello, mas aplicativo hello requer o conteúdo que existe fora desse caminho.

Por exemplo, se você publicar Olá caminho https://yourapp/app mas aplicativo hello chamadas imagens em https://yourapp/media, eles não processados. Certifique-se de que você publique o aplicativo hello usando Olá caminho nível mais alto é necessário tooinclude todo o conteúdo relevante. Neste exemplo, seria http://yourapp/.

Se você altera o conteúdo do caminho tooinclude referenciado, mas ainda precisa tooland de usuários em um link mais profundo no caminho hello, consulte Olá postagem de blog [link à direita de saudação de configuração para aplicativos de Proxy de aplicativo no painel de acesso de saudação do AD do Azure e o aplicativo do Office 365 iniciador](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Erros de conector

Saudação de uso [ferramenta de teste das portas conector do Azure AD aplicativo Proxy](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que seu conector possa acessar o serviço de Proxy de aplicativo hello. No mínimo, certifique-se de que que a região do hello centro dos EUA e Olá região mais próxima tooyou tenham todas as marcas de seleção verdes. Além disso, um número maior de marcas de seleção verdes significa maior resiliência. 

Se o registro falhar durante a instalação do Assistente de conector de saudação, há duas maneiras de motivo Olá tooview falha hello. Em Pesquisar no log de eventos de saudação em **aplicativos e serviços Logs\Microsoft\AadApplicationProxy\Connector\Admin**, ou Olá executar comando do Windows PowerShell a seguir:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Quando você encontrar um erro de conector Olá Olá do log de eventos, use esta tabela de problema de saudação de tooresolve erros comuns:

| Erro | Etapas recomendadas |
| ----- | ----------------- |
| Falha no registro do conector: Verifique se você habilitou o Proxy de aplicativo no Portal de gerenciamento de saudação e que você inseriu o nome de usuário do Active Directory e a senha corretamente. Erro: "ocorreram um ou mais erros”. | Se você fechou a janela de registro de saudação sem entrar no tooAzure AD, execute novamente o Assistente de conector hello e registre Olá conector. <br><br> Se a janela de registro de saudação abre e fecha imediatamente sem permitir que você toolog no, você provavelmente obterá este erro. Esse erro ocorre quando há algum erro de rede em seu sistema. Certifique-se de que é possível tooconnect de um site público do navegador tooa e se as portas de saudação estão abertas conforme especificado em [pré-requisitos do Proxy de aplicativo](active-directory-application-proxy-enable.md). |
| Apagar erro é apresentado na janela de registro de saudação. Não é possível continuar | Se você vir esse erro e, em seguida, fecha a janela de hello, você inseriu errado Olá de nome de usuário ou senha. Tente novamente. |
| Falha no registro do conector: Verifique se você habilitou o Proxy de aplicativo no Portal de gerenciamento de saudação e que você inseriu o nome de usuário do Active Directory e a senha corretamente. Erro: ' AADSTS50059: nenhuma informação de identificação de locatário encontrada em qualquer solicitação hello ou implícita por quaisquer fornecido as credenciais e pesquisa por serviço principal URI falhou. | Você está tentando toosign usando um Account da Microsoft e não um domínio que faz parte da ID de organização de saudação do diretório Olá tentar tooaccess. Certifique-se de que o administrador Olá faz parte da saudação mesmo nome de domínio como domínio de locatário hello, por exemplo, se o domínio de saudação do AD do Azure for contoso.com, Olá administrador deve ser admin@contoso.com. |
| Falha ao tooretrieve Olá política de execução atual para executar scripts do PowerShell. | Se Olá instalação do conector falhar, verifique toomake-se de que a política de execução do PowerShell não está desabilitada. <br><br>1. Olá abrir Editor de diretiva de grupo.<br>2. Vá muito**configuração do computador** > **modelos administrativos** > **componentes do Windows**  >   **O Windows PowerShell** e clique duas vezes em **ativar a execução do Script**.<br>3. é possível definir política de execução Olá tooeither **não configurado** ou **habilitado**. Se definir muito**habilitado**, certifique-se que em Opções, Olá política de execução é definido tooeither **permitir scripts locais e scripts remotos assinados** ou muito**permitir todos os scripts**. |
| Configuração de saudação toodownload falha no conector. | certificado do cliente do conector Hello, que é usado para autenticação, expirou. Isso também poderá ocorrer se você tiver Olá que Connector instalado atrás de um proxy. Nesse caso, hello conector não é possível acessar a saudação da Internet e não será capaz de tooprovide aplicativos tooremote os usuários. Renovar a relação de confiança manualmente usando Olá `Register-AppProxyConnector` cmdlet do Windows PowerShell. Se seu conector estiver atrás de um proxy, é necessário toogrant Internet acesso toohello conector contas "serviços de rede" e "sistema local". Isso pode ser feito ao conceder a eles acesso toohello Proxy ou definindo-los toobypass Olá proxy. |
| Falha no registro do conector: Verifique se você for um Administrador Global do seu Olá tooregister do Active Directory Connector. Erro: 'hello registro solicitação foi negada.' | alias de saudação com que estiver tentando toolog não é um administrador neste domínio. O conector é sempre instalado para diretório de saudação que possui o domínio do usuário hello. Certifique-se de que você está tentando toosign com conta de administrador do hello tem locatário de AD do Azure de toohello permissões globais. |

## <a name="kerberos-errors"></a>Erros de Kerberos

Esta tabela abrange hello mais comuns erros que vêm de Kerberos a instalação e configuração e também inclui sugestões para resolução.

| Erro | Etapas recomendadas |
| ----- | ----------------- |
| Falha ao tooretrieve Olá política de execução atual para executar scripts do PowerShell. | Se Olá instalação do conector falhar, verifique toomake-se de que a política de execução do PowerShell não está desabilitada.<br><br>1. Olá abrir Editor de diretiva de grupo.<br>2. Vá muito**configuração do computador** > **modelos administrativos** > **componentes do Windows**  >   **O Windows PowerShell** e clique duas vezes em **ativar a execução do Script**.<br>3. é possível definir política de execução Olá tooeither **não configurado** ou **habilitado**. Se definir muito**habilitado**, certifique-se que em Opções, Olá política de execução é definido tooeither **permitir scripts locais e scripts remotos assinados** ou muito**permitir todos os scripts**. |
| 12008 - azure AD excedido Olá número máximo de autenticação Kerberos permitidos tentativas toohello servidor de back-end. | Esse erro pode indicar uma configuração incorreta entre o Azure AD e Olá back-end servidor de aplicativos, ou um problema na configuração de data e hora nos dois computadores. servidor de back-end Olá recusou o tíquete de Kerberos de saudação criado pelo AD do Azure. Verifique se que o Azure AD e o servidor de aplicativos back-end Olá estão configurados corretamente. Certifique-se de que a configuração data e hora Olá Olá AD do Azure e o servidor de aplicativos de back-end de saudação são sincronizados. |
| 13016 - azure AD não pode recuperar um tíquete Kerberos em nome de usuário de saudação porque não há nenhum UPN no edge Olá token ou no cookie de acesso de saudação. | Há um problema com a configuração de STS hello. Corrigi a saudação de declaração de UPN configuração Olá STS. |
| 13019 - azure AD não pode recuperar um tíquete Kerberos em nome de usuário de saudação devido a saudação erro geral de API a seguir. | Esse evento pode indicar uma configuração incorreta entre o Azure AD e servidor do controlador de domínio hello, ou um problema na configuração de data e hora nos dois computadores. controlador de domínio de Olá recusou o tíquete do Kerberos Olá criado pelo AD do Azure. Verifique se que o Azure AD e servidor de aplicativos back-end Olá estão configurados corretamente, especialmente Olá SPN configuração. Certifique-se de saudação do AD do Azure é ingressado no domínio toohello mesmo domínio como Olá tooensure de controlador de domínio que Olá controlador de domínio estabelece a relação de confiança com o Azure AD. Certifique-se de que a configuração de data e hora de saudação em Olá AD do Azure e o controlador de domínio de saudação estão sincronizados. |
| 13020 - azure AD não pode recuperar um tíquete Kerberos em nome de usuário de saudação porque o servidor de back-end Olá SPN não está definido. | Esse evento pode indicar uma configuração incorreta entre o Azure AD e servidor do controlador de domínio hello, ou um problema na configuração de data e hora nos dois computadores. controlador de domínio de Olá recusou o tíquete do Kerberos Olá criado pelo AD do Azure. Verifique se que o Azure AD e servidor de aplicativos back-end Olá estão configurados corretamente, especialmente Olá SPN configuração. Certifique-se de saudação do AD do Azure é ingressado no domínio toohello mesmo domínio como Olá tooensure de controlador de domínio que Olá controlador de domínio estabelece a relação de confiança com o Azure AD. Certifique-se de que a configuração de data e hora de saudação em Olá AD do Azure e o controlador de domínio de saudação estão sincronizados. |
| 13022 - azure AD não pode autenticar o usuário Olá porque o servidor de back-end Olá responde tooKerberos tentativas de autenticação com um erro HTTP 401. | Esse evento pode indicar uma configuração incorreta entre o Azure AD e Olá back-end servidor de aplicativos, ou um problema na configuração de data e hora nos dois computadores. servidor de back-end Olá recusou o tíquete de Kerberos de saudação criado pelo AD do Azure. Verifique se que o Azure AD e o servidor de aplicativos back-end Olá estão configurados corretamente. Certifique-se de que a configuração data e hora Olá Olá AD do Azure e o servidor de aplicativos de back-end de saudação são sincronizados. |

## <a name="end-user-errors"></a>Erros de usuário final

Essa lista aborda os erros que os usuários finais podem encontrar quando eles tentam tooaccess Olá aplicativo e falham. 

| Erro | Etapas recomendadas |
| ----- | ----------------- |
| site de saudação não é possível exibir a página de saudação. | O usuário pode receber esse erro ao tentar tooaccess Olá aplicativo publicado se o aplicativo hello é um aplicativo de IWA. Olá definido SPN para este aplicativo pode estar incorreto. Para aplicativos IWA, certifique-se de que Olá SPN configurado para este aplicativo está correto. |
| site de saudação não é possível exibir a página de saudação. | O usuário pode receber esse erro ao tentar tooaccess Olá aplicativo publicado se o aplicativo hello é um aplicativo do OWA. Isso pode ser causado por um dos seguintes hello:<br><li>Olá definido o SPN para este aplicativo está incorreto. Certifique-se de que Olá SPN configurado para este aplicativo está correto.</li><li>usuário de saudação que a tentativa de aplicativo de hello tooaccess está usando uma conta da Microsoft em vez de hello toosign conta corporativa apropriada no ou usuário Olá é um usuário convidado. Certifique-se de que Olá usuário se autentica usando sua conta corporativa correspondências Olá domínio da saudação aplicativo publicado. Convidados e usuários de Conta da Microsoft não podem acessar aplicativos IWA.</li><li>usuário Olá que tentou aplicativo hello de tooaccess não está definido corretamente para esse aplicativo hello no lado local. Certifique-se de que esse usuário tem permissões adequadas Olá conforme definido para este aplicativo de back-end em Olá na máquina local. |
| Não foi possível acessar este aplicativo corporativo. Você são tooaccess não autorizadas deste aplicativo. Falha na autorização. Verifique se o usuário tooassign Olá com aplicativos de toothis de acesso. | Os usuários podem receber esse erro ao tentar tooaccess Olá aplicativo publicado se usarem contas da Microsoft em vez de toosign sua conta corporativa no. Os usuários convidados também podem receber esse erro. Convidados e usuários de Conta da Microsoft não podem acessar aplicativos IWA. Certifique-se de que Olá usuário se autentica usando sua conta corporativa correspondências Olá domínio da saudação aplicativo publicado.<br><br>Você não pode ter atribuído usuário Olá para este aplicativo. Vá toohello **aplicativo** guia e, em **usuários e grupos**, atribua esse usuário ou aplicativo de toothis de grupo do usuário. |
| Não foi possível acessar esse aplicativo corporativo no momento. Tente novamente mais tarde... conector Olá atingiu o tempo limite. | Os usuários podem receber esse erro ao tentar tooaccess Olá aplicativo publicado se eles não estão definidos corretamente para esse aplicativo hello no lado local. Certifique-se de que os usuários tenham as permissões adequadas Olá conforme definido para este aplicativo de back-end em Olá na máquina local. |
| Não foi possível acessar este aplicativo corporativo. Você são tooaccess não autorizadas deste aplicativo. Falha na autorização. Certifique-se de que o usuário Olá tem uma licença para o Azure Active Directory Premium ou Basic. | Os usuários podem receber esse erro ao tentar tooaccess Olá aplicativo publicado se eles não foram atribuídos explicitamente com uma licença Premium/básica pelo administrador do assinante hello. Vá do Active Directory do assinante toohello **licenças** guia e certifique-se de que este usuário ou grupo de usuários é atribuído uma licença Premium ou básica. |

## <a name="my-error-wasnt-listed-here"></a>Meu erro não estava listado aqui

Se você encontrar um erro ou problema com o Proxy de aplicativo do Azure AD que não está listado neste guia de solução de problemas, gostaríamos toohear sobre ele. Enviar um email tooour [equipe comentários](mailto:aadapfeedback@microsoft.com) com detalhes de saudação do erro Olá encontrou.

## <a name="see-also"></a>Consulte também
* [Habilitar o Proxy de Aplicativo para o Azure Active Directory](active-directory-application-proxy-enable.md)
* [Publique aplicativos com proxy de aplicativo](active-directory-application-proxy-publish.md)
* [Habilitar logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
