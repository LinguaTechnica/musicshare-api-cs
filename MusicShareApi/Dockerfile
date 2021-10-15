FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["MusicShareApi/MusicShareApi.csproj", "MusicShareApi/"]
RUN dotnet restore "MusicShareApi/MusicShareApi.csproj"
COPY . .
WORKDIR "/src/MusicShareApi"
RUN dotnet build "MusicShareApi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MusicShareApi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MusicShareApi.dll"]
