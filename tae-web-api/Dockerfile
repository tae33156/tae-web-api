FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["tae-web-api/tae-web-api.csproj", "tae-web-api/"]
RUN dotnet restore "tae-web-api/tae-web-api.csproj"
COPY . .
WORKDIR "/src/tae-web-api"
RUN dotnet build "tae-web-api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "tae-web-api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "tae-web-api.dll"]