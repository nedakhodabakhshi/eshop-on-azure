# ----------------------
# Build stage
# ----------------------
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set working directory
WORKDIR /src

# Copy only csproj and restore as distinct layers (to cache dependencies)
COPY ./src/WebApp/WebApp.csproj ./WebApp/
RUN dotnet restore ./WebApp/WebApp.csproj

# Copy everything else and build
COPY ./src/WebApp/ ./WebApp/
WORKDIR /src/WebApp
RUN dotnet publish -c Release -o /app

# ----------------------
# Runtime stage
# ----------------------
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final

WORKDIR /app
COPY --from=build /app .

# Expose port (optional, e.g. 80)
EXPOSE 80

# Define entrypoint
ENTRYPOINT ["dotnet", "WebApp.dll"]

