<span data-ttu-id="079d9-101">tooenable refinada redefinição de senha em seu aplicativo, você precisará toocreate uma política de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="079d9-101">tooenable fine-grained password reset on your application, you will need toocreate a password reset policy.</span></span> <span data-ttu-id="079d9-102">Observe que essa senha de todo locatário Olá redefinir a opção especificada [aqui](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="079d9-102">Note that hello tenant-wide password reset option specified [here](../articles/active-directory-b2c/active-directory-b2c-reference-sspr.md).</span></span> <span data-ttu-id="079d9-103">Essa política descreve experiências Olá consumidores Olá revisará durante a redefinição de senha e conteúdo de saudação de tokens que Olá aplicativo receberá mediante a conclusão bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="079d9-103">This policy describes hello experiences that hello consumers will go through during password reset and hello contents of tokens that hello application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="079d9-104">Na seção de políticas de saudação de configurações, selecione **políticas de redefinição de senha** e clique em **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="079d9-104">In hello policies section of settings, select **Password reset policies** and click **+ Add**.</span></span>

![Selecione inscrever-se ou entrar políticas e clique no botão Adicionar de saudação](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-policy.png)

<span data-ttu-id="079d9-106">Insira uma política **nome** para tooreference seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="079d9-106">Enter a policy **Name** for your application tooreference.</span></span> <span data-ttu-id="079d9-107">Por exemplo, insira: `SSPR`.</span><span class="sxs-lookup"><span data-stu-id="079d9-107">For example, enter `SSPR`.</span></span>

<span data-ttu-id="079d9-108">Selecione **Provedores de identidade** e marque **Redefinir senha usando endereço de email**.</span><span class="sxs-lookup"><span data-stu-id="079d9-108">Select **Identity providers** and check **Reset password using email address**.</span></span> <span data-ttu-id="079d9-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="079d9-109">Click **OK**.</span></span>

![Selecione a redefinição de senha usando o endereço de email como um provedor de identidade e clique botão de saudação Okey](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-identity-providers.png)

<span data-ttu-id="079d9-111">Selecione **Declarações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="079d9-111">Select **Application claims**.</span></span> <span data-ttu-id="079d9-112">Escolha declarações que ser retornado em tokens de autorização de saudação enviadas tooyour back aplicativo após a redefinição de senha bem-sucedida experiência.</span><span class="sxs-lookup"><span data-stu-id="079d9-112">Choose claims you want returned in hello authorization tokens sent back tooyour application after a successful password reset experience.</span></span> <span data-ttu-id="079d9-113">Por exemplo, selecione **ID de Objeto do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="079d9-113">For example, select **User's Object ID**.</span></span>

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-password-reset-policy/add-b2c-password-reset-application-claims.png)

<span data-ttu-id="079d9-115">Clique em **criar** tooadd política de saudação.</span><span class="sxs-lookup"><span data-stu-id="079d9-115">Click **Create** tooadd hello policy.</span></span> <span data-ttu-id="079d9-116">Olá diretiva é listada como **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="079d9-116">hello policy is listed as **B2C_1_SSPR**.</span></span> <span data-ttu-id="079d9-117">Olá **B2C_1_** prefixo é o nome de toohello anexado.</span><span class="sxs-lookup"><span data-stu-id="079d9-117">hello **B2C_1_** prefix is appended toohello name.</span></span>

<span data-ttu-id="079d9-118">Abrir a diretiva de saudação selecionando **B2C_1_SSPR**.</span><span class="sxs-lookup"><span data-stu-id="079d9-118">Open hello policy by selecting **B2C_1_SSPR**.</span></span> <span data-ttu-id="079d9-119">Verifique as configurações de saudação especificadas na tabela hello, em seguida, clique em **executar agora**.</span><span class="sxs-lookup"><span data-stu-id="079d9-119">Verify hello settings specified in hello table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-password-reset-policy/run-b2c-password-reset-policy.png)

| <span data-ttu-id="079d9-121">Configuração</span><span class="sxs-lookup"><span data-stu-id="079d9-121">Setting</span></span>      | <span data-ttu-id="079d9-122">Valor</span><span class="sxs-lookup"><span data-stu-id="079d9-122">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="079d9-123">**Aplicativos**</span><span class="sxs-lookup"><span data-stu-id="079d9-123">**Applications**</span></span> | <span data-ttu-id="079d9-124">Aplicativo B2C da Contoso</span><span class="sxs-lookup"><span data-stu-id="079d9-124">Contoso B2C app</span></span> |
| <span data-ttu-id="079d9-125">**Selecionar URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="079d9-125">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="079d9-126">Abre uma nova guia do navegador e você pode verificar a experiência do consumidor em seu aplicativo de redefinição de senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="079d9-126">A new browser tab opens, and you can verify hello password reset consumer experience in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="079d9-127">Ele ocupa tooa minuto para criação de políticas e atualiza tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="079d9-127">It takes up tooa minute for policy creation and updates tootake effect.</span></span>
>
