<span data-ttu-id="e1e80-101">perfil de tooenable edição em seu aplicativo, você precisará toocreate um política de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="e1e80-101">tooenable profile editing on your application, you will need toocreate a profile editing policy.</span></span> <span data-ttu-id="e1e80-102">Essa política descreve as experiências de saudação consumidores revisará durante o conteúdo de edição e saudação do perfil de tokens que o aplicativo hello receberá mediante a conclusão bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e1e80-102">This policy describes hello experiences that consumers will go through during profile editing and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="e1e80-103">Na seção de políticas de saudação de configurações, selecione **políticas de edição de perfil** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-103">In hello policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selecione a edição de políticas de perfil e clique no botão Adicionar de saudação](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="e1e80-105">Insira uma política **nome** para tooreference seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e1e80-105">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="e1e80-106">Por exemplo, insira: `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="e1e80-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="e1e80-107">Clique em **Provedores de identidade** e marque **Entrada na Conta Local**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="e1e80-108">Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado.</span><span class="sxs-lookup"><span data-stu-id="e1e80-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="e1e80-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-109">Click **OK**.</span></span>

![Selecione o Local de conta como um provedor de identidade e clique em botão Olá Okey](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="e1e80-111">Selecione **Atributos do perfil**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-111">Select **Profile attributes**.</span></span> <span data-ttu-id="e1e80-112">Escolha o consumidor de saudação de atributos pode exibir e editar seu perfil.</span><span class="sxs-lookup"><span data-stu-id="e1e80-112">Choose attributes hello consumer can view and edit in their profile.</span></span> <span data-ttu-id="e1e80-113">Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="e1e80-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-114">Click **OK**.</span></span>

![Selecione alguns atributos e clique botão de saudação Okey](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="e1e80-116">Selecione **Declarações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-116">Select **Application claims**.</span></span> <span data-ttu-id="e1e80-117">Escolha a ser retornado em tokens de autorização de saudação de declarações enviadas tooyour back aplicativo após um experiência de edição de perfil bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e1e80-117">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful profile editing experience.</span></span> <span data-ttu-id="e1e80-118">Por exemplo, selecione **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="e1e80-120">Clique em **criar** tooadd política de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1e80-120">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="e1e80-121">Olá diretiva é listada como **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-121">hello policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="e1e80-122">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="e1e80-122">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="e1e80-123">Abrir a diretiva de saudação selecionando **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-123">Open hello policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="e1e80-124">Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="e1e80-124">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="e1e80-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="e1e80-126">Setting</span></span>      | <span data-ttu-id="e1e80-127">Valor</span><span class="sxs-lookup"><span data-stu-id="e1e80-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="e1e80-128">**Aplicativos**</span><span class="sxs-lookup"><span data-stu-id="e1e80-128">**Applications**</span></span> | <span data-ttu-id="e1e80-129">Aplicativo B2C da Contoso</span><span class="sxs-lookup"><span data-stu-id="e1e80-129">Contoso B2C app</span></span> |
| <span data-ttu-id="e1e80-130">**Selecionar URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="e1e80-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="e1e80-131">Abre uma nova guia do navegador e você pode verificar o perfil de saudação editando experiência do consumidor, conforme configurado.</span><span class="sxs-lookup"><span data-stu-id="e1e80-131">A new browser tab opens, and you can verify hello profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="e1e80-132">Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="e1e80-132">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>