---
title: "Azure Active Directory B2C: Uso da personalização de idiomas | Microsoft Docs"
description: 
services: active-directory-b2c
documentationcenter: 
author: sama
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: sama
ms.openlocfilehash: a8e4037014f5adf929dac7b5dc4db72ba0f5b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-using-language-customization"></a>Azure Active Directory B2C: uso da personalização de idiomas

>[!NOTE] 
>Esse recurso está em uma versão prévia.  Recomendamos que você use um locatário de teste ao usar esse recurso.  Não pretendemos quaisquer alterações de versão de disponibilidade geral do hello visualização toohello quebra, mas reservamos toomake direita Olá recursos alterações tooimprove hello.  Depois de ter um recurso de tootry chance, forneça comentários sobre suas experiências e como podemos-lo melhor.  Você pode fornecer comentários por meio do portal do Azure de saudação com a ferramenta de rosto feliz Olá na parte superior de saudação à direita.   Se houver um requisito comercial para você toogo ao vivo usando esse recurso durante a fase de visualização hello, nos informar seus cenários e pode fornecer assistência e orientação adequada hello.  Você pode em contato conosco em [aadb2cpreview@microsoft.com](mailto:aadb2cpreview@microsoft.com).

Personalização de idioma permite que você toochange seu usuário jornada tooa toosuit de idioma diferentes necessidades do seu cliente.  Podemos fornecer traduções para 36 idiomas (consulte [Informações adicionais](#additional-information)).  Mesmo que sua experiência é fornecida somente para um único idioma, você pode personalizar qualquer texto no hello páginas toosuit suas necessidades.  

## <a name="how-does-language-customization-work"></a>Como funciona a personalização de idiomas?
Personalização de idioma permite que você tooselect quais idiomas sua jornada de usuário está disponível no.  Quando Olá recurso estiver habilitado, você pode fornecer o parâmetro de cadeia de caracteres de consulta hello, ui_locales, do seu aplicativo.  Quando você chama B2C do Azure AD, podemos chegar sua localidade toohello de página que você indicou.  Usar o tipo de configuração lhe dá controle total sobre idiomas de saudação em sua jornada de usuário e ignora as configurações de idioma de saudação do navegador saudação do cliente. Como alternativa, você talvez não precise desse nível de controle sobre quais idiomas o seu cliente vê.  Se você não fornecer um parâmetro ui_locales, experiência saudação do cliente é determinada pelas configurações do seu navegador.  Você ainda pode controlar quais idiomas sua jornada de usuário é convertida tooby adicioná-lo como um idioma com suporte.  Se o navegador do cliente é set tooshow um idioma você não quer toosupport, em seguida, idioma Olá selecionado como um padrão de culturas com suporte é mostrado em vez disso.

1. **idioma de localidades de interface do usuário especificado** -depois de habilitar personalização de idioma, sua jornada de usuário é o idioma traduzido toohello especificado aqui
2. **Navegador solicitou o idioma** -se nenhuma interface do usuário-localidades foi especificado, ele converte toohello navegador solicitou o idioma, **se ele foi incluído nos idiomas com suporte**
3. **Idioma padrão de política** -se navegador Olá não especifica um idioma ou especifica que não tem suporte, ele converte o idioma do toohello política padrão

>[!NOTE]
>Se você estiver usando os atributos de usuário personalizada, você precisa tooprovide seus próprios traduções. Confira "[Como personalizar suas cadeias de caracteres](#customize-your-strings)" para obter mais detalhes.
>

## <a name="support-uilocales-requested-languages"></a>Suporte aos idiomas ui_locales solicitados 
Habilitando 'Personalização de linguagem' em uma política, agora você pode controlar o idioma de saudação do jornada de usuário Olá adicionando Olá ui_locales parâmetro.
1. [Siga estas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure.](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#navigate-to-b2c-settings)
2. Navegue tooa política que você deseja tooenable para traduções.
3. Clique em **Personalização de idiomas**.
4. Saudação de leitura de aviso com cuidado.  Uma vez habilitada, você não pode desativar a "personalização de idiomas".
5. Ativar o recurso de saudação e clique em **Okey**.
6. Salvar a política no canto superior esquerdo de saudação do seu **Editar política** folha.

## <a name="select-which-languages-your-user-journey-supports"></a>Selecione quais idiomas oferecem suporte a seu percurso do usuário 
Crie uma lista de idiomas permitidos para sua toobe jornada de usuário traduzido quando Olá ui_locales parâmetro não for fornecido.
1. Verifique se a sua política tem "Personalização de idiomas" habilitada nas instruções anteriores.
2. A partir da folha **Editar política**, selecione **Personalização de idiomas**.
3. Você será direcionado tooyour **idiomas com suporte** folha.  Aqui, você pode selecionar **Adicionar idioma**.
4. Selecione todos os idiomas de saudação que você gostaria de toobe com suporte.  

>[!NOTE]
>Se não for fornecido um parâmetro ui_locales, em seguida, Olá página é idioma do navegador do cliente toohello traduzido somente se ele estiver na lista
>

5. Clique em **Okey** na parte inferior da saudação
6. Olá fechar **personalização de idioma** folha e **salvar** sua política.

## <a name="customize-your-strings"></a>Como personalizar suas cadeias de caracteres
Personalização do idioma permite que você toocustomize qualquer cadeia de caracteres em sua jornada de usuário.
1. Certifique-se de que sua política tem 'Personalização de linguagem' habilitada de instruções anterior hello.
2. A partir da folha **Editar política**, selecione **Personalização de idiomas**.
3. No menu de navegação do lado esquerdo do hello, selecione **baixar conteúdo**.
4. Selecione a página de saudação ser tooedit.
5. No menu suspenso hello, selecione o idioma de saudação desejado tooedit para.
6. Clique em **Download**. 

Essas etapas fornecer um arquivo JSON que você pode usar toostart editando suas cadeias de caracteres.

### <a name="changing-any-string-on-hello-page"></a>Alterar qualquer cadeia de caracteres na página Olá
1. Olá abrir arquivo JSON é obtido por instruções anteriores em um editor de JSON.
2. Localizar Olá elemento a ser toochange.  Você pode encontrar hello `StringId` de cadeia de caracteres de saudação você está procurando ou procure Olá `Value` toochange desejado.
3. Saudação de atualização `Value` atributo com o que você deseja exibir.
4. Salve o arquivo hello e carregar suas alterações.

### <a name="changing-extension-attributes"></a>Alteração dos atributos de extensão
Se você estiver buscando a cadeia de caracteres de saudação toochange um atributo de usuário personalizada, ou tooadd um toohello JSON, é em Olá formato a seguir:
```JSON
{
  "LocalizedStrings": [
    {
      "ElementType": "ClaimType",
      "ElementId": "extension_<ExtensionAttribute>",
      "StringId": "DisplayName",
      "Override": false,
      "Value": "<ExtensionAttributeValue>"
    }
    [...]
}
```
>[!IMPORTANT]
>Se você precisar toooverride uma cadeia de caracteres, fazer se Olá de tooset `Override` valor muito`true`.  Se o valor de saudação não será alterado, entrada hello é ignorada. 
>

Substituir `<ExtensionAttribute>` com o nome de saudação do seu atributo de usuário personalizada.  
Substituir `<ExtensionAttributeValue>` com hello nova cadeia de caracteres toobe exibida.

### <a name="using-localizedcollections"></a>Uso do LocalizedCollections
Se você quiser tooprovide lista um conjunto de valores para respostas, será necessário toocreate um `LocalizedCollections`.  Um `LocalizedCollections` é uma matriz de pares de `Name` e `Value`.  Olá `Name` é o que é exibido e Olá `Value` é o que é retornado na declaração de saudação.  tooadd um `LocalizedCollections`, ele tem Olá formato a seguir:

```JSON
{
  "LocalizedStrings": [...],
  "LocalizedCollections": [{
      "ElementType":"ClaimType", 
      "ElementId":"<UserAttribute>",
      "TargetCollection":"Restriction",
      "Override": false,
      "Items":[
           {
                "Name":"<Response1>",
                "Value":"<Value1>"
           },
           {
                "Name":"<Response2>",
                "Value":"<Value2>"
           }
     ]
  }]
}
```
>[!IMPORTANT]
>Se você precisar toooverride uma cadeia de caracteres, fazer se Olá de tooset `Override` valor muito`true`.  Se o valor de saudação não será alterado, entrada hello é ignorada. 
>

* `ElementId`é hello usuário atributo que este `LocalizedCollections` é uma resposta a
* `Name`Olá valor mostrado toohello usuário
* `Value`é o que é retornado na declaração de saudação quando essa opção é selecionada.

### <a name="upload-your-changes"></a>Carregamento das suas alterações
1. Depois que você concluiu o arquivo do hello alterações tooyour JSON, navegar tooyour back B2C locatário.
2. A partir da folha **Editar política**, selecione **Personalização de idiomas**.
3. No menu de navegação do lado esquerdo do hello, selecione **carregar conteúdo**.
4. Selecione página Olá para que deseja tooupload suas alterações.
5. Se você quiser tooupload uma linguagem que você forneceu anteriormente um JSON para, é necessário entrada do toodelete Olá anterior.  Você poderá excluí-la clicando Olá `...` Olá direita do idioma e selecione **excluir**.
6. Clique em **adicionar** na parte superior esquerda do hello.
7. Selecione o idioma de saudação do arquivo JSON.
8. Clique botão pasta Olá Olá direito e navegue para o arquivo JSON.
9. Clique em Olá **carregar** botão na parte inferior da saudação da folha de saudação.
10. Voltar tooyour **Editar política** folha e clique em **salvar**.

## <a name="additional-information"></a>Informações adicionais
### <a name="recommendations-for-language-customization"></a>Recomendações para "Personalização de idiomas"
É recomendável somente colocando em recursos de idioma tooyour entradas para cadeias de caracteres é explicitamente tooreplace desejado.  Vamos aplicar um arquivo de toohello de limite de tamanho que é compilado fora de todas as suas traduções de JSON.  Se os arquivos muito grandes, ele afeta o desempenho da saudação de sua jornada de usuário.
### <a name="page-ui-customization-labels-are-removed-once-language-customization-is-enabled"></a>Rótulos de personalização de IU da página são removidos após a "personalização de idiomas" estar habilitada
Quando você habilita a "personalização de idiomas", as edições anteriores dos rótulos usando as personalizações da IU da página são removidas, exceto os atributos de usuário personalizados.  Essa alteração é feita tooavoid conflitos no qual você pode editar suas cadeias de caracteres.  Você pode continuar toochange os rótulos e outras cadeias de caracteres ao carregar recursos de idioma na personalização do idioma.
### <a name="microsoft-is-committed-tooprovide-hello-most-up-to-date-translations-for-your-use"></a>A Microsoft está confirmada tooprovide hello mais atualizadas traduções para uso
Vamos aprimorar continuamente as traduções e mantê-las em conformidade para você.  Vamos identificar bugs e alterações na terminologia global e fazer atualizações Olá que funcionam perfeitamente em sua jornada de usuário.
### <a name="support-for-right-to-left-languages"></a>Suporte para idiomas da direita para a esquerda
Não há suporte para idiomas da direita para a esquerda, se você precisar desse recurso, vote para ele nos [Comentários do Azure](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/19393000-provide-language-support-for-right-to-left-languag).
### <a name="social-identity-provider-translations"></a>Traduções de provedor de identidade social
Fornecemos Olá ui_locales logons de toosocial parâmetro OIDC, mas eles não são respeitados por alguns provedores de identidade de redes sociais, incluindo o Facebook e do Google. 
### <a name="browser-behavior"></a>Comportamento do navegador
Chrome e Firefox ambos solicitam seu conjunto de idioma e se é uma linguagem com suporte, ele será exibido antes de padrão de saudação.  Borda atualmente não solicita um idioma e passa o idioma padrão de toohello retas.
### <a name="known-issues"></a>Problemas conhecidos
* Carregar recursos de idioma para a página MFA de saudação em uma política de perfil Editar está disponível no momento.
* `LocalizedCollections`não são gerados para valores quando ele é necessário para o tipo de resposta Olá
### <a name="what-if-i-want-a-language-that-isnt-supported"></a>E se eu desejar um idioma que não tem suporte?
Planejamos tooprovide uma extensão desse recurso que permite que você tooupload um recurso JSON para 'linguagens personalizadas'.  Olá recurso permite que você toospecify nome de saudação e linguagem de código para qualquer idioma e fornecer *todos os* Olá traduções para esse idioma.  Se você precisar desse recurso, envie-nos o cenário para [ aadb2cpreview@microsoft.com ](mailto:aadb2cpreview@microsoft.com).  

### <a name="what-languages-are-supported"></a>Quais são os idiomas com suporte?

| idioma              | Código de idioma |
|-----------------------|---------------|
| Bangla                | bn            |
| Tcheco                 | cs            |
| Dinamarquês                | da            |
| Alemão                | de            |
| Grego                 | el            |
| Inglês               | en            |
| Espanhol               | es            |
| Finlandês               | fi            |
| Francês                | fr            |
| Guzerate              | gu            |
| Híndi                 | hi            |
| Croata              | hr            |
| Húngaro             | hu            |
| Italiano               | it            |
| Japonês              | ja            |
| Kannada               | kn            |
| Coreano                | ko            |
| Malaiala             | ml            |
| Marati               | mr            |
| Malaio                 | ms            |
| Norueguês Bokmal      | nb            |
| Holandês                 | nl            |
| Punjabi               | pa            |
| Polonês                | pl            |
| Português - Brasil   | pt-br         |
| Português - Portugal | pt-pt         |
| Romeno              | ro            |
| Russo               | ru            |
| Eslovaco                | sk            |
| Sueco               | sv            |
| Tâmil                 | ta            |
| Télugo                | te            |
| Tailandês                  | th            |
| Turco               | tr            |
| Chinês - Simplificado  | zh-hans       |
| Chinês - Tradicional | zh-hant       |
