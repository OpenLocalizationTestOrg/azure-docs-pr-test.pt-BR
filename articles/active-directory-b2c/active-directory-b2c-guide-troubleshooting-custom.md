---
title: "Azure Active Directory B2C: solucionar problemas de políticas personalizadas | Microsoft Docs"
description: "Saiba mais sobre as abordagens toosolving erros ao trabalhar com políticas personalizadas no Active Directory do Azure."
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: joroja
ms.openlocfilehash: b9e1b46df1ddb29cdb90953e4a0d6f1dd085441f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-ad-b2c-custom-policies-and-identity-experience-framework"></a>Solucionar problemas de políticas personalizadas do Azure AD B2C e da Estrutura de Experiência de Identidade

Se você usar o Azure Active Directory B2C (Azure AD B2C) de políticas personalizadas, você pode experimentar desafios Configurando Olá a estrutura de experiência de identidade em seu formato XML de idioma de política.  Políticas personalizadas de toowrite de aprendizado podem ser como uma nova linguagem de aprendizado. Neste artigo, descreveremos ferramentas e dicas que podem ajudar a identificar e resolver problemas. 

> [!NOTE]
> Este artigo concentra-se na solução de problemas da configuração de política personalizada do Azure AD B2C. Ele não aborda Olá terceira o aplicativo de terceiros ou sua biblioteca de identidade.

## <a name="xml-editing"></a>Edição de XML

Olá erro mais comuns na configuração de políticas personalizadas está incorretamente formatado XML. Um bom editor de XML é praticamente essencial. Um bom editor de XML exibe XML nativamente, codifica o conteúdo por cor, preenche os termos comuns com antecedência, mantém os elementos XML indexados e pode validar no esquema. Aqui estão dois dos nossos editores de XML favoritos:

* [Visual Studio Code](https://code.visualstudio.com/)
* [Bloco de Notas++](https://notepad-plus-plus.org/)

A validação de esquema XML identifica os erros antes do upload do arquivo XML. Na pasta raiz de saudação do pacote de inicializador Olá, obter a definição de esquema XML Olá TrustFrameworkPolicy_0.3.0.0.xsd. Para obter mais informações, na documentação de saudação do seu editor XML, procure *ferramentas XML* e *validação de XML*.

Talvez seja útil examinar as regras de XML. O Azure AD B2C rejeita qualquer erro de formatação de XML que detecta. Ocasionalmente, um XML formatado incorretamente pode causar mensagens de erros falsos.

## <a name="upload-policies-and-policy-validation"></a>Políticas de upload e validação de política

 A validação de upload de arquivo XML é automática. A maioria dos erros causar Olá toofail de carregamento. Validação inclui o arquivo de política de saudação que você está carregando. Ele também inclui a cadeia de saudação de arquivos de arquivo de carregamento da saudação refere-se muito (Olá o arquivo de política de terceira parte confiável, o arquivo de extensões de hello e o arquivo base Olá). 
 
 Erros de validação comuns incluem o seguinte hello.

Trecho de código de erro: `... makes a reference tooClaimType with id "displaName" but neither hello policy nor any of its base policies contain such an element`
* Olá ClaimType valor pode estar incorreto ou não existe no esquema de saudação.
* ClaimType valores devem ser definidos em pelo menos um dos arquivos de saudação na política de saudação. 
    Por exemplo: ` <ClaimType Id="socialIdpUserId">`
* Se ClaimType está definida no arquivo de extensões de saudação, mas ele também é usado em um valor de TechnicalProfile no arquivo de base Olá, carregamento de arquivo base Olá resulta em um erro.

Trecho de código de erro: `...makes a reference tooa ClaimsTransformation with id...`
* Olá causas para erro Olá pode ser Olá mesmo para erro de ClaimType hello.

Trecho de código de erro: `Reason: User is currently logged as a user of 'yourtenant.onmicrosoft.com' tenant. In order toomanage 'yourtenant.onmicrosoft.com', please login as a user of 'yourtenant.onmicrosoft.com' tenant`
* Verificar esse valor de TenantId em Olá Olá  **\<TrustFrameworkPolicy\>**  e  **\<BasePolicy\>**  elementos correspondem o destino do Azure AD B2C locatário.  

## <a name="troubleshoot-hello-runtime"></a>Solucionar problemas de tempo de execução de saudação

* Use `Run Now` e `https://jwt.io` tootest suas políticas independentemente de sua web ou aplicativo móvel. Este site funciona como um aplicativo de terceira parte confiável. Ele exibe conteúdo Olá Olá JSON Web Token (JWT) que é gerada pela sua política do Azure AD B2C. toocreate um aplicativo de teste na estrutura de experiência de identidade, use Olá valores a seguir:
    * Nome: TestApp
    * Aplicativo Web/API Web: não
    * Cliente nativo: Não

* troca de saudação do tootrace de mensagens entre o navegador do cliente e o Azure AD B2C, use [Fiddler](http://www.telerik.com/fiddler). Ele pode ajudá-lo a obter uma indicação de onde sua jornada de usuário está falhando nas etapas de orquestração.

* Em **modo de desenvolvimento**, use **Application Insights** tootrace atividade de saudação de sua jornada de usuário do Framework de experiência de identidade. Em **modo de desenvolvimento**, você pode observar o intercâmbio de saudação de declarações entre hello Framework de experiência de identidade e hello vários provedores de declarações que são definidos por perfis de técnicos, como provedores de identidade, serviços baseados na API diretório de usuário de saudação do Azure AD B2C e outros serviços, como o Azure Multi-Factor-Authentication.  

## <a name="recommended-practices"></a>Práticas recomendadas

**Mantenha várias versões de seus cenários. Agrupe-os em um projeto com seu aplicativo.** Olá base, extensões e arquivos de terceira parte confiável são diretamente dependentes entre si. Salve-os como um grupo. À medida que novos recursos são adicionados tooyour políticas, manter versões separadas de trabalho. Versões de trabalho do estágio em seu próprio arquivo de sistema com eles interagem com o código do aplicativo hello.  Os aplicativos podem invocar várias políticas de terceira parte confiável diferentes em um locatário. Eles podem se tornar dependentes Olá declarações que esperam de suas políticas do Azure AD B2C.

**Desenvolver e testar perfis técnicos com jornadas de usuário conhecidas.** Use starter testado pacote políticas tooset seus perfis técnica. Teste-as separadamente antes de incorporá-las em suas próprias jornadas de usuário.

**Desenvolva e teste jornadas de usuário com perfis técnicos testados.** Altere etapas de orquestração de saudação da jornada de um usuário incrementalmente. Crie os seus cenários desejados de forma progressiva.

## <a name="next-steps"></a>Próximas etapas

* No GitHub, baixe o arquivo de arquivos. zip (https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/archive/master.zip) [active-directory-b2c-custom-policy-starterpack] de saudação.
