FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY WebSiteTest/WebSiteTest.csproj WebSiteTest/
RUN dotnet restore WebSiteTest/WebSiteTest.csproj
COPY . .
WORKDIR /src/WebSiteTest
RUN dotnet build WebSiteTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WebSiteTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebSiteTest.dll"]
