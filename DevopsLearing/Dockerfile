FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DevopsLearing/DevopsLearing.csproj", "DevopsLearing/"]
RUN dotnet restore "DevopsLearing/DevopsLearing.csproj"
COPY . .
WORKDIR "/src/DevopsLearing"
RUN dotnet build "DevopsLearing.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DevopsLearing.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DevopsLearing.dll"]
