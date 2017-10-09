<span data-ttu-id="28edb-101">Criar credenciais de implantação com hello [usuário az webapp implantação definido](/cli/azure/webapp/deployment/user#set) comando.</span><span class="sxs-lookup"><span data-stu-id="28edb-101">Create deployment credentials with hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command.</span></span>

<span data-ttu-id="28edb-102">Um usuário de implantação é necessário para FTP e Git implantação tooa o aplicativo web local.</span><span class="sxs-lookup"><span data-stu-id="28edb-102">A deployment user is required for FTP and local Git deployment tooa web app.</span></span> <span data-ttu-id="28edb-103">Olá nome de usuário e senha são o nível de conta.</span><span class="sxs-lookup"><span data-stu-id="28edb-103">hello user name and password are account level.</span></span> <span data-ttu-id="28edb-104">_Eles são diferentes das credenciais da sua assinatura do Azure._</span><span class="sxs-lookup"><span data-stu-id="28edb-104">_They are different from your Azure subscription credentials._</span></span>

<span data-ttu-id="28edb-105">Olá a seguir de comando, substitua  *\<nome de usuário >* e  *\<senha >* com um novo nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="28edb-105">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="28edb-106">nome de usuário Olá deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="28edb-106">hello user name must be unique.</span></span> <span data-ttu-id="28edb-107">Hello senha deve ter pelo menos oito caracteres, com dois Olá após três elementos: letras, números, símbolos.</span><span class="sxs-lookup"><span data-stu-id="28edb-107">hello password must be at least eight characters long, with two of hello following three elements: letters, numbers, symbols.</span></span> 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="28edb-108">Se você receber um ` 'Conflict'. Details: 409` erro, o nome de usuário de saudação de alteração.</span><span class="sxs-lookup"><span data-stu-id="28edb-108">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="28edb-109">Se receber um erro ` 'Bad Request'. Details: 400`, use uma senha mais forte.</span><span class="sxs-lookup"><span data-stu-id="28edb-109">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

<span data-ttu-id="28edb-110">Você só cria esse usuário de implantação uma vez; é possível usá-lo para todas as implantações do Azure.</span><span class="sxs-lookup"><span data-stu-id="28edb-110">You create this deployment user only once; you can use it for all your Azure deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="28edb-111">Nome de usuário de saudação do registro e a senha.</span><span class="sxs-lookup"><span data-stu-id="28edb-111">Record hello user name and password.</span></span> <span data-ttu-id="28edb-112">Você precisa-los toodeploy Olá web aplicativo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="28edb-112">You need them toodeploy hello web app later.</span></span>
>
>