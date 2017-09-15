<span data-ttu-id="9d5af-101">Para habilitar a entrada no aplicativo, você precisará criar uma política de entrada.</span><span class="sxs-lookup"><span data-stu-id="9d5af-101">To enable sign-in on your application, you will need to create a sign-in policy.</span></span> <span data-ttu-id="9d5af-102">Essa política descreve as experiências pelas quais os consumidores passarão durante a entrada e o conteúdo de tokens que o aplicativo receberá de entradas bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="9d5af-102">This policy describes the experiences that consumers will go through during sign-in and the contents of tokens that the application will receive on successful sign-ins.</span></span>

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="9d5af-103">Na seção de políticas das configurações, selecione **Políticas de inscrição ou entrada** e clique em **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-103">In the policies section of settings, select **Sign-up or sign-in policies** and click **+ Add**.</span></span>

![Selecione as políticas de inscrição ou entrada e clique no botão Adicionar](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-policy.png)

<span data-ttu-id="9d5af-105">Insira um **Nome** de política para referência de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9d5af-105">Enter a policy **Name** for your application to reference.</span></span> <span data-ttu-id="9d5af-106">Por exemplo, insira: `SiUpIn`.</span><span class="sxs-lookup"><span data-stu-id="9d5af-106">For example, enter `SiUpIn`.</span></span>

<span data-ttu-id="9d5af-107">Selecione **Provedores de identidade** e marque **Inscrição por email**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-107">Select **Identity providers** and check **Email signup**.</span></span> <span data-ttu-id="9d5af-108">Opcionalmente, você também pode selecionar provedores de identidade social, se já configurado.</span><span class="sxs-lookup"><span data-stu-id="9d5af-108">Optionally, you can also select social identity providers, if already configured.</span></span> <span data-ttu-id="9d5af-109">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-109">Click **OK**.</span></span>

![Selecione Inscrição por email como provedor de identidade e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-identity-providers.png)

<span data-ttu-id="9d5af-111">Selecione **Atributos de inscrição**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-111">Select **Sign-up attributes**.</span></span> <span data-ttu-id="9d5af-112">Escolha os atributos que você deseja coletar do consumidor durante a inscrição.</span><span class="sxs-lookup"><span data-stu-id="9d5af-112">Choose attributes you want to collect from the consumer during sign-up.</span></span> <span data-ttu-id="9d5af-113">Por exemplo, marque **País/Região**, **Nome de Exibição** e **CEP**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-113">For example, check **Country/Region**, **Display Name**, and **Postal Code**.</span></span> <span data-ttu-id="9d5af-114">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-114">Click **OK**.</span></span>

![Selecione alguns atributos e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-sign-up-attributes.png)

<span data-ttu-id="9d5af-116">Selecione **Declarações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-116">Select **Application claims**.</span></span> <span data-ttu-id="9d5af-117">Escolha as declarações que você deseja retornar nos tokens de autorização enviados ao aplicativo após uma experiência de inscrição ou entrada bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="9d5af-117">Choose claims you want returned in the authorization tokens sent back to your application after a successful sign-up or sign-in experience.</span></span> <span data-ttu-id="9d5af-118">Por exemplo, selecione **Nome de Exibição**, **Provedor de Identidade**, **CEP**, **Novo Usuário** e **ID de Objeto do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-118">For example, select **Display Name**, **Identity Provider**, **Postal Code**, **User is new** and **User's Object ID**.</span></span>

![Selecione algumas declarações de aplicativo e clique no botão OK](media/active-directory-b2c-create-sign-in-sign-up-policy/add-b2c-signup-signin-application-claims.png)

<span data-ttu-id="9d5af-120">Clique em **Criar** para adicionar a política.</span><span class="sxs-lookup"><span data-stu-id="9d5af-120">Click **Create** to add the policy.</span></span> <span data-ttu-id="9d5af-121">A política está listada como **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-121">The policy is listed as **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="9d5af-122">O prefixo **B2C_1_** está anexado ao nome.</span><span class="sxs-lookup"><span data-stu-id="9d5af-122">The **B2C_1_** prefix is appended to the name.</span></span>

<span data-ttu-id="9d5af-123">Abra a política selecionando **B2C_1_SiUpIn**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-123">Open the policy by selecting **B2C_1_SiUpIn**.</span></span> <span data-ttu-id="9d5af-124">Verifique as configurações especificadas na tabela e, depois, clique em **Executar agora**.</span><span class="sxs-lookup"><span data-stu-id="9d5af-124">Verify the settings specified in the table then click **Run now**.</span></span>

![Selecione a política e execute-a](media/active-directory-b2c-create-sign-in-sign-up-policy/run-b2c-signup-signin-policy.png)

| <span data-ttu-id="9d5af-126">Configuração</span><span class="sxs-lookup"><span data-stu-id="9d5af-126">Setting</span></span>      | <span data-ttu-id="9d5af-127">Valor</span><span class="sxs-lookup"><span data-stu-id="9d5af-127">Value</span></span>  |
| ------------ | ------ |
| <span data-ttu-id="9d5af-128">**Aplicativos**</span><span class="sxs-lookup"><span data-stu-id="9d5af-128">**Applications**</span></span> | <span data-ttu-id="9d5af-129">Aplicativo B2C da Contoso</span><span class="sxs-lookup"><span data-stu-id="9d5af-129">Contoso B2C app</span></span> |
| <span data-ttu-id="9d5af-130">**Selecionar URL de resposta**</span><span class="sxs-lookup"><span data-stu-id="9d5af-130">**Select reply url**</span></span> | `https://localhost:44316/` |

<span data-ttu-id="9d5af-131">Uma nova guia do navegador é aberta e você poderá verificar a experiência de inscrição ou entrada do consumidor, conforme configurado.</span><span class="sxs-lookup"><span data-stu-id="9d5af-131">A new browser tab opens, and you can verify the sign-up or sign-in consumer experience as configured.</span></span>

> [!NOTE]
> <span data-ttu-id="9d5af-132">Leva até um minuto para a criação de políticas e as atualizações entrem em vigor.</span><span class="sxs-lookup"><span data-stu-id="9d5af-132">It takes up to a minute for policy creation and updates to take effect.</span></span>
>