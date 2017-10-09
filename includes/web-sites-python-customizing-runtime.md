<span data-ttu-id="d8aa0-101">Azure determinará a versão de saudação do Python toouse para seu ambiente virtual com hello prioridade a seguir:</span><span class="sxs-lookup"><span data-stu-id="d8aa0-101">Azure will determine hello version of Python toouse for its virtual environment with hello following priority:</span></span>

1. <span data-ttu-id="d8aa0-102">versão especificada em runtime.txt na pasta raiz de saudação</span><span class="sxs-lookup"><span data-stu-id="d8aa0-102">version specified in runtime.txt in hello root folder</span></span>
2. <span data-ttu-id="d8aa0-103">versão especificada pela configuração de Python na configuração de aplicativo da web hello (Olá **configurações** > **configurações de aplicativo** folha para seu aplicativo web no hello Portal do Azure)</span><span class="sxs-lookup"><span data-stu-id="d8aa0-103">version specified by Python setting in hello web app configuration (hello **Settings** > **Application Settings** blade for your web app in hello Azure Portal)</span></span>
3. <span data-ttu-id="d8aa0-104">Python 2.7 é o padrão de saudação se Olá acima são especificados</span><span class="sxs-lookup"><span data-stu-id="d8aa0-104">python-2.7 is hello default if none of hello above are specified</span></span>

<span data-ttu-id="d8aa0-105">Valores válidos para o conteúdo de saudação do</span><span class="sxs-lookup"><span data-stu-id="d8aa0-105">Valid values for hello contents of</span></span> 

    \runtime.txt

<span data-ttu-id="d8aa0-106">são:</span><span class="sxs-lookup"><span data-stu-id="d8aa0-106">are:</span></span>

* <span data-ttu-id="d8aa0-107">python-2.7</span><span class="sxs-lookup"><span data-stu-id="d8aa0-107">python-2.7</span></span>
* <span data-ttu-id="d8aa0-108">python-3.4</span><span class="sxs-lookup"><span data-stu-id="d8aa0-108">python-3.4</span></span>

<span data-ttu-id="d8aa0-109">Se versão micro hello (terceiro dígito) for especificado, ele será ignorado.</span><span class="sxs-lookup"><span data-stu-id="d8aa0-109">If hello micro version (third digit) is specified, it is ignored.</span></span>

