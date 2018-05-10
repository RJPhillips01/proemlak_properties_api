FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY proemlakapi.properties/proemlakapi.properties.csproj proemlakapi.properties/
RUN dotnet restore proemlakapi.properties/proemlakapi.properties.csproj
COPY . .
WORKDIR /src/proemlakapi.properties
RUN dotnet build proemlakapi.properties.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish proemlakapi.properties.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "proemlakapi.properties.dll"]
