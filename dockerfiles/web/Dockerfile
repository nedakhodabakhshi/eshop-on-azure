
# ---------------------
# Build stage
# ---------------------
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build

# Set working directory
WORKDIR /src

# Copy everything into container
COPY . .

# Restore dependencies for WebApp
RUN dotnet restore ./src/WebApp/WebApp.csproj

# Build and publish WebApp
WORKDIR /src/WebApp
RUN dotnet publish -c Release -o /app

# ---------------------
# Runtime stage
# ---------------------
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS final

WORKDIR /app

# Copy published output from build stage
COPY --from=build /app .

# Expose port 80
EXPOSE 80

# Define entrypoint
ENTRYPOINT ["dotnet", "WebApp.dll"]
