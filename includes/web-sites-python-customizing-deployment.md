<span data-ttu-id="d5e2c-101">O Azure determinará que o aplicativo usa Python **se estas duas condições forem verdadeiras**:</span><span class="sxs-lookup"><span data-stu-id="d5e2c-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="d5e2c-102">arquivo requirements.txt na pasta raiz</span><span class="sxs-lookup"><span data-stu-id="d5e2c-102">requirements.txt file in the root folder</span></span>
* <span data-ttu-id="d5e2c-103">qualquer arquivo .py na pasta raiz OU um runtime.txt que especifica o python</span><span class="sxs-lookup"><span data-stu-id="d5e2c-103">any .py file in the root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="d5e2c-104">Quando é o caso desta última opção, ele usará um script de implantação específico do Python, que executa a sincronização padrão de arquivos e também outras operações de Python, como:</span><span class="sxs-lookup"><span data-stu-id="d5e2c-104">When that's the case, it will use a Python specific deployment script, which performs the standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="d5e2c-105">Gerenciamento automático do ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="d5e2c-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="d5e2c-106">Instalação de pacotes listados em requirements.txt usando o pip</span><span class="sxs-lookup"><span data-stu-id="d5e2c-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="d5e2c-107">Criação do web.config apropriado com base na versão do Python selecionada.</span><span class="sxs-lookup"><span data-stu-id="d5e2c-107">Creation of the appropriate web.config based on the selected Python version.</span></span>
* <span data-ttu-id="d5e2c-108">Coletar arquivos estáticos para aplicativos Django</span><span class="sxs-lookup"><span data-stu-id="d5e2c-108">Collect static files for Django applications</span></span>

<span data-ttu-id="d5e2c-109">Você pode controlar determinados aspectos das etapas de implantação padrão sem precisar personalizar o script.</span><span class="sxs-lookup"><span data-stu-id="d5e2c-109">You can control certain aspects of the default deployment steps without having to customize the script.</span></span>

<span data-ttu-id="d5e2c-110">Se você quiser ignorar todas as etapas de implantação específica de Python, você pode criar esse arquivo vazio:</span><span class="sxs-lookup"><span data-stu-id="d5e2c-110">If you want to skip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="d5e2c-111">Para obter mais controle sobre a implantação, você pode substituir o script de implantação padrão ao criar os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="d5e2c-111">For more control over deployment, you can override the default deployment script by creating the following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="d5e2c-112">Você pode usar o [interface de linha de comando do Azure] [ Azure command-line interface] para criar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="d5e2c-112">You can use the [Azure command-line interface][Azure command-line interface] to create the files.</span></span>  <span data-ttu-id="d5e2c-113">Use este comando da pasta do projeto:</span><span class="sxs-lookup"><span data-stu-id="d5e2c-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="d5e2c-114">Quando esses arquivos não existem, o Azure cria um script de implantação temporária e o executa.</span><span class="sxs-lookup"><span data-stu-id="d5e2c-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="d5e2c-115">Ele é idêntico àquele que você cria com o comando acima.</span><span class="sxs-lookup"><span data-stu-id="d5e2c-115">It is identical to the one you create with the command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
