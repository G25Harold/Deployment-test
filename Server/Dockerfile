# BUILD STAGE
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

# Copy project files
COPY Server/API/*.csproj ./Server/API/
COPY Server/Infra/*.csproj ./Server/Infra/
COPY Server/Service/*.csproj ./Server/Service/

# Restore dependencies
RUN dotnet restore ./Server/API/API.csproj

# Copy source code
COPY Server/API/ ./Server/API/
COPY Server/Infra/ ./Server/Infra/
COPY Server/Service/ ./Server/Service/

# Publish application
WORKDIR /src/Server/API

RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false


# RUNTIME STAGE
FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:5000

EXPOSE 5000

ENTRYPOINT ["dotnet", "API.dll"]