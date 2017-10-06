---
title: aaaTranslate links e URLs Proxy do aplicativo do AD do Azure | Microsoft Docs
description: "Abrange Olá Noções básicas sobre conectores de Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Redirecione os links inseridos no código para aplicativos publicados com o Proxy de Aplicativo do Azure AD

Proxy de aplicativo do AD do Azure torna sua toousers de aplicativos disponíveis de local remoto ou em seus próprios dispositivos. No entanto, alguns aplicativos, foram desenvolvidos com links locais inseridos na Olá HTML. Esses links não funcionam corretamente quando o aplicativo hello é usado remotamente. Quando você tiver vários locais aplicativos ponto tooeach outros, os usuários esperam Olá links tookeep trabalhando quando não estiver no escritório de saudação. 

Olá melhor maneira toomake se os links funcionem Olá mesmo dentro e fora da sua rede corporativa é tooconfigure URLs externas de saudação do seu toobe aplicativos Olá mesmo como suas URLs internos. Use [domínios personalizados](active-directory-application-proxy-custom-domains.md) tooconfigure sua toohave URLs externa seu domínio corporativo nome em vez do domínio de proxy de aplicativo hello padrão.

Se você não pode usar domínios personalizados em seu locatário, o recurso de conversão de link de saudação do Proxy de aplicativo mantém seus vínculos de trabalho, independentemente de onde os usuários estão. Quando você tiver aplicativos que aponte diretamente de pontos de extremidade de toointernal ou portas, você pode mapear essas toohello URLs interno publicado URLs externas de Proxy de aplicativo. Quando a conversão de link está habilitada, o Proxy de Aplicativo pesquisa em HTML, CSS e seleciona marcas de JavaScript para os links internos publicados. Em seguida, Olá serviço Proxy de aplicativo converte-as para que os usuários podem obter uma experiência ininterrupta.

>[!NOTE]
>Olá recurso de conversão de link é para locatários que, por qualquer motivo, não é possível usar domínios personalizados toohave Olá mesmo URLs internos e externos para seus aplicativos. Antes de habilitar esse recurso, verifique se [domínios personalizados no Proxy de Aplicativo do Azure AD](active-directory-application-proxy-custom-domains.md) podem funcionar para você.
>
>Ou, se o aplicativo hello necessário tooconfigure com conversão de link de SharePoint, consulte [configurar mapeamentos alternativos de acesso para o SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) para links de toomapping outra abordagem.

## <a name="how-link-translation-works"></a>Como a translação de link funciona

Após a autenticação, quando o servidor de proxy de saudação transmite o usuário para toohello de dados do aplicativo hello, Proxy de aplicativo examina o aplicativo hello para links codificado e substitui com suas respectivas publicado URLs externas.

O Proxy de Aplicativo pressupõe que os aplicativos estejam codificados em UTF-8. Se não for o caso de Olá, especifique o tipo de codificação Olá em um cabeçalho de resposta http, como `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Quais links são afetados?

o recurso de conversão de link Olá somente procura links que estão nas marcas de código no corpo de saudação de um aplicativo. O Proxy de Aplicativo tem um recurso separado para converter cookies ou URLs em cabeçalhos. 

Há dois tipos comuns de links internos em aplicativos locais:

- **Links internos relativos** tooa esse ponto compartilhado recursos em uma estrutura de arquivo local como `/claims/claims.html`. Esses links automaticamente funcionam em aplicativos que são publicados por meio do Proxy de aplicativo e continuam toowork com ou sem conversão de link. 
- **Links internos codificado** tooother aplicativos como o local `http://expenses` ou publicado arquivos como `http://expenses/logo.jpg`. o recurso de conversão de link Olá funciona em links internos codificado e alterá-las toopoint toohello URLs externas que os usuários remotos precisam toogo por meio de.

### <a name="how-do-apps-link-tooeach-other"></a>Como os aplicativos de link tooeach outros?

Conversão de link está habilitado para cada aplicativo, para que você tenha controle sobre a experiência do usuário Olá no nível do hello por aplicativo. Ativar a conversão de link para um aplicativo quando desejar que os links de saudação *de* toobe esse aplicativo traduzido, links não *para* esse aplicativo. 

Por exemplo, suponha que você tenha três aplicativos publicados por meio do Proxy de aplicativo que todos os link tooeach outros: benefícios, despesas e viagem. Há um quarto aplicativo, Comentários, que não está publicado pelo Proxy de Aplicativo.

Quando você habilita a conversão de link para o aplicativo de benefícios hello, Olá links tooExpenses e viagem são URLs externas de toohello redirecionado para esses aplicativos, mas Olá tooFeedback de link não será redirecionada porque há uma URL externa. Links de despesas e viagem tooBenefits back não funcionam porque a conversão de link não foi habilitado para os dois aplicativos.

![Links de benefícios tooother aplicativos quando a conversão de link está habilitada](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Quais links não são convertidos?

tooimprove desempenho e segurança, alguns links não são traduzidos:

- Links que não estão dentro de marcas de código. 
- Links que não estão em HTML, CSS ou JavaScript. 
- Links internos abertos de outros programas. Links enviados por email, mensagem instantânea ou incluídos em outros documentos não serão convertidos. Olá precisam toogo de tooknow toohello URL externa.

Se você precisar toosupport esses dois cenários, usar Olá mesmo URLs internas e externas, em vez de conversão de link.  

## <a name="enable-link-translation"></a>Habilitar a translação de link

Começar a trabalhar com a translação de link é tão fácil quanto clicar em um botão:

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Vá muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos** > Olá selecione aplicativo deseja toomanage > **Proxy de aplicativo**.
3. Ativar **traduzir URLs no corpo do aplicativo** muito**Sim**.

   ![Selecione Sim tootranslate URLs no corpo do aplicativo](./media/application-proxy-link-translation/select_yes.png).
4. Selecione **salvar** tooapply suas alterações.

Agora, quando os usuários acessam esse aplicativo, proxy Olá examinará automaticamente para URLs internas que foram publicadas por meio do Proxy de aplicativo em seu locatário.

## <a name="send-feedback"></a>Enviar comentários

Queremos toomake sua ajuda esse recurso funcione para todos os seus aplicativos. Podemos pesquisar mais de 30 marcas HTML e CSS e considerando que toosupport de casos de JavaScript. Se você tiver um exemplo de links gerados que não estão sendo convertidos, envie um trecho de código muito[comentários de Proxy de aplicativo](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Próximas etapas
[Usar domínios personalizados com o Proxy de aplicativo do Azure AD](active-directory-application-proxy-custom-domains.md) toohave Olá a mesma URL interna e externa

[Configurar mapeamentos alternativos de acesso para o SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx)
