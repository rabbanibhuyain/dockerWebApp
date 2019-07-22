FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["dockerWebApp/dockerWebApp.csproj", "dockerWebApp/"]
RUN dotnet restore "dockerWebApp/dockerWebApp.csproj"
COPY . .
WORKDIR "/src/dockerWebApp"
RUN dotnet build "dockerWebApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "dockerWebApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "dockerWebApp.dll"]