FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env
WORKDIR /app

# Copy everything
COPY ./your/backend/admin-api/*.sln ./your/backend/admin-api/
# COPY Backends/CheckVat/CheckVat.Shared/*.csproj ./Backends/CheckVat/CheckVat.Shared/


COPY ./your/backend/sharedlibs/EmailService/*.csproj ./your/backend/sharedlibs/EmailService/

# Restore as distinct layers
RUN dotnet restore ./your/backend/admin-api/admin-api.sln

COPY . .
# Build and publish a release
RUN dotnet publish ./your/backend/admin-api/admin-api/admin-api.csproj -c Release -o publish

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:6.0

# Change current directory to publish directory to run the app
WORKDIR /publish

COPY --from=build-env /app/publish .

# Start app in specific url. Typically used to specify the port on the app's localhost
ENV ASPNETCORE_URLS="http://*:5000"

# Change the environment to Development to use swagger UI. Default available env(Production, Staging, Development). That can be overrided by app configuration to use custom env(PRD,ACC,TST,DEV,...).
ENV ASPNETCORE_ENVIRONMENT=Development

ENTRYPOINT ["dotnet", "admin-api.dll"]
