Set-Content -Path "Server/Dockerfile" -Value @'
FROM ://microsoft.com AS build
WORKDIR /src

COPY Server/API/*.csproj ./Server/API/
COPY Server/Infra/*.csproj ./Server/Infra/
COPY Server/Service/*.csproj ./Server/Service/
RUN dotnet restore ./Server/API/API.csproj

COPY Server/API/ ./Server/API/
COPY Server/Infra/ ./Server/Infra/
COPY Server/Service/ ./Server/Service/

WORKDIR /src/Server/API
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false

FROM ://microsoft.com AS final
WORKDIR /app
COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:5000;https://+:7055

ENTRYPOINT ["dotnet", "API.dll"]
'@
