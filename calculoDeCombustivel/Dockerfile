FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src
COPY ["calculoDeCombustivel.csproj", "."]
RUN dotnet restore "./calculoDeCombustivel.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "calculoDeCombustivel.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "calculoDeCombustivel.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "calculoDeCombustivel.dll"]