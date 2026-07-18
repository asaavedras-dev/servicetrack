FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

COPY ["ServiceTrack.Api/ServiceTrack.Api.csproj", "ServiceTrack.Api/"]
COPY ["ServiceTrack.Application/ServiceTrack.Application.csproj", "ServiceTrack.Application/"]
COPY ["ServiceTrack.Domain/ServiceTrack.Domain.csproj", "ServiceTrack.Domain/"]
COPY ["ServiceTrack.Infrastructure/ServiceTrack.Infrastructure.csproj", "ServiceTrack.Infrastructure/"]

RUN dotnet restore "ServiceTrack.Api/ServiceTrack.Api.csproj"

COPY . .

WORKDIR /src/ServiceTrack.Api

RUN dotnet publish "ServiceTrack.Api.csproj" \
    --configuration Release \
    --output /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:8080
ENV ASPNETCORE_ENVIRONMENT=Production

EXPOSE 8080

ENTRYPOINT ["dotnet", "ServiceTrack.Api.dll"]