FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY pluralsight-dotnetcore/pluralsight-dotnetcore.csproj pluralsight-dotnetcore/
RUN dotnet restore pluralsight-dotnetcore/pluralsight-dotnetcore.csproj
COPY . .
WORKDIR /src/pluralsight-dotnetcore
RUN dotnet build pluralsight-dotnetcore.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish pluralsight-dotnetcore.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "pluralsight-dotnetcore.dll"]
