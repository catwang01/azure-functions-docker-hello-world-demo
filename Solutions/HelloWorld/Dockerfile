FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS installer-env

WORKDIR /src/dotnet-function-app
COPY *.csproj .
RUN dotnet restore *.csproj
COPY . .
RUN mkdir -p /home/site/wwwroot && \
    dotnet publish *.csproj --output /home/site/wwwroot

FROM mcr.microsoft.com/azure-functions/dotnet:2.0-arm32v7
ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
    AzureFunctionsJobHost__Logging__Console__IsEnabled=true

COPY --from=installer-env ["/home/site/wwwroot", "/home/site/wwwroot"]
