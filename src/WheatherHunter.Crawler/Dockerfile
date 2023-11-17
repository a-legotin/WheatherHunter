FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WheatherHunter.Crawler/WheatherHunter.Crawler.csproj", "WheatherHunter.Crawler/"]
RUN dotnet restore "WheatherHunter.Crawler/WheatherHunter.Crawler.csproj"
COPY . .
WORKDIR "/src/WheatherHunter.Crawler"
RUN dotnet build "WheatherHunter.Crawler.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WheatherHunter.Crawler.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WheatherHunter.Crawler.dll"]
