
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

COPY src/Web/WebMVC/*.csproj ./WebMVC/
RUN dotnet restore ./WebMVC/WebMVC.csproj

COPY . .
WORKDIR /app/WebMVC
RUN dotnet publish WebMVC.csproj -c Release -o /out

FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build /out .
ENTRYPOINT ["dotnet", "WebMVC.dll"]
