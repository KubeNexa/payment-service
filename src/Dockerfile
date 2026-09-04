
# --- Stage 1: build -------------------------------------------------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

COPY src/PaymentService.Api/PaymentService.Api.csproj src/PaymentService.Api/
RUN dotnet restore src/PaymentService.Api/PaymentService.Api.csproj

COPY src/PaymentService.Api/ src/PaymentService.Api/

RUN dotnet publish src/PaymentService.Api/PaymentService.Api.csproj \
    -c Release \
    --no-restore \
    -o /app/publish

# --- Stage 2: runtime -------------------------------------------------
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

COPY --from=build /app/publish .

USER $APP_UID

ENV ASPNETCORE_URLS=http://+:8083
EXPOSE 8083

ENTRYPOINT ["dotnet", "PaymentService.Api.dll"]
