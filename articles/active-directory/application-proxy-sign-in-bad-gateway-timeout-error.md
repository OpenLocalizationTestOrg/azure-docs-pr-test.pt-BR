---
title: "AAA \"não pode acessar esse erro de aplicativo corporativo usando um aplicativo de Proxy de aplicativo | Microsoft Docs\""
description: Como acesso comuns tooresolve problemas com aplicativos de Proxy de aplicativo do Azure AD.
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 490b106b7d774ee43fc076cc5d082997a1df85e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cant-access-this-corporate-application-error-when-using-an-application-proxy-application"></a>Erro "Não é possível Acessar este Aplicativo Corporativo" ao usar um aplicativo de Proxy de Aplicativo

Este artigo ajuda tootroubleshoot problemas comuns que quando você vir um erro "Este aplicativo corporativo não pode ser acessado" em um aplicativo de Proxy de aplicativo do Azure AD.

## <a name="overview"></a>Visão geral
Quando você vir esse erro, a página Olá também compartilhar um código de status. Esse código é provavelmente uma das seguintes hello:

-   **Tempo limite do gateway**: Olá serviço Proxy de aplicativo é o conector de saudação do tooreach não é possível. Isso geralmente indica um problema com a atribuição de conector hello, conector em si ou Olá regras de conector de saudação do sistema de rede.

-   **Gateway incorreto**: conector Olá é o aplicativo de back-end hello tooreach não é possível. Isso pode indicar um erro de configuração de aplicativo hello.

-   **Proibido**: Olá usuário não está autorizado tooaccess Olá aplicativo. Isso pode acontecer quando o usuário Olá não está atribuído a toohello aplicativo no Azure Active Directory, ou se no back-end de Olá Olá usuário não tem aplicativo de hello tooaccess permissão.

código de saudação toofind, examine o texto de saudação na Olá inferior esquerda da mensagem de saudação do erro para o campo de "Código de Status" Olá. Além disso, procure as anotações final Olá muito Olá página com dicas adicionais.

   ![Erro de tempo limite de gateway](./media/application-proxy/connection-problem.png)

Para obter detalhes sobre como tootroubleshoot Olá causa desses erros e obter mais detalhes sobre as correções sugeridas, consulte Olá seção correspondente.

## <a name="gateway-timeout-errors"></a>Erros de Tempo limite de gateway

Um tempo limite de gateway ocorre quando o serviço Olá tenta tooreach conector de saudação e é a janela de tempo limite de saudação toowithin não é possível. Isso normalmente é causado por um aplicativo atribuído tooa grupo com nenhum trabalho conectores ou algumas portas exigidas pelo Olá conector não estiverem abertas.


## <a name="bad-gateway-errors"></a>Erros de gateway incorreto

Um erro de gateway incorreto indica que esse conector Olá é o aplicativo de back-end hello tooreach não é possível. Certifique-se de que você tenha publicado o aplicativo correto hello. Incorreções comuns que causam esse erro:

-   Um erro de digitação ou erro no URL interna Olá

-   Publicando não raiz de saudação do aplicativo hello. Por exemplo, publicação <http://expenses/reimbursement> mas tentando tooaccess <http://expenses>

-   Problemas de configuração de delegação restrita de Kerberos (KCD) Olá

-   Problemas com o aplicativo de back-end hello

## <a name="forbidden-errors"></a>Erros proibidos

Se você vir um erro proibido, usuário Olá não recebeu toohello aplicativo. Isso pode ser no Azure Active Directory ou no aplicativo de back-end hello.

toolearn como o aplicativo de toohello tooassign usuários no Azure, consulte Olá [documentação de configuração](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal#add-a-test-user).

Se você confirmar que o usuário Olá recebe toohello aplicativo no Azure, verifique a configuração de usuário Olá no aplicativo de back-end hello. Se você estiver usando Delegação Restrita de Kerberos/Autenticação Integrada do Windows, será possível ver nossa página Solucionar problemas de KCD para obter algumas diretrizes.

## <a name="check-hello-applications-internal-url"></a>Verifique a URL interna do aplicativo hello

Como uma primeira etapa rápida, verifique Verifique e corrija as URL interna Olá abrindo o aplicativo hello por meio de **aplicativos empresariais**, em seguida, selecionando Olá **Proxy de aplicativo** menu. Se que este é o URL de interno correto do hello, Olá usado do seu aplicativo de saudação do tooaccess de rede local.

## <a name="check-hello-application-is-assigned-tooa-working-connector-group"></a>Verifique o aplicativo hello recebe tooa conector de grupo de trabalho

aplicativo de hello tooverify recebe tooa conector de grupo de trabalho:

1.  Abra o aplicativo hello no portal de saudação indo muito**Active Directory do Azure**, clicando em **aplicativos empresariais**, em seguida, **todos os aplicativos.** Abra o aplicativo hello e selecione **Proxy de aplicativo** no menu esquerdo hello.

2.  Examine o campo de grupo de saudação. Se não há nenhum conector ativo no grupo de Olá, você verá um aviso. Se você não vir todos os avisos, passe muito "Verifique se todas as portas necessárias estão na lista de permissões".

3.  Se isso for Olá grupo errado, use Olá suspensa grupo correto do tooselect Olá e confirmar que você não verá mais todos os avisos. Se isso for Olá se destina a grupo, clique em página de Olá Olá aviso mensagem tooopen com o gerenciamento de conector.

4.  Aqui, há alguns toodrill maneiras em adicional:

  * Mover um conector para active para grupo de saudação: se você tiver um conector para active que deve pertencer toothis grupo e tem o aplicativo de back-end de destino de toohello de linha de visão, você pode mover Olá conector para o grupo Olá atribuído. toodo, clique em Olá conector. No campo de "Grupo" Olá, usar grupo correto do Olá Olá tooselect da lista suspensa e clique em Salvar.

  * Baixar um novo conector para esse grupo: nesta página, você pode obter o link de saudação muito[baixar um novo conector](https://download.msappproxy.net/Subscription/d3c8b69d-6bf7-42be-a529-3fe9c2e70c90/Connector/Download). necessidades de conector Olá toobe instalado em um computador com o aplicativo de back-end toohello linha direta de visão e geralmente é posicionado no hello mesmo servidor que o aplicativo hello. Olá Use baixar toodownload de link de conector um conector para o computador de destino de saudação. Em seguida, clique Olá conector e use hello "Grupo" suspensa toomake-se de que o grupo correto toohello pertence.

  * Investigar um conector inativo: se um conector mostra como inativo, é possível tooreach Olá serviço. Normalmente, isso é devido a toosome necessárias portas que estão sendo bloqueadas. toosolve esse problema, a mudança na muito "Verifique se todas as portas necessárias estão na lista de permissões".

Depois de usar essas etapas aplicativo hello de tooensure é grupo tooa atribuído ao trabalho conectores, aplicativo de saudação do teste novamente. Se ele ainda não está funcionando, continue toohello próxima seção.

## <a name="check-all-required-ports-are-whitelisted"></a>Verifique se todas as portas exigidas estão na lista de permissões

tooverify todas as necessárias portas estão abertas, consulte nossa documentação sobre a abertura de portas. Se todos os Olá portas necessárias estejam abertas, mova toohello próxima seção.

## <a name="check-for-other-connector-errors"></a>Verifique se há outros Erros de Conectores

Se nenhum dos Olá acima resolvê-Olá, Olá próxima etapa é toolook para problemas ou erros com hello conector em si. Você pode ver alguns erros comuns no hello [documento de solução de problemas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). 

Você também pode examinar diretamente Olá conector logs tooidentify erros. Muitas das nossas mensagens de erro ser capaz de tooshare recomendações mais específicas para correções. toolearn como logs de saudação tooview, consulte [nossa documentação de conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="additional-resolutions"></a>Resoluções Adicionais

Se Olá acima não corrigir o problema de hello, há algumas causas possíveis diferentes. problema de saudação tooidentify:

Se seu aplicativo for configurado toouse Windows IWA (autenticação integrada), teste Olá aplicativo sem logon único. Caso contrário, mova o parágrafo seguinte toohello. aplicativo de hello toocheck sem logon único, abra o aplicativo por meio de **aplicativos corporativos,** e vá toohello **Single Sign-On** menu. Saudação de alteração lista suspensa de "Autenticação integrada do Windows" muito "logon único do AD do Azure desabilitado". 

Agora, abra um navegador e tente o aplicativo de hello tooaccess novamente. Você deve ser solicitado para autenticação e entrar no aplicativo hello. Se isso funcionar, o problema de saudação é com a configuração de delegação restrita de Kerberos (KCD) Olá habilita logon único hello. Consulte a página de KCD solucionar problemas de saudação.

Se você continuar erro de saudação toosee, vá toohello máquina onde Olá Connector é instalado, abra um navegador e tente tooreach Olá URL interna usada para o aplicativo hello. Olá Connector atua como outro cliente de saudação mesma máquina. Se você não conseguir acessar o aplicativo hello, investigue por que a máquina seja aplicativo hello de tooreach não é possível, ou usar um conector em um servidor que é capaz de tooaccess Olá aplicativo.

Se você pode acessar o aplicativo hello dessa máquina, toolook para problemas ou erros com hello conector em si. Você pode ver alguns erros comuns no hello [documento de solução de problemas](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-troubleshoot#connector-errors). Você também pode examinar diretamente Olá conector logs tooidentify erros. Muitas das nossas mensagens de erro ser capaz de tooshare recomendações mais específicas para correções. toolearn como logs de saudação tooview, consulte [nossa documentação de conectores](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors#under-the-hood).

## <a name="next-steps"></a>Próximas etapas
[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
