## <a name="prerequisites"></a>Pré-requisitos
Antes, podemos gravar o código de gerenciamento de CDN, é preciso toodo tooenable alguma preparação toointeract nosso código com hello Azure Resource Manager.  toodo isso, você precisará:

* Criar uma saudação de toocontain do grupo de recursos perfil CDN criamos neste tutorial
* Configurar a autenticação do Active Directory do Azure tooprovide para nosso aplicativo
* Aplicar permissões ao grupo de recursos de toohello para que somente usuários autorizados do nosso locatário do Azure AD pode interagir com nosso perfil CDN

### <a name="creating-hello-resource-group"></a>Criando grupo de recursos de saudação
1. Faça logon no hello [Portal do Azure](https://portal.azure.com).
2. Clique em Olá **novo** botão na parte superior esquerda de Olá e, em seguida, **gerenciamento**, e **grupo de recursos**.

    ![Criando um novo grupo de recursos](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Chame seu grupo de recursos de *CdnConsoleTutorial*.  Selecione sua assinatura e escolha uma localização perto de você.  Se desejar, você pode clicar em Olá **toodashboard Pin** caixa de seleção toopin Olá recurso grupo toohello painel no portal de saudação.  Isso tornará mais fácil toofind mais tarde.  Após fazer suas seleções, clique em **Criar**.

    ![Nomear o grupo de recursos de saudação](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Depois que o grupo de recursos de saudação é criado, se você não fixar tooyour painel, você pode encontrá-lo clicando **procurar**, em seguida, **grupos de recursos**.  Clique em tooopen de grupo de recursos de saudação-lo.  Anote sua **ID da assinatura**.  Precisaremos dela mais tarde.

    ![Nomear o grupo de recursos de saudação](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Criando aplicativo hello AD do Azure e aplicação de permissões
Há duas abordagens tooapp autenticação com o Active Directory do Azure: usuários individuais ou a uma entidade de serviço. Uma entidade de serviço é uma conta de serviço de tooa semelhante no Windows.  Em vez de conceder um toointeract de permissões de usuário específico com perfis CDN hello, em vez disso, Concedemos permissões Olá toohello entidade de serviço.  As entidades de serviço geralmente são usadas para processos automatizados não interativos.  Apesar deste tutorial é escrever um aplicativo de console interativo, vamos nos concentrar na abordagem principal do serviço de saudação.

A criação de uma entidade de serviço abarca várias etapas, incluindo o desenvolvimento de um aplicativo do Azure Active Directory.  toodo isso, vamos muito[siga este tutorial](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Ser toofollow-se de que todas as etapas Olá Olá [tutorial vinculado](../articles/resource-group-create-service-principal-portal.md).  É *extremamente importante* que você faça exatamente o que está descrito.  Certifique-se de que toonote seu **ID do locatário**, **nome de domínio de locatário** (normalmente um *. c o m* domínio, a menos que você especificou um domínio personalizado), **ID do cliente** , e **chave de autenticação de cliente**, como podemos precisará deles mais tarde.  Seja muito cuidadoso tooguard seu **ID do cliente** e **chave de autenticação de cliente**, como essas credenciais podem ser usadas por qualquer pessoa tooexecute operações como entidade de serviço hello.
>
> Quando você receber etapa toohello chamada configurar aplicativo multilocatário, selecione **não**.
>
> Quando você obtém etapa toohello [atribuir aplicativo toorole](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), usar o grupo de recursos de saudação criado anteriormente, *CdnConsoleTutorial*, mas em vez da saudação **leitor** função, atribuir Olá **CDN perfil Colaborador** função.  Depois de atribuir Olá Olá do aplicativo **CDN perfil Colaborador** função em seu grupo de recursos, toothis retorno tutorial. 
>
>

Depois de criar sua saudação do serviço principal e atribuídos **CDN perfil Colaborador** funções, hello **usuários** folha para seu grupo de recursos deve ter aparência semelhante toothis.

![Folha de usuários](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Autenticação de usuário interativo
Se, em vez de uma entidade de serviço, que prefere ter autenticação de usuário interativo, o processo de saudação é toothat muito semelhante para uma entidade de serviço.  Na verdade, você precisará toofollow Olá mesmo procedimento, mas fazer algumas pequenas alterações.

> [!IMPORTANT]
> Apenas siga as etapas a seguir se você está escolhendo toouse autenticação de usuário individual em vez de uma entidade de serviço.
>
>

1. Ao criar seu aplicativo, em vez de **Aplicativo Web**, escolha **Aplicativo nativo**.

    ![Aplicativo nativo](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Na página seguinte do hello, você será solicitado para uma **URI de redirecionamento**.  Olá URI não ser validada, mas lembre-se de que você inseriu.  Você precisará dela mais tarde.
3. Não há nenhuma necessidade toocreate um **chave de autenticação de cliente**.
4. Em vez de atribuir um toohello principal do serviço **CDN perfil Colaborador** função, vamos tooassign usuários ou grupos individuais.  Neste exemplo, você pode ver que foi atribuído *CDN demonstração usuário* toohello **CDN perfil Colaborador** função.  

    ![Acesso de usuário individual](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
