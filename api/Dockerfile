FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
#COPY Basic3TierAPI/Basic3TierAPI.csproj Basic3TierAPI/
#RUN dotnet restore "Basic3TierAPI/Basic3TierAPI.csproj"
#COPY Basic3Tier.Core/Basic3Tier.Core.csproj Basic3Tier.Core/
#COPY Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj Basic3Tier.Infrastructure/
#RUN dotnet restore "Basic3Tier.Core/Basic3Tier.Core.csproj"
#RUN dotnet restore "Basic3Tier.Infrastructure/Basic3Tier.Infrastructure.csproj"
COPY . .
WORKDIR "/src/Basic3TierAPI"
RUN dotnet build -c Release -o /app/build
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Basic3TierAPI.dll"]