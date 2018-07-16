---
title: Impor HTTPS no núcleo do ASP.NET
author: rick-anderson
description: Mostra como exigir HTTPS/TLS em um núcleo de ASP.NET aplicativo web.
ms.author: riande
ms.date: 2/9/2018
uid: security/enforcing-ssl
ms.openlocfilehash: 6a16bb2253fcb6e81a294f1c484db1a3e80796e2
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36277264"
---
# <a name="enforce-https-in-aspnet-core"></a>Impor HTTPS no núcleo do ASP.NET

Por [Rick Anderson](https://twitter.com/RickAndMSFT)

Este documento demonstra como:

* Exigir HTTPS para todas as solicitações.
* Redirecione todas as solicitações HTTP para HTTPS.

> [!WARNING]
> **Não** use [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) em Web APIs que recebe informações confidenciais. `RequireHttpsAttribute` usa códigos de status HTTP para redirecionar navegadores de HTTP para HTTPS. Clientes de API podem não entender ou obedecer redirecionamentos de HTTP para HTTPS. Esses clientes podem enviar informações sobre HTTP. APIs da Web deverá:
>
> * Não escuta no HTTP.
> * Feche a conexão com o código de status 400 (Bad Request) e não atender à solicitação.

<a name="require"></a>
## <a name="require-https"></a>Exigir HTTPS

::: moniker range=">= aspnetcore-2.1"

É recomendável que todos os aplicativos web do ASP.NET Core chamar Middleware de redirecionamento de HTTPS ([UseHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpspolicybuilderextensions.usehttpsredirection)) para redirecionar todas as solicitações HTTP para HTTPS.

O código a seguir chama `UseHttpsRedirection` no `Startup` classe:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=13)]

O código a seguir chama [AddHttpsRedirection](/dotnet/api/microsoft.aspnetcore.builder.httpsredirectionservicesextensions.addhttpsredirection) para configurar as opções de middleware:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=14-99)]

O código realçado acima:

* Conjuntos de [HttpsRedirectionOptions.RedirectStatusCode](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.redirectstatuscode) para `Status307TemporaryRedirect`, que é o valor padrão. Aplicativos de produção devem chamar [UseHsts](#hsts).
* Define a porta HTTPS para 5001. O valor padrão é 443.

Os seguintes mecanismos defina a porta automaticamente:

* O middleware pode descobrir as portas por meio de [IServerAddressesFeature](/dotnet/api/microsoft.aspnetcore.hosting.server.features.iserveraddressesfeature) quando as seguintes condições se aplicam:
  - Kestrel ou HTTP. sys é usado diretamente com pontos de extremidade HTTPS (também se aplica ao executar o aplicativo com o depurador do Visual Studio Code).
  - Somente **uma porta HTTPS** é usada pelo aplicativo.
* O Visual Studio é usado:
  - O IIS Express tem habilitadas para HTTPS.
  - *launchSettings.json* define o `sslPort` para IIS Express.

> [!NOTE]
> Quando um aplicativo é executado por trás de um proxy reverso (por exemplo, IIS, IIS Express), `IServerAddressesFeature` não está disponível. A porta deve ser configurada manualmente. Quando a porta não for definida, as solicitações não são redirecionadas.

A porta pode ser configurada definindo o:

* A variável de ambiente `ASPNETCORE_HTTPS_PORT`.
* `http_port` chave de configuração de host (por exemplo, via *hostsettings.json* ou um argumento de linha de comando).
* [HttpsRedirectionOptions.HttpsPort](/dotnet/api/microsoft.aspnetcore.httpspolicy.httpsredirectionoptions.httpsport). Consulte o exemplo anterior que mostra como definir a porta como 5001.

> [!NOTE]
> A porta pode ser configurada indiretamente definindo a URL com o `ASPNETCORE_URLS` variável de ambiente. A variável de ambiente configura o servidor e, em seguida, o middleware indiretamente descobre a porta HTTPS por meio de `IServerAddressesFeature`.

Se a porta não está definida:

* As solicitações não são redirecionadas.
* O middleware registra um aviso.

> [!NOTE]
> Uma alternativa ao uso de Middleware de redirecionamento de HTTPS (`UseHttpsRedirection`) é usar o Middleware de regravação de URL (`AddRedirectToHttps`). `AddRedirectToHttps` também pode definir o código de status e a porta quando o redirecionamento é executado. Para obter mais informações, consulte [Middleware de regravação de URL](xref:fundamentals/url-rewriting).
>
> Ao redirecionar para HTTPS sem a necessidade de regras de redirecionamento adicionais, é recomendável usar HTTPS redirecionamento Middleware (`UseHttpsRedirection`) descrito neste tópico.

::: moniker-end

::: moniker range="< aspnetcore-2.1"

O [RequireHttpsAttribute](/dotnet/api/microsoft.aspnetcore.mvc.requirehttpsattribute) é usada para exigir HTTPS. `[RequireHttpsAttribute]` pode decorar controladores ou métodos, ou podem ser aplicadas globalmente. Para aplicar o atributo global, adicione o seguinte código ao `ConfigureServices` em `Startup`:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet2&highlight=4-999)]

O código realçado anterior requer todas as solicitações usar `HTTPS`; portanto, as solicitações HTTP são ignoradas. O seguinte código realçado redireciona todas as solicitações HTTP para HTTPS:

[!code-csharp[](authentication/accconfirm/sample/WebApp1/Startup.cs?name=snippet_AddRedirectToHttps&highlight=7-999)]

Para obter mais informações, consulte [Middleware de regravação de URL](xref:fundamentals/url-rewriting). O middleware também permite que o aplicativo para definir o código de status ou o código de status e a porta quando o redirecionamento é executado.

Exigir HTTPS globalmente (`options.Filters.Add(new RequireHttpsAttribute());`) é uma prática recomendada de segurança. Aplicar o `[RequireHttps]` atributo para todas as páginas Razor/controladores não é considerado mais seguro que exijam HTTPS globalmente. Você não pode garantir a `[RequireHttps]` atributo é aplicado quando forem adicionadas novos controladores e páginas Razor.

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="hsts"></a>
## <a name="http-strict-transport-security-protocol-hsts"></a>Protocolo de segurança de transporte estrito de HTTP (HSTS)

Por [OWASP](https://www.owasp.org/index.php/About_The_Open_Web_Application_Security_Project), [segurança de transporte estrito HTTP (HSTS)](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) é um aprimoramento de segurança de aceitação é especificado por um aplicativo web com o uso de um cabeçalho de resposta especial. Depois que um navegador com suporte recebe esse cabeçalho navegador impedirá todas as comunicações do que está sendo enviada via HTTP no domínio especificado e enviará, em vez disso, todas as comunicações via HTTPS. Ele também evita avisos em navegadores de cliques HTTPS.

2.1 ou posterior do ASP.NET Core implementa HSTS com o `UseHsts` método de extensão. O código a seguir chama `UseHsts` quando o aplicativo não está em [modo de desenvolvimento](xref:fundamentals/environments):

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet1&highlight=10)]

`UseHsts` não é recomendado em desenvolvimento porque o cabeçalho HSTS é altamente armazenável em cache por navegadores. Por padrão, `UseHsts` exclui o endereço de loopback local.

O código a seguir:

[!code-csharp[](enforcing-ssl/sample/Startup.cs?name=snippet2&highlight=5-12)]

* Define o parâmetro de pré-carregamento do cabeçalho de segurança de transporte Strict. Pré-carregamento não é parte do [especificação RFC HSTS](https://tools.ietf.org/html/rfc6797), mas é compatível com navegadores da web para pré-carregar sites HSTS nova instalação. Veja [https://hstspreload.org/](https://hstspreload.org/) para obter mais informações.
* Permite [includeSubDomain](https://tools.ietf.org/html/rfc6797#section-6.1.2), que se aplica a política HSTS a subdomínios de Host. 
* Define explicitamente o parâmetro de idade máxima do cabeçalho de segurança de transporte Strict para 60 dias. Se não for definido, o padrão é 30 dias. Consulte o [max-age diretiva](https://tools.ietf.org/html/rfc6797#section-6.1.1) para obter mais informações.
* Adiciona `example.com` à lista de hosts a serem excluídos.

`UseHsts` Exclui os seguintes hosts de loopback:

* `localhost` : O endereço de loopback do IPv4.
* `127.0.0.1` : O endereço de loopback do IPv4.
* `[::1]` : O endereço de loopback de IPv6.

O exemplo anterior mostra como adicionar outros hosts.
::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<a name="https"></a>
## <a name="opt-out-of-https-on-project-creation"></a>Recusar HTTPS na criação do projeto

Os modelos de aplicativos do ASP.NET Core web 2.1 ou posterior (do Visual Studio ou a linha de comando dotnet) habilitam [redirecionamento HTTPS](#require) e [HSTS](#hsts). Para implantações que não exijam HTTPS, você pode recusar o HTTPS. Por exemplo, alguns serviços de back-end onde HTTPS está sendo tratado externamente na borda, usando HTTPS em cada nó não é necessária.

Para recusar o HTTPS:

# <a name="visual-studiotabvisual-studio"></a>[Visual Studio](#tab/visual-studio) 

Desmarque o **configurar para HTTPS** caixa de seleção.

![Diagrama de entidade](enforcing-ssl/_static/out.png)

#   <a name="net-core-clitabnetcore-cli"></a>[CLI do .NET Core](#tab/netcore-cli) 

Use a opção `--no-https`. Por exemplo

```console
dotnet new webapp --no-https
```

[!INCLUDE[](~/includes/webapp-alias-notice.md)]

---

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="how-to-setup-a-developer-certificate-for-docker"></a>Como configurar um certificado do desenvolvedor para Docker

Consulte [esse problema do GitHub](https://github.com/aspnet/Docs/issues/6199).

::: moniker-end
