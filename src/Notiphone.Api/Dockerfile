FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 52340
EXPOSE 44381

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY src/Notiphone.Api/Notiphone.Api.csproj src/Notiphone.Api/
RUN dotnet restore src/Notiphone.Api/Notiphone.Api.csproj
COPY . .
WORKDIR /src/src/Notiphone.Api
RUN dotnet build Notiphone.Api.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Notiphone.Api.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Notiphone.Api.dll"]
