---
title: 'Perguntas frequentes: SSPR do Azure AD | Microsoft Docs'
description: "Perguntas frequentes sobre o autoatendimento de redefinição de senha do Azure AD"
services: active-directory
keywords: "Gerenciamento de senhas do Active Directory, gerenciamento de senhas, autoatendimento de redefinição de senha do Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a>Perguntas frequentes sobre gerenciamento de senhas

Olá a seguir está algumas perguntas frequentes para tudo relacionado toopassword redefinir.

Se você tiver uma pergunta geral sobre o Azure AD e a senha de autoatendimento redefinição, que não foi respondida aqui, solicite comunidade Olá para obter assistência no hello [fóruns do Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD). Membros da comunidade Olá incluem engenheiros, gerentes de produto, MVPs e colega profissionais de TI.

Perguntas Frequentes é dividido em Olá seções a seguir:

* [**Perguntas sobre o registro de redefinição de senha**](#password-reset-registration)
* [**Perguntas sobre a redefinição de senha**](#password-reset)
* [**Perguntas sobre alteração de senha**](#password-change)
* [**Perguntas sobre relatórios de gerenciamento de senha**](#password-management-reports)
* [**Perguntas sobre o write-back de senha**](#password-writeback)

## <a name="password-reset-registration"></a>Registro de redefinição de senha
* **P: meus usuários podem registrar seus próprios dados de redefinição de senha?**

  > **R:** Sim, contanto que a redefinição de senha está habilitada e eles sejam licenciados, eles podem ir toohello portal de registro de redefinição de senha em http://aka.ms/ssprsetup tooregister suas informações de autenticação. Os usuários também podem registrar pelo painel de acesso vai toohello em http://myapps.microsoft.com, clicando em Guia do perfil hello e Olá registrar para a opção de redefinição de senha.
  >
  >
* **P: posso definir dados de redefinição de senha em nome dos meus usuários?**

  > **R:** Sim, você pode fazer isso com o Azure AD Connect, PowerShell, Olá [portal do Azure](https://portal.azure.com), ou o portal de administração do Office de hello. Para obter mais informações, consulte o artigo Olá [dados usados pelo Azure AD autoatendimento de redefinição de senha](active-directory-passwords-data.md).
  >
  >
* **P: posso sincronizar dados de perguntas de segurança do local?**

  > **R:** isso não é possível atualmente.
  >
  >
* **P: meus usuários podem registrar dados de forma que outros usuários não possam ver esses dados?**

  > **R:** Sim, quando os usuários registram dados usando Olá Portal redefinição de senha registro é salvo em campos de autenticação particulares que só são visíveis pelo usuário de administradores globais e hello.
    >
    > [!NOTE]
    > Se um **conta de administrador do Azure** registra o número de telefone de autenticação ele também é preenchido no campo de telefone celular hello e é visível.
    >
  >
  >
* **P: meus usuários tem toobe registrado antes que eles podem usar a redefinição de senha?**

  > **R:** não, se você definir informações de autenticação suficientes em seu nome, os usuários não têm tooregister. A redefinição de senha funciona enquanto você formatou corretamente os dados armazenados nos campos apropriados de saudação no diretório de saudação.
  >
  >
* **P: posso sincronizar ou definir campos de telefone de autenticação, Email de autenticação ou telefone de autenticação alternativo Olá em nome de meus usuários?**

  > **R:** isso não é possível atualmente.
  >
  >
* **P: como portal de registro Olá sabe quais opções tooshow meus usuários?**

  > **R:** portal de registro de redefinição de senha Olá somente mostra Olá opções que você habilitou para seus usuários. Essas opções são encontradas na seção de política de redefinição de senha de usuário da guia Configurar do diretório de saudação. Por exemplo, isso significa que se você não habilitar a perguntas de segurança, em seguida, os usuários não são tooregister possível para essa opção.
  >
  >
* **P: quando um usuário é considerado registrado?**

  > **R:** um usuário é considerado registrado para SSPR quando eles foram registrados pelo menos Olá **número de tooreset necessários métodos** que você definiu no hello [portal do Azure](https://portal.azure.com).
  >
  >
## <a name="password-reset"></a>Redefinição de senha
* **P: quanto tempo deve esperar tooreceive um email, SMS ou chamada telefônica da redefinição de senha?**

  > **R:** Email, mensagens SMS e chamadas telefônicas devem chegar em menos de um minuto, com o caso comum hello, sendo 5 a 20 segundos.
    >Se você não recebe a notificação de saudação nesse período de tempo:
        > * Verifique a pasta Lixo Eletrônico.
        > * Verifique o número de saudação ou email que está sendo contatado é hello um esperado.
        > * Verifique se os dados de autenticação Olá no diretório hello estão formatados corretamente.
                >     * Exemplo: “+1 4255551234” ou “user@contoso.com”
  >
  >
* **P: quais idiomas são compatíveis com a redefinição de senha?**

  > **R:** Olá IU de redefinição de senha, mensagens SMS e voz chamadas são localizadas no hello mesmos idiomas que têm suporte no Office 365.
  >
  >
* **Guia Configurar do p: quais partes da experiência de redefinição de senha Olá obtenham marcadas quando defino organizacional de identidade visual no meu diretório?**

  > **R:** Olá portal de redefinição de senha mostra o logotipo da sua organização e permite que você tooconfigure Olá entre em contato com seu email personalizado do administrador link toopoint tooa ou URL. Nenhum email que é enviado pela redefinição de senha inclui o logotipo da sua organização, cores, o nome no corpo de saudação do email Olá e personalizadas a partir do nome.
  >
  >
* **P: como eu posso instruir meus usuários sobre onde toogo tooreset suas senhas?**

  > **R:** toohttps://passwordreset.microsoftonline.com seus usuários podem ser enviados diretamente ou instruir Olá tooclick **não é possível acessar o link de conta** encontrado em qualquer página entrar ou de estudante. Você também pode publicar esses links no lugar tooyour facilmente acessível aos usuários.
  >
  >
* **P: posso usar essa página em um dispositivo móvel?**

  > **R:** sim, essa página funciona em dispositivos móveis.
  >
  >
* **P: há suporte para desbloqueio das contas locais do active directory quando os usuários redefinirem as suas senhas?**

  > **R:** Sim. Quando um usuário redefine a senha e o write-back de senha foi implantado usando o Azure AD Connect, a conta desse usuário é desbloqueada automaticamente quando ele redefine a senha.
  >
  >
* **P: como posso integrar a redefinição de senha diretamente à experiência de entrada na área de trabalho do usuário?**

  > **R:** se você for um cliente do Azure AD Premium, você pode instalar o Microsoft Identity Manager sem nenhum custo adicional e implantar Olá local senha redefinição solução toomeet esse requisito.
  >
  >
* **P: posso definir perguntas de segurança diferentes para diferentes localidades?**

  > **R:** isso não é possível atualmente.
  >
  >
* **P: quantas perguntas podemos configurar opção de autenticação de perguntas de segurança Olá?**

  > **R:** você pode configurar as perguntas de segurança personalizada too20 em Olá [portal do Azure](https://portal.azure.com).
  >
  >
* **P: qual o tamanho máximo das perguntas de segurança?**

  > **R:** as perguntas de segurança podem ter entre 3 e 200 caracteres.
  >
  >
* **P: quanto tempo podem ter as respostas toosecurity perguntas?**

  > **R:** respostas podem ser 3 too40 caracteres.
  >
  >
* **P: são rejeitadas respostas duplicadas toosecurity perguntas?**

  > **R:** Sim, rejeitamos respostas duplicadas toosecurity perguntas.
  >
  >
* **P: maio um registro de usuário Olá mesma pergunta de segurança mais de uma vez?**

  > **R:** Não. Quando um usuário registra uma pergunta específica, ele não pode se registrar nessa pergunta uma segunda vez.
  >
  >
* **P: é possível tooset um limite mínimo de perguntas de segurança para registro e redefinição?**

  > **R:** sim, um limite pode ser definido para o registro e outro para a redefinição. Podem ser necessárias de três a cinco perguntas de segurança para o registro e de três a cinco perguntas para a redefinição.
  >
  >
* **P: se um usuário tiver registrado mais do que o número máximo de saudação de tooreset necessário de perguntas, como perguntas de segurança são selecionadas durante a redefinição?**

  > **R:** segurança N perguntas são selecionadas aleatoriamente sem o número total de saudação de perguntas que um usuário tiver registrado, onde N é hello **número de tooreset necessário perguntas**. Por exemplo, se um usuário tiver 5 perguntas de segurança registradas, mas apenas 3 são necessário tooreset, 3 de saudação 5 são selecionado aleatoriamente e apresentadas na reinicialização. Se o usuário Olá obtém respostas Olá toohello perguntas errado, o processo de seleção de saudação ocorrer tooprevent hammering da pergunta.
  >
  >
* **P: vocês impedem os usuários de tentar redefinir a senha várias vezes em um curto período de tempo?**

  > **R:** Sim, há recursos de segurança incorporados tooprotect de redefinição de senha de uso indevido. Os usuários têm somente cinco tentativas de redefinição de senha em uma mesma hora antes de serem bloqueados por 24 horas. Os usuários somente podem experimentar toovalidate um número de telefone 5 vezes dentro de uma hora antes do bloqueio por 24 horas. Os usuários somente podem experimentar um único método de autenticação cinco vezes em uma mesma hora antes de serem bloqueados por 24 horas.
  >
  >
* **P: por quanto tempo são email hello e a senha de uso único de SMS válido?**

  > **R:** Olá a duração da sessão para redefinição de senha é 105 minutos. Operação de redefinição de senha do início de saudação do hello, usuário Olá tem 105 minutos tooreset sua senha. Hello email e senha de uso único de SMS são inválidos depois que esse período de tempo expira.
  >
  >

## <a name="password-change"></a>Alteração de senha
* **P: onde meus usuários deveríamos toochange suas senhas?**

  > **R:** os usuários podem alterar suas senhas em qualquer lugar, eles verão sua imagem do perfil ou ícone (como no canto superior direito de saudação do seu [Office 365](https://portal.office.com) ou [painel de acesso](https://myapps.microsoft.com) experiências. Os usuários podem alterar suas senhas da saudação [página de perfil do painel de acesso](https://account.activedirectory.windowsazure.com/r#/profile). Os usuários também podem ser solicitado toochange suas senhas automaticamente na tela de entrada hello AD do Azure se suas senhas expiradas. Por fim, os usuários podem navegar toohello [Portal de alteração de senha do AD do Azure](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) diretamente se desejarem toochange suas senhas.
  >
  >
* **P: meus usuários notificados no Portal do Office de hello quando sua senha local expira?**

  > **R:** hoje isso é possível se você estiver usando o AD FS, seguindo as instruções de saudação aqui: [enviar declarações de política de senha com o ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396). Se você está usando a sincronização de hash de senha, isso não é possível atualmente. Isso é porque nós não sincronizar as políticas de senha local, portanto, não é possível para que possamos experiências toopost toocloud de notificações de expiração. Em ambos os casos, também é possível muito[notificar os usuários cujas senhas estão sobre tooexpire usando PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).
  >
  >

## <a name="password-management-reports"></a>Relatórios de gerenciamento de senha
* **P: quanto tempo leva para tooshow dados backup nos relatórios de gerenciamento de senha Olá?**

  > **R:** dados devem ser exibidos nos relatórios de gerenciamento de senha hello dentro de 5 a 10 minutos. Ele algumas instâncias pode levar até tooan tooappear de hora.
  >
  >
* **P: como posso filtrar Olá relatórios de gerenciamento de senha?**

  > **R:** você pode filtrar relatórios de gerenciamento de senha Olá clicando Olá Lupa pequena toohello direita dos rótulos de coluna hello, superior de saudação do relatório de saudação. Se você quiser toodo de filtragem mais avançada, você pode baixar Olá relatório tooexcel-lo e criar uma tabela dinâmica.
  >
  >
* **P: qual é o número máximo de saudação de eventos são armazenados nos relatórios de gerenciamento de senha Olá?**

  > **R:** backup too75, 000 senha senha ou redefinição redefinição registro eventos são armazenados nos relatórios de gerenciamento de senha hello, abrangendo backup too30 dias.  Estamos trabalhando tooexpand esse número tooinclude mais eventos.
  >
  >
* **P: quanto vão Olá relatórios de gerenciamento de senha?**

  > **R:** relatórios de gerenciamento de senha Olá Mostrar operações que ocorrem dentro Olá últimos 30 dias. Por enquanto, se você precisar tooarchive dos dados, você pode baixar relatórios de saudação periodicamente e salvá-los em um local separado.
  >
  >
* **P: há um número máximo de linhas que podem ser exibidas nos relatórios de gerenciamento de senha Olá?**

  > **R:** Sim, um máximo de 75.000 linhas pode aparecer em qualquer um dos relatórios de gerenciamento de senha hello, se elas estão sendo mostradas no hello interface do usuário ou que estão sendo baixadas.
  >
  >
* **P: há uma API tooaccess Olá senha redefinição ou registro de dados de relatório?**

  > **R:** Sim, consulte Olá toolearn documentação a seguir como você pode acessar a senha Olá redefinir o fluxo de dados de relatório.  [Saiba como tooaccess de redefinição de senha relatar eventos programaticamente](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).
  >
  >

## <a name="password-writeback"></a>Write-back de senha
* **P: como funciona em segundo plano de saudação do Write-back de senha?**

  > **R:** consulte [como funciona o write-back de senha](active-directory-passwords-writeback.md) para obter uma explicação sobre o que acontece quando você habilita o write-back de senha e como os dados fluem pelo sistema Olá volta para seu ambiente local.
  >
  >
* **P: quanto tempo o write-back de senha leva toowork?  Há um atraso de sincronização como com a sincronização com hash de senha?**

  > **R:** o write-back de senha é instantâneo. É um pipeline síncrono que funciona de forma essencialmente diferente da sincronização com hash de senha. Write-back de senha permite aos usuários tooget de comentários em tempo real sobre o êxito de saudação de sua senha redefinir ou alterar a operação. tempo médio de saudação para um write-back bem-sucedido de uma senha é em 500 ms.
  >
  >
* **P: Se minha conta local estiver desabilitada, como minha conta ou meu acesso na nuvem será afetado?**

  > **R:** se sua ID de local estiver desabilitada, sua nuvem de ID/acesso também será desabilitado no próximo intervalo de sincronização Olá via conexão AAD byt padrão isso é a cada 30 minutos.
  >
  >
* **P: se a minha conta local é restrito por uma política de senha do Active Directory local, SSPR obedece a essa política ao alterar senha Olá?**

  > **R:** Sim, SSPR depende e age de acordo com hello a política de senha do AD, incluindo a política de senha de domínio de AD típica, bem como as políticas de senha refinada definido tooa dado de usuário de destino no local.
  >
  >
* **P: o write-back de senha funciona com quais tipos de conta?**

  > **R:** O write-back de senha funciona com usuários Federados e Sincronizados com Hash de Senha.
  >
  >
* **P: o write-back de senha impõe as políticas de senha do meu domínio?**

  > **R:** Sim, o write-back de senha impõe a duração, o histórico e a complexidade da senha, filtros e qualquer outra restrição que você possa impor nas senhas no domínio local.
  >
  >
* **P: o write-back de senha é seguro?  Como posso ter certeza de que não serei invadido por um hacker?**

  > **R:** Sim, o write-back de senha é seguro. tooread mais informações sobre camadas Olá quatro de segurança implementado pelo serviço de write-back de senha Olá, confira o hello [modelo de segurança de write-back de senha](active-directory-passwords-writeback.md#password-writeback-security-model) seção como funciona o write-back de senha.
  >
  >

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Política**](active-directory-passwords-policy.md) – entenda e defina políticas de senha do Azure AD
* [**Write-back de senha** ](active-directory-passwords-writeback.md) - Como o write-back de senha opera com o seu diretório local
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR
