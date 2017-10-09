---
title: aplicativo do autenticador aaaMicrosoft ajuda e suporte | Microsoft Docs
description: "Fornece uma lista de perguntas frequentes e respostas relacionadas toohello Microsoft Authentication aplicativo e autenticação multifator do Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Perguntas frequentes sobre o aplicativo Microsoft Authenticator

Este artigo responde as perguntas comuns que recebemos sobre o aplicativo do Microsoft Authenticator hello. Se você não vir uma pergunta com resposta tooyour, vá toohello [Fórum do aplicativo Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp). Também temos outra perguntas Frequentes sobre um recurso específico em aplicativo hello, [entrar com sua perguntas frequentes sobre o telefone](microsoft-authenticator-app-phone-signin-faq.md).

Olá Microsoft Authenticator aplicativo substituído aplicativo do Azure Authenticator hello e é Olá recomendado aplicativo quando você usa a autenticação multifator do Azure. Olá Microsoft Authenticator aplicativo está disponível para [do Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), e [IOS](http://go.microsoft.com/fwlink/?Linkid=825073).

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Quais são os códigos de saudação no aplicativo hello para? Por que o número de saudação Manter contagem regressiva?

Quando você abre o aplicativo do Microsoft Authenticator hello, você verá contas Olá que você adicionou e um número de seis ou oito dígitos por cada um deles. Você pode ver um temporizador de 30 segundos realizando uma contagem regressiva.

Esses códigos são usados quando você entrar na conta tooyour. Depois de você inserir seu nome de usuário e senha, você poderá ser solicitado tooenter um código de verificação. Abra Olá Microsoft Authenticator aplicativo e copie Olá código exibido atualmente. Digite esse código na toofinish de página de entrada hello.

Olá motivo códigos Olá é de alteração a cada 30 segundos para que você nunca use Olá mesmo código de duas vezes. Não é como uma senha que você deverá tooremember. Olá, trata que somente uma pessoa com o telefone de tooyour acesso conhece seu código de verificação.

códigos de saudação não exigem internet ou dados, para não ter tooworry sobre ter toosign do serviço de telefone em. Quando você fechar o aplicativo hello, ele não manter em execução no plano de fundo hello e ele não esgotar a bateria. Você pode fechar o aplicativo hello e ignorá-la até Olá próxima vez que você entrar.  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>Posso obter somente notificações quando houver Olá aplicativo abrir. Se o aplicativo hello não estiver aberto, não obtenho as notificações.

Se você obter notificações, mas eles não fazer ruído ou Vibrar apesar do toque de, primeiro verifique as configurações do aplicativo hello. Ativar o som de toouse aplicativo hello ou Vibrar com suas notificações.

Se você não receber notificações em todos os, verifique Olá casos a seguir:

- Seu telefone está no modo Silencioso ou Não Incomodar? Esse modo pode impedir que os aplicativos recebam notificações.
- Você consegue receber notificações em outros aplicativos? Caso contrário, pode haver um problema com conexões de rede de saudação em seu telefone ou canal de notificações de saudação do Android ou Apple. Você pode lidar com opção primeira Olá em suas configurações de telefone, mas talvez seja necessário tootalk tooyour provedor para obter ajuda com a segunda opção de saudação.
- Você pode receber notificações para algumas contas de aplicativo hello, mas não outras? Se Sim, remover conta problemática saudação do seu aplicativo e adicioná-lo novamente as notificações por push de tooenable. 

Se você tentou essas sugestões de solução de problemas, mas ainda está tendo problemas, envie-nos seus logs de diagnóstico. Ir toohello configurações do aplicativo, selecione **Ajuda & comentários** e **enviar logs de**. Em seguida, ir toohello [Fórum do aplicativo Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) e informe o problema que você está vendo e quais etapas você tentou até o momento. 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>Já estou usando Olá aplicativo Authenticator da Microsoft para códigos de verificação. Como alternar as notificações por push de clique tooone?
Aprovar uma entrada por meio da notificação por push só está disponível para contas pessoais da Microsoft ou para contas corporativas e de estudante da Microsoft, não para contas de terceiros como Google ou Facebook. Se você tiver um trabalho ou escola conta da Microsoft, sua organização poderá toodisable essa opção.

Se você usar uma conta da Microsoft para sua conta pessoal e deseja tooswitch pela toopush notificações, você precisa tooadd sua conta novamente. Registre novamente o dispositivo de saudação à sua conta e configurar notificações por push.  

Se você usar o Microsoft Authenticator para sua conta corporativa ou de estudante, sua organização decidir se tooallow notificações de um clique.

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>Notificações por push de um clique funcionam para contas que não são da Microsoft?
Não, as notificações por push só funcionam com contas da Microsoft e contas do Azure Active Directory. Se sua empresa ou escola usar as contas do Azure AD, elas poderão desabilitar esse recurso.  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>Eu restaurei meu dispositivo de um backup, e os códigos de minha conta estão ausentes ou não estão funcionando. O que aconteceu?
Para fins de segurança, nós não restauramos contas de backups de aplicativo.  Depois de restaurar o aplicativo hello, exclua as contas e adicioná-los novamente.

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>Eu tenho um novo dispositivo. Como remover o aplicativo do Microsoft Authenticator de saudação do meu dispositivo antigo e mover toohello um novo?
Adicionando Olá Microsoft Authenticator tooa novo dispositivo de aplicativo não removê-lo automaticamente de quaisquer outros dispositivos. toomanage quais dispositivos estão configurados para sua conta, visite Olá mesmo site que você usa a verificação de duas etapas toomanage e escolher tooremove aplicativos antigos.

Para contas pessoais da Microsoft, esse site é sua página de [segurança da conta](https://account.microsoft.com/security). Para contas da Microsoft corporativa ou de estudante, esse site pode ser [MyApps](https://myapps.microsoft.com) ou um portal personalizado que sua organização configurou.

### <a name="how-do-i-remove-an-account-from-hello-app"></a>Como remover uma conta do aplicativo hello?
* iOS: na tela principal de hello, passe o dedo deixado em um bloco de conta. Selecione **Excluir**.
* Windows Phone: Na tela principal de Olá, selecione botão de menu Olá, em seguida **editar contas**. Toque em Olá **X** próximo nome de conta de toohello.
* Android: Na tela principal de hello, selecione botão de menu Olá, em seguida, **editar contas**. Toque em Olá **X** próximo nome de conta de toohello.

Se você tiver um dispositivo que está registrado com a sua organização, talvez seja necessário toocomplete tooremove uma etapa extra em sua conta. Nesses dispositivos, Olá Microsoft Authenticator aplicativo é registrado automaticamente como um administrador do dispositivo. Se você quiser toocompletely desinstalação Olá aplicativo, será necessário toofirst cancelar o registro do aplicativo hello nas configurações de aplicativo hello.

### <a name="why-does-hello-app-request-so-many-permissions"></a>Por que o aplicativo hello solicitar permissões tantas?
Aqui está uma lista completa de permissões que pode pedir e como eles são usados no aplicativo hello. permissões específicas Hello, que você verá dependem do tipo hello de telefone que você tem.

* **Câmera**: podemos usar seus códigos de tooscan QR câmera quando você adicionar uma conta do trabalho, escola ou não-Microsoft.
* **Contatos e telefone**: quando você entrar com sua conta pessoal da Microsoft, tentamos toosimplify processo de saudação localizando contas existentes que você usa em seu telefone.
* **SMS**: quando você entrar com sua conta pessoal da Microsoft para Olá primeira vez, é necessário toomake-se de que seu correspondências de número de telefone Olá um temos no registro. Enviamos um telefone de toohello de mensagem de texto onde você baixou o aplicativo hello. mensagem contém um código de verificação de dígitos de 6 a 8. Em vez de solicitando que você toofind esse código e inseri-lo no aplicativo hello, achamos na mensagem de saudação do texto para você.
* **Desenha sobre outros aplicativos**: quando você receber uma notificação tooverify sua identidade, podemos exibir notificação sobre qualquer outro aplicativo pode estar em execução.
* **Receber dados de saudação internet**: essa permissão é necessária para enviar notificações.
* **Impedir que o telefone entre em suspensão**: se você registrar seu dispositivo com sua organização, eles podem alterar essa política em seu telefone.
* **Controlar vibração**: você pode escolher se deseja uma vibração sempre que você receber uma notificação tooverify sua identidade.
* **Usar o hardware de impressão digital**: algumas contas corporativas e de estudantes exigem um PIN adicional sempre que você verifica sua identidade. processo de saudação toomake mais fácil, permitimos que você toouse sua impressão digital em vez de inserir Olá PIN.
* **Exibir conexões de rede**: quando você adiciona uma conta da Microsoft, o aplicativo hello requer conexão de rede/internet.
* **Ler o conteúdo de saudação do seu armazenamento**: essa permissão é usada somente quando você relata um problema técnico por meio de configurações do aplicativo hello. Algumas informações de seu armazenamento são coletadas toodiagnose problema de saudação.
* **Acesso de rede completo**: essa permissão é necessária para enviar notificações tooverify sua identidade.
* **Executar na inicialização**: se você reiniciar seu telefone, essa permissão garante que você continue a receber notificações tooverify sua identidade.

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>Por que Olá aplicativo autenticador da Microsoft permite que você tooapprove uma solicitação sem o dispositivo de desbloqueio Olá?

Você não tem toounlock que a verificação de tooapprove dispositivo solicita porque você só precisa tooprove é que você tenha seu telefone com você. A verificação em duas etapas exige a comprovação de duas coisas — algo que você sabe e algo que você tem. coisa Olá que você saber é a senha. Olá que é seu telefone (configurado com o aplicativo do Microsoft Authenticator hello e registrado como uma prova de MFA). Portanto, ter phone hello e aprovação de solicitação de saudação atende Olá critérios para o segundo fator Olá de autenticação. 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>O que significa o ícone de cadeado Olá na lista de contas Olá?

ícone de cadeado Olá indica dispositivo Olá é registrado no AD do Azure e registradas toohello conta. O registro de dispositivo para o iOS ocorre durante o registro do Microsoft Intune.

## <a name="next-steps"></a>Próximas etapas

### <a name="contact-us"></a>Fale conosco
Se sua pergunta não foi respondida aqui, queremos toohear por você. Vá toohello [Fórum do aplicativo Microsoft Authenticator](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp) toopost sua pergunta e obter ajuda da comunidade hello, ou deixam um comentário nesta página.


### <a name="related-topics"></a>Tópicos relacionados
* [Sobre a verificação em duas etapas](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification) da conta da Microsoft
* [Está com dificuldades com a verificação de duas etapas](multi-factor-authentication-end-user-troubleshoot.md) para sua conta corporativa ou de estudante?
* [Usar toosign de Microsoft Authenticator Olá em seu telefone](microsoft-authenticator-app-phone-signin-faq.md)

