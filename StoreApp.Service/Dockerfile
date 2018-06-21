FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY StoreApp.Service/StoreApp.Service.csproj StoreApp.Service/
RUN dotnet restore StoreApp.Service/StoreApp.Service.csproj
COPY . .
WORKDIR /src/StoreApp.Service
RUN dotnet build StoreApp.Service.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish StoreApp.Service.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "StoreApp.Service.dll"]
