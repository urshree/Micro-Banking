FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["Microhard.Transfer.Api/Microhard.Transfer.Api.csproj", "Microhard.Transfer.Api/"]
RUN dotnet restore "Microhard.Transfer.Api/Microhard.Transfer.Api.csproj"
COPY . .
WORKDIR "/src/Microhard.Transfer.Api"
RUN dotnet build "Microhard.Transfer.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Microhard.Transfer.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Microhard.Transfer.Api.dll"]