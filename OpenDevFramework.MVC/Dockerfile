FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY OpenDevFramework.MVC/OpenDevFramework.MVC.csproj OpenDevFramework.MVC/
RUN dotnet restore OpenDevFramework.MVC/OpenDevFramework.MVC.csproj
COPY . .
WORKDIR /src/OpenDevFramework.MVC
RUN dotnet build OpenDevFramework.MVC.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish OpenDevFramework.MVC.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OpenDevFramework.MVC.dll"]
