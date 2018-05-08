FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY TestWebService/TestWebService.csproj TestWebService/
RUN dotnet restore TestWebService/TestWebService.csproj
COPY . .
WORKDIR /src/TestWebService
RUN dotnet build TestWebService.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TestWebService.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestWebService.dll"]
