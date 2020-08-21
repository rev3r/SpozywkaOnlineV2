FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["SpozywkaOnlineV2/SpozywkaOnlineV2.csproj", "SpozywkaOnlineV2/"]
RUN dotnet restore "SpozywkaOnlineV2/SpozywkaOnlineV2.csproj"
COPY . .
WORKDIR "/src/SpozywkaOnlineV2"
RUN dotnet build "SpozywkaOnlineV2.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SpozywkaOnlineV2.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SpozywkaOnlineV2.dll"]