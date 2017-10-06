---
title: "Azure Active Directory B2C: Políticas personalizadas | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: Políticas personalizadas

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>O que são políticas personalizadas?

Políticas personalizadas são arquivos de configuração que definem o comportamento de saudação do seu locatário do Azure AD B2C. Enquanto **políticas internas** são predefinidas no portal de saudação do Azure AD B2C para hello tarefas mais comuns de identidade, as políticas personalizadas podem ser totalmente editado por um toocomplete do desenvolvedor de identidade um próximo número ilimitado de tarefas. Leitura toodetermine se políticas personalizadas são ideal para você e seu cenário de identidade.

**A edição da política personalizada não se destina a todas as pessoas.** Olá curva de aprendizado é mais exigentes, Olá inicialização mais tempo, e políticas de toocustom alterações futuras exigirá toomaintain de experiência semelhante. As políticas internas devem ser cuidadosamente consideradas primeiro para o cenário antes do uso de políticas personalizadas.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Comparando políticas internas e personalizadas

| | Políticas internas | Políticas personalizadas |
|-|-------------------|-----------------|
|Usuários de destino | Todos os desenvolvedores de aplicativos com ou sem conhecimentos sobre identidade | Profissionais de identidade: integradores de sistemas, consultores e equipes internas de identidade. Estão familiarizados com fluxos do OpenIDConnect e têm conhecimento sobre a autenticação baseada em declarações e os provedores de identidade |
|Método de configuração | Portal do Azure com uma interface do usuário amigável | Editar diretamente os arquivos XML e, em seguida, carregar toohello portal do Azure |
|Personalização da interface do usuário | Personalização completa da interface do usuário, incluindo suporte a HTML, CSS e jscript (exige um domínio personalizado)<br><br>Suporte a várias linguagens com cadeias de caracteres Personalizadas | Idêntico |
| Personalização de atributos | Atributos padrão e personalizados | Idêntico |
|Gerenciamento de tokens e sessões | Token personalizado e opções de várias sessões | Idêntico |
|Provedores de Identidade| **Hoje**: provedor social e local predefinido<br><br>**Futuro**: OIDC baseado em padrões, SAML, OAuth | **Hoje**: OIDC baseado em padrões, OAUTH, SAML<br><br>**Futuro**: WsFed |
|Tarefas de identidade (exemplos) | Inscrever-se ou entrar com contas locais e várias contas sociais<br><br>Redefinição de senha de autoatendimento<br><br>Edição de perfil<br><br>Cenários de Autenticação Multifator<br><br>Personalizar tokens e sessões<br><br>Acessar fluxos de token | Concluir Olá mesmo tarefas como as políticas internas usando provedores de identidade personalizado ou usar escopos personalizados<br><br>Provisionar o usuário em outro sistema no tempo de saudação do registro<br><br>Enviar um email de boas-vindas usando seu próprio provedor de serviços de email<br><br>Usar um repositório de usuários fora do B2C<br><br>Validar as informações fornecidas pelo usuário com um sistema confiável por meio da API |

## <a name="policy-files"></a>Arquivos de política

Uma política personalizada é representada como um ou vários arquivos de formato XML que se referem a tooeach em uma cadeia hierárquica. definem os elementos XML Olá: declarações de esquema de declarações, transformações, definições de conteúdo, perfis de provedores/técnico de declarações e as etapas da orquestração de Userjourney, entre outros elementos.

Recomendamos o uso de saudação dos três tipos de arquivos de política:

- **Um arquivo de BASE**, que contém a maioria das definições de saudação e para qual Azure fornece um exemplo completo.  É recomendável que fazer um número mínimo de alterações toothis arquivo toohelp na solução de problemas e manutenção de longo prazo das suas políticas
- **um arquivo de extensões** que contém as alterações de configuração exclusivas Olá para seu locatário
- **um arquivo de terceira parte confiável (RP)** Olá única tarefa determinada arquivo que é invocado diretamente pelo aplicativo hello ou serviço (também conhecido como terceira parte confiável).  Leia o artigo Olá nas definições do arquivo de política para obter mais informações.  Cada tarefa exclusiva requer seu próprio RP e dependendo de requisitos de marca número Olá pode ser "total de aplicativos x número total de casos de uso".


Políticas internas no Azure AD B2C seguem o padrão de 3-arquivo de saudação descrito acima, mas o desenvolvedor Olá somente vê Olá arquivo da terceira parte confiável (RP), enquanto o portal de saudação faz alterações no arquivo de EXTenstions de toohello de plano de fundo de saudação.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Conceitos fundamentais que você deve saber ao usar políticas personalizadas

### <a name="azure-active-directory-b2c"></a>Active Directory B2C do Azure

Serviço de CIAM (gerenciamento de identidades e acessos do cliente) do Azure. o serviço de saudação inclui:

1. Um diretório de usuário na forma de saudação de uma finalidade especial do Azure Active Directory acessível por meio do Microsoft Graph e que mantém os dados de usuário para as contas locais e contas federadas 
2. Acessar toohello **identidade experiência Framework** que coordena a relação de confiança entre usuários e entidades e passa declarações entre eles toocomplete uma tarefa de gerenciamento de acesso e identidade 
3. Um serviço de token segurança (STS) emitir id tokens, atualização de tokens e acesso tokens (e declarações de SAML equivalentes) e validá-las tooprotect recursos.

B2C do Azure AD interage com outros sistemas, usuários, provedores de identidade e com o diretório de usuário local Olá na sequência tooachieve uma tarefa de identidade (por exemplo, logon de um usuário, registrar um novo usuário, redefinir uma senha). Olá plataforma subjacente que estabelece a relação de confiança de várias partes e executa essas etapas é chamada hello Framework de experiência de identidade e uma política (também chamado de jornada de um usuário ou uma política de estrutura de relação de confiança) define explicitamente atores hello, ações de Olá Olá protocolos e Olá sequência de etapas toocomplete.

### <a name="identity-experience-framework"></a>Identity Experience Framework

Uma plataforma Azure totalmente configurável, orientada por política e baseada em nuvem que orquestra a relação de confiança entre entidades (amplamente, Provedores de Declarações) nos formatos de protocolo padrão, como OpenIDConnect, OAuth, SAML, WSFed e alguns não padrão (por exemplo, trocas de declarações entre sistemas baseadas na API REST). Olá I2E cria amigável, whitelabelled experiências que oferecem suporte a HTML, CSS e jscript.  Hoje, Olá identidade experiência Framework está disponível apenas no contexto de saudação do hello serviço do Azure AD B2C e priorizadas para tooCIAM de tarefas relacionadas.

### <a name="built-in-policies"></a>Políticas internas

Arquivos de configuração que comportamento Olá direta da identidade do Azure AD B2C tooperform hello mais comumente usada tarefas (por exemplo, o registro de usuário, entrar, redefinição de senha) e interagir com partes confiáveis cuja relação também é predefinida no Azure AD B2C (de predefinidos Por exemplo, Facebook provedor de identidade, LinkedIn, Account da Microsoft, contas do Google).  Em Olá futuras, políticas internas também podem fornecer para personalização de provedores de identidade que são normalmente no realm do enterprise hello como Azure Active Directory Premium do Active Directory/ADFS, equipe de vendas da ID do provedor etc.


### <a name="custom-policies"></a>Políticas personalizadas

Arquivos de configuração que definem o comportamento de saudação do Framework de experiência de identidade em seu locatário do Azure AD B2C. Uma política personalizada é acessível como um ou vários arquivos XML (consulte as definições de política de arquivos) que são executados pelo saudação do Framework de experiência de identidade quando invocado por uma terceira parte confiável (por exemplo, um aplicativo). Políticas personalizadas podem ser editados diretamente por um toocomplete do desenvolvedor de identidade um próximo número ilimitado de tarefas. Desenvolvedores devem definir a configuração de políticas personalizadas Olá relações de confiança em pontos de extremidade de metadados de tooinclude detalhes cuidado, declarações exatas definições do exchange e configure segredos de certificados e chaves conforme necessário para cada provedor de identidade.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Definições de arquivo de política para Trustframeworks da Estrutura de Experiência de Identidade

### <a name="policy-files"></a>Arquivos de Política

Uma política personalizada é representada como um ou vários arquivos de formato XML que se referem a tooeach em uma cadeia hierárquica. definem os elementos XML Olá: declarações de esquema de declarações, transformações, definições de conteúdo, perfis de provedores/técnico de declarações e as etapas da orquestração de Userjourney, entre outros elementos.  Recomendamos o uso de saudação dos três tipos de arquivos de política:

- **Um arquivo de BASE**, que contém a maioria das definições de saudação e para qual Azure fornece um exemplo completo.  É recomendável que fazer um número mínimo de alterações toothis arquivo toohelp na solução de problemas e manutenção de longo prazo das suas políticas
- **um arquivo de extensões** que contém as alterações de configuração exclusivas Olá para seu locatário
- **um arquivo de terceira parte confiável (RP)** Olá única tarefa determinada arquivo que é invocado diretamente pelo aplicativo hello ou serviço (também conhecido como terceira parte confiável).  Leia o artigo Olá nas definições do arquivo de política para obter mais informações.  Cada tarefa exclusiva requer seu próprio RP e dependendo de requisitos de marca número Olá pode ser "total de aplicativos x número total de casos de uso".

![Tipos de arquivo de política](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| Tipo de arquivo de política | Nome de arquivo de exemplo | Uso recomendado | É herdado de |
|---------------------|--------------------|-----------------|---------------|
| BASE |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_BASE1.xml | Inclui esquema de declarações principal hello, transformação de declarações, provedores de declarações e Jornadas de usuário definidas pela Microsoft<br><br>Fazer alterações mínimas toothis arquivo | Nenhum |
| Extensão (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com-B2C-1A_EXT.xml | Consolidar sua alterações toohello BASE arquivo aqui<br><br>Provedores de declarações modificados<br><br>Percursos do usuário modificados<br><br>Suas próprias definições de esquema personalizadas | Arquivo BASE |
| RP (Terceira Parte Confiável) | B2C_1A_sign_up_sign_in.xml| Altere as configurações de forma e sessão do token aqui| Arquivo Extensions(EXT) |

### <a name="inheritance-model"></a>Modelo de herança

Quando um aplicativo chama o arquivo de política de RP Olá, Olá Identity Framework de experiência em B2C adicionar todos os elementos de saudação de BASE e de extensões e por fim de tooassemble de arquivo de política RP Olá Olá em vigor política atual.  Elementos de saudação mesmo tipo e nome no arquivo RP Olá substituirão as que estão Olá extensões e substituições de extensões BASE.

**Políticas internas** no Azure AD B2C seguem o padrão de 3-arquivo de saudação descrito acima, mas o desenvolvedor Olá somente vê Olá arquivo da terceira parte confiável (RP), enquanto o portal de saudação faz alterações no arquivo de EXTenstions de toohello de plano de fundo de saudação.  Todos os Azure AD B2C compartilha um arquivo de política BASE que está sob controle de saudação da equipe Olá B2C do Azure e é atualizado com frequência.
