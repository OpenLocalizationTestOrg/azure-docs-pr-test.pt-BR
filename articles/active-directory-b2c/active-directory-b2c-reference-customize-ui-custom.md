---
title: "B2C de diretório ativo do Azure: Referência: personalizar a interface do usuário de uma viagem de usuário com as políticas personalizadas de saudação | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 11f2a7575b95a186399d83266850fe44d650371b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-ui-of-a-user-journey-with-custom-policies"></a>Personalizar a interface do usuário de uma viagem de usuário com as políticas personalizadas de saudação

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

> [!NOTE]
> Este artigo é uma descrição avançada de como funciona a personalização da interface do usuário e como tooenable com as políticas personalizadas B2C, usando Olá do Framework de experiência de identidade


Uma experiência perfeita para o usuário é a chave para qualquer solução para negócios para consumidor. Com a experiência do usuário perfeita, queremos dizer uma experiência no dispositivo ou navegador, onde jornada de um usuário por meio de nosso serviço não pode ser diferenciada do hello atendimento ao cliente que estão usando.

## <a name="understand-hello-cors-way-for-ui-customization"></a>Compreender a maneira CORS Olá para personalização da interface do usuário

B2C do Azure AD permite que você toocustomize Olá aparência e funcionalidade de experiência do usuário (UX) Olá várias páginas que podem ser potencialmente atendidas e exibidas pelo Azure AD B2C por meio de suas políticas personalizadas.

Para essa finalidade, o Azure AD B2C executa o código no navegador do cliente e usa Olá abordagem moderna e padrão [compartilhamento de recursos entre origens (CORS)](http://www.w3.org/TR/cors/) conteúdo personalizado do tooload de uma URL específica que você especificar em uma política personalizada modelos de HTML5/CSS de tooyour toopoint. CORS é um mecanismo que permite que os recursos restritos, como fontes, em um toobe de página da web solicitada de outro domínio fora Olá domínio de origem do recurso de saudação.

Em comparação com o antigo modo tradicional toohello, onde as páginas de modelo pertencentes a solução Olá onde fornecido limitada de texto e imagens, onde controle limitado de layout e aparência era oferecido toomore à esquerda que dificuldades tooachieve uma experiência perfeita, Olá CORS modo compatível com HTML5 e CSS e permitem que você:

- Hospedar conteúdo hello e solução hello injeta seus controles usando script do lado do cliente.
- Tenha controle total sobre cada pixel de layout e aparência.

Você pode fornecer quantas páginas de conteúdo quiser ao criar arquivos de HTML5/CSS conforme a conveniência.

> [!NOTE]
> Por motivos de segurança, uso de saudação do JavaScript está bloqueado no momento para personalização. toounblock JavaScript, o uso de um nome de domínio personalizado para seu locatário do Azure AD B2C é necessária.

Em cada um dos seus modelos de HTML5/CSS, você deve fornecer um *âncora* elemento, que corresponde a toohello necessária `<div id=”api”>` elemento Olá HTML ou hello página de conteúdo como ilustram daqui por diante. O Azure AD B2C requer que todas as páginas de conteúdo tenham essa divisão específica.

```
<!DOCTYPE html>
<html>
  <head>
    <title>Your page content’s tile!</title>
  </head>
  <body>
    <div id="api"></div>
  </body>
</html>
```

Conteúdo relacionado AD B2C do Azure para a página de saudação será injetada neste div, enquanto o restante de saudação da página de saudação é sua toocontrol. código JavaScript de saudação do Azure AD B2C extrai seu conteúdo e injeta o HTML nesse elemento div específico. B2C do Azure AD injeta Olá seguintes controles conforme apropriado: controle de seletor, controles de logon, multi-factor (atualmente baseado em telefone) controles e controles de coleção de atributo de conta. B2C do AD do Azure garante que todos os controles de saudação HTML5 acessível e não compatíveis, todos os controles de saudação podem ser totalmente com o estilo e uma versão de controle será diminua.

Olá conteúdo mesclado é eventualmente exibido como consumidor de tooyour documento dinâmico Olá.

tooensure de saudação acima funciona conforme o esperado, você deve:

- Certifique-se de que seu conteúdo esteja em conformidade com HTML5 e acessível
- Verifique se que o servidor de conteúdo está habilitado para CORS.
- Forneça conteúdo por HTTPS.
- Use URLS absolutas como https://yourdomain/content para todos os links e conteúdo CSS.

> [!TIP]
> tooverify que Olá site que você estiver hospedando o conteúdo em tiver CORS habilitado e solicitações CORS de teste, você pode usar o hello site http://test-cors.org/. Site de toothis Obrigado, você pode simplesmente enviar Olá CORS solicitação tooa ao servidor remoto (tootest se houver suporte para CORS) ou enviar o servidor de teste do hello CORS solicitação tooa (tooexplore determinados recursos de CORS).

> [!TIP]
> Olá site http://enable-cors.org/ também constitui uma mais de recursos úteis sobre o CORS.

Graças toothis abordagem baseada em CORS, os usuários finais de saudação terá experiências consistentes entre seu aplicativo e páginas de saudação servidas pelo Azure AD B2C.

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento

Como pré-requisito, você precisa toocreate uma conta de armazenamento. Você precisará de uma assinatura do Azure de toocreate uma conta de armazenamento de BLOBs do Azure. Você pode inscrever uma avaliação gratuita em Olá [site do Azure](https://azure.microsoft.com/en-us/pricing/free-trial/).

1. Abra uma sessão de navegação e navegue toohello [portal do Azure](https://portal.azure.com).
2. Entre com suas credenciais administrativas.
3. Clique em **Novo** > **Dados + armazenamento** > **Conta de armazenamento**.  Uma folha **Criar conta de armazenamento** abre.
4. Em **nome**, forneça um nome para a conta de armazenamento hello, por exemplo, *contoso369b2c*. Esse valor será posteriormente mencionado como muito*storageAccountName*.
5. Escolha as seleções apropriadas Olá Olá tipo de preço, grupo de recursos de saudação e assinatura hello. Certifique-se de que você tenha Olá **tooStartboard Pin** opção marcada. Clique em **Criar**.
6. Voltar toohello quadro inicial e clique na conta de armazenamento Olá que você acabou de criar.
7. Em Olá **serviços** seção, clique em **Blobs**. A **folha do serviço Blob** abre.
8. Clique em **+ Contêiner**.
9. Em **nome**, forneça um nome para o contêiner de hello, por exemplo, *b2c*. Esse valor será posteriormente chamado tooas *containerName*.
9. Selecione **Blob** como Olá **acessar tipo**. Clique em **Criar**.
10. contêiner de saudação que você criou aparecerá na lista de saudação em Olá **folha do serviço Blob**.
11. Olá fechar **Blobs** folha.
12. Em Olá **folha da conta de armazenamento**, clique em Olá **chave** ícone. Uma **folha chaves de acesso** abre.  
13. Anote o valor de saudação do **key1**. Esse valor será referenciado mais tarde como *key1*.

## <a name="downloading-hello-helper-tool"></a>Baixar a ferramenta auxiliar do hello

1.  Baixar a ferramenta de auxiliar de saudação do [GitHub](https://github.com/azureadquickstarts/b2c-azureblobstorage-client/archive/master.zip).
2.  Salvar Olá *B2C AzureBlobStorage-cliente master.zip* arquivo em seu computador local.
3.  Extrair o conteúdo de saudação do arquivo hello B2C AzureBlobStorage-cliente master.zip em seu disco local, por exemplo, sob Olá **pacote de personalização da interface do usuário** pasta. Isso criará uma pasta *B2C-AzureBlobStorage-Client-master*.
4.  Abra essa pasta e extrair o conteúdo de saudação do arquivo hello *B2CAzureStorageClient.zip* dentro dele.

## <a name="upload-hello-ui-customization-pack-sample-files"></a>Carregar arquivos de exemplo de pacote de personalização de IU Olá

1.  Usando o Windows Explorer, navegue pasta toohello *B2C AzureBlobStorage-cliente mestre* localizado sob Olá *pacote de personalização da interface do usuário* pasta criada na seção anterior hello.
2.  Executar Olá *B2CAzureStorageClient.exe* arquivo. Esse programa simplesmente carregará todos os arquivos Olá Olá diretório que você especifica a conta de armazenamento tooyour e habilita o acesso CORS para os arquivos.
3.  Quando solicitado, especifique: um.  nome de saudação da sua conta de armazenamento, *storageAccountName*, por exemplo *contoso369b2c*.
    b.  chave de acesso primária de saudação do seu armazenamento de BLOBs do azure, *key1*, por exemplo *contoso369b2c*.
    c.  nome de saudação do seu contêiner de armazenamento de blob de armazenamento, *containerName*, por exemplo *b2c*.
    d.  caminho de saudação do hello *pacote de inicializador* exemplos de arquivos, por exemplo *... \B2CTemplates\wingtiptoys*.

Se você seguiu as etapas de saudação acima, Olá arquivos HTML5 e CSS do hello *pacote de personalização da interface do usuário* para a empresa fictícia Olá **wingtiptoys** agora estar apontando tooyour conta de armazenamento.  Você pode verificar que o conteúdo de saudação foi carregado corretamente abrindo a folha de contêineres relacionados Olá no hello portal do Azure. Como alternativa, você pode verificar que o conteúdo de saudação foi carregado corretamente, acessando a página de saudação de um navegador. Para obter mais informações, consulte [do Azure Active Directory B2C: uma ferramenta de auxiliar usada recurso personalização de interface de usuário do toodemonstrate Olá página](active-directory-b2c-reference-ui-customization-helper-tool.md).

## <a name="ensure-hello-storage-account-has-cors-enabled"></a>Certifique-se a conta de armazenamento de saudação tem CORS habilitado

CORS (Cross-Origin Resource Sharing) deve ser habilitado em seu ponto de extremidade para tooload Premium do Azure AD B2C seu conteúdo. Isso ocorre porque o conteúdo é hospedado em um domínio diferente do domínio Olá B2C do Azure AD Premium estarão servindo da página hello.

tooverify armazenamento Olá estiver hospedando o conteúdo em tem CORS habilitado, prossiga com hello etapas a seguir:

1. Abra uma sessão de navegação e navegue página toohello *unified.html* usando a URL completa do seu local em sua conta de armazenamento, Olá `https://<storageAccountName>.blob.core.windows.net/<containerName>/unified.html`. Por exemplo, https://contoso369b2c.blob.core.windows.net/b2c/unified.html.
2. Navegue toohttp://test-cors.org. Este site permite que você tooverify que Olá página que você está usando tem CORS habilitado.  
<!--
![test-cors.org](../../media/active-directory-b2c-customize-ui-of-a-user-journey/test-cors.png)
-->

3. Em **URL remota**, insira a URL completa Olá para o seu conteúdo unified.html e clique em **enviar solicitação**.
4. Verifique se essa saída Olá Olá **resultados** seção contém *status XHR: 200*. Isso indica que o CORS está habilitado.
<!--
![CORS enabled](../../media/active-directory-b2c-customize-ui-of-a-user-journey/cors-enabled.png)
-->
conta de armazenamento Olá agora deve conter um contêiner de blob denominado *b2c* na nossa ilustração contém Olá seguir wingtiptoys modelos de saudação *pacote de inicializador*.

<!--
![Correctly configured storage account](../../articles/active-directory-b2c/media/active-directory-b2c-reference-customize-ui-custom/storage-account-final.png)
-->

Olá tabela a seguir descreve finalidade Olá Olá acima das páginas do HTML5.

| Modelo do HTML5 | Descrição |
|----------------|-------------|
| *phonefactor.html* | Esta página pode ser usada como modelo para uma página de autenticação multifator. |
| *resetpassword.html* | Esta página pode ser usada como modelo para uma página de esquecimento de senha. |
| *selfasserted.html* | Esta página pode ser usada como modelo para uma página de inscrição de conta social ou uma página de inscrição de conta local. |
| *unified.html* | Esta página pode ser usada como modelo para uma página de inscrição ou entrada unificada. |
| *updateprofile.html* | Esta página pode ser usada como modelo para uma página de atualização de perfil. |

## <a name="add-a-link-tooyour-html5css-templates-tooyour-user-journey"></a>Adicionar uma viagem de usuário do link tooyour HTML5/CSS modelos tooyour

Você pode adicionar uma viagem de usuário do link tooyour HTML5/CSS modelos tooyour editando uma política personalizada diretamente.

Olá personalizado HTML5/CSS modelos toouse em sua jornada de usuário têm toobe especificado em uma lista de definições de conteúdo que pode ser usado nas Jornadas de usuário. Para essa finalidade, um recurso opcional  *<ContentDefinitions>*  elemento XML deve ser declarado em Olá  *<BuildingBlocks>*  seção do arquivo XML política personalizada.

Olá, tabela a seguir descreve Olá conjunto de ids de definição de conteúdo reconhecido pelo mecanismo de experiência de identidade Olá B2C do Azure AD e o tipo de saudação de páginas que relaciona toothem.

| Id de definição de conteúdo | Descrição |
|-----------------------|-------------|
| *api.error* | **Página de erro**. Essa página é exibida quando uma exceção ou um erro é encontrado. |
| *api.idpselections* | **Página de seleção de provedor de identidade**. Esta página contém uma lista de provedores que Olá o usuário podem escolher durante o logon de identidade. Esses são os provedores de identidade empresarial ou provedores de identidade social, como Facebook e Google+, ou contas locais (baseadas em endereço de email ou nome de usuário). |
| *api.idpselections.signup* | **Seleção de provedor de identidade para inscrição**. Esta página contém uma lista de provedores que Olá o usuário podem escolher durante a inscrição de identidade. Esses são os provedores de identidade empresarial ou provedores de identidade social, como Facebook e Google+, ou contas locais (baseadas em endereço de email ou nome de usuário). |
| *api.localaccountpasswordreset* | **Página de esquecimento de senha**. Esta página contém um formulário que o usuário Olá tem tooinitiate toofill redefinir sua senha.  |
| *api.localaccountsignin* | **Página de entrada da conta local**. Esta página contém um formulário de entrada que o usuário Olá tem toofill em quando entrar com uma conta local com base em um endereço de email ou um nome de usuário. formulário de saudação pode conter uma caixa de entrada de texto e a caixa de entrada de senha. |
| *api.localaccountsignup* | **Página de inscrição da conta local**. Esta página contém um formulário de inscrição que o usuário Olá tem toofill em ao se inscrever para uma conta local com base em um endereço de email ou um nome de usuário. formulário de saudação pode conter controles de entrada diferentes, como a caixa de entrada de texto, caixa de entrada de senha, botão de opção, caixas de lista suspensa de seleção única e selecionar várias caixas de seleção. |
| *api.phonefactor* | **Página de autenticação multifator**. Nesta página, os usuários pode verificar seus números de telefone (usando mensagem de texto ou por voz) durante a inscrição ou entrada. |
| *api.selfasserted* | **Página de inscrição de conta social**. Esta página contém um formulário de inscrição que Olá possui toofill ao inscrever-se usando uma existente de conta de um provedor de identidade de redes sociais, como Facebook ou Google +. Esta página é semelhante toohello acima da página de inscrição de conta social com exceção de saudação de campos de entrada de senha hello. |
| *api.selfasserted.profileupdate* | **Página de atualização de perfil**. Esta página contém um formulário que o usuário Olá pode usar tooupdate seu perfil. Esta página é semelhante toohello acima da página de inscrição de conta social com exceção de saudação de campos de entrada de senha hello. |
| *api.signuporsignin* | **Página de inscrição ou entrada unificada**.  Esta página controla tanto a inscrição quanto a entrada de usuários que podem usar provedores de identidade empresarial ou provedores de identidade social, como Facebook, Google+ ou contas locais.

## <a name="next-steps"></a>Próximas etapas
[Referência: Entender as políticas personalizadas como funcionam com saudação do Framework de experiência de identidade em B2C](active-directory-b2c-reference-custom-policies-understanding-contents.md)
