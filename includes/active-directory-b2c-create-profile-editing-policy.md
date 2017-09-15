<span data-ttu-id="1bc20-101">Para habilitar a edição de perfil no aplicativo, você precisará criar uma política de edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="1bc20-101">To enable profile editing on your application, you will need to create a profile editing policy.</span></span> <span data-ttu-id="1bc20-102">Essa política descreve as experiências pelas quais os consumidores passarão durante a edição do perfil e o conteúdo de tokens que o aplicativo receberá na conclusão bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1bc20-102">This policy describes the experiences that consumers will go through during profile editing and the contents of tokens that the application will receive on successful completion.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="1bc20-103">Na seção de políticas das configurações, selecione **Políticas de edição de perfil** e clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-103">In the policies section of settings, select **Profile editing policies** and click **+ Add**.</span></span>

![Selecione as Políticas de edição de perfil e clique no botão Adicionar](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-policy.png)

<span data-ttu-id="1bc20-105">Insira um **Nome** de política para referência de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1bc20-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="1bc20-106">Por exemplo, insira: `SiPe`.</span><span class="sxs-lookup"><span data-stu-id="1bc20-106">For example, enter `SiPe`.</span></span>

<span data-ttu-id="1bc20-107">Clique em **Provedores de identidade** e marque **Entrada na Conta Local**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-107">Select **Identity providers** and check **Local Account Signin**.</span></span> <span data-ttu-id="1bc20-108">Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado.</span><span class="sxs-lookup"><span data-stu-id="1bc20-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="1bc20-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-109">Click **OK**.</span></span>

![Selecione Inscrição na Conta Local como provedor de identidade e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-identity-providers.png)

<span data-ttu-id="1bc20-111">Selecione **Atributos do perfil**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-111">Select **Profile attributes**.</span></span> <span data-ttu-id="1bc20-112">Escolha os atributos que o consumidor pode exibir e editar no perfil.</span><span class="sxs-lookup"><span data-stu-id="1bc20-112">Choose attributes the consumer can view and edit in their profile.</span></span> <span data-ttu-id="1bc20-113">Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="1bc20-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-114">Click **OK**.</span></span>

![Selecione alguns atributos e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-attributes.png)

<span data-ttu-id="1bc20-116">Selecione **Declarações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-116">Select **Application claims**.</span></span> <span data-ttu-id="1bc20-117">Escolha as declarações que você quer retornar nos tokens de autorização enviados ao aplicativo após uma experiência de edição de perfil bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1bc20-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful profile editing experience.</span></span> <span data-ttu-id="1bc20-118">Por exemplo, selecione **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-118">For example, select **Display Name**, **Postal Code**.</span></span>

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-profile-editing-policy/add-b2c-editing-application-claims.png)

<span data-ttu-id="1bc20-120">Clique em **Criar** para adicionar a política.</span><span class="sxs-lookup"><span data-stu-id="1bc20-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="1bc20-121">A política está listada como **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-121">The policy is listed as **B2C_1_SiPe**.</span></span> <span data-ttu-id="1bc20-122">O prefixo **B2C_1_** está anexado ao nome.</span><span class="sxs-lookup"><span data-stu-id="1bc20-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="1bc20-123">Abra a política selecionando **B2C_1_SiPe**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-123">Open the policy by selecting **B2C_1_SiPe**.</span></span> <span data-ttu-id="1bc20-124">Verifique as configurações especificadas na tabela e, depois, clique em **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="1bc20-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-profile-editing-policy/run-b2c-editing-policy.png)

| <span data-ttu-id="1bc20-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="1bc20-126">Setting</span></span>      | <span data-ttu-id="1bc20-127">Valor</span><span class="sxs-lookup"><span data-stu-id="1bc20-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="1bc20-128">**Aplicativos**</span><span class="sxs-lookup"><span data-stu-id="1bc20-128">**Applications**</span></span> | <span data-ttu-id="1bc20-129">Aplicativo B2C da Contoso</span><span class="sxs-lookup"><span data-stu-id="1bc20-129">Contoso B2C app</span></span> |
| <span data-ttu-id="1bc20-130">**Selecionar URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="1bc20-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="1bc20-131">Uma nova guia do navegador é aberta e você poderá verificar a experiência de edição de perfil do consumidor, conforme configurado.</span><span class="sxs-lookup"><span data-stu-id="1bc20-131">A new browser tab opens, and you can verify the profile editing consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="1bc20-132">Leva até um minuto para a criação de políticas e as atualizações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="1bc20-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>