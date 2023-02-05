#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["money-list-app.API/money-list-app.API.csproj", "money-list-app.API/"]
RUN dotnet restore "money-list-app.API/money-list-app.API.csproj"
COPY . .
WORKDIR "/src/money-list-app.API"
RUN dotnet build "money-list-app.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "money-list-app.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "money-list-app.API.dll"]