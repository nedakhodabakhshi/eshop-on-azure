
# ---------------------
# Build stage
# ---------------------
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set working directory
WORKDIR /src

# Copy everything (نه فقط WebApp) چون پروژه WebApp به بقیه پروژه‌ها وابسته است
COPY . .

# Restore dependencies for WebApp
RUN dotnet restore ./WebApp/WebApp.csproj

# Build and publish WebApp
WORKDIR /src/WebApp
RUN dotnet publish -c Release -o /app

# ---------------------
# Runtime stage
# ---------------------
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS final

WORKDIR /app

# Copy published output from build stage
COPY --from=build /app .

# Expose port 80 (اختیاری)
EXPOSE 80

# Define entrypoint
ENTRYPOINT ["dotnet", "WebApp.dll"]
