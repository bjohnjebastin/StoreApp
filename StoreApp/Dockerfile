FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY StoreApp/StoreApp.csproj StoreApp/
RUN dotnet restore StoreApp/StoreApp.csproj
COPY . .
WORKDIR /src/StoreApp
RUN dotnet build StoreApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish StoreApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "StoreApp.dll"]
