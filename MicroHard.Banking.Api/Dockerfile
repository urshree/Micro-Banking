FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MicroHard.Banking.Api/MicroHard.Banking.Api.csproj", "MicroHard.Banking.Api/"]
RUN dotnet restore "MicroHard.Banking.Api/MicroHard.Banking.Api.csproj"
COPY . .
WORKDIR "/src/MicroHard.Banking.Api"
RUN dotnet build "MicroHard.Banking.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroHard.Banking.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroHard.Banking.Api.dll"]