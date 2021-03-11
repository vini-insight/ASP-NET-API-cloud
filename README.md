# SQLserverEFcoreMVC
SQLserverEFcoreMVC


PASSO - tem um passo que cria XML não sei pra q. e outras coisas. acho que funciona se copiar isso no .csproj:

    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
      <DocumentationFile>C:\Users\Short\source\repos\CursoDigitalOne\CursoAPI\CursoAPI.xml</DocumentationFile>
    </PropertyGroup>

    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
      <DocumentationFile>C:\Users\Short\source\repos\CursoDigitalOne\CursoAPI\CursoAPI.xml</DocumentationFile>
    </PropertyGroup>

PASSO - adicionar pacote que dá suporte ao SWAGGER e OpenApi:

    dotnet add package Swashbuckle.AspNetCore --version 5.0.0-rc5

 - injetar dependência do SWAGGER e do EFcore em Startup.cs no método ConfigureServices():

    services.AddSwaggerGen(c => { c.SwaggerDoc("v1", new OpenApiInfo { Title = "Curso API", Version = "v1" }); });
    services.AddDbContext<Context>();
    services.AddDbContext<Context>(options => options.UseSqlServer(connection));

- Adicionar Middlewares em Statup.cs no método Configure():

    app.UseSwagger();
    app.UseSwaggerUI(c => { c.SwaggerEndpoint("/swagger/v1/swagger.json", "Curso API"); });

PASSO - adicionar referencia do projeto anterior no projeto atual:

no .csproj fazer:

    <ItemGroup>
      <ProjectReference Include="..\SQLserverEFcoreMVC\SQLserverEFcoreMVC.csproj" />
    </ItemGroup>

desse jeito o projeto atual vai ter acesso aos modelos e contextos de BD já criados.

Dependencias:

    dotnet add package Microsoft.EntityFrameworkCore.Tools --version 3.1.1

    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 3.1.1

    dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 3.1.1

COMMANDS:

    dotnet aspnet-codegenerator controller -name ExampleController -actions -api -outDir Controllers
    dotnet aspnet-codegenerator controller -name CategoriaController -actions -nv -m Categoria -dc Context -outDir Controllers

    dotnet aspnet-codegenerator controller -name CategoriaController -api -m Categoria -dc Context -outDir Controllers    
    
    dotnet aspnet-codegenerator controller -name ProdutoController -api -m Produto -dc Context -outDir Controllers


# Command Controller Generator Options:

    dotnet aspnet-codegenerator controller -h



    –controllerName | -name : Name of the controller

    –useAsyncActions | -async : Switch to indicate whether to generate async controller actions

    –noViews | -nv : Switch to indicate whether to generate CRUD views. Observe que para gerar views você apenas deve omitir esta opção de comando.

    –restWithNoViews | -api : Specify this switch to generate a Controller with REST style API, noViews is assumed and any view related options are ignored

    –readWriteActions | -actions : Specify this switch to generate Controller with read/write actions when a Model class is not used

    –model | -m : Model class to use

    –dataContext | -dc : DbContext class to use

    –referenceScriptLibraries | -scripts : Switch to specify whether to reference script libraries in the generated views

    –layout | -l : Custom Layout page to use

    –useDefaultLayout | -udl : Switch to specify that default layout should be used for the views

    –force | -f : Use this option to overwrite existing files

    –relativeFolderPath | -outDir : Specify the relative output folder path from project where the file needs to be generated, if not specified, file will be generated in the project folder

    –controllerNamespace | -namespace : Specify the name of the namespace to use for the generated controller


# para acessar SWAGGER

    https://localhost:5001/swagger/index.html



_______________________________________________________________________________________________________________________________________________________________________________

SQL server Entity Framework core Migrations MVC

projeto criado com o comando

    dotnet new mvc

Usando o modelo Code First do Enntity Framework

    [X] code first
    [ ] model first
    [ ] database first


Dependencias:

    dotnet add package Microsoft.EntityFrameworkCore.Tools --version 3.1.1

    dotnet add package Microsoft.EntityFrameworkCore.SqlServer --version 3.1.1

    dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 3.1.1


EFcore --version 3.1.3 INSTALADO GLOBALMENTE:
    
    dotnet tool install --global dotnet-ef --version 3.1.3

MIGRATIONS AND UPDATE DATABASE

    dotnet ef migrations add CreateDatabase

    dotnet ef database update

tentar instalar globalmente

    dotnet tool install --global dotnet-aspnet-codegenerator --version 3.1.1

pra ver se não precisa isntalar o pacote abaixo?

    dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design --version 3.1.1


Baseado nos seguintes Tutoriais:

    https://www.youtube.com/watch?v=knCH5cEo-Vo
    https://gavilan.blog/2018/04/28/asp-net-core-2-doing-scaffolding-with-dotnet-cli-aspnet-codegenerator/
    https://github.com/gavilanch/example-scaffolding-with-dotnet-cli
    https://github.com/Clavico/CursoDigitalOne
    https://github.com/Clavico/CursoDigitalOne/tree/master/CursoMVC


COMANDS:

    dotnet aspnet-codegenerator controller -name PeopleController -actions -m Person -dc ApplicationDbContext -outDir Controllers

    dotnet aspnet-codegenerator controller -name CategoriaController -actions -m Categoria -dc Context -outDir Controllers

    dotnet aspnet-codegenerator controller -name ProdutoController -actions -m Produto -dc Context -outDir Controllers


END README.

acessível em: 

    https://localhost:5001/

    https://localhost:5001/Produto
    
    https://localhost:5001/produto/Create

