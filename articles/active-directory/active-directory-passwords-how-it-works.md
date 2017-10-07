---
title: 'Aprofundamento: SSPR do Azure AD | Microsoft Docs'
description: "Aprofundamento no autoatendimento de redefinição de senha no Azure AD"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 618c5908-5bf6-4f0d-bf88-5168dfb28a88
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: c177192bbe69d179a25d174b06a0813ec28e2615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-password-reset-in-azure-ad-deep-dive"></a>Aprofundamento no autoatendimento de redefinição de senha no Azure AD

Como funciona o SSPR? O que essa opção significa na interface Olá? Continuar a ler toofind mais informações sobre a senha de autoatendimento do AD do Azure redefinir.

## <a name="how-does-hello-password-reset-portal-work"></a>Como a senha de saudação redefinir trabalho portal

Quando um usuário navega toohello portal de redefinição de senha, um fluxo de trabalho é iniciado toodetermine:

   * Como página Olá deve ser localizada
   * Conta de usuário de saudação é válido?
   * Qual organização o usuário Olá pertencem a?
   * Onde a senha do usuário Olá é gerenciada?
   * É Olá usuário licenciado toouse Olá recurso?


Ler Olá etapas abaixo toolearn sobre a lógica de saudação por trás da página de redefinição de senha hello.

1. O usuário clica Olá não pode acessar o link de conta ou vai diretamente muito[https://passwordreset.microsoftonline.com](https://passwordreset.microsoftonline.com).
2. Com base em Olá Olá de localidade do navegador experiência é renderizada no idioma adequado hello. Olá experiência de redefinição de senha está localizada em Olá mesmos idiomas que ofereça suporte a Office 365.
3. O usuário insere uma id de usuário e passa  por um captcha.
4. AD do Azure verifica se o usuário de saudação é capaz de toouse esse recurso fazendo Olá seguinte:
   * Verifica que o usuário Olá tem esse recurso habilitado e uma licença do AD do Azure atribuída.
     * Se o usuário Olá não tem esse recurso habilitado ou uma licença atribuída, usuário Olá é solicitado toocontact tooreset seu administrador sua senha.
   * Verifica que o usuário Olá tem dados de desafio direita Olá definidos na sua conta de acordo com a política do administrador.
     * Se a política exigir apenas um desafio, certifica-se que o usuário Olá tem dados de apropriado Olá definidos para pelo menos um dos desafios de saudação habilitados pela política do administrador de saudação.
       * Se o usuário de saudação não está configurado, Olá usuário é aconselhável toocontact tooreset seu administrador sua senha.
     * Se a política de saudação exigir dois desafios, certifica-se que o usuário Olá tem dados de apropriado Olá definidos para pelo menos duas das Olá desafios habilitados pela política do administrador de saudação.
       * Se usuário Olá não estiver configurado, podemos Olá usuário é aconselhável toocontact tooreset seu administrador sua senha.
   * Verifica se Olá a senha de usuário é gerenciada no local (federados ou sincronizados de hash de senha).
     * Se Write-back for implantado e Olá a senha de usuário é gerenciada no local, o usuário Olá é permitido tooproceed tooauthenticate e redefinir sua senha.
     * Se Write-back não é implantado e Olá a senha de usuário é gerenciada no local, o usuário Olá é solicitado toocontact tooreset seu administrador sua senha.
5. Se for determinado que o usuário Olá é capaz de toosuccessfully redefinir sua senha, Olá será guiado pelo processo de redefinição de saudação.

## <a name="authentication-methods"></a>Métodos de autenticação

Se a redefinição de senha de autoatendimento (SSPR) estiver habilitado, você deve selecionar pelo menos um dos Olá opções para métodos de autenticação a seguir. É altamente recomendável escolher pelo menos dois métodos de autenticação para que os usuários tenham mais flexibilidade.

* Email
* Telefone celular
* Telefone comercial
* Perguntas de segurança

### <a name="what-fields-are-used-in-hello-directory-for-authentication-data"></a>Quais campos são usados no diretório Olá para dados de autenticação

* Telefone comercial corresponde tooOffice telefone
    * Os usuários são tooset não é possível que esse campo se ele deve ser definido por um administrador
* Telefone celular corresponde tooeither telefone de autenticação (não visível publicamente) ou telefone celular (publicamente visível)
    * Olá serviço procura primeiro o telefone de autenticação, em seguida, reverterá tooMobile telefone se não apresentar
* Endereço de Email alternativo corresponde tooeither Email de autenticação (não visível publicamente) ou Email alternativo
    * serviço Olá procura por Email de autenticação pela primeira vez, em seguida, falha tooAlternate back Email

Por padrão, somente Olá atributos de nuvem telefone do escritório e telefone celular são sincronizados tooyour diretório na nuvem do seu diretório local para dados de autenticação.

Os usuários podem apenas redefinir sua senha se tiverem dados presentes nos métodos de autenticação Olá administrador Olá habilitada e requer.

Se os usuários não desejar seu toobe de número de telefone celular visível no diretório Olá mas prefere como toouse-lo para redefinição de senha, os administradores não devem preenchê-la no diretório hello e usuário hello, em seguida, preencha seus **telefone de autenticação**  atributo via Olá [portal de registro de redefinição de senha](http://aka.ms/ssprsetup). Os administradores podem ver essas informações no perfil do usuário hello, mas não é publicado em outro lugar. Se uma conta de administrador do Azure registra o número de telefone de autenticação, ele é preenchido no campo de telefone celular hello e é visível.

### <a name="number-of-authentication-methods-required"></a>Quantidade necessária de métodos de autenticação

Essa opção determina o número mínimo de saudação de métodos de autenticação disponíveis Olá um usuário deve passar pelo tooreset ou desbloquear sua senha e pode ser definido tooeither 1 ou 2.

Os usuários podem escolher toosupply mais métodos de autenticação se estiverem habilitados pelo administrador de saudação.

Se um usuário não tem métodos Olá mínimo necessário registrados, ele verá uma página de erro que direciona toorequest tooreset um administrador sua senha.

### <a name="how-secure-are-my-security-questions"></a>Qual o nível de segurança de minhas perguntas de segurança

Se você usar perguntas de segurança, recomendamos-los em uso com outro método como eles podem ser menos seguros do que outros métodos, pois algumas pessoas podem saber as respostas de saudação tooanother perguntas de usuários.

> [!NOTE] 
> Perguntas de segurança são armazenadas com segurança em particular em um objeto de usuário no diretório hello e só podem ser respondidas pelos usuários durante o registro. Não é possível para um administrador tooread ou modificar um usuário perguntas ou respostas.
>

### <a name="security-question-localization"></a>Localização das perguntas de segurança

Todas as perguntas predefinidas que seguem são localizadas em todo o conjunto de idiomas do Office 365 com base na localidade do navegador do usuário Olá Olá.

* Em qual cidade você conheceu seu primeiro cônjuge/parceiro?
* Em qual cidade seus pais se conheceram?
* Em qual cidade seu irmão mais próximo mora?
* Em qual cidade seu pai nasceu?
* Em qual cidade você teve seu primeiro emprego?
* Em qual cidade sua mãe nasceu?
* Em qual cidade você estava no ano de 2000?
* O que é o sobrenome de saudação de seu professor favorito no alto * escola?
* O que é o nome de saudação de uma faculdade à qual você aplicou toobut não frequentou?
* Qual é o nome de saudação do local de saudação em que você realizou sua primeira recepção de casamento?
* Qual é o segundo nome de seu pai?
* Qual é sua comida favorita?
* Qual é o nome e sobrenome de sua avó materna?
* Qual é o segundo nome de sua mãe?
* Qual é o mês e ano de aniversário de seu irmão mais velho? (por exemplo, novembro de 1985)
* Qual é o segundo nome de seu irmão mais velho?
* Qual é o nome e sobrenome de seu avô paterno?
* Qual é o segundo nome de seu irmão mais novo?
* Em qual escola você concluiu a sexta série?
* O que foi Olá primeiro nome e sobrenome de seu melhor amigo de infância?
* O que foi Olá primeiro nome e sobrenome de seu primeiro cônjuge?
* Qual foi o último o nome de seu professor favorito do ensino Olá?
* Qual era Olá marca e modelo do seu primeiro carro ou moto?
* O que é o nome de saudação da primeira escola de saudação em que você estudou?
* O que é o nome de saudação do hospital Olá em que você nasceu?
* O que é o nome de saudação da rua de saudação da primeira morou?
* O que é o nome de saudação de seu herói de infância?
* O que é o nome de saudação de seu animal de pelúcia?
* O que é o nome de saudação do seu primeiro animal de estimação?
* Qual era seu apelido de infância?
* Qual era seu esporte favorito no ensino médio?
* Qual foi seu primeiro emprego?
* O que foram Olá os quatro últimos dígitos de seu número de telefone de infância?
* Quando criança, o que você queria toobe quando crescesse?
* Quem é a pessoa mais famosa Olá que você já conheceu?

### <a name="custom-security-questions"></a>Perguntas de segurança personalizadas

As perguntas de segurança personalizadas não são localizadas para localidades diferentes. Todas as perguntas personalizadas são exibidas no hello mesmo idioma são inseridos na interface de usuário administrativo hello, mesmo se a localidade do navegador do usuário Olá é diferente. Se você precisar localizadas perguntas, use perguntas Olá predefinido.

comprimento máximo de saudação de uma pergunta de segurança personalizada é 200 caracteres.

### <a name="security-question-requirements"></a>Requisitos das perguntas de segurança

* O limite mínimo para a resposta é de 3 caracteres
* O limite máximo para a resposta é de 40 caracteres
* Os usuários não podem responder Olá mesma pergunta mais de uma vez
* Os usuários não podem fornecer Olá mesma resposta toomore que uma pergunta
* Qualquer conjunto de caracteres pode ser usado toodefine perguntas e respostas, incluindo caracteres Unicode
* número de saudação de perguntas definidas deve ser maior que ou igual a toohello inúmeros tooregister de perguntas necessárias

## <a name="registration"></a>Registro

### <a name="require-users-tooregister-when-signing-in"></a>Exigir usuários tooregister ao entrar

A habilitação dessa opção requer que um usuário que está habilitado para senha redefinir o registro de redefinição de senha toocomplete Olá se eles logon tooapplications usando toosign do AD do Azure em como as que seguem:

* Office 365
* Portal do Azure
* Painel de acesso
* Aplicativos federados
* Aplicativos personalizados que usam o Azure AD

Desabilitar este recurso ainda permitirá que os usuários toomanually registrar suas informações de contato visitando [http://aka.ms/ssprsetup](http://aka.ms/ssprsetup) ou clicando Olá **registrar para redefinição de senha** link em Olá guia perfil no painel de acesso de saudação.

> [!NOTE]
> Os usuários podem ignorar o portal de registro de redefinição de senha Olá clicando cancelar ou fechando a janela Olá, mas são solicitados sempre que eles logon até concluir o registro.
>

### <a name="number-of-days-before-users-are-asked-tooreconfirm-their-authentication-information"></a>Número de dias antes dos usuários frequentes tooreconfirm suas informações de autenticação

Essa opção determina o período de saudação de tempo entre a configuração e reconfirmando informações de autenticação e só estará disponível se você habilitar Olá **exigem tooregister usuários ao entrar** opção.

Os valores válidos são 0 e 730 dias com 0, que significa nunca perguntar usuários tooreconfirm suas informações de autenticação

## <a name="notifications"></a>Notificações

### <a name="notify-users-on-password-resets"></a>Notificar os usuários sobre as redefinições de senha

Se essa opção for definida tooyes, usuário de saudação que é redefinir sua senha recebe um email notificando que sua senha foi alterada por meio de saudação SSPR tootheir portal principal e endereços de email alternativo no arquivo no AD do Azure. Ninguém mais é notificado desse evento de redefinição.

### <a name="notify-all-admins-when-other-admins-reset-their-passwords"></a>Notificar todos os administradores quando outros administradores redefinirem suas senhas

Se essa opção for definida, em seguida, tooyes, **todos os administradores** receber um endereço de email principal do email tootheir no arquivo no AD do Azure, notificando que outro administrador alterou sua senha usando o SSPR.

Exemplo: Há quatro administradores em um ambiente. O administrador “A” redefine sua senha usando o SSPR. Os administradores B, C e D recebem um email avisando-os que isso está ocorrendo.

## <a name="on-premises-integration"></a>Integração local

Se você instalou, configurou e habilitou o Azure AD Connect, terá mais opções de integrações locais.

### <a name="write-back-passwords-tooyour-on-premises-directory"></a>Write-back de diretório de local de tooyour de senhas

Controla se o write-back de senha está habilitada ou não para este diretório e, se o write-back estiver ativado, indica o status de saudação do serviço de write-back local hello. Isso é útil se você quiser tootemporarily desabilitar Olá senha write-back sem configurar novamente a conexão do AD do Azure.

* Se o comutador hello é tooyes de conjunto de write-back estiver habilitado e federado e os usuários sincronizado de hash de senha será capaz de tooreset suas senhas.
* Se o comutador hello é toono de conjunto de write-back será desabilitado e federado e os usuários sincronizado de hash de senha não será capaz de tooreset suas senhas.

### <a name="allow-users-toounlock-accounts-without-resetting-their-password"></a>Permitir que os usuários toounlock contas sem redefinir sua senha

Designa se os usuários que visitam o portal de redefinição de senha Olá devem ser determinado Olá opção toounlock seu Active Directory no local de contas sem redefinir sua senha. Por padrão, o AD do Azure sempre desbloquear contas ao realizar uma redefinição de senha, essa configuração permite que você tooseparate essas duas operações. 

* Se definir muito "Sim", em seguida, os usuários serão Olá determinada opção tooreset sua senha e desbloquear conta hello, ou toounlock sem redefinir senha hello.
* Se definido muito "não", em seguida, os usuários só será capaz de tooperform uma redefinição de senha combinada e uma conta de operação de desbloqueio.

## <a name="network-requirements"></a>Requisitos de rede

### <a name="firewall-rules"></a>Regras de firewall

[Lista de URLs e endereços IP do Microsoft Office](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)

Para o Azure AD Connect versão 1.1.443.0 e posterior, você precisará de HTTPS de saída acesso toohello a seguir
* passwordreset.microsoftonline.com
* servicebus.windows.net

Para um acesso mais granular, você pode encontrar lista atualizada de saudação do Microsoft Azure Datacenter intervalos de IP que é atualizado toda quarta-feira e coloque o seguinte de saudação do efeito segunda-feira [aqui](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="idle-connection-timeouts"></a>Tempos limite de conexão ociosa

ferramenta do Hello Azure AD Connect envia pings/keepalives periódica tooServiceBus pontos de extremidade tooensure que conexões Olá permaneçam ativos. Ferramenta Olá deve detectar a que muitas conexões estão sendo eliminados, automaticamente aumentará a frequência de saudação do ponto de extremidade de toohello pings. Olá menor 'ping intervalos' descarta toois 1 ping a cada 60 segundos, no entanto, recomendamos enfaticamente que firewalls/proxies permite conexões ociosas toopersist de pelo menos 2 a 3 minutos. *Para versões mais antigas, sugerimos quatro minutos ou mais.

## <a name="active-directory-permissions"></a>Permissões do Active Directory

Olá conta especificada no utilitário do hello Azure AD Connect deve ter Redefinir senha, alterar a senha, permissões de gravação em lockoutTime e permissões de gravação em pwdLastSet, estendido direitos sobre o objeto raiz de saudação do **cada domínio** nessa floresta **ou** no usuário Olá UOs desejar toobe no escopo para SSPR.

Se você não tiver certeza de quais Olá de conta acima se refere a, abra hello Azure Active Directory Connect interface de configuração e clique em opção de configuração Olá exibição atual. conta de saudação que necessário tooadd toois de permissão listadas em "Diretórios sincronizados"

Definir essas permissões permite que a conta de serviço de MA Olá para senhas de toomanage cada floresta em nome de contas de usuário dentro dessa floresta. **Se você não tooassign essas permissões, em seguida, mesmo que o write-back aparece toobe configurado corretamente, os usuários encontram erros ao tentar toomanage suas senhas locais da nuvem de saudação.**

> [!NOTE]
> Pode levar até tooan horas ou mais desses objetos de tooall tooreplicate permissões em seu diretório.
>

tooset as permissões apropriadas Olá toooccur de write-back de senha

1. Abra usuários do Active Directory e computadores com uma conta que tenha permissões de administração de domínio apropriado Olá
2. No menu de exibição hello, certifique-se de que recursos avançados está ativado
3. No painel esquerdo do hello, clique no objeto de saudação que representa a raiz de saudação do domínio hello e escolha Propriedades
    * Guia de segurança do hello
    * Em seguida, clique em Avançado.
4. Na guia permissões de saudação, clique em Adicionar
5. Selecione conta Olá que permissões estão sendo aplicadas muito (da configuração de conexão do AD do Azure)
6. No hello aplica-se toodrop caixa suspensa, selecione objetos de usuário descendentes
7. Em permissões marque as caixas de saudação seguinte Olá
    * Unexpire-Password
    * Redefinir senha
    * Alterar senha
    * Gravar lockoutTime
    * Gravar pwdLastSet
8. Clique em Aplicar/Okey tooapply e saia de todas as caixas de diálogo Abrir.

## <a name="how-does-password-reset-work-for-b2b-users"></a>Como a redefinição de senha funciona para usuários B2B?
A redefinição e a alteração de senhas têm suporte completo em todas as configurações B2B.  Leia abaixo Olá três explícita B2B casos com suporte pela redefinição de senha.

1. **Os usuários de uma organização de parceiro com um locatário existente do AD do Azure** - se a organização de saudação são está em parceria com tem um locatário existente do AD do Azure, estamos **respeita quaisquer políticas de redefinição de senha estão habilitadas no locatário**. Para senha redefinir toowork, Olá parceiro organização necessidades apenas toomake se SSPR do AD do Azure está habilitado, que é sem custos adicionais para os clientes do O365, e pode ser habilitada, seguindo as etapas em Olá nosso [guia de Introdução ao gerenciamento de senhas ](https://azure.microsoft.com/documentation/articles/active-directory-passwords-getting-started/#enable-users-to-reset-or-change-their-aad-passwords) guia.
2. **Os usuários que se inscreveu usando [inscrição de autoatendimento](active-directory-self-service-signup.md)**  - se a organização Olá são está em parceria com usado Olá [inscrição de autoatendimento](active-directory-self-service-signup.md) tooget de recurso em um locatário, podemos deixá-los redefinido com email Olá registrados.
3. **Usuários de B2B** -novos usuários B2B criados usando Olá novo [recursos do Azure AD B2B](active-directory-b2b-what-is-azure-ad-b2b.md) também será capaz de tooreset suas senhas com email Olá eles registrados durante o processo de convite hello.

tootest isso, vá toohttp://passwordreset.microsoftonline.com com um desses usuários do parceiro. Desde que eles tenham um email alternativo ou um email de autenticação definido, a redefinição de senha funcionará como esperado.

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Política** ](active-directory-passwords-policy.md) - Como entender e definir políticas de senha do Azure AD
* [**Write-back de senha** ](active-directory-passwords-writeback.md) - Como o write-back de senha opera com o seu diretório local
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Perguntas frequentes**](active-directory-passwords-faq.md) – Como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

