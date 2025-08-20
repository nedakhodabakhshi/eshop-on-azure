# Use official .NET SDK image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src

# Copy and restore only the .csproj to cache dependencies
COPY src/WebApp/*.csproj ./WebApp/
RUN dotnet restore ./WebApp/WebApp.csproj

# Copy everything and build
COPY src/WebApp/. ./WebApp/
WORKDIR /src/WebApp
RUN dotnet publish -c Release -o /app

# Final image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "WebApp.dll"]
