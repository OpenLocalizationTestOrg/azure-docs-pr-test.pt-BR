<span data-ttu-id="fe72b-101">tooenable entrar em seu aplicativo, você precisará de política de toocreate uma entrada.</span><span class="sxs-lookup"><span data-stu-id="fe72b-101">tooenable sign-in on your application, you will need toocreate a sign-in policy.</span></span> <span data-ttu-id="fe72b-102">Essa política descreve experiências Olá consumidores revisará durante o logon e conteúdo de saudação de tokens que Olá aplicativo receberá em logons com êxito.</span><span class="sxs-lookup"><span data-stu-id="fe72b-102">This policy describes hello experiences that consumers will go through during sign-in and hello contents of tokens that hello application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="fe72b-103">Na seção de políticas de saudação de configurações, selecione **políticas inscrever-se ou entrar** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-103">In hello policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Selecione as políticas de inscrição ou entrada e clique no botão Adicionar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="fe72b-105">Insira uma política **nome** para tooreference seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fe72b-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="fe72b-106">Por exemplo, insira: `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="fe72b-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="fe72b-107">Selecione **Provedores de identidade** e marque **Inscrição por email**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="fe72b-108">Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado.</span><span class="sxs-lookup"><span data-stu-id="fe72b-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="fe72b-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-109">Click **OK**.</span></span>

![Selecione a assinatura de Email como um provedor de identidade e clique em botão Olá Okey](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="fe72b-111">Selecione **Atributos de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="fe72b-112">Escolha os atributos desejados toocollect de consumidor Olá durante a inscrição.</span><span class="sxs-lookup"><span data-stu-id="fe72b-112">Choose attributes you want toocollect from hello consumer during sign-up.</span></span> <span data-ttu-id="fe72b-113">Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="fe72b-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-114">Click **OK**.</span></span>

![Selecione alguns atributos e clique botão de saudação Okey](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="fe72b-116">Selecione **Declarações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-116">Select **Application claims**.</span></span> <span data-ttu-id="fe72b-117">Escolha declarações que ser retornado em tokens de autorização de saudação enviadas tooyour back aplicativo após uma experiência de inscrição ou entrada bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fe72b-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="fe72b-118">Por exemplo, selecione **Nome de Exibição**, **Provedor de Identidade**, **CEP**, **Novo Usuário** e **ID de Objeto do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="fe72b-120">Clique em **criar** tooadd política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe72b-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="fe72b-121">Olá diretiva é listada como **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-121">hello policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="fe72b-122">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="fe72b-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="fe72b-123">Abrir a diretiva de saudação selecionando **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-123">Open hello policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="fe72b-124">Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="fe72b-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="fe72b-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="fe72b-126">Setting</span></span>      | <span data-ttu-id="fe72b-127">Valor</span><span class="sxs-lookup"><span data-stu-id="fe72b-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="fe72b-128">**Aplicativos**</span><span class="sxs-lookup"><span data-stu-id="fe72b-128">**Applications**</span></span> | <span data-ttu-id="fe72b-129">Aplicativo B2C da Contoso</span><span class="sxs-lookup"><span data-stu-id="fe72b-129">Contoso B2C app</span></span> |
| <span data-ttu-id="fe72b-130">**Selecionar URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="fe72b-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="fe72b-131">Abre uma nova guia do navegador e você pode verificar a experiência do consumidor de inscrever-se ou entrar hello como configurado.</span><span class="sxs-lookup"><span data-stu-id="fe72b-131">A new browser tab opens, and you can verify hello sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="fe72b-132">Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="fe72b-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>