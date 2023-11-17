FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["WheatherHunter.Forecast/WheatherHunter.Forecast.csproj", "WheatherHunter.Forecast/"]
RUN dotnet restore "WheatherHunter.Forecast/WheatherHunter.Forecast.csproj"
COPY . .
WORKDIR "/src/WheatherHunter.Forecast"
RUN dotnet build "WheatherHunter.Forecast.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "WheatherHunter.Forecast.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "WheatherHunter.Forecast.dll"]
