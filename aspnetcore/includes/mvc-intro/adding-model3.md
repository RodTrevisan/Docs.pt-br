
## <a name="test-the-app"></a><span data-ttu-id="ae52b-101">Testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ae52b-101">Test the app</span></span>

* <span data-ttu-id="ae52b-102">Execute o aplicativo e toque no link **Filme Mvc**.</span><span class="sxs-lookup"><span data-stu-id="ae52b-102">Run the app and tap the **Mvc Movie** link.</span></span>
* <span data-ttu-id="ae52b-103">Toque no link **Criar Novo** e crie um filme.</span><span class="sxs-lookup"><span data-stu-id="ae52b-103">Tap the **Create New** link and create a movie.</span></span>

  ![Criar exibição com campos para título, gênero, preço e data de lançamento](../../tutorials/first-mvc-app/adding-model/_static/movies.png)

* <span data-ttu-id="ae52b-105">Talvez você não possa inserir pontos decimais ou vírgulas no campo `Price`.</span><span class="sxs-lookup"><span data-stu-id="ae52b-105">You may not be able to enter decimal points or commas in the `Price` field.</span></span> <span data-ttu-id="ae52b-106">Para dar suporte à [validação jQuery](http://jqueryvalidation.org/) para localidades de idiomas diferentes do inglês que usam uma vírgula (",") para ponto decimal e formatos de data diferentes do inglês dos EUA, você deve tomar medidas para globalizar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ae52b-106">To support [jQuery validation](http://jqueryvalidation.org/) for non-English locales that use a comma (",") for a decimal point, and non US-English date formats, you must take steps to globalize your app.</span></span> <span data-ttu-id="ae52b-107">Consulte https://github.com/aspnet/Docs/issues/4076 e [Recursos adicionais](#additional-resources) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ae52b-107">See https://github.com/aspnet/Docs/issues/4076 and [Additional resources](#additional-resources) for more information.</span></span> <span data-ttu-id="ae52b-108">Por enquanto, digite apenas números inteiros como 10.</span><span class="sxs-lookup"><span data-stu-id="ae52b-108">For now, just enter whole numbers like 10.</span></span>

<a name="displayformatdatelocal"></a>

* <span data-ttu-id="ae52b-109">Em algumas localidades, você precisa especificar o formato da data.</span><span class="sxs-lookup"><span data-stu-id="ae52b-109">In some locales you need to specify the date format.</span></span> <span data-ttu-id="ae52b-110">Consulte o código realçado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ae52b-110">See the highlighted code below.</span></span>

<span data-ttu-id="ae52b-111">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateFormat.cs?name=snippet_1&highlight=2,10)]</span><span class="sxs-lookup"><span data-stu-id="ae52b-111">[!code-csharp[Main](../../tutorials/first-mvc-app/start-mvc/sample/MvcMovie/Models/MovieDateFormat.cs?name=snippet_1&highlight=2,10)]</span></span>

<span data-ttu-id="ae52b-112">Falaremos sobre `DataAnnotations` posteriormente no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ae52b-112">We'll talk about `DataAnnotations` later in the tutorial.</span></span>

<span data-ttu-id="ae52b-113">Tocar em **Criar** faz com que o formulário seja enviado para o servidor, no qual as informações do filme são salvas em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ae52b-113">Tapping **Create** causes the form to be posted to the server, where the movie information is saved in a database.</span></span> <span data-ttu-id="ae52b-114">O aplicativo redireciona para a URL */Movies*, em que as informações do filme recém-criadas são exibidas.</span><span class="sxs-lookup"><span data-stu-id="ae52b-114">The app redirects to the */Movies* URL, where the newly created movie information is displayed.</span></span>

![Exibição de filme mostrando a listagem de filmes recém-criados](../../tutorials/first-mvc-app/adding-model/_static/h.png)

<span data-ttu-id="ae52b-116">Crie duas mais entradas de filme adicionais.</span><span class="sxs-lookup"><span data-stu-id="ae52b-116">Create a couple more movie entries.</span></span> <span data-ttu-id="ae52b-117">Experimente os links **Editar**, **Detalhes** e **Excluir**, que estão todos funcionais.</span><span class="sxs-lookup"><span data-stu-id="ae52b-117">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>