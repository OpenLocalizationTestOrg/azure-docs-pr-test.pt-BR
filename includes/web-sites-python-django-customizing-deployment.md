<span data-ttu-id="08c78-101">O Azure determinará que o aplicativo usa Python **se estas duas condições forem verdadeiras**:</span><span class="sxs-lookup"><span data-stu-id="08c78-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="08c78-102">arquivo Requirements.txt na pasta raiz de saudação</span><span class="sxs-lookup"><span data-stu-id="08c78-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="08c78-103">qualquer arquivo py na pasta raiz de saudação ou um runtime.txt que especifica o python</span><span class="sxs-lookup"><span data-stu-id="08c78-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="08c78-104">Quando esse for o caso de Olá, ele usará um script de implantação específica do Python, que executa a sincronização de saudação padrão de arquivos, bem como as operações de Python adicionais, como:</span><span class="sxs-lookup"><span data-stu-id="08c78-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="08c78-105">Gerenciamento automático do ambiente virtual</span><span class="sxs-lookup"><span data-stu-id="08c78-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="08c78-106">Instalação de pacotes listados em requirements.txt usando o pip</span><span class="sxs-lookup"><span data-stu-id="08c78-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="08c78-107">Criação de saudação apropriado Web. config com base em Olá selecionado versão do Python.</span><span class="sxs-lookup"><span data-stu-id="08c78-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="08c78-108">Coletar arquivos estáticos para aplicativos Django</span><span class="sxs-lookup"><span data-stu-id="08c78-108">Collect static files for Django applications</span></span>

<span data-ttu-id="08c78-109">Você pode controlar determinados aspectos de etapas de implantação padrão de saudação sem ter toocustomize Olá script.</span><span class="sxs-lookup"><span data-stu-id="08c78-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="08c78-110">Se você quiser tooskip todas as etapas de implantação específica do Python, você pode criar esse arquivo vazio:</span><span class="sxs-lookup"><span data-stu-id="08c78-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="08c78-111">Se você quiser tooskip coleção de arquivos estáticos para seu aplicativo Django:</span><span class="sxs-lookup"><span data-stu-id="08c78-111">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango 

<span data-ttu-id="08c78-112">Para obter mais controle sobre implantação, você pode substituir o script de implantação padrão de saudação criando Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="08c78-112">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="08c78-113">Você pode usar o hello [interface de linha de comando do Azure] [ Azure command-line interface] toocreate arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="08c78-113">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="08c78-114">Use este comando da pasta do projeto:</span><span class="sxs-lookup"><span data-stu-id="08c78-114">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="08c78-115">Quando esses arquivos não existem, o Azure cria um script de implantação temporária e o executa.</span><span class="sxs-lookup"><span data-stu-id="08c78-115">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="08c78-116">É idêntico toohello criado com o comando Olá acima.</span><span class="sxs-lookup"><span data-stu-id="08c78-116">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
